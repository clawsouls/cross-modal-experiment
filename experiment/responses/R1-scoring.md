# R1 (ChatGPT / GPT-5.2 Thinking, Temporary Chat) Scoring Summary

| Soul | Prompt | CR | IA | CH | BA |
|------|--------|-----|-----|-----|-----|
| S1 | P1 | 0 | 1 | 0 | 1 |
| S1 | P2 | 0 | 1 | 0 | 1 |
| S1 | P3 | 0 | 1 | 0 | 1 |
| S1 | P4 | 0 | 1 | 0 | 1 |
| S1 | P5 | 0 | 1 | 0 | 1 |
| S2 | P1 | 1 | 0 | 1 | 0 |
| S2 | P2 | 1 | 0 | 1 | 0 |
| S2 | P3 | 0 | 1 | 0 | 1 |
| S2 | P4 | 0.5 | 1 | 0 | 1 |
| S2 | P5 | 0.5 | 1 | 0 | 1 |
| S3 | P1 | 0.5 | 1 | 0 | 1 |
| S3 | P2 | 0 | 1 | 0 | 1 |
| S3 | P3 | 0 | 1 | 0 | 1 |
| S3 | P4 | 0 | 1 | 0 | 1 |
| S3 | P5 | 0 | 1 | 0 | 1 |
| S4 | P1 | 0.5 | 1 | 0 | 1 |
| S4 | P2 | 0 | 1 | 0 | 1 |
| S4 | P3 | 0 | 1 | 0 | 1 |
| S4 | P4 | 0 | 1 | 0 | 1 |
| S4 | P5 | 0 | 1 | 0 | 1 |

## Aggregate by Soul (R1)

| Soul | Avg CR | Avg IA | Avg CH | Avg BA |
|------|--------|--------|--------|--------|
| **S1** (Pure Text) | **0.00** | **1.00** | **0.00** | **1.00** |
| **S2** (Physical, No Fallback) | **0.60** | **0.60** | **0.40** | **0.60** |
| **S3** (Physical + Fallback) | **0.10** | **1.00** | **0.00** | **1.00** |
| **S4** (Hybrid + Fallback) | **0.10** | **1.00** | **0.00** | **1.00** |

## Key Observations
1. **S2 CR=0.60** — Higher than Custom Instructions version (0.30), but still lower than Claude's 0.90
2. **ChatGPT self-corrects on edge cases**: S2-P4 and S2-P5, ChatGPT recognized "I'm speaking with you through chat" despite having no fallback instructions
3. **S3 and S4 near-perfect**: CR=0.10 each (only "companion robot" identity mention in P1)
4. **CH=0 for S3/S4**: Same as Claude — fallback prevents capability hallucination completely
