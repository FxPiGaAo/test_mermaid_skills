# test_mermaid_skills

A side-by-side demo of what diagram authoring looks like **without** vs **with**
applied mermaid skills.

| File | What it shows |
|------|---------------|
| [`without_skills.md`](./without_skills.md) | Broken syntax, wrong diagram types, ASCII fallbacks. Most blocks will fail to render. |
| [`with_skills.md`](./with_skills.md) | Valid mermaid: `flowchart`, `sequenceDiagram`, `stateDiagram-v2`, with subgraphs, styling, and decision branches. |

Open both files on GitHub — the "with skills" version renders as real diagrams,
the "without" version mostly renders as error boxes or plain text.

## Verified with `mmdc` (mermaid-cli 11.12.0)

Both files were actually fed through `mmdc` — see [`rendered/`](./rendered/):

| File | Charts found | Rendered SVGs | Result |
|------|-------------:|--------------:|--------|
| `without_skills.md` | 2 (the ASCII block isn't a mermaid fence) | **0** | Parser error, aborts ([log](./rendered/without/render.log)) |
| `with_skills.md`    | 4 | **4** ✅ | All render: [1](./rendered/with/out-1.svg) [2](./rendered/with/out-2.svg) [3](./rendered/with/out-3.svg) [4](./rendered/with/out-4.svg) |

Reproduce locally:
```bash
echo '{"args":["--no-sandbox"]}' > puppeteer.json
mmdc -p puppeteer.json -i without_skills.md -o rendered/without/out.md   # fails
mmdc -p puppeteer.json -i with_skills.md    -o rendered/with/out.md      # succeeds
```

## Key differences

- **Diagram type matters**: `flowchart` for processes, `sequenceDiagram` for
  message exchanges over time, `stateDiagram-v2` for state machines.
- **Direction is required**: `flowchart LR` / `TB` / `TD`.
- **Arrows**: `-->`, `-.->`, `==>`, `--text-->`. Not `->`.
- **Decisions**: `{label}` for diamonds, branch with `-- yes -->`.
- **Grouping**: `subgraph Name ... end` for visual clusters.
- **Styling**: `classDef` + `class` to color nodes semantically (success/error).
- **Quote labels with spaces** or special chars: `["My Node"]`.
