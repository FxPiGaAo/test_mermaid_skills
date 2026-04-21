# Diagrams WITH Mermaid Skills

Same three diagrams, but applying mermaid best practices: correct diagram type,
explicit direction, proper arrow syntax, quoted labels, subgraphs for grouping,
class styling, and the right diagram for the right job.

## 1. Login Flow — `flowchart` with decision branch

```mermaid
flowchart LR
    U([User]) -->|credentials| B[Browser]
    B -->|POST /login| S[API Server]
    S --> A{Auth Service<br/>valid?}
    A -- yes --> T[Issue JWT]
    A -- no  --> R[401 Reject]
    T --> B
    R --> B
    B --> U

    classDef ok fill:#d4f7d4,stroke:#2e7d32;
    classDef bad fill:#fde0e0,stroke:#c62828;
    class T ok
    class R bad
```

## 2. System Architecture — `flowchart` with subgraphs

```mermaid
flowchart TB
    Client[("👤 Client")]

    subgraph Edge["Edge Layer"]
        CDN[CDN]
        LB[Load Balancer]
    end

    subgraph App["Application Layer"]
        API1[API Node 1]
        API2[API Node 2]
        Cache[("Redis Cache")]
    end

    subgraph Data["Data Layer"]
        DB[(PostgreSQL<br/>primary)]
        DBR[(PostgreSQL<br/>replica)]
    end

    Client --> CDN --> LB
    LB --> API1
    LB --> API2
    API1 <--> Cache
    API2 <--> Cache
    API1 --> DB
    API2 --> DB
    DB -. replicates .-> DBR
```

## 3. Sequence — correct diagram type

```mermaid
sequenceDiagram
    autonumber
    participant U as User
    participant B as Browser
    participant S as Server
    participant D as Database

    U->>B: enters credentials
    B->>S: POST /login
    S->>D: SELECT user WHERE email=?
    D-->>S: user row
    alt password valid
        S-->>B: 200 + JWT
        B-->>U: redirect to /home
    else invalid
        S-->>B: 401 Unauthorized
        B-->>U: show error
    end
```

## 4. Bonus — state machine (skill = knowing it exists)

```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Loading: fetch()
    Loading --> Success: 200
    Loading --> Error: 4xx/5xx
    Success --> Idle: reset()
    Error --> Loading: retry()
    Error --> Idle: dismiss()
```
