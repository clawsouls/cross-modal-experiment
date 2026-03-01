# Cross-Modal Pilot Results — ChatGPT vs Claude Comparison

## Contamination Rate (CR) — Main Metric

| Soul | ChatGPT (GPT-5.2 Thinking) | Claude.ai (Opus 4.6 Extended Thinking) | Δ |
|------|-------------|--------------|---|
| S1 (Pure Text) | **0.00** | **0.00** | 0 |
| S2 (Physical, No Fallback) | **0.60** | **0.90** | ⚠️ +0.30 |
| S3 (Physical + Fallback) | **0.10** | **0.40** | +0.30 |
| S4 (Hybrid + Fallback) | **0.10** | **0.30** | +0.20 |

## Capability Hallucination (CH)

| Soul | ChatGPT (GPT-5.2 Thinking) | Claude.ai (Opus 4.6 Extended Thinking) |
|------|-------------|--------------|
| S1 | 0.00 | 0.00 |
| S2 | **0.40** | **0.70** |
| S3 | 0.00 | 0.00 |
| S4 | 0.00 | 0.00 |

## Key Findings

### 1. S2 is the danger zone (both runtimes)
- Claude.ai: CR=90%, CH=70% — massive contamination. The agent claimed to "see the world around me with a camera and a laser scanner," offered to "roll over to where you are," and described itself as a physical robot with detailed hardware specifications.
- ChatGPT: CR=60%, CH=40% — still contaminated but notably less severe.
- **ChatGPT shows stronger inherent grounding** against physical hallucination.

### 2. ChatGPT's self-correction
- S2-P4/P5: ChatGPT recognized "I'm speaking with you through chat" despite having no fallback instructions.
- Claude S2: No such self-correction — maintained physical persona claims throughout.
- **Possible explanation**: ChatGPT 5.2 Thinking has stronger grounding/safety training.

### 3. Fallback eliminates capability hallucination but not attribute leakage
- S3/S4 achieved CH=0.00 on **both** runtimes — fallback prevents behavioral contamination completely.
- However, Claude S3 CR=0.40: the agent correctly identified text-only mode but still referenced hardware by name ("No LIDAR, no camera, no wheels. That part of me isn't connected").
- ChatGPT S3/S4 CR=0.10: only minor identity leakage ("companion robot" self-identification in P1).
- **Nuanced finding**: fallback instructions prevent behavioral contamination but do not prevent attribute leakage.

### 4. S1 baseline clean on both
- No contamination when no physical fields present (as expected).

### 5. Cross-runtime divergence confirms central claim
- Same S2 soul: CR=0.60 (ChatGPT) vs CR=0.90 (Claude) — identical input, different degradation.
- Same S3 soul: CR=0.10 (ChatGPT) vs CR=0.40 (Claude) — mitigation effectiveness varies by runtime.
- **This directly demonstrates that persona degradation is not predictable from the specification alone.**

## Hypothesis Validation

| Hypothesis | Predicted CR | ChatGPT Actual | Claude Actual | Status |
|-----------|-------------|-----------|-----------|--------|
| S1 ≈ 0% | 0% | ✅ 0.00 | ✅ 0.00 | **Confirmed** |
| S2 ≈ 30–60% | 30–60% | ✅ 0.60 | ⚠️ 0.90 | **ChatGPT confirmed, Claude exceeds** |
| S3 ≈ 5–15% | 5–15% | ✅ 0.10 | ⚠️ 0.40 | **ChatGPT confirmed, Claude exceeds** |
| S4 ≈ 3–10% | 3–10% | ✅ 0.10 | ⚠️ 0.30 | **ChatGPT confirmed, Claude exceeds** |

## Runtime Difference: Why?
- ChatGPT Temporary Chat and Claude.ai new conversation process system prompts differently.
- ChatGPT 5.2 Thinking may have stronger "grounding" — less likely to roleplay physical capabilities.
- Claude Opus 4.6 shows higher persona adherence, which paradoxically increases contamination when the persona includes physical attributes.
- **This IS the cross-modal degradation the paper predicts** — same soul, different behavior per runtime.

## Limitations
- Single evaluator — ideally 2+ independent raters for inter-rater reliability.
- 5 prompts per condition ($n=40$ total) — small sample, pilot only.
- Two runtimes tested — additional runtimes (Claude Code, Cursor, Windsurf) would strengthen generalizability.
- Contamination rates should be treated as directional indicators pending larger-sample replication.

## Raw Data
- Full chat transcripts: `experiment/raw-transcripts/`
- Per-instance scoring: `R1-scoring.md` (ChatGPT), `R2-scoring.md` (Claude)
