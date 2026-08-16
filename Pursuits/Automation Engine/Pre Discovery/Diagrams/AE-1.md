For details: https://chatgpt.com/share/6a805238-7d78-83e8-9503-c27a6dc46bf9
```
                             USER
                               │
                               ▼
                    ┌────────────────────┐
                    │   TASK INTERFACE   │
                    └─────────┬──────────┘
                              │
                              ▼
                    ┌────────────────────┐
                    │   TASK ANALYZER    │
                    │                    │
                    │ intent             │
                    │ constraints        │
                    │ decomposition      │
                    └─────────┬──────────┘
                              │
                 ┌────────────┴────────────┐
                 ▼                         ▼
       ┌─────────────────┐       ┌─────────────────┐
       │ LONG-TERM MEMORY│       │ MODEL REGISTRY  │
       │                 │       │                 │
       │ policies        │       │ capabilities    │
       │ skills          │       │ cost            │
       │ knowledge       │       │ reliability     │
       │ projects        │       │ latency         │
       └────────┬────────┘       └────────┬────────┘
                │                         │
                └────────────┬────────────┘
                             ▼
                  ┌──────────────────────┐
                  │ COUNCIL ORCHESTRATOR │
                  │                      │
                  │ decompose            │
                  │ route                │
                  │ contract             │
                  │ schedule             │
                  └──────────┬───────────┘
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
          ▼                  ▼                  ▼
      ┌────────┐         ┌────────┐         ┌────────┐
      │ LLM A  │         │ LLM B  │         │ LLM C  │
      │Reasoner│         │ Critic │         │Expert  │
      └───┬────┘         └───┬────┘         └───┬────┘
          │                  │                  │
          └──────────────────┼──────────────────┘
                             ▼
                  ┌──────────────────────┐
                  │ COUNCIL WORKING      │
                  │ MEMORY               │
                  │                      │
                  │ claims               │
                  │ evidence             │
                  │ findings             │
                  │ conflicts            │
                  │ dependencies         │
                  └──────────┬───────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
          ┌────────┐    ┌──────────┐   ┌──────────┐
          │ Tools  │    │ Critics  │   │Verifier  │
          │        │    │          │   │          │
          │ Python │    │ LLM D    │   │ LLM E    │
          │ SQL    │    │ LLM F    │   │ Tests    │
          │ Search │    └────┬─────┘   └────┬─────┘
          └────────┘         │              │
                             └──────┬───────┘
                                    ▼
                         ┌─────────────────────┐
                         │     ARBITRATOR      │
                         │                     │
                         │ evidence            │
                         │ conflicts           │
                         │ confidence          │
                         │ unresolved issues   │
                         └──────────┬──────────┘
                                    ▼
                         ┌─────────────────────┐
                         │   FINAL SYNTHESIS   │
                         └──────────┬──────────┘
                                    ▼
                                  USER
```