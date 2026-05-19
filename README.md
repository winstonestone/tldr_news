# AI News Daily Briefing — 2026-05-19

# AI Daily Briefing — May 19, 2026

---

### 1. New Models & Benchmarks

- **Gemini 3.5 confirmed by Google DeepMind employee** — spotted ahead of Google I/O today. No specs yet. [r/singularity](https://reddit.com/r/singularity/comments/1thg4n1/gemini_35_confirmed_by_google_deepmind_employee/)
- **Gemini 3.2 Flash solves IMO 2025 P6** — previously only GPT-5.5-Pro could solve this without scaffolding. Strong signal for reasoning capability in a Flash-tier model. [r/singularity](https://reddit.com/r/singularity/comments/1tgn8qt/gemini_32_flash_is_capable_of_solving_imo_2025_p6/)
- **Qwen 3.7 spotted on the Qwen website** — no details, just a placeholder. Expect imminent release given community hype. [r/singularity](https://reddit.com/r/singularity/comments/1tgpwdh/qwen_37_has_been_spotted_on_the_qwen_website/), [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tgrpqc/qwen_cant_wait_to_release_37_models/)
- **Lance by ByteDance** — 3B param Apache-2.0 unified model for image/video understanding, generation, and editing. Uses dual-stream MoE architecture. Worth watching for lightweight multimodal pipelines. [r/StableDiffusion](https://reddit.com/r/StableDiffusion/comments/1tgjrm2/lance_by_bytedance_3b_apache2_model_for_image_and/), [arXiv](https://arxiv.org/abs/2605.18678v1)

### 2. Framework & Tooling Updates

- **ik_llama.cpp beats upstream llama.cpp for Qwen3.6 27B on RTX 3090** — 72.9 tok/s decode vs ~59.5 tok/s upstream, with 156k context, q8 KV, MTP, all in 24GB VRAM. The `IQ4_KS` quant + `--merge-qkv --merge-up-gate-experts` flags are the key. Best single-3090 setup tested. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tgis7s/qwen_36_27b_on_24gb_vram_setup_backend/)
- **Quantizing MTP draft KV cache is free lunch** — `-cache-type-k-draft q8_0 -cache-type-v-draft q8_0` saves VRAM with zero quality loss (identical accept rates). Most people don't know this flag exists. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tgk9y6/quantizing_mtp_kv_cache_free_lunch/)
- **Lemonade v10.5.1** — one-command MTP + ROCm 7.13 setup for Strix Halo, plus Fedora 43 fix. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1th0z6k/lemonade_v1051_an_mtp_rocm_713_quick_start_for/), [GitHub](https://github.com/lemonade-sdk/lemonade)

### 3. Infrastructure & Deployment

- **Modal cuts inference cold starts by 40x** — combines LP (lazy provisioning), FUSE filesystem, checkpoint/restore, and CUDA-checkpoint to achieve near-instant GPU cold starts for serverless inference. Directly relevant if you serve models on Modal or similar platforms. [Hacker News](https://modal.com/blog/truly-serverless-gpus)
- **RTX 3090 power limits matter more than expected** — re-benchmarking 26 models at 200W vs 450W showed +70% to +113% throughput on dense 27-32B models. If you're running multi-GPU rigs on limited circuits, you're leaving massive performance on the table. [calebcoffie.com](https://calebcoffie.com/blog/how-much-do-power-limits-affect-llm-benchmark-tok-s)

### 4. Industry Moves

- **Anthropic acquires Stainless** — Stainless builds the auto-generated typed SDKs (Python, TypeScript, Go, etc.) that Anthropic, OpenAI, and others use for their APIs. This brings SDK generation in-house for Anthropic. Could affect third-party SDK quality for other providers long-term. [Anthropic Blog](https://www.anthropic.com/news/anthropic-acquires-stainless)
- **OpenAI + Dell: Codex goes on-premise** — enterprise partnership to bring Codex to hybrid and on-prem environments. Targets regulated industries that can't send code to external APIs. [OpenAI Blog](https://openai.com/index/dell-codex-enterprise-partnership)
- **Musk loses OpenAI lawsuit** — federal jury dismissed all claims, ruling he filed too late. This is now settled. [TechCrunch](https://techcrunch.com/2026/05/18/elon-musk-has-lost-his-lawsuit-against-sam-altman-and-openai/), [CNBC](https://www.cnbc.com/2026/05/18/musk-altman-openai-trial-verdict.html)
- **Hugging Face revives PapersWithCode** — new site at paperswithcode.co with AI-parsed leaderboards, trending papers by GitHub stars, citation counts, and harness reports for coding benchmarks like Terminal Bench. Meta's original site is no longer maintained. [r/MachineLearning](https://reddit.com/r/MachineLearning/comments/1tgmwqr/reviving_paperswithcode_by_hugging_face_p/)
- **314 npm packages compromised (Mini Shai-Hulud)** — supply chain attack. Check your dependencies. [Hacker News](https://safedep.io/mini-shai-hulud-strikes-again-314-npm-packages-compromised/)
- **RAM prices may drop in 2027 H2** — CXMT (Chinese memory maker) had 1,688% profit surge, expanding to 300k+ wafers/month, investing in HBM and DDR5. Good news for local inference long-term. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1th3r5q/memory_expert_suspects_ram_price_drop_in_2027h2/), [wccftech](https://wccftech.com/ex-samsung-chip-boss-says-chinas-dram-blitz-could-crush-the-414-ddr5-price-spike-within-a-year/)
- **Cloudflare publishes honest review of Anthropic Mythos Preview** — confirms the model chains exploit primitives like a senior researcher, but guardrails are inconsistent: same task framed differently produces different outcomes. [r/artificial](https://reddit.com/r/artificial/comments/1tgy0j4/cloudflare_just_published_what_they_found_after/)
- **Schiff proposes bill requiring data centers to pay for own power** — would shift energy costs currently subsidized by ratepayers. [r/singularity](https://reddit.com/r/singularity/comments/1tgsqd9/schiff_proposes_bill_requiring_data_centers_to/), [Bloomberg Government](https://news.bgov.com/bloomberg-government-news/schiff-proposes-bill-requiring-data-centers-to-pay-for-own-power)
- **Kilo Code data: Chinese models dominate token volume** — Step 3.5 Flash, MiniMax M2.5, and Ling-2.6-1T account for ~58% of Kilo Code's OpenRouter token usage. Price-driven, not necessarily quality-driven. [r/artificial](https://reddit.com/r/artificial/comments/1tgpqaa/tools_is_this_a_technical_victory_or_a_price_war/)

### 5. Research Highlights

- **DashAttention: differentiable adaptive sparse attention** — achieves full-attention accuracy at 75% sparsity and beats NSA/InfLLMv2 in high-sparsity regimes. Triton implementation faster than FlashAttention-3 at inference. Care about this if you're deploying long-context models. [arXiv](https://arxiv.org/abs/2605.18753v1)
- **PopPy: auto-parallelization for compound AI Python apps** — finds parallelism in Python code with heavy external calls (LLM APIs, DB queries), up to 6.4x speedup with no code changes. Directly useful for multi-step agent pipelines. [arXiv](https://arxiv.org/abs/2605.18697v1)
- **EnvFactory: scaling tool-use RL with synthetic environments** — auto-generates executable tool environments from real APIs, +15% on BFCLv3 for Qwen3 models. Relevant if you're training function-calling models. [arXiv](https://arxiv.org/abs/2605.18703v1)
- **Predictable Confabulations: factual recall scales with model size × topic frequency** — recall follows a sigmoid in log(params) + log(topic frequency), explaining 60-94% of variance. Practically: if your domain is underrepresented in training data, bigger models won't save you — you need RAG. [arXiv](https://arxiv.org/abs/2605.18732v1)

### 6. Technology Adoption

- **InsForge (open-source Heroku for coding agents)** — YC P26, Apache 2.0. One CLI install gives Claude Code/Cursor full backend control: hosting, DB, auth, storage, cron, edge functions, vector DB. Key feature: backend branching (like Neon) so agents can't destroy your DB. Early but worth tracking if you let agents deploy code. [GitHub](https://github.com/InsForge/InsForge), [Hacker News](https://news.ycombinator.com)
- **Sieve: scans AI coding tool transcripts for leaked API keys** — Cursor, Claude Code, Copilot, Cline, etc. all persist .env contents in plaintext SQLite. Sieve finds and redacts them. Mac only. Real gap that standard secret scanners miss. [Hacker News](https://apps.apple.com/us/app/sieve-secret-scanner/id6767409365?mt=12)
- **LLMCap: dollar-cap proxy for LLM API calls** — hard-stops spend at a configured limit. Simple, solves a real problem for personal/team use. [llmcap.io](https://www.llmcap.io/)
- **Pi coding agent gaining traction for local models** — only 4 tools, ~2K token system prompt, works well with Qwen 27B locally. Multiple r/LocalLLaMA users now preferring it over Claude Code/Codex CLI for local setups. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1th5t1b/favorite_agentic_coding_harness/), [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1th8a43/we_have_subagents_at_home/)
- **paperswithcode.co** — HF's revival of the original. Already has leaderboards, trending papers, citation counts, and Terminal Bench harness reports. Bookmark it. [paperswithcode.co](https://paperswithcode.co), [r/MachineLearning](https://reddit.com/r/MachineLearning/comments/1tgmwqr/reviving_paperswithcode_by_hugging_face_p/)

### 8. Watchlist Updates

- **Google I/O 2026 is TODAY (May 19)** — Gemini 3.5 confirmed, Gemini Omni (video model) expected, possible new Flash model. Watch for model specs, API pricing, and vLLM compatibility announcements. [r/singularity](https://reddit.com/r/singularity/comments/1thagv4/google_io_is_tomorrow_what_are_we_expecting/), [r/singularity](https://reddit.com/r/singularity/comments/1thg4n1/gemini_35_confirmed_by_google_deepmind_employee/)
- **NEW WATCHLIST: Qwen 3.7 release** — placeholder spotted on Qwen website. No timeline but likely imminent. [r/singularity](https://reddit.com/r/singularity/comments/1tgpwdh/qwen_37_has_been_spotted_on_the_qwen_website/)
- **NEW WATCHLIST: Anthropic Stainless acquisition impact** — monitor whether OpenAI/other providers' SDK quality changes now that Stainless is Anthropic-owned. [Anthropic Blog](https://www.anthropic.com/news/anthropic-acquires-stainless)
- **llama.cpp MTP production readiness** — MTP KV cache quantization confirmed zero-loss, ik_llama.cpp pushing 73 tok/s on single 3090. Rapidly maturing. Keep on watchlist for vLLM MTP parity.
- **EU AI Act enforcement (August 2, 2026)** — 75 days. No change.



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