---
layout: post
title: "AI News Briefing — 2026-05-17"
date: 2026-05-17
---

# AI Daily Briefing — 2026-05-17

---

### 1. New Models & Benchmarks

- **Qwopus3.5-9B-Coder released** — Qwen3.5-9B fine-tuned for agentic coding and tool calling using "Trace Inversion" data augmentation. Targets the 8–16GB VRAM sweet spot. Community finetune, no independent benchmarks yet; treat claims with caution. Open-weight. [HuggingFace](https://huggingface.co/Jackrong/Qwopus3.5-9B-Coder-GGUF) · [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tfin40/jackrongqwopus359bcodergguf_hugging_face/)

- **DeepSeek V4 1M context: practical limits mapped** — Independent testing across production codebases shows solid recall under 150K tokens, degraded precision past 300K (approximate line numbers, architectural summaries instead of implementation detail), and 94% hallucination rate on unknown-answer tasks. Practical sweet spot: **150–250K tokens** for coding work. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tfhl0q/deepseek_v4s_1m_context_window_the_breaking_point/)

- **CAISI (NIST) evaluates DeepSeek V4 Pro** — Nathan Lambert's roundup notes CAISI's assessment concludes open models are lagging further behind the US frontier over time, not closing the gap. [Interconnects](https://www.interconnects.ai/p/latest-open-artifacts-21-open-model)

---

### 2. Framework & Tooling Updates

- **llama.cpp merges MTP (Multi-Token Prediction) support** — [PR #22673](https://github.com/ggml-org/llama.cpp/pull/22673) landed in master. This is the native speculative decoding path using Qwen3.6's built-in draft heads — no separate draft model needed. Requires `--parallel 1` and Unsloth's MTP-tagged GGUFs. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tes1wx/mtp_support_merged_into_llamacpp/)

- **MTP benchmarks across hardware** — Community results are pouring in. The pattern: **generation speed jumps 85–136%, but prompt processing drops 12–42%**. Net wall-clock improvement depends heavily on workload shape:

  | Hardware | Model | TG Speedup | PP Slowdown | Net Wall-Clock |
  |----------|-------|-----------|-------------|----------------|
  | RTX 3090 | Qwen3.6-27B Q4_K_M | +85% (27→50 t/s) | −42% | **41% faster** (39→23 min @ 85K ctx) |
  | RTX 5090 | Qwen3.6-27B Q5_K_M | +112% | −12% | Faster overall |
  | Strix Halo | Qwen3.6-27B Q8_0 | +136% (7.6→18 t/s) | −18% | **22% faster** (5-turn chat) |
  | Strix Halo | Qwen3.6-35B-A3B Q8_0 | +25% | −15% | **~tied or slightly slower** |

  Bottom line: MTP is a clear win for generation-heavy workloads on dense models. MoE models (35B-A3B) see less benefit because they're already fast at generation. [RTX 5090](https://reddit.com/r/LocalLLaMA/comments/1tfgxc8/testing_llamacpp_mtp_support_on_qwen36_rtx_5090/) · [RTX 3090](https://reddit.com/r/LocalLLaMA/comments/1tfilwx/llamacpp_mtp_with_qwen36_27b_on_headless_rtx_3090/) · [Strix Halo](https://reddit.com/r/LocalLLaMA/comments/1teypb8/strix_halo_llamacpp_mtp_benchmarks_27b_gets_much/)

- **Qwen3.5-122B MTP on Strix Halo** — 20 t/s sustained at Q5, 17 t/s at Q6. Impressive for a 122B model on integrated graphics. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tf6qeb/qwen35122bq5mtp_qwen35122bq6mtp/)

- **Zerostack 1.0** — Unix-inspired coding agent written in pure Rust. 392 points on HN. Worth evaluating if you want a lightweight, non-Python agent. [crates.io](https://crates.io/crates/zerostack/1.0.0)

- **codegraph** — Pre-indexed code knowledge graph for Claude Code. Reduces token usage and tool calls by giving Claude a structural map of your codebase. 416 stars on day one. [GitHub](https://github.com/colbymchenry/codegraph)

---

### 3. Infrastructure & Deployment

- **Cross-hardware inference comparison (5070 vs 3090 vs Strix Halo)** — 55-run benchmark harness with controlled methodology. Key findings: RTX 5070 (12GB GDDR7) beats RTX 3090 on models that fit in 12GB thanks to bandwidth advantage. RTX 3090 wins decisively in the 14–31B band. Strix Halo Vulkan is slightly faster than ROCm on the same chip. Qwen3.6-27B Q4_K_M is the quant sweet spot on 3090 (Q2 buys only 14% speed over Q4). [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tf9iyk/ran_the_same_models_across_strix_halo_rtx_3090/)

- **ROCm still fragile for research** — RX 7900 XTX user reports NaN explosions on backward passes with custom flow-matching code, while nanoGPT trains fine. ROCm appears stable on well-known codebases but breaks on slightly uncommon architectures. Avoid for novel research workloads. [r/MachineLearning](https://reddit.com/r/MachineLearning/comments/1tedjwo/rocm_with_pytorch_and_pytorch_lightning_seems_to/)

---

### 4. Industry Moves

- **OpenAI + Malta: ChatGPT Plus for all citizens** — First country to offer ChatGPT Plus free for a year, requiring completion of a University of Malta AI literacy course (not OpenAI-designed). Interesting policy experiment. [OpenAI Blog](https://openai.com/index/malta-chatgpt-plus-partnership/) · [r/singularity](https://reddit.com/r/singularity/comments/1tezctw/openai_and_malta_partner_to_bring_chatgpt_plus_to/)

- **Depthfirst claims its AI finds critical vulns that Anthropic Mythos missed, at 1/10th cost** — Startup says task-specific optimization lets it do for $1K what Mythos does for $10K. Claims include critical flaws affecting "the majority of people using the web." [Forbes](https://www.forbes.com/sites/thomasbrewster/2026/05/12/ai-finds-critical-vulnerabilities-that-anthropic-mythos-missed/)

- **Claude Mythos spotted on Google Vertex** — Screenshot shows Mythos model available in Vertex AI, suggesting imminent broader availability beyond Anthropic's direct API. [r/singularity](https://reddit.com/r/singularity/comments/1tf6ukh/claude_mythos_has_been_spotted_in_google_vertex/)

- **DeepSeek V4 steering vectors work** — Sean Goedecke reports that V4-Flash's architecture makes activation steering practical again, after it had become unreliable on heavily RLHF'd models. Useful for researchers doing interpretability or behavioral control. [seangoedecke.com](https://www.seangoedecke.com/steering-vectors/)

---

### 5. Research Highlights

- **Token Superposition Training (TST)** — Nous Research. 2.5× pre-training wall-clock reduction at 10B-A1B MoE scale (4,768 vs 12,311 B200-GPU-hours) with lower final loss, without changing architecture or optimizer. If validated independently, this meaningfully reduces the cost floor for training open models. [arXiv](https://arxiv.org/abs/2605.06546) · [Nous Research](https://nousresearch.com/token-superposition)

- **δ-mem: Efficient Online Memory for LLMs** — Proposes a memory mechanism for LLMs that operates online (streaming) rather than requiring full context. Relevant if you're building agents that need to maintain state across very long sessions. [arXiv](https://arxiv.org/abs/2605.12357)

- **SANA-WM: 2.6B open-source world model** — NVIDIA Labs releases a 2.6B-parameter model that generates 1-minute 720p video. Small enough to run on consumer hardware. [NVIDIA Labs](https://nvlabs.github.io/Sana/WM/)

- **LLM architecture trends: KV sharing, mHC, compressed attention** — Sebastian Raschka's deep dive covers the architectural tricks in Gemma 4, DeepSeek V4, ZAYA1-8B, and Laguna XS.2 that reduce KV-cache costs for long-context workloads. Worth reading if you care about why some models are more memory-efficient than others. [Ahead of AI](https://magazine.sebastianraschka.com/p/recent-developments-in-llm-architectures)

---

### 6. Technology Adoption

- **codegraph for Claude Code** — If you use Claude Code on large repos, this is worth trying immediately. It pre-indexes your codebase into a knowledge graph so Claude navigates with fewer tool calls and less token waste. 416 GitHub stars on day one signals strong early adoption. [GitHub](https://github.com/colbymchenry/codegraph)

- **Zerostack (Rust coding agent)** — A minimalist alternative to Python-based coding agents. Unix philosophy: small composable tools. At v1.0 with 392 HN points. Worth evaluating if you want fast startup and low overhead, but ecosystem is nascent. [crates.io](https://crates.io/crates/zerostack/1.0.0)

- **OpenClaw name history** — Simon Willison traces OpenClaw's lineage (Warelay → CLAWDIS → CLAWDBOT → Clawdbot → Moltbot → OpenClaw) ahead of his PyCon US lightning talk. No functional updates, just context on the project's evolution. [Simon Willison](https://simonwillison.net/2026/May/16/openclaw-names/#atom-everything)

---

### 8. Watchlist Updates

- **Anthropic Mythos Preview** — Now spotted on Google Vertex AI, suggesting rollout to cloud partners is underway. Depthfirst claims to find critical vulns Mythos missed at 10% of the cost. Mythos is moving from "preview" toward general availability. [r/singularity](https://reddit.com/r/singularity/comments/1tf6ukh/claude_mythos_has_been_spotted_in_google_vertex/) · [Forbes](https://www.forbes.com/sites/thomasbrewster/2026/05/12/ai-finds-critical-vulnerabilities-that-anthropic-mythos-missed/)

- **Orthrus vLLM/llama.cpp integration** — llama.cpp now has native MTP support (PR #22673 merged), which is a related but distinct speculative decoding approach. No Orthrus-specific integration yet. MTP uses the model's own draft heads rather than Orthrus's diffusion-attention approach.

- **NEW WATCHLIST: llama.cpp MTP production readiness** — MTP is merged but requires `--parallel 1` (no concurrent requests) and has significant PP regressions. Watch for parallel support and PP optimization in coming builds.



---
*Current Model Rankings*

Agentic Coding
_Updated: 2026-05-05_
1. *Claude Opus 4.6* — Highest peak on FoodTruck Bench agentic workload | _closed (API-only)_ | r/LocalLLaMA FoodTruck Bench
2. *GPT-5.2* — Strong agentic median, but $14/M output pricing | _closed (API-only)_ | r/LocalLLaMA FoodTruck Bench
3. *DeepSeek V4 Pro* — Matches GPT-5.2 median at 17x less cost, tightest variance | _open-weight_ | r/LocalLLaMA FoodTruck Bench
4. *Grok 4.3* — Ties DeepSeek median but wider variance, more food waste | _closed (API-only)_ | r/LocalLLaMA FoodTruck Bench
5. *Qwen 3.6 27B* — Finds bugs missed by frontier models via extended reasoning; best local option | _open-weight_ | r/LocalLLaMA user reports

Chat / Conversation
_Updated: 2026-05-05_
1. *Claude Opus 4.7* — Latest Opus, strongest overall quality | _closed (API-only)_ | Anthropic Blog
2. *GPT-5.5* — Fast, strong general chat but expensive | _closed (API-only)_ | r/LocalLLaMA community
3. *DeepSeek V4 Pro* — Frontier quality at Chinese pricing | _open-weight_ | r/LocalLLaMA FoodTruck Bench
4. *MiniMax-M2.7* — "Accessible Sonnet at home" per community consensus | _open-weight_ | r/LocalLLaMA Best Local LLMs Apr 2026
5. *Qwen 3.6 27B* — Strong reasoning, multimodal, runs on single 48GB GPU | _open-weight_ | r/LocalLLaMA