## 🧭 Aetherflow System Architecture (First Draft)

```mermaid
flowchart TD

%% === Event Layer ===
subgraph Dev["👨‍💻 Developer Environment"]
    IDE[Code Editor / Git Client]
    CLI["Command Line (Typer CLI)"]
    Sched[Time/Event Scheduler]
end

%% === Core Orchestration Layer ===
subgraph Core["🧠 Aetherflow Core (FastAPI Backend)"]
    TRG[Trigger Manager]
    PLAN["AI Planner (LangChain + Ollama)"]
    EXEC[Execution Engine]
    MEM["Workflow Memory (SQLite)"]
end

%% === Connectors & Integrations ===
subgraph Conn["🔌 Connectors"]
    GH[GitHub API]
    AWS[AWS SDK / Lambda]
    Slack[Slack / Teams Bot]
    Local[Local Scripts & Tools]
end

%% === Cloud & Infrastructure ===
subgraph Cloud["☁️ AWS Free Tier (Optional)"]
    EC2["EC2 t2.micro Host"]
    S3["S3 Bucket for Files / Configs"]
    EVB[EventBridge for Triggers]
    CW[CloudWatch Logs]
end

%% === Flow Connections ===
IDE -->|Commits / Builds / CLI commands| TRG
Sched --> TRG
TRG --> PLAN
PLAN --> EXEC
EXEC --> MEM

%% Connect execution to individual connectors (not to the subgraph id)
EXEC --> GH
EXEC --> Slack
EXEC --> AWS
EXEC --> Local

%% Optional: show traffic direction from connectors
GH -->|External APIs / Systems| EXEC
Slack --> EXEC
AWS --> EXEC
Local --> EXEC

%% Deployments / Infra links
EXEC -->|Deployed on| EC2
EC2 --> S3
EC2 --> CW
EVB --> TRG
