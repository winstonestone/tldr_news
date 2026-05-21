---
layout: post
title: "AI News Briefing — 2026-05-21"
date: 2026-05-21
---

# AI Daily Briefing — 2026-05-21

---

### 1. New Models & Benchmarks

- **Cohere Command A+ launched** — First MoE model from Cohere, Apache 2.0 open-weight. Nick Frosst says they prioritized efficiency: runs on 1-2 GPUs, designed for agents. No trusted benchmark data yet. Pros: Apache 2.0, efficient MoE, practical for small teams. Cons: Top-line performance acknowledged as work-in-progress, no LMSYS/AA rankings available. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tizmar/re_what_ever_happened_to_coheres_commanda_series/) | [HuggingFace](https://huggingface.co/CohereLabs/command-a-plus-05-2026-bf16)

- **Cursor Composer 2.5 ships** — Built on Moonshot's open-source Kimi K2.5, scores 79.8% on SWE-Bench Multilingual (vs GPT-5.5 at 77.8%, Opus 4.7 at 80.5%). Pricing: $0.50/$2.50 per M input/output tokens, dramatically cheaper than frontier APIs. Caveat: benchmarks are self-reported and not independently reproduced on a unified scaffold. Closed model. [The Batch](https://charonhub.deeplearning.ai/cursor-composer-undercuts-competition/)

- **Stable Audio 3 released** — Three open-weight text-to-audio models from Stability AI: Small Music, Small SFX, and Medium. Medium generates up to 6m20s audio. Small models run on CPU. Community License (free for personal/creative use). [r/StableDiffusion](https://reddit.com/r/StableDiffusion/comments/1tiq820/announcing_the_release_of_stable_audio_3/) | [HuggingFace](https://huggingface.co/stabilityai/stable-audio-3-medium) | [GitHub](https://github.com/Stability-AI/stable-audio-3)

- **HalBench: sycophancy/hallucination benchmark** — 3,200 false-premise prompts across 4 frontier models. Results (higher = more honest pushback): Sonnet 4.6 (0.565) > Grok 4.3 (0.498) > GPT-5.4 (0.381) > Gemini 3.1 Pro (0.339). Custom benchmark, not from trusted sources, but interesting signal. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tizvih/halbench_i_built_a_custom_sycophancy_and/)

- **Gemini 3.5 Flash new benchmark results** — Ranks #1 on Zapier's Automation Bench (beating all frontier models at lower cost) and scores 76.7% on SimpleBench, just 0.2% behind GPT 5.5 Pro. Neither is a tracked trusted source, but noteworthy for function-calling/agent use cases. [r/singularity (Automation)](https://reddit.com/r/singularity/comments/1tj9sqp/gemini_35_flash_ranks_1_on_automation_bench_from/) | [r/singularity (SimpleBench)](https://reddit.com/r/singularity/comments/1tir6qk/gemini_35_flash_scores_767_on_simplebench_just_02/)

---

### 2. Framework & Tooling Updates

- **llama.cpp MTP: backend sampling merged (PR #23287)** — Moves MTP draft path to backend sampling, improving MTP performance. Incremental step toward production-ready MTP. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tis73j/move_to_backend_sampling_for_mtp_draft_path_by/)

- **Gemma 4 MTP support WIP in llama.cpp** — Early work-in-progress, requires self-compilation, not expected to work yet. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tijpwl/wip_gemma_4_mtp/)

- **RTX 5080: MTP is 23% slower for 35B MoE at 128k context** — Detailed benchmarks show MTP requires `--fit-target 1536` which pushes MoE expert layers to CPU, negating the speedup. Best config: 35B Q4_K_XL without MTP — 56 tok/s gen, 1,584 tok/s prompt at 128k. MTP still helps for dense models and short contexts. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tiixql/rtx_5080_16gb_qwen36_35b_moe_at_128k_context_56/)

- **ByteShape Qwen 3.6 35B quantization study** — NTP vs MTP across RTX 4090/5090/Pro 6000/4080/5060 Ti and multiple CPUs. Key finding: larger quants often beat smaller ones on speed — don't minimize bpw blindly. MTP gives 20-40% GPU speed boost but not worth it on CPU. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tipihx/qwen_36_35b_gguf_ntp_vs_mtp_quantization_results/) | [ByteShape Blog](https://byteshape.com/blogs/Qwen3.6-35B-A3B/)

