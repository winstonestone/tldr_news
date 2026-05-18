---
layout: post
title: "AI News Briefing — 2026-05-18"
date: 2026-05-18
---

# Daily AI Briefing — 2026-05-18

---

### 1. New Models & Benchmarks

- **Gemma-4-Gembrain-31B-it-uncensored-heretic released** — community merge of multiple Gemma 4 31B finetunes targeting creative prose and reduced refusals (13/100). Open-weight, available in safetensors and GGUF. Niche creative-writing model, not a general-purpose upgrade. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tg7s7j/gemma4gembrain31bituncensoredheretic_is_out_now_a/) | [HuggingFace](https://huggingface.co/llmfan46/Gemma-4-Gembrain-31B-it-uncensored-heretic)

- **Google I/O 2026 is tomorrow (May 19)** — Gemini 4, Android 17, and possibly new AI glasses expected to be announced. Worth watching for model releases and API changes. [Towards AI](https://pub.towardsai.net/google-i-o-2026-everything-google-is-about-to-announce-on-may-19-df54edefe634?source=rss----98111c9905da---4)

- **Cerebras CFO confirms GPT-5.4 and GPT-5.5 running internally on Cerebras chips** — public access "coming soon." If true, Cerebras-speed inference on frontier models would be significant. [r/singularity](https://reddit.com/r/singularity/comments/1tftg9h/cerebras_cfo_says_they_are_currently_running/) | [CNBC](https://www.cnbc.com/video/2026/05/14/the-years-largest-ipo-acerebras-joins-the-hottest-trade-in-ai.html)

---

### 2. Framework & Tooling Updates

- **llama.cpp b9200 released — fixes MTP memory traffic overhead** — avoids copying full logits during prompt decode in MTP, directly improving prompt processing speed. Combined with tuned MTP flags (`--spec-draft-n-max 3`, `--parallel 1`, drop `--spec-draft-p-min`), agent workflows on a single RTX 3090 with Qwen3.6-27B jumped from ~7-8 t/s to significantly better throughput and draft acceptance rates. [PR #23198](https://reddit.com/r/LocalLLaMA/comments/1tft1il/llama_avoid_copying_logits_during_prompt_decode/) | [b9200 benchmarks](https://reddit.com/r/LocalLLaMA/comments/1tg6j9u/benchmarking_the_new_b9200_update_optimizing_qwen/)

- **llama.cpp dual-GPU tensor parallelism now works with quantized KV caches** — community fork fixes `--split-mode tensor` to support q8_0 KV caches. On 3060+4070 Super (24GB combined), Qwen3.6-27B-Q4_K_M gets 30 t/s generation (up from 21 t/s without tensor split) and 545 t/s prompt processing. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tflngz/dual_gpu_llamacpp_speedup/) | [GitHub fork](https://github.com/RedToasty/llama.cpp_qts)

- **ROCm 7.13 tech preview released with Strix Halo optimizations** — new optimizations specifically for Ryzen AI Max 300 "Strix Halo" APUs, plus ROCprof Trace Decoder is now open-source. Available via TheRock on GitHub. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tftg09/rocm_713_nightly_adds_strix_halo_optimizations/) | [Phoronix](https://www.phoronix.com/news/ROCm-7.13-Released) | [Release notes](https://rocm.docs.amd.com/en/7.13.0-preview/about/release-notes.html)

- **Semble: code search MCP server using 98% fewer tokens than grep** — combines static embeddings (potion-code-16M) with BM25, runs on CPU. 0.854 NDCG@10 (99% of a 137M transformer), ~250ms indexing, ~1.5ms per query. Drop-in for Claude Code, Cursor, Codex, OpenCode. Install: `claude mcp add semble -s user -- uvx --from "semble[mcp]" semble`. [Hacker News](https://github.com/MinishLab/semble)

---

### 3. Infrastructure & Deployment

- **vLLM dominates mixed-GPU pipeline parallelism** — on a 7-GPU Blackwell/Ada cluster (RTX PRO 6000 + PRO 5000 + 5090s + modded 4090s), vLLM outperformed llama.cpp by 4-6x on long-context prefill. SGLang nearly matched vLLM on pure Blackwell but **crashes when mixing Ada cards** (no FP4 software fallback). vLLM handles uneven GPU splits seamlessly via `VLLM_PP_LAYER_PARTITION`. MiniMax-M2.7 at 82k tokens: vLLM 6,212 t/s vs llama.cpp 1,065 t/s on 6 mixed GPUs. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tg4mw0/benchmarking_vllm_vs_sglang_vs_llamacpp_on_a/)

- **M5 Mac vs DGX Spark vs Strix Halo vs RTX 6000 — standardized benchmarks published** — maxed M5 aggressively outperforms DGX Spark (2x+ memory bandwidth: ~600 vs ~256 GB/s). RTX 6000 (~1,800 GB/s) still leads on raw tok/s. EVO X2 has thermal issues on extended runs; M5 MacBook holds at ~80°C but sounds like a "blow dryer." More backends being added. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tfzsd6/m5_vs_dgx_spark_vs_strix_halo_vs_rtx_6000/)

- **Apple silicon costs more per-token than OpenRouter** — analysis confirms local inference on Apple hardware is currently more expensive, unless you factor in privacy, hardware reuse, or the risk that OpenRouter providers are burning investor cash on subsidized pricing (which won't last). [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tg0y2h/apple_silicon_costs_more_than_openrouter_an/)

---

### 4. Industry Moves

- **Claude overtakes ChatGPT in business adoption for the first time** — Anthropic's annualized revenue crossed $30B (up from ~$9B end of 2025), surpassing OpenAI's ~$24-25B. 8 of Fortune 10 are Claude customers. More U.S. businesses paid for Claude than ChatGPT in April 2026. [r/artificial](https://reddit.com/r/artificial/comments/1tg1at4/for_the_first_time_in_years_chatgpt_falls_to/) 

- **EU AI Act full enforcement starts August 2, 2026 (75 days)** — applies to any team serving EU clients regardless of company location. High-risk systems (credit scoring, recruitment, healthcare triage) need decision logging, 6-month retention, bias testing docs. Fines up to €35M or 7% global turnover. [r/artificial](https://reddit.com/r/artificial/comments/1tgf0gm/eu_ai_act_enforcement_starts_in_75_days_affects/)

- **Uber struggling with Anthropic AI costs despite $3.4B spend** — CTO cites budget challenges scaling Claude across the organization. A cautionary signal on enterprise AI cost control. [r/singularity](https://reddit.com/r/singularity/comments/1tg4l4l/ubers_anthropic_ai_push_hits_a_wallcto_says/) | [Yahoo Finance](https://finance.yahoo.com/sectors/technology/articles/ubers-anthropic-ai-push-hits-223109852.html)

- **GPT-5.5 autonomously ran 150+ hours improving protein folding models** — notable demonstration of long-horizon autonomous research by a frontier model. [r/singularity](https://reddit.com/r/singularity/comments/1tg7w59/gpt55_autonomously_spent_150_hours_improving/)

- **Florida enacts data center restrictions** — new law shields residents from water and energy costs driven by data center expansion. Could affect AI infrastructure buildout in the state. [r/singularity](https://reddit.com/r/singularity/comments/1tfc48i/florida_law_enacts_data_center_restrictions_to/) | [Substack](https://centralflorida.substack.com/i/197170843/desantis-enacts-data-center-restrictions-to-shield-residents-from-water-energy-costs)

---

### 5. Research Highlights

- **Argus: evidence assembly for scalable deep research agents** — Searcher+Navigator architecture treats deep research as assembling complementary evidence pieces rather than parallel brute-force. 35B-A3B MoE backbone reaches 86.2 on BrowseComp with 64 searchers, beating proprietary agents. Navigator context stays under 21.5K tokens. [arxiv.org/abs/2605.16217v1](https://arxiv.org/abs/2605.16217v1) — *Directly applicable architecture pattern for building research agents with small models.*

- **FORGE: self-evolving agent memory via population broadcast, no weight updates** — evolves prompt-injected natural-language memory for ReAct agents. Improves returns 1.7-7.7x over zero-shot across four LLM families. Weaker models benefit disproportionately. [arxiv.org/abs/2605.16233v1](https://arxiv.org/abs/2605.16233v1) — *Practical technique for improving agent performance without fine-tuning.*

- **Formal methods for LLM compliance monitoring (LTL-based)** — proposes auditing and runtime monitoring of LLM behavioral constraints using Linear Temporal Logic. Small-model labelers match or exceed frontier LLM judges for violation detection. Intervening monitors reduce violation rates while preserving task performance. [arxiv.org/abs/2605.16198v1](https://arxiv.org/abs/2605.16198v1) — *Relevant with EU AI Act in 75 days; concrete technique for compliance monitoring.*

- **Probabilistic Chunk Masking (PCM) for VLA RL** — 2.38x wall-clock speedup over standard GRPO by backpropagating through <20% of trajectory chunks, targeting only phases where successful/failed rollouts diverge. [arxiv.org/abs/2605.16154v1](https://arxiv.org/abs/2605.16154v1) — *Gradient efficiency technique potentially applicable to broader RL fine-tuning.*

- **Layer Equivalence: how you test redundancy changes what you find** — replacement vs interchange swap-KL probes can disagree by several-fold on which layers are safe to prune. At 8B scale, Qwen3-8B and Llama-3.1-8B behave very differently. [arxiv.org/abs/2605.16234v1](https://arxiv.org/abs/2605.16234v1) — *If you're pruning layers for inference speed, test with both protocols.*

---

### 6. Technology Adoption

- **Semble (MCP code search) — worth adopting now** — if you use Claude Code or Cursor on large codebases, this is a direct upgrade over grep-based code search. Zero config, CPU-only, 98% token reduction. The 0.854 NDCG@10 is solid. Install is one command. [GitHub](https://github.com/MinishLab/semble)

- **SmallCode: coding agent designed for small local models (4B params, 87% benchmark)** — uses compound tools, improvement loops, decompose-on-failure, and optional cloud escalation. Interesting scaffold if you want to run coding agents on consumer hardware. Not yet battle-tested at scale. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tgecrq/i_built_a_coding_agent_that_gets_87_on_benchmarks/)

- **Shannon: autonomous AI pentester (white-box)** — analyzes source code, identifies attack vectors, executes real exploits. 200 GitHub stars today. Worth evaluating if you need automated security testing, but verify it against your own stack before trusting results. [GitHub](https://github.com/KeygraphHQ/shannon)

- **Hermes Agent vs Claude Code vs OpenClaw comparison on 18 real tasks** — Towards AI published a head-to-head. Worth reading if you're evaluating agent options. [Towards AI](https://pub.towardsai.net/i-tested-hermes-agent-vs-claude-code-vs-openclaw-on-18-real-tasks-the-10-week-old-one-cheats-by-0f2881a10213?source=rss----98111c9905da---4)

- **Abliterlitics: 85 GPU-hours comparing 5 abliteration methods on Qwen3.6-27B** — rigorous open-source toolkit. Heretic and Huihui preserve capabilities best; AEON's "enhanced capabilities" claim contradicted by data; Abliterix worst for capability preservation. Useful reference if you use uncensored models. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tfmocw/85_gpuhours_comparing_5_abliteration_methods_on/) | [HuggingFace](https://huggingface.co/DreamFast/Qwen3.6-27B-Uncensored-HauhauCS-Aggressive-Safetensor-Benchmark)

---

### 8. Watchlist Updates

- **llama.cpp MTP production readiness** — b9200 is a meaningful step forward. The logits-copying fix directly addresses MTP memory overhead. Community benchmarks show default MTP flags are suboptimal for agent workflows; tuned settings (`--spec-draft-n-max 3`, single slot, no p-min) dramatically improve draft acceptance. MTP is becoming usable for production agent serving on consumer GPUs. Not yet resolved, but progressing. [PR #23198](https://reddit.com/r/LocalLLaMA/comments/1tft1il/llama_avoid_copying_logits_during_prompt_decode/) | [b9200 benchmarks](https://reddit.com/r/LocalLLaMA/comments/1tg6j9u/benchmarking_the_new_b9200_update_optimizing_qwen/)

- **Orthrus vLLM/llama.cpp integration** — no new updates today.

- **Anthropic Mythos Preview** — no new updates today.

- **U.S. pre-deployment AI model evaluation mandate** — no new updates today.

- **NEW WATCHLIST: Google I/O 2026 (May 19)** — Gemini 4 and potentially new model APIs expected tomorrow. Could affect model rankings across multiple tasks.

- **NEW WATCHLIST: Cerebras public access to GPT-5.4/5.5** — CFO says "coming soon." If realized, frontier-model inference at Cerebras speeds would reshape the serving landscape.

- **NEW WATCHLIST: EU AI Act enforcement (August 2, 2026)** — 75 days out. Any team serving EU clients with high-risk AI systems needs logging, documentation, and bias testing in place.



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