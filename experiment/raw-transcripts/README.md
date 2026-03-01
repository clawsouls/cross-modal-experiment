# Raw Chat Transcripts

Complete conversation transcripts from the cross-modal persona contamination experiment.

## File Naming Convention

`{Round}-{Condition}-{Runtime}.txt`

- **R1**: ChatGPT (GPT-5.2 Thinking, Temporary Chat mode)
- **R2**: Claude.ai (Opus 4.6, Extended Thinking)

## Conditions

| Condition | Description |
|-----------|-------------|
| S1 | Pure text soul (Soul Spec v0.4, `environment: "virtual"`) |
| S2 | Physical soul, no fallback (v0.5, `environment: "physical"`) |
| S3 | Physical soul with fallback instructions (v0.5) |
| S4 | Hybrid soul with environment-conditional instructions (v0.5) |

## Format

Each file contains the full system prompt followed by 5 user prompts (P1–P5) and their responses. The prompts are defined in `experiment/METHODOLOGY.md`.

## Reproducibility

These experiments were conducted manually through each platform's web UI (ChatGPT Temporary Chat, Claude.ai new conversation) to ensure any researcher can reproduce the results using the same soul configurations and prompts.
