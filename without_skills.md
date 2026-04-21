# Diagrams WITHOUT Mermaid Skills

A naive attempt — no awareness of mermaid syntax conventions, layout direction,
node shapes, styling, or rendering quirks. Just "I think this is how it works."

## 1. Login Flow (broken / messy)

```mermaid
graph
    User -> Browser -> Server -> DB
    Server -> "Auth Service"
    if valid then "Send Token" else "Reject"
    User <- Token
```

Problems:
- `graph` requires a direction (`TD`, `LR`...).
- Arrows must be `-->`, not `->`.
- No `if/then/else` syntax — that's pseudocode, not mermaid.
- Node IDs with spaces aren't quoted properly.
- Will fail to render.

## 2. System Architecture (ASCII fallback because mermaid was "too hard")

```
 +--------+      +---------+      +----------+
 | Client | ---> | Backend | ---> | Database |
 +--------+      +---------+      +----------+
                     |
                     v
                  [ Cache ]
```

Problems:
- Not actually a diagram — just text. No interactivity, no GitHub native rendering as a real graph.
- Hard to maintain, hard to extend.

## 3. Sequence (wrong diagram type)

```mermaid
flowchart
    A: Hello B
    B: Hi A
    A: How are you
```

Problems:
- This is a sequence diagram, but uses `flowchart`.
- Syntax is invented.
- Won't render.
