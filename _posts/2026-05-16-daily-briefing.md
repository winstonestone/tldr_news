---
layout: post
title: "AI News Briefing — 2026-05-16"
date: 2026-05-16
---

# AI Daily Briefing — 2026-05-16

---

### 1. New Models & Benchmarks

- **Intern-S2-Preview released** — 35B scientific multimodal model (continued pretraining from Qwen3.5) matching the trillion-scale Intern-S1-Pro on core scientific tasks. Open-weight. Includes MTP with KL loss and CoT compression for faster inference. First open-source model with crystal structure generation + strong general capabilities. [HuggingFace](https://huggingface.co/internlm/Intern-S2-Preview)

- **Qwen3.6-35B-A3B hits 24.6% on Terminal-Bench 2.0** via the little-coder scaffold, beating Gemini 2.5 Pro on Gemini CLI (19.6%) and Qwen3-Coder-480B (23.9%). Shows small MoE models can compete on hard agentic benchmarks with the right scaffolding. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1temio0/qwen3635ba3b_and_9b_are_officially_on_the_public/) · [Terminal-Bench Leaderboard](https://www.tbench.ai/leaderboard/terminal-bench/2.0) · [little-coder GitHub](https://github.com/itayinbarr/little-coder)

- **Anthropic Mythos Preview surfaces in security research** — researchers used it to find a kernel-level macOS exploit on Apple M5 in 5 days. Separate benchmark shows Mythos got 18/41 n-day exploits vs GPT-5.5's 1/41; open-weight models scored 0. No public API yet. [x.com (exploit)](https://x.com/intcyberdigest/status/2055281844816384262) · [x.com (benchmark)](https://x.com/i/status/2055314585058693601)

- **OpenAI ships GPT-Realtime-2** — speech-to-speech model with 5 configurable reasoning levels (1.12s to 2.33s first-audio latency), parallel tool calls, and tone control. Also: GPT-Realtime-Translate (70+ input → 13 output languages) and GPT-Realtime-Whisper for transcription. All via Realtime API. [The Batch](https://charonhub.deeplearning.ai/openai-challenges-speech-to-speech-leaders/)

- **Cola-DLM (ByteDance)** — continuous latent diffusion language model combining a Text VAE with block-causal DiT prior via Flow Matching. Research-stage; Apache 2.0. Not practical for serving yet but architecturally novel. [HuggingFace](https://huggingface.co/ByteDance-Seed/Cola-DLM) · [arXiv](https://arxiv.org/abs/2605.06548)

---

### 2. Framework & Tooling Updates

- **Anthropic publishes `anthropics/skills` repo** — 689 GitHub stars on day one. Public repository of agent skills for Claude-based workflows. [GitHub](https://github.com/anthropics/skills)

- **Anima being added to HuggingFace diffusers** — PR open for native support, which should unlock OneTrainer compatibility. Primarily relevant if you work with video/image generation pipelines. [GitHub PR](https://github.com/huggingface/diffusers/pull/13732)

---

### 3. Infrastructure & Deployment

- **Orthrus: 7.8× tokens/forward on Qwen3-8B with frozen backbone** — injects a trainable diffusion attention head that projects 32 tokens in parallel; AR head verifies. Output distribution is provably identical. No external drafter, no separate KV cache, zero TTFT penalty. Acceptance length 11.7 vs EAGLE-3's 3.5. Weights available for Qwen3 1.7B/4B/8B. [arXiv](https://arxiv.org/abs/2605.12825) · [GitHub](https://github.com/chiennv2000/orthrus) · [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1te5xpu/orthrusqwen38b_up_to_78tokensforward_on_qwen38b/)

- **4×RTX 3090 vLLM v0.20.2 efficiency benchmarks** — running Qwen3.6-27B FP16 at TP=4. Sweet spot at 220W/GPU: 27 tok/s output, 220 tok/s prefill, 1.13 tok/joule. Going above 250W gives negligible throughput gain. Useful reference if you're building multi-3090 rigs. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1te9o18/finding_the_4x_3090_sweet_spot/)

- **Luce Megakernel** — claims 1.8× speed over standard llama.cpp CUDA by avoiding CPU dispatches at layer boundaries (~100 kernel launches per token normally). Companion to DFlash/PFlash. Discussion suggests it's significant for power efficiency on multi-GPU setups but needs independent validation. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tecfxm/luce_megakernal_why_nobody_is_taking_about_this/)

- **Microsoft Research: "LLMs Corrupt Your Documents When You Delegate"** — chained transformation-and-inversion tasks show models accumulate fidelity degradation over repeated edits. Clarification post: this is a diagnostic for delegation patterns, not a claim against using AI. Practically: add verification loops in long-horizon agentic workflows. [Microsoft Research Blog](https://www.microsoft.com/en-us/research/blog/further-notes-on-our-recent-research-on-ai-delegation-and-long-horizon-reliability/)

---

### 4. Industry Moves

- **China blocks Meta's $2.5B acquisition of Manus** — China's economic regulator killed the deal despite Manus having relocated to Singapore. Upends the "build in China, sell from Singapore" strategy for AI startups. [The Batch / AP News](https://charonhub.deeplearning.ai/china-nixes-meta-manus-tie-up/)

- **U.S. NIST announces pre-deployment AI model evaluation** — new multi-agency task force will assess national-security risks (cyber, bio, chemical) before release. Leading AI companies agreed to submit models. White House considering an executive order requiring pre-deployment approval. [The Batch](https://charonhub.deeplearning.ai/us-to-evaluate-upcoming-models/)

- **Databricks adopts GPT-5.5 for enterprise agent workflows** — set new SOTA on OfficeQA Pro benchmark. [OpenAI Blog](https://openai.com/index/databricks)

- **ChatGPT adds personal finance with Plaid bank account integration** — Pro users in U.S. only. Securely connects financial accounts for AI-powered insights. [OpenAI Blog](https://openai.com/index/personal-finance-chatgpt) · [Hacker News](https://firethering.com/chatgpt-bank-account-plaid-openai/)

- **Frontier AI has broken the open CTF format** — AI performance now dominates capture-the-flag competitions, forcing the competitive security community to rethink the format. [Hacker News](https://kabir.au/blog/the-ctf-scene-is-dead)

- **Amazon workers under pressure to increase AI usage are making up tasks** — internal mandate backfiring. [Fast Company](https://www.fastcompany.com/91541586/amazon-workers-pressured-to-up-ai-use-extraneous-tasks)

---

### 5. Research Highlights

- **Orthrus: Diffusion-attention speculative decoding** — 7.8× TPF with frozen backbone, provably identical output. Eliminates the external drafter model entirely. Developer implication: if this gets vLLM/llama.cpp integration, it could meaningfully cut serving costs for Qwen3 models. [arXiv:2605.12825](https://arxiv.org/abs/2605.12825)

- **Self-Guided Self-Play (SGS)** — solves the Conjecturer collapse problem in LLM self-play by having the model itself guide problem quality. A 7B model after 200 rounds of self-play solves more Lean4 theorems than a 671B model at pass@4. Developer implication: practical path to strong math/reasoning from small models without massive compute. [arXiv:2604.20209](https://arxiv.org/abs/2604.20209) · [GitHub](https://github.com/LukeBailey181/sgs)

- **Architecture-aware scaling laws (Amazon/ICLR)** — two models with identical param counts can differ by 40% in inference throughput depending on hidden size and attention/MLP ratio. Provides a framework for optimizing architecture choices at fixed compute budgets. [Amazon Science](https://www.amazon.science/blog/making-llms-faster-without-sacrificing-accuracy)

---

### 6. Technology Adoption

- **Equibles: self-hosted MCP server for U.S. financial data** — serves SEC filings, 13F holdings, insider/congressional trades, FRED indicators, and more as MCP tools. No API keys, no cloud dependency. Worth evaluating if you're building financial agents with Claude Code or local models. [GitHub](https://github.com/daniel3303/Equibles)

- **little-coder agentic scaffold** — lightweight orchestrator that pushed Qwen3.6-35B-A3B to 24.6% on Terminal-Bench 2.0, above much larger models. Worth evaluating if you run small local models for agentic coding tasks. [GitHub](https://github.com/itayinbarr/little-coder)

---

### 8. Watchlist Updates

- No updates on existing watchlist items today.
- **NEW WATCHLIST: Anthropic Mythos Preview** — demonstrated extraordinary cybersecurity capability (18/41 n-day exploits vs 1/41 for GPT-5.5). No public API yet. Watch for general availability and pricing.
- **NEW WATCHLIST: Orthrus vLLM/llama.cpp integration** — 7.8× speedup with identical output is compelling, but currently Qwen3-only with custom inference code. Integration into mainstream serving frameworks would be the unlock.
- **NEW WATCHLIST: U.S. pre-deployment AI model evaluation mandate** — could slow frontier model releases if executive order materializes.



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