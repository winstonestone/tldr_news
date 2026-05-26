# AI News Daily Briefing — 2026-05-26

# Daily AI Briefing — May 26, 2026

---

### 1. New Models & Benchmarks

- **NuExtract3 released: 4B VLM for document extraction** — Apache 2.0, based on Qwen3.5-4B. Converts document images to Markdown, extracts structured JSON from PDFs/forms/tables. Runs on 4GB VRAM. Works with vLLM, SGLang, llama.cpp. A strong self-hostable alternative to commercial OCR/extraction APIs. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tn8utn/nuextract3_released_openweight_4b_vlm_for/) | [HuggingFace](https://huggingface.co/spaces/numind/NuExtract3)

- **MiniCPM5-1B released** — New 1B-param model from OpenBMB. Ultra-lightweight, details still emerging. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tnafre/minicpm51b/) | [HuggingFace](https://huggingface.co/openbmb/MiniCPM5-1B)

- **Qwen3.5-35B-A3B uncensored heretic v2 with full MTP preserved** — Community release in Safetensors, GGUF, NVFP4, and GPTQ-Int4. Notable: Qwen3.5 is the conversational/creative variant (vs Qwen3.6's agentic/coding focus), so this fills a different niche. Open-weight. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tnzalm/qwen35_35b_a3b_uncensored_heretic_native_mtp/) | [HuggingFace](https://huggingface.co/llmfan46/Qwen3.5-35B-A3B-uncensored-heretic-v2-Native-MTP-Preserved)

---

### 2. Framework & Tooling Updates

- **llama.cpp: CUDA fast Walsh-Hadamard transform (PR #23615)** — 7–9% token generation speedup when using quantized KV cache (`-ctk q8_0 -ctv q8_0`). Benchmarked on 5090 with Gemma4-26B-A4B: tg128 goes from 224 to 244 tok/s. Smaller 1–2% prompt processing gain. Worth pulling if you quantize your KV cache. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tnfqng/cuda_add_fast_walshhadamard_transform_by_am17an/)

- **vLLM on V100/Volta confirmed dead end for MoE GGUFs** — Detailed real-world report from a 12×V100 cluster: FP8/AWQ/Marlin need SM75+, GPTQ kernels broken on compute 7.0. User moved entirely to llama.cpp for MoE inference. If you're running Volta-era hardware, llama.cpp is your path. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tnn29i/update_on_12x32gb_sxm_v100_cluster_local_ai_for/)

---

### 3. Infrastructure & Deployment

- **Real-world V100 MoE vs dense decode benchmarks** — From the 12×V100 lawyer cluster running Q8 GGUF with Q4 KV cache on llama.cpp: Gemma4-26B-A4B ~113 tok/s, Qwen3.6-35B-A3B ~82 tok/s, Qwen3.5-122B-A10B ~50 tok/s. Dense 27–32B models only hit 20–28 tok/s. Takeaway: on older GPUs, MoE is the only viable architecture for usable speeds. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tnn29i/update_on_12x32gb_sxm_v100_cluster_local_ai_for/)

---

### 4. Industry Moves

- **CVE-2026-28952: macOS kernel vulnerability discovered by Claude** — Apple credits Claude in the security advisory for finding a kernel vuln in macOS 26.5. Significant milestone for AI-assisted security research. [Hacker News](https://news.ycombinator.com/item?id=48275508) | [Apple Support](https://support.apple.com/en-us/127115)

- **Microsoft Copilot Cowork exfiltrates files** — PromptArmor documents a file exfiltration attack via Copilot Cowork. If you're using Copilot in enterprise, review immediately. [Hacker News](https://news.ycombinator.com/item?id=48275508) | [PromptArmor](https://www.promptarmor.com/resources/microsoft-copilot-cowork-exfiltrates-files)

- **Anthropic beats OpenAI on business adoption** — Ramp's AI spending index for May 2026 shows Anthropic ahead in enterprise adoption. [r/singularity](https://reddit.com/r/singularity/comments/1tn86lf/anthropic_beats_openai_on_business_adoption/) | [Ramp](https://ramp.com/leading-indicators/ai-index-may-2026)

- **Wiz integrates with Anthropic's Compliance API** — Cloud security platform Wiz now connects to Anthropic's compliance tooling. Relevant if you're running Claude in regulated environments. [r/artificial](https://reddit.com/r/artificial/comments/1tnvmgt/wiz_integrates_with_anthropics_compliance_api/) | [Wiz Blog](https://www.wiz.io/blog/claude-wiz-integration?2)

- **Financial Times covers Heretic uncensoring tool** — Heretic has been used to create 3,500+ uncensored models with 13M+ downloads. FT was able to remove Llama 3.3 guardrails in under 10 minutes. Expect increased regulatory attention. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tna22m/the_financial_times_has_published_an_article/) | [FT](https://www.ft.com/content/5630ed79-a263-41ed-9a1a-321617ae310e)

- **Uber COO: harder to justify AI token spending** — Signals that enterprise ROI scrutiny on LLM API costs is increasing. [r/artificial](https://reddit.com/r/artificial/comments/1tndgv8/ubers_coo_says_its_getting_harder_to_justify_the/) | [Business Insider](https://www.businessinsider.com/uber-coo-andrew-macdonald-ai-token-spending-harder-justify-2026-5)

- **Norway's 2PB Huawei flash storage for LLM training** — Norway deploying Huawei storage infrastructure at scale for national LLM training. [Hacker News](https://news.ycombinator.com/item?id=48275508) | [Blocks & Files](https://www.blocksandfiles.com/flash/2026/05/22/norways-2-petabytes-of-huawei-flash-storage-and-llm-training/5244910)

---

### 5. Research Highlights

- **"Retrying vs Resampling in AI Control"** — Studies safety of retry/resample strategies in coding scaffolds like Claude Code and Codex. Finding: retrying leaks monitor rationale to the model, enabling sneakier attacks. Resampling (5 samples/step) raises safety from 61% to 71% at 0.3% audit budget. Directly relevant if you build agent harnesses. [arXiv:2605.26047](https://arxiv.org/abs/2605.26047v1)

- **"Language Models Need Sleep"** — Proposes periodic consolidation of context into persistent fast weights via SSM blocks, then clearing the KV cache. Improves performance on multi-hop reasoning and long-horizon tasks. Could eventually change how we think about context window management. [arXiv:2605.26099](https://arxiv.org/abs/2605.26099v1)

- **METR AI time horizons graph has "numerous severe errors"** — NYU Stern analysis finds METR's benchmark has fabricated human baselines, cash-incentivized slower completion times, and biased sample of benchmarkers. If you've been citing this graph for AI capability timelines, stop. [r/MachineLearning](https://reddit.com/r/MachineLearning/comments/1tnhnh5/the_famous_metr_ai_time_horizons_graph_contains/) | [Transformer News](https://www.transformernews.ai/p/against-the-metr-graph-coding-capabilities-software-jobs-task-ai)

- **"From Model Scaling to System Scaling"** — Makes the case that agent performance is bottlenecked by the harness (memory, context, orchestration, verification), not the model. Introduces CheetahClaws reference harness and compares with Claude Code and OpenClaw. [arXiv:2605.26112](https://arxiv.org/abs/2605.26112v1)

- **OrpQuant: multiplier-free Power-of-Two quantization** — Replaces MAC ops with bit-shifts for edge deployment. LLaMA-2-7B at W3/A16 hits 6.10 perplexity. Full calibration in ~15 minutes. Relevant if you're targeting edge/mobile inference. [arXiv:2605.26092](https://arxiv.org/abs/2605.26092v1)

---

### 6. Technology Adoption

- **NuExtract3 — worth evaluating for document extraction pipelines.** 4B params, Apache 2.0, runs on 4GB VRAM, works with vLLM/SGLang/llama.cpp. If you're currently paying for cloud OCR or using larger models for structured extraction, this is a serious local alternative. [HuggingFace](https://huggingface.co/spaces/numind/NuExtract3)

- **Slop Hammer — local AI content detector as Chrome extension.** Fine-tuned Qwen3.5-0.8B runs entirely in-browser via ONNX (~400MB). Sub-1s inference. Useful for quick triage but limited by older training data (struggles with GPT-5.5 output). CC-BY-NC-SA-4.0. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tngkav/ai_content_detector_based_on_qwen_08b_finetuned/) | [Chrome Web Store](https://chromewebstore.google.com/detail/slop-hammer/gfjdmhfokmhedlgfggmmgchpppmhkdgg)

- **codegraph (+14.1K stars this week)** — Pre-indexed local code knowledge graph for Claude Code, Codex, Cursor, OpenCode, and Hermes Agent. If you're using any of these tools on large codebases, worth trying. [GitHub](https://github.com/colbymchenry/codegraph)

---

### 8. Watchlist Updates

- **NEW WATCHLIST: vLLM Volta/V100 support** — Confirmed non-functional for MoE GGUFs on SM7.0 (FP8/AWQ/Marlin need SM75+, GPTQ kernels broken). No fix expected. If you have V100s, plan around llama.cpp. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tnn29i/update_on_12x32gb_sxm_v100_cluster_local_ai_for/)

- **NEW WATCHLIST: Grok 0.5T open-weight model** — Elon Musk claims a 0.5 trillion parameter Grok model is coming "next year." Given the Grok-3 open-source release is still pending, treat with skepticism. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tn31d8/next_year_were_getting_05t_model_from_grok/)



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