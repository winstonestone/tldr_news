---
layout: post
title: "AI News Briefing — 2026-05-25"
date: 2026-05-25
---

# Daily AI Briefing — 2026-05-25

---

### 1. New Models & Benchmarks

- **MiMo-V2.5-coder released** — a 128GB model positioned as an alternative to Qwen3.6 and DeepSeek V4 for coding, with "reliable tool calling." Community release, no formal benchmarks yet. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tn3455/mimov25coder/)

- **BitCPM-CANN: 1.58-bit ternary QAT models up to 8B** — trained on Ascend NPU, retains 95.7–97.2% of full-precision MiniCPM4 performance at 1B/3B/8B scale across 11 benchmarks. Up to 8x weight memory reduction at inference. Only 4.5% training throughput overhead. Open-weight. Niche hardware (Ascend), but validates extreme quantization-aware training at scale. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tmf63y/bitcpmcann_native_158bit_large_language_model/) | [Paper](https://github.com/OpenBMB/MiniCPM/blob/main/docs/BitCPM_CANN.pdf)

---

### 2. Framework & Tooling Updates

- **llama.cpp PR #22929: checkpoint fix for agentic coding** — fixes full prompt re-processing triggered by context-rewriting tools (like opencode). After this patch, llama.cpp only reprocesses what actually changed instead of the entire 70k+ token context. Significant responsiveness improvement for agentic coding workflows. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tn0jyp/server_fix_checkpoints_creation_by_jacekpoplawski/)

- **hipEngine: ROCm-native inference engine for AMD RDNA3** — new open-source (AGPLv3) engine from shisa-ai targeting 7900 XTX and Strix Halo. No PyTorch dependency on the hot path. Benchmarks show hipEngine with ParoQuant beating llama.cpp HIP on prefill at all context lengths (512–128K), while llama.cpp Vulkan still leads on decode. Worth watching if you're on AMD. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tmq4s6/hipengine_fast_native_qwen_36_inference_for_rdna3/) | [GitHub](https://github.com/shisa-ai/hipEngine)

- **Qwen3.6 27B hitting 1000 tok/s generation on V100s** — at batch 128 concurrent requests. Single-user (batch 1) gets ~80 tok/s decode and 3000 tok/s prefill, no MTP. Demonstrates that older hardware can still serve current models effectively. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tmyln6/1000_tps_generation_on_qwen36_27b_with_v100s/)

---

### 3. Infrastructure & Deployment