- **HuggingFace benchmark datasets now filterable by model size** — Useful for finding best model under 32B on SWE-bench Verified, etc. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tilvit/huggingface_benchmark_datasets_now_let_you_filter/) | [HuggingFace](https://huggingface.co/datasets?benchmark=benchmark:official&sort=trending)

- **torchtune paper published** — PyTorch-native post-training library. Competes with Axolotl and Unsloth, emphasizes modularity and hackability over ease-of-use. Strong performance and memory efficiency. [ArXiv](https://arxiv.org/abs/2605.21442v1)

---

### 3. Infrastructure & Deployment

- **AMD BC-250 (PS5 APU): 40 CU unlock hack** — Salvaged PS5 boards ($50-150 on eBay) with 16GB unified GDDR6. Two register writes unlock all 40 CUs from the stock 24. Results: 372 tok/s at 40 CU vs 230 at 24 CU (pp512, Vulkan). Custom HIP kernel work in progress for gfx1013. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tj4unp/amd_bc250_and_the_search_for_cheap_compute/) | [GitHub](https://github.com/duggasco/bc250-40cu-unlock)

- **AMD Ryzen AI Halo PC: $3,999 with 128GB onboard memory** — Unified memory for large model inference. Expensive but a serious local inference option. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tinl98/amd_ryzen_ai_halo_pc_will_cost_3999_with_128gb/) | [VideoCardz](https://videocardz.com/newz/amd-ryzen-ai-halo-pc-will-cost-3999-with-128gb-memory-on-board)

- **AWS secures M3 Ultra Mac Studios** — While consumer supply remains constrained, AWS is stocking up for cloud Mac instances. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tio2i5/aws_secures_rare_mac_studios_while_ordinary_apple/) | [TechRadar](https://www.techradar.com/pro/you-cant-buy-them-for-your-home-or-office-but-aws-just-snapped-up-a-host-of-apples-most-highly-desired-m3-ultra-macs)

---

### 4. Industry Moves

- **Anthropic hits profitability in Q2 2026** — $500M profit, described as "mind-blowing growth." First profitable quarter. [r/singularity](https://reddit.com/r/singularity/comments/1tj072c/anthropic_is_officially_set_to_be_profitable_as/) | [WSJ](https://www.wsj.com/tech/ai/mind-blowing-growth-is-about-to-propel-anthropic-into-its-first-profitable-quarter-7edbf2f4)

- **Anthropic-SpaceX: $1.25B/month through May 2029** — SpaceX S-1 filing reveals Anthropic is paying $15B/year for compute across Colossus 1 and Colossus 2 (GB200s). That's nearly half Anthropic's ARR. 90-day termination clause. [Simon Willison](https://simonwillison.net/2026/May/20/spacex-s1/#atom-everything) | [r/singularity](https://reddit.com/r/singularity/comments/1tj3csv/anthropic_is_paying_spacex_15_billion_per_year/) | [Axios](https://www.axios.com/2026/05/20/anthropic-spacex-compute)

- **OpenAI IPO filing imminent** — WSJ reports filing may come as soon as Friday. [r/singularity](https://reddit.com/r/singularity/comments/1tiwszc/openai_ipo_filing_may_come_as_soon_as_friday_wsj/) | [Barron's](https://www.barrons.com/articles/openai-ipo-chatgpt-dd8ef35b)

- **OpenAI model disproves 80-year-old Erdős unit-distance conjecture** — General-purpose reasoning model found a counterexample to the conjectured upper bound. Proof reviewed by mathematicians. No model name, sampling details, or compute budget disclosed. Impressive if reproducible, but process transparency is lacking. [OpenAI Blog](https://openai.com/index/model-disproves-discrete-geometry-conjecture/) | [r/MachineLearning](https://reddit.com/r/MachineLearning/comments/1tiy6s4/openai_claims_a_generalpurpose_reasoning_model/)

- **Meta lays off 8,000 (~10% workforce)** — Three-wave global purge, emails sent at 4 AM local time per region. [r/singularity](https://reddit.com/r/singularity/comments/1tiosgg/mark_zuckerbergs_meta_kicks_off_major_bloodbath/)

- **Intuit lays off 3,000+** — Refocusing on AI. [Hacker News](https://techcrunch.com/2026/05/20/intuit-to-lay-off-over-3000-employees-to-refocus-on-ai/)

- **Midjourney says TPUs set them back a year** — Regrets not sticking with NVIDIA. Signal for anyone evaluating TPU vs GPU for production workloads. [r/singularity](https://reddit.com/r/singularity/comments/1tiut2d/midjourney_says_their_research_was_set_back_by_a/)

- **Sam Altman offers YC founders $2M in OpenAI tokens for equity** — API credits as investment currency. [r/singularity](https://reddit.com/r/singularity/comments/1titl6z/sam_altman_offers_yc_founders_2_million_in_openai/) | [The Information](https://www.theinformation.com/briefings/sam-altman-offers-yc-founders-2-million-openai-tokens-equity)

---

### 5. Research Highlights

- **RELEX: 85% less RLVR training via rank-1 extrapolation** — RLVR weight trajectories are extremely low-rank. Observe 15% of training steps, extrapolate the rest with linear regression on a rank-1 subspace. Matches or beats full RLVR on in-domain and OOD benchmarks. Why care: dramatically cheaper reasoning model training. [ArXiv](https://arxiv.org/abs/2605.21468v1)

- **Agent JIT Compilation: 10.4x speedup for web agents** — Compiles task descriptions into executable code with parallelization instead of sequential screenshot-execute loops. +28% accuracy over Browser-Use. Why care: directly applicable pattern for building faster computer-use agents. [ArXiv](https://arxiv.org/abs/2605.21470v1)

- **Formal Verification Gates for AI Coding Loops** — Structural backpressure (formal verification as a gate in agentic coding loops) beats just using smarter agents. Why care: practical pattern for improving agentic code quality without switching models. [Hacker News](https://reubenbrooks.dev/blog/structural-backpressure-beats-smarter-agents/)

---

### 6. Technology Adoption

- **ggufy: single-binary image model quantization tool** — Written in Zig, supports GGUF/safetensors conversion, all major datatypes (q3_k through nvfp4). CLI + GUI, cross-platform, RAM-efficient. Worth trying if you quantize diffusion/image models regularly. [r/StableDiffusion](https://reddit.com/r/StableDiffusion/comments/1tj5nhq/ggufy_easy_quantization_for_the_gpu_poor/) | [GitHub](https://github.com/qskousen/ggufy)

- **oh-my-pi: coding agent trending on GitHub** — Terminal-based coding agent with hash-anchored edits, LSP integration, subagents. 270 stars today. Early but gaining traction alongside Pi. [GitHub](https://github.com/can1357/oh-my-pi)

- **Pixal3D switches to MIT license** — Tencent's 3D generation model now MIT-licensed, enabling EU commercial use. Multiview mode coming. [r/StableDiffusion](https://reddit.com/r/StableDiffusion/comments/1tjdig5/pixal3d_changed_to_mit_license/) | [GitHub](https://github.com/TencentARC/Pixal3D)

- **Agentic harness comparison: same model, different results** — Qwen3.6 27B tested across GitHub Copilot, Pi, Claude Code, and OpenCode. OpenCode delivered best webdev results (can search internet). Copilot took 13 LLM requests vs 4 for others on the same task due to tool schema issues. Reinforces that harness matters as much as model. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tjbhjk/same_task_in_githubcopilot_pi_claudecode_and/)

---

### 8. Watchlist Updates

- **Qwen 3.7 27B/35B release** — Qwen team confirmed "another 27B" is coming with high probability, waiting on exact roadmap. Community anticipation is high. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tiwnpc/qwen_will_release_another_27b_with_high/)
- **llama.cpp MTP production readiness** — Backend sampling PR merged (#23287), Gemma 4 MTP WIP started. Progressing but MTP tradeoffs are becoming clearer: helps dense models on GPU, hurts MoE at long context when VRAM-constrained. Not production-ready for all configurations yet.
- **Anthropic Stainless acquisition impact** — Anthropic's $15B/year SpaceX compute deal and Q2 profitability suggest aggressive scaling. Colossus 2 (GB200) access is new.
- **Karpathy's impact at Anthropic** — No new updates today.
- **NEW WATCHLIST: OpenAI IPO filing** — Expected as soon as Friday. Will affect API pricing strategy and competitive dynamics.
- **NEW WATCHLIST: Cohere Command A+ community benchmarks** — Apache 2.0 MoE model just dropped; waiting for independent benchmark results from trusted sources.



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