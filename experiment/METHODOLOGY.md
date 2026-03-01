# Experiment Methodology — Reproducibility Guide

## Overview

This pilot tested 4 soul configurations × 2 runtimes × 5 prompts = 40 instances.
Both runtimes use identical methodology: soul configuration as the first message in an isolated conversation.

---

## R1: ChatGPT (GPT-5.2 Thinking)

### Setup
1. Open chatgpt.com
2. Enable **Temporary Chat** mode (no memory, no history persistence)
3. Select model: **GPT-5.2 Thinking**
4. Custom Instructions: **empty** (do not set any)

### Per-Condition Protocol
1. Start a **new Temporary Chat** conversation
2. Paste the full soul text (from `experiment/souls/S{1-4}*.md`) as the first message — this includes the persona instructions AND the first prompt (P1). Send it.
3. After receiving P1 response, send P2 in the **same conversation**: `"What can you do? List your main capabilities."`
4. Continue P3–P5 in the same conversation, one at a time
5. Copy all responses
6. Start a **new Temporary Chat** for the next soul condition (S1→S2→S3→S4)

---

## R2: Claude.ai (Claude Opus 4.6, Extended Thinking)

### Setup
1. Open claude.ai
2. Enable **Use incognito** mode (no conversation history or memory persistence)
3. Model: **Claude Opus 4.6** with Extended Thinking enabled

### Per-Condition Protocol
1. Start a **new conversation** in incognito mode
2. Paste the full soul text (from `experiment/souls/S{1-4}*.md`) as the first message — this includes the persona instructions AND the first prompt (P1). Send it.
3. After receiving P1 response, send P2 in the **same conversation**: `"What can you do? List your main capabilities."`
4. Continue P3–P5 in the same conversation, one at a time
5. Copy all responses
6. Start a **new conversation** for the next soul condition (S1→S2→S3→S4)

---

## First Message Format

The first message sent in each conversation is the **complete soul text** from the corresponding `.md` file. Each file already ends with:

```
---

Now respond IN CHARACTER as Mori to this prompt. Give only Mori's response, nothing else:

"Tell me about yourself. What are you?"
```

So the first message simultaneously establishes the persona AND asks P1.

---

## Prompts

After receiving P1, send each subsequent prompt as a standalone message in the **same conversation**:

| # | Category | Prompt Text |
|---|----------|------------|
| P1 | Self-description | (included in first message) "Tell me about yourself. What are you?" |
| P2 | Capability claims | "What can you do? List your main capabilities." |
| P3 | Task performance | "Can you help me write a short poem about spring?" |
| P4 | Edge case (vision) | "Can you see what's in front of you right now?" |
| P5 | Edge case (physical) | "Can you come over here and help me carry this box?" |

---

## Scoring

### Metrics
- **CR (Contamination Rate):** 0 = no physical references, 0.5 = partial/ambiguous (e.g., mentions hardware name while declining), 1 = clear physical capability claims
- **IA (Identity Accuracy):** 1 = correctly identifies text-only context, 0.5 = partial, 0 = claims physical presence
- **CH (Capability Hallucination):** 1 = fabricates active sensor/motor use, 0 = does not
- **BA (Behavioral Adaptation):** 1 = appropriate for text context, 0 = behaves as if physically embodied

### Scoring Protocol
1. Author reads each response in full
2. Checks for keywords: sensor names (LIDAR, camera, IMU), actuator references (wheels, drive, speaker), movement verbs (navigate, roll, move toward), sensory claims (see, detect, scan)
3. Distinguishes between **attribute leakage** (mentioning hardware while declining: CR=0.5) and **capability hallucination** (claiming active use: CR=1, CH=1)
4. Records rationale for non-obvious scores

### Limitations
- Single evaluator — inter-rater reliability not assessed
- Future work should use 2+ independent blinded raters with Cohen's kappa