- **Custom C++ engine for MiniCPM-V 4.6 on Orange Pi AIPro ($149)** — bypasses torch_npu entirely, runs both text and SigLIP vision tower natively on Ascend 310B NPU. Custom AscendC kernels deliver 2x speedup (2.88 → 5.90 tok/s FP16). Open source. Interesting proof-of-concept for budget edge VLM deployment. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tmy4g9/wrote_a_custom_c_engine_for_minicpmv_46_on_orange/) | [GitHub](https://github.com/lvyufeng/minicpm-v-4.6-orangepi)

- **768GB Intel Optane DIMMs running 1T-param Kimi K2.5 locally** — ~4 tok/s with a single GPU. Novelty hack, not practical, but demonstrates that cheap decommissioned Optane can make trillion-param models loadable on consumer-ish hardware. [r/singularity](https://reddit.com/r/singularity/comments/1tm1u3l/768gb_of_cheap_intel_optane_dimm_memory_sticks/) | [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/enthusiast-runs-1-trillion-parameter-llm-from-768gb-of-intel-optane-dimm-memory-sticks-local-kimi-k2-5-install-achieved-roughly-4-tokens-per-second)

- **NVIDIA PiD: pixel diffusion decoder replacing VAE** — plug-and-play decoder that eliminates VAE artifacts. Weights on HuggingFace. Relevant if you work with image generation pipelines. [r/StableDiffusion](https://reddit.com/r/StableDiffusion/comments/1tn3m6n/nvidia_solved_vae_fast_and_highresolution_latent/) | [Project page](https://research.nvidia.com/labs/sil/projects/pid/) | [HuggingFace](https://huggingface.co/nvidia/PiD)

---

### 4. Industry Moves

- **Anthropic releases "knowledge-work-plugins"** — open-source repo of plugins for knowledge workers to use in Claude Cowork. 550 GitHub stars on day one. Signals Anthropic pushing Claude beyond coding into general knowledge work. [GitHub](https://github.com/anthropics/knowledge-work-plugins)

- **DeepSeek Reasonix** — community-built native coding agent optimized for DeepSeek V4 with high cache hit rates and low cost. Not an official DeepSeek product. [Hacker News](https://esengine.github.io/DeepSeek-Reasonix/)

- **Memory now ~two-thirds of AI chip component costs** — Epoch AI analysis. Reinforces the memory pricing watchlist item. As memory becomes the dominant cost driver, expect continued pressure on consumer GPU pricing. [Epoch AI](https://epoch.ai/data-insights/ai-chip-component-cost-shares) (HN: 387 pts, 396 comments)

- **PapersWithCode revival by HuggingFace** — now supports multiple metrics per benchmark, external papers (not just arXiv), and paper lineage. Useful for tracking SOTA. [r/MachineLearning](https://reddit.com/r/MachineLearning/comments/1tmawv5/paperswithcode_new_features_week_1_p/) | [paperswithcode.co](http://paperswithcode.co)

---

### 5. Research Highlights

- **"Constraint Decay: The Fragility of LLM Agents in Back End Code Generation"** — shows LLM agents progressively lose adherence to constraints during multi-step backend code generation. 240 points on HN. Directly relevant if you're using agents for autonomous coding — validates the intuition that agent reliability degrades over longer tasks. [arXiv](https://arxiv.org/abs/2605.06445)

- **Google DeepMind's AI agent solved 9 of 353 open Erdős problems** — at a few hundred dollars per problem. Impressive demonstration of mathematical reasoning capability, though the practical ceiling is unclear. [r/singularity](https://reddit.com/r/singularity/comments/1tmjdru/google_deepminds_al_agent_autonomously_solved_9/)

- **Auditory prompt injection via inaudible sounds** — hidden audio in YouTube videos/podcasts can trigger AI voice assistants to execute unauthorized commands. New attack class worth knowing about if you build voice-enabled AI features. [r/singularity](https://reddit.com/r/singularity/comments/1tmb7mz/inaudible_sounds_to_humans_can_be_hidden_in/) | [CyberNews](https://cybernews.com/security/ai-voice-bots-hidden-audio-hijack-attacks/)

---

### 6. Technology Adoption

- **pi (earendil-works)** — AI agent toolkit offering coding agent CLI, unified LLM API, TUI & web UI, Slack bot, and vLLM pod support. 456 stars on first trending day. Notable that Armin Ronacher (Flask creator) is already dealing with AI-generated slop issues filed against it — a sign of real adoption. Worth evaluating as a lightweight alternative to heavier agent frameworks. [GitHub](https://github.com/earendil-works/pi) | [Armin Ronacher on slop issues](https://simonwillison.net/2026/May/24/armin-ronacher/#atom-everything)

- **cmux** — Ghostty-based macOS terminal with vertical tabs and notifications designed for running AI coding agents. 696 stars trending. If you run multiple coding agents in parallel, this addresses a real workflow pain point. macOS only. [GitHub](https://github.com/manaflow-ai/cmux)

---

### 7. Model Rankings Update

No ranking changes today. MiMo-V2.5-coder lacks trusted benchmark data. BitCPM-CANN models are impressive for their quantization approach but target niche hardware. Will update if credible third-party benchmarks appear.

---

### 8. Watchlist Updates

- **Anthropic Mythos release** — Politico article covers the "cyber models" (Mythos/5.5) and their policy impact in Washington. No new technical details or release date beyond what's already reported. Still watchlist. [Politico](https://www.politico.com/news/2026/05/24/anthropic-openai-mythos-what-to-know-00934668)

- **Memory price increases** — Epoch AI data confirms memory is now ~2/3 of AI chip costs, reinforcing upward pressure on hardware pricing. No resolution. [Epoch AI](https://epoch.ai/data-insights/ai-chip-component-cost-shares)



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