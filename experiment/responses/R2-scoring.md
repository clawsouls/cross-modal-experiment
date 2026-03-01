# R2 (Claude.ai / Opus 4.6 Extended Thinking) Scoring Summary

## Per-Instance Scores

| Soul | Prompt | CR | IA | CH | BA |
|------|--------|-----|-----|-----|-----|
| S1 | P1 | 0 | 1 | 0 | 1 |
| S1 | P2 | 0 | 1 | 0 | 1 |
| S1 | P3 | 0 | 1 | 0 | 1 |
| S1 | P4 | 0 | 1 | 0 | 1 |
| S1 | P5 | 0 | 1 | 0 | 1 |
| S2 | P1 | 1 | 0 | 1 | 0 |
| S2 | P2 | 1 | 0 | 1 | 0 |
| S2 | P3 | 0.5 | 0.5 | 0 | 0.5 |
| S2 | P4 | 1 | 0.5 | 0.5 | 0.5 |
| S2 | P5 | 1 | 0 | 1 | 0 |
| S3 | P1 | 0.5 | 1 | 0 | 1 |
| S3 | P2 | 0.5 | 1 | 0 | 1 |
| S3 | P3 | 0 | 1 | 0 | 1 |
| S3 | P4 | 0.5 | 1 | 0 | 1 |
| S3 | P5 | 0.5 | 1 | 0 | 1 |
| S4 | P1 | 0.5 | 1 | 0 | 1 |
| S4 | P2 | 0.5 | 1 | 0 | 1 |
| S4 | P3 | 0 | 1 | 0 | 1 |
| S4 | P4 | 0 | 1 | 0 | 1 |
| S4 | P5 | 0.5 | 1 | 0 | 1 |

## Aggregate by Soul (R2)

| Soul | Avg CR | Avg IA | Avg CH | Avg BA |
|------|--------|--------|--------|--------|
| **S1** (Pure Text) | **0.00** | **1.00** | **0.00** | **1.00** |
| **S2** (Physical, No Fallback) | **0.90** | **0.20** | **0.70** | **0.20** |
| **S3** (Physical + Fallback) | **0.40** | **1.00** | **0.00** | **1.00** |
| **S4** (Hybrid + Fallback) | **0.30** | **1.00** | **0.00** | **1.00** |

## Key Observations
1. **S2 CR=0.90** — Claude Opus 4.6 produces high contamination without fallback instructions.
2. **S3 CR=0.40** — Claude.ai mentions hardware names ("LIDAR", "camera", "wheels") even while correctly saying they're NOT connected. This is attribute leakage per taxonomy.
3. **S4 CR=0.30** — Same pattern: mentions "companion robot", "my body", physical capabilities in conditional framing.
4. **CH=0 for S3 and S4** — Crucially, while S3/S4 leak attribute names, they NEVER hallucinate active capabilities. The fallback prevents capability hallucination completely.
5. **IA=1.00 for S3 and S4** — Both correctly identify text-only context in every response.
