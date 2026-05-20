---
layout: post
title: "AI News Briefing — 2026-05-20"
date: 2026-05-20
---

# AI Daily Briefing — May 20, 2026

---

### 1. New Models & Benchmarks

- **Gemini 3.5 Flash released (GA)** — 1M input / 65K output tokens, model ID `gemini-3.5-flash`, knowledge cutoff Jan 2025. Skipped preview, straight to GA. **Pricing is controversial:** $1.50/$9 per 1M input/output tokens — 3x more than previous Flash, 30x more than 1.5 Flash. Artificial Analysis scores it at **55 intelligence** vs Gemini 3.1 Pro's **57**, while costing more in their benchmark ($1,552 vs $892). Cursor evals suggest it's mediocre at coding. Closed. [Google Blog](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-5/) · [Simon Willison](https://simonwillison.net/2026/May/19/gemini-35-flash/#atom-everything) · [Artificial Analysis data via r/singularity](https://reddit.com/r/singularity/comments/1thvfxo/gemini_35_flash_looks_worse_than_it_seems_on/)

- **Gemini Omni launched at Google I/O** — Native multimodal model with video generation and editing built in. Early demos show strong video editing capabilities (style transfer, object replacement, lip-sync). No standalone API pricing yet. Closed. [Google DeepMind](https://deepmind.google/models/gemini-omni/) · [HN discussion](https://news.ycombinator.com/item?id=44030000)

- **Qwen 3.7 Max benchmarked by Artificial Analysis** — Sits at 5th place, on par with GPT-5.4 (xhigh), above Gemini 3.5 Flash. The 27B/35B open-weight versions are still unreleased. Closed (Max only). [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tie6gy/qwen37_max_scored_by_artificial_analysis_27b35b/)

- **NVIDIA Nemotron-Labs-Diffusion (3B/8B/14B)** — Tri-mode model supporting AR, diffusion-based parallel decoding, and self-speculation in a single model. Key claim: **5.9x tokens per forward vs Qwen3-8B (no MTP)** at same accuracy. 850 tok/s on GB200 (8B), 112 tok/s on DGX Spark. Includes vision-language variants. Open-weight. [HuggingFace](https://huggingface.co/nvidia/Nemotron-Labs-Diffusion-VLM-8B) · [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1thv6du/nemotronlabsdiffusion_from_nvidia/)

- **OlmoEarth v1.1** — More efficient family from Allen AI. Incremental improvement. Open-weight. [HuggingFace Blog](https://huggingface.co/blog/allenai/olmoearth-v1-1)

---

### 2. Framework & Tooling Updates

- **LM Studio 0.4.14 Build 2 adds MTP Speculative Decoding** — Requires llama.cpp engine 2.15.0. Must manually enable MTP in model load parameters before loading. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1ti99an/lm_studio_finally_added_support_for_mtp/)

- **Gemini CLI will stop working June 18, 2026** — Google is transitioning to Antigravity CLI. If you have Gemini CLI in any automation, migrate now. [Google Developers Blog](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/)

- **Ettin Reranker Family released** — New reranker models on HuggingFace. Relevant if you're building RAG pipelines. [HuggingFace Blog](https://huggingface.co/blog/ettin-reranker)

- **rtk — CLI proxy reducing LLM token consumption by 60-90%** — Single Rust binary, zero dependencies. Sits between your dev tools and LLM APIs to compress common CLI output before sending to the model. 704 GitHub stars today. [GitHub](https://github.com/rtk-ai/rtk)

- **Google AI Edge Gallery v1.0.13-14** — Gemma 4 Multi-Token Prediction, Pixel TPU support, experimental MCP, chat history persistence. [GitHub](https://github.com/google-ai-edge/gallery/releases)

- **llm-gemini 0.32** — Simon Willison's LLM plugin adds `gemini-3.5-flash` model support. [Simon Willison](https://simonwillison.net/2026/May/19/llm-gemini-2/#atom-everything)

---

### 3. Infrastructure & Deployment

- **DeepSeek-V4 running on 4x RTX 2080 Ti for under $2,500** — Custom Turing CUDA kernels with W8A8 quantization achieve 255 prefill tok/s. Uses heterogeneous inference across 44GB VRAM + 1TB system RAM. Impressive proof-of-concept for budget MoE serving. Fully open-sourced with tech report. [GitHub](https://github.com/lvyufeng/deepseek-v4-2080ti) · [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1ti5sxu/running_deepseekv4_locally_with_4x_legacy_rtx/)

- **Intel Crescent Island PCB leaks: 160GB LPDDR5X** — Xe3P data center GPU bypasses HBM shortage with 20x 8GB LPDDR5X modules. Estimated 704-760 GB/s bandwidth. Worth watching for future local inference. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1thxig9/intels_crescent_island_pcb_leaks_showing_a/)

- **Cerebras running Kimi K2.6 (trillion-parameter MoE) at 1,000 tok/s** — Enterprise deployment. Shows Cerebras hardware scaling to truly massive MoE models. [Cerebras Blog](https://www.cerebras.ai/blog/cerebras-kimi-k2-Enterprise) · [r/singularity](https://reddit.com/r/singularity/comments/1thw41i/cerebras_is_running_a_trillion_parameter_model/)

- **Forge: guardrails take 8B local model from 53% to 99% on agentic tasks** — Open-source reliability layer for self-hosted LLM tool-calling. Peer-reviewed (ACM CAIS '26): Ministral 8B + Forge (99.3%) outperforms Claude Sonnet without Forge (87.2%). Adds retry nudges, step enforcement, error recovery, VRAM-aware context management. [GitHub](https://github.com/antoinezambelli/forge) · [HN](https://news.ycombinator.com/item?id=44030000)

- **NVIDIA Nemotron self-speculation as MTP alternative** — 3x higher acceptance length and 2.2x speedup vs Qwen3-8B-Eagle3 in SGLang. Moves generation from memory-bound to compute-bound. Worth evaluating if you serve 8B-14B models. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1thv6du/nemotronlabsdiffusion_from_nvidia/)

---

### 4. Industry Moves

- **Andrej Karpathy joins Anthropic** — Major talent acquisition. Previously co-founded OpenAI, led Tesla AI. Broad consensus this is a significant win for Anthropic. [Twitter](https://twitter.com/karpathy/status/2056753169888334312) · [Axios](https://www.axios.com/2026/05/19/anthropic-openai-karpathy-andrej-claude) · [HN](https://news.ycombinator.com/item?id=44030000)

- **Mistral AI acquires Emmi AI** — Details sparse, but 261 HN points with 76 comments suggests significant interest. Expands Mistral's capabilities. [Emmi AI](https://www.emmi.ai/news/mistral-ai-acquires-emmi-ai)

- **KPMG integrates Claude across 276,000-person workforce** — Strategic alliance with Anthropic for core business operations. Follows the trend of Claude overtaking ChatGPT in enterprise (previously reported). [Anthropic Blog](https://www.anthropic.com/news/anthropic-kpmg)

- **OpenAI adopts Google's SynthID watermark** — Also launching a verification tool for AI-generated media. Content Credentials integration. [OpenAI Blog](https://openai.com/index/advancing-content-provenance)

- **X open-sources its Grok-powered feed algorithm** — 187 files, 18,000 lines of code. The recommendation system black box is now inspectable. [Towards AI](https://pub.towardsai.net/x-open-sourced-its-feed-algorithm-powered-by-grok-e5a13d67e741?source=rss----98111c9905da---4)

- **Google Antigravity 2.0 demonstrated at I/O** — Agentic coding platform built 93 parallel sub-agents to create a working OS from scratch in 12 hours for under $1K. Marketing demo, but shows Google's bet on agent-first development. [r/singularity](https://reddit.com/r/singularity/comments/1thug7n/googles_antigravity_20_creates_an_operating/) · [Google Blog](https://blog.google/innovation-and-ai/sundar-pichai-io-2026/)

- **Railway blocked by Google Cloud (resolved)** — GCP suspended Railway's account, causing outage. Cautionary tale for single-cloud dependency. [Railway Blog](https://blog.railway.com/p/incident-report-may-19-2026-gcp-account-outage)

---

### 5. Research Highlights

- **Nemotron-Labs-Diffusion: Self-Speculation via Diffusion Drafting** — Same model does diffusion-based parallel drafting + AR verification with shared KV cache. Practical implication: potentially replaces MTP as the dominant speculative decoding approach. 5.9x tokens per forward pass. [HuggingFace model card](https://huggingface.co/nvidia/Nemotron-Labs-Diffusion-VLM-8B)

- **Carbon: DNA Foundation Models (HuggingFace)** — 3B model matching Evo2-7B SOTA while being 275x faster. Uses 6-mer tokenization and factorized loss. Not directly relevant to coding, but demonstrates that LLM training techniques transfer to biology. [GitHub tech report](https://github.com/huggingface/carbon/blob/main/tech-report.pdf) · [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1thsw7b/carbon_decoding_the_language_of_life/)

---

### 6. Technology Adoption

- **Forge (guardrails for local models) — worth evaluating now** if you run local agentic workflows. The 53% → 99% improvement on 8B models is peer-reviewed across 97 configurations. The key insight: error recovery scores 0% for *every* model without retry mechanisms — this is an architectural gap, not a model gap. [GitHub](https://github.com/antoinezambelli/forge)

- **rtk (CLI token compression proxy) — worth trying** if you're spending on LLM API calls for dev tooling. 60-90% token reduction, single Rust binary. 704 stars in one day suggests strong early adoption signal. [GitHub](https://github.com/rtk-ai/rtk)

- **claude-plugins-official — Anthropic's managed plugin directory for Claude Code** is now live. If you use Claude Code, check what's available. [GitHub](https://github.com/anthropics/claude-plugins-official)

- **andrej-karpathy-skills CLAUDE.md** — A single CLAUDE.md file derived from Karpathy's observations on LLM coding pitfalls. 1,955 stars today. Drop-in improvement for Claude Code behavior. [GitHub](https://github.com/multica-ai/andrej-karpathy-skills)

---

### 7. Model Rankings Update

No ranking changes today. Key observations:

- **Gemini 3.5 Flash** (AA score: 55) does not crack top 5 for any tracked task. It scores below Gemini 3.1 Pro (57) while costing more. Cursor evals show weak coding performance. The "Flash" branding no longer means "cheap."
- **Qwen 3.7 Max** AA data is promising (5th on AA, on par with GPT-5.4 xhigh), but the open-weight 27B/35B versions aren't released yet. Rankings will update when they are.
- **Nemotron-Labs-Diffusion** is an inference efficiency breakthrough, not a quality improvement — doesn't affect task rankings.

---

### 8. Watchlist Updates

- **RESOLVED: Google I/O 2026 (May 19)** — Happened. Gemini 3.5 Flash, Gemini Omni, Antigravity 2.0, Interactions API all launched.
- **Qwen 3.7 27B/35B release** — Still waiting. Max version benchmarked but open-weight variants not yet available.
- **NEW WATCHLIST: Gemini CLI deprecation (June 18, 2026)** — Migrate to Antigravity CLI. [Google Developers Blog](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/)
- **NEW WATCHLIST: Nemotron self-speculation in vLLM/SGLang** — Already benchmarked in SGLang. Watch for vLLM integration.
- **NEW WATCHLIST: Karpathy's impact at Anthropic** — Could accelerate Claude model development or open-source efforts.
- **Cerebras public access to GPT-5.4/5.5** — No update. Now also running Kimi K2.6 at 1000 tok/s.
- **EU AI Act enforcement (August 2, 2026)** — 74 days remaining.
- **llama.cpp MTP production readiness** — LM Studio now supports it (v0.4.14 Build 2). Getting closer to mainstream.
- **Anthropic Stainless acquisition impact** — Karpathy hire may overshadow this; no new details.



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