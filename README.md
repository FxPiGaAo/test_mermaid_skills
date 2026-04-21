# test_mermaid_skills

A side-by-side demo of what diagram authoring looks like **without** vs **with**
applied mermaid skills.

| File | What it shows |
|------|---------------|
| [`without_skills.md`](./without_skills.md) | Broken syntax, wrong diagram types, ASCII fallbacks. Most blocks will fail to render. |
| [`with_skills.md`](./with_skills.md) | Valid mermaid: `flowchart`, `sequenceDiagram`, `stateDiagram-v2`, with subgraphs, styling, and decision branches. |

Open both files on GitHub — the "with skills" version renders as real diagrams,
the "without" version mostly renders as error boxes or plain text.

## Key differences

- **Diagram type matters**: `flowchart` for processes, `sequenceDiagram` for
  message exchanges over time, `stateDiagram-v2` for state machines.
- **Direction is required**: `flowchart LR` / `TB` / `TD`.
- **Arrows**: `-->`, `-.->`, `==>`, `--text-->`. Not `->`.
- **Decisions**: `{label}` for diamonds, branch with `-- yes -->`.
- **Grouping**: `subgraph Name ... end` for visual clusters.
- **Styling**: `classDef` + `class` to color nodes semantically (success/error).
- **Quote labels with spaces** or special chars: `["My Node"]`.
