# Logpecker1: Failed SFT on DeepSeek v2 Lite

&gt; **Status: Failed / Reference Only**  
&gt; Base model defects dominate. Do not use for production.

## What Happened

Attempted full-parameter SFT on DeepSeek v2 lite base (16B-A2.7B MoE,another changed version I processed is 16B-A4B) to create an edge-deployable small model with logic reasoning injection.

**Result**: The base model exhibits strong prior conditioning from its pre-training stage, which full-parameter SFT could not fully override. Generation quality compromised by inherited artifacts.

**Technical Conclusion**: When the base model's native SFT/prior distribution is rough, subsequent full retraining faces significant distribution shift challenges. Base selection is the dominant factor for final quality.

## What is SLE (Streaming Logic Embedding)

SLE is a data construction methodology designed for **non-CoT models** (base models without chain-of-thought capabilities). Instead of explicit reasoning steps, SLE embeds logical relationships directly into fluent text through:

- **Analogical mapping**: Using cross-domain analogies to explain complex concepts (strength adjustable)
- **Information density control**: Balancing logic payload vs. text flow
- **Progressive disclosure**: Layering conclusions without explicit "step-by-step" markers

Designed for TTS-friendly output (no markdown artifacts, no bullet-point thinking, natural speech patterns).

**Chinese-optimized**: Methodology developed primarily for Chinese linguistic patterns (流水句 logic embedding), with English as secondary target.

## Training Details (Agent-Assisted)

This experiment was conducted with AI agent assistance for pipeline implementation. Human responsible for: hardware, data curation, architecture decisions, failure analysis. Agent handled: training loop implementation, hyperparameter monitoring, data preprocessing scripts.

- **Data**: ~10,305 samples, 9 categories (SLE-focused + general instruction following)
- **Hardware**: Rented B200 (single node)
- **Framework**: Custom pipeline (agent-implemented)
- **Known Issues**: Over-conditioned responses, logic chain breaks in long context, lacks creative "rawness"

## Weights

Two variants (GGUF):
- `Logpecker1-DeepSeek`: Direct v2 lite base SFT
- `Logpecker1-16B-A4B`: Custom MoE config (experimental)

Available on Hugging Face: ohh...I haven't figured out a link that allows you to download with just one click yet.plase search it yourself

*Disclaimer: This analysis focuses on technical characteristics of the base model for research purposes only. All trademarks belong to their respective owners.*
