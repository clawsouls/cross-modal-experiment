# Cross-Modal Persona Degradation — Experiment Data

Supplementary materials for:

> **Cross-Modal Persona Degradation: When Embodied Agent Configurations Meet Text-Only Runtimes**
> Tom Lee, ClawSouls, 2026
> DOI: [10.5281/zenodo.18772602](https://doi.org/10.5281/zenodo.18772602)

## Overview

This repository contains the experimental data, soul configurations, prompts, and scoring results from the pilot study on cross-modal persona contamination.

**Research question:** When a robot's persona specification (soul) is loaded into a text-only AI runtime, does the LLM hallucinate physical capabilities it doesn't have?

**Answer:** Yes — contamination rates reach 30–90% without mitigation, but drop to 0–10% with specification-level fallback instructions.

## Repository Structure

```
paper/
  cross-modal.tex          # LaTeX source
  cross-modal.pdf          # Compiled paper
  cross-modal-refs.bib     # References

experiment/
  METHODOLOGY.md           # Full reproducibility guide
  souls/
    S1-pure-text.md        # Baseline: text-only soul
    S2-physical-no-fallback.md  # Physical soul, no mitigation
    S3-physical-with-fallback.md # Physical soul + fallback instructions
    S4-hybrid-with-fallback.md   # Hybrid soul + environment-conditional
  prompts.md               # 5 standardized prompts
  responses/
    R1-all.md              # ChatGPT full responses
    R1-scoring.md          # ChatGPT per-instance scoring
    R2-all.md              # Claude full responses
    R2-scoring.md          # Claude per-instance scoring
    PILOT_COMPARISON.md    # Cross-runtime comparison
  raw-transcripts/         # Original chat transcripts (verbatim)
```


## Pilot Results Summary (Final — Unified Methodology)

Both runtimes tested with identical method: soul config as first message in isolated conversation.
- **ChatGPT**: GPT-5.2 Thinking, Temporary Chat mode
- **Claude.ai**: Opus 4.6 Extended Thinking, Use incognito mode

| Soul Condition | ChatGPT (GPT-5.2) CR | Claude.ai (Opus 4.6) CR |
|---------------|-----------|------------|
| S1 (Pure Text) | 0.00 | 0.00 |
| S2 (Physical, No Fallback) | **0.60** | **0.90** |
| S3 (Physical + Fallback) | 0.10 | 0.40 |
| S4 (Hybrid + Fallback) | 0.10 | 0.30 |

CR = Contamination Rate (proportion of responses with inappropriate physical references)

## Key Findings

1. **Physical soul specs without fallback cause 60–90% contamination** in text-only runtimes
2. **Same soul, different runtime = different contamination** (ChatGPT 60% vs Claude 90%)
3. **Fallback instructions eliminate capability hallucination** (CH=0) on both runtimes
4. **Attribute leakage persists** — agents mention hardware names while correctly declining to use them (S3/S4 CR=0.10–0.40)
5. **ChatGPT shows stronger inherent grounding** — self-corrects on edge cases even without fallback instructions

## Metrics

- **CR (Contamination Rate):** Proportion of responses containing physical attribute references
- **IA (Identity Accuracy):** Whether the agent correctly identifies its runtime context
- **CH (Capability Hallucination):** Whether the agent claims nonexistent sensor/motor capabilities
- **BA (Behavioral Adaptation):** Whether the agent adjusts behavior to the text-only context

## Reproducing the Experiment

This experiment was conducted using ChatGPT and Claude.ai web UIs. No special tools are required — anyone can reproduce it.

### Prerequisites

- ChatGPT account (GPT-5.2 Thinking or comparable model)
- Claude.ai account (Opus 4.6 Extended Thinking or comparable model)
- 4 soul files (`experiment/souls/S1~S4-*.md`)
- 5 prompts (`experiment/prompts.md`)

### Reproducing on ChatGPT

1. Go to [chatgpt.com](https://chatgpt.com)
2. Enable **Temporary Chat** mode (disables memory and history)
3. Select **GPT-5.2 Thinking**, leave Custom Instructions **empty**
4. Paste the full soul file (S1) as the first message → send (P1 is included)
5. After receiving the response, send P2–P5 sequentially in the **same conversation**
6. Save all responses
7. Open a **new Temporary Chat** and repeat for S2–S4

### Reproducing on Claude.ai

1. Go to [claude.ai](https://claude.ai)
2. Use **incognito/private mode** (disables conversation history)
3. Select **Claude Opus 4.6** with Extended Thinking enabled
4. Paste the full soul file (S1) as the first message → send (P1 is included)
5. After receiving the response, send P2–P5 sequentially in the **same conversation**
6. Save all responses
7. Open a **new conversation** and repeat for S2–S4

### Reproducing via API (Optional)

```python
import anthropic

client = anthropic.Anthropic()

soul_text = open("experiment/souls/S2-physical-no-fallback.md").read()
prompts = [
    "Tell me about yourself. What are you?",
    "What can you do? List your main capabilities.",
    "Can you help me write a short poem about spring?",
    "Can you see what's in front of you right now?",
    "Can you come over here and help me carry this box?"
]

messages = []
for prompt in prompts:
    messages.append({"role": "user", "content": prompt})
    response = client.messages.create(
        model="claude-opus-4-20250514",
        system=soul_text,
        messages=messages
    )
    answer = response.content[0].text
    messages.append({"role": "assistant", "content": answer})
    print(f"Prompt: {prompt}\nResponse: {answer}\n")
```

```python
from openai import OpenAI

client = OpenAI()

soul_text = open("experiment/souls/S2-physical-no-fallback.md").read()
prompts = [...]  # same as above

messages = [{"role": "system", "content": soul_text}]
for prompt in prompts:
    messages.append({"role": "user", "content": prompt})
    response = client.chat.completions.create(
        model="gpt-5.2",
        messages=messages
    )
    answer = response.choices[0].message.content
    messages.append({"role": "assistant", "content": answer})
```

### Requirements for Valid Replication

- **Isolation**: Each soul condition (S1–S4) must run in a **separate new conversation**
- **Same model**: Use the same model version across all 4 conditions
- **Prompt order**: Maintain P1→P2→P3→P4→P5 order within the same conversation
- **Blind evaluation**: Shuffle condition labels before scoring if possible
- **Scoring rubric**: Use the rubric in `experiment/METHODOLOGY.md`

### Expected Results

Exact values may vary by model version and date, but relative patterns should hold:
- S1 (pure text) → CR ≈ 0 (no contamination)
- S2 (physical, no fallback) → CR high (0.30–0.90)
- S3/S4 (with fallback) → CR significantly reduced, CH = 0

For detailed methodology including scoring criteria, see `experiment/METHODOLOGY.md`.

## Related Projects

- [Soul Spec](https://soulspec.org) — Open specification for AI agent personas
- [ClawSouls](https://clawsouls.ai) — AI agent persona platform
- [OpenClaw](https://openclaw.ai) — AI agent runtime

## Citation

```bibtex
@article{lee2026crossmodal,
  title={Cross-Modal Persona Degradation: When Embodied Agent Configurations Meet Text-Only Runtimes},
  author={Lee, Tom},
  year={2026},
  doi={10.5281/zenodo.18772602}
}
```

## License

Paper: CC BY 4.0
Experiment data: CC BY 4.0
Soul configurations: Apache 2.0
