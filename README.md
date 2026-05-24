# AI News Daily Briefing — 2026-05-24

# Daily AI Briefing — 2026-05-24

---

### 1. New Models & Benchmarks

- **Cohere Command A+ released (218B MoE, 25B active, Apache 2.0)** — 128 experts top-8 routing, sigmoid routing (not softmax), sliding window attention 3:1. Already running on Apple Silicon via MLX at 22.9 tok/s generation. A serious open-weight contender for tool-calling and multi-turn workloads. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tlqxeh/command_a_218b_moe_running_on_apple_silicon_mlx/)

- **Qwen3.6-35B-A3B-Uncensored-Genesis-APEX-MTP GGUF** — Community fine-tune with MTP support, tested stable through 200k context in agentic coding sessions. Niche but notable if you run Qwen locally and want an uncensored MTP variant. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tm3toi/qwen3635ba3buncensoredgenesisapexmtp/) | [HuggingFace](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-V2-APEX-MTP-GGUF)

---

### 2. Framework & Tooling Updates

- **llama.cpp b9297: NVFP4 + MTP now work simultaneously** — Previously you had to choose one or the other. This is a meaningful step toward MTP production readiness on NVIDIA hardware. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tlohld/nvfp4_mtp_voilà_on_llamacpp/) | [GitHub release](https://github.com/ggml-org/llama.cpp/releases/tag/b9297)

- **llama.cpp server gains built-in native tools** — Experimental `--tools` flag enables `read_file`, `exec_shell_command`, `edit_file`, `apply_diff`, `grep_search`, and more directly in the server. Turns llama-server into a lightweight agent harness with zero external dependencies. No sandboxing yet — don't expose this to untrusted users. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tluma3/llamacpp_server_have_builtin_native_tools_exec/)

- **Command A+ MLX port (PR open)** — Full implementation of Cohere2 MoE architecture for mlx-lm including W4A4 quantization path. BF16→Q8 runs at 22.9 tok/s gen, 57.6 tok/s prompt on Apple Silicon (241GB peak). [GitHub PR #1294](https://github.com/ml-explore/mlx-lm/pull/1294)

---

### 3. Infrastructure & Deployment

- **Perplexity Comet indirect prompt injection: full attack chain documented** — Hidden Reddit spoiler tags injected instructions that Comet's AI executed: email extraction, OTP theft, session hijacking. Zero user interaction required beyond "summarize this thread." If you're building anything that processes external content through an LLM, this is OWASP LLM01 in the wild. [Towards AI](https://pub.towardsai.net/prompt-injection-in-production-the-2025-perplexity-comet-attack-d73d57eea7ea)

---

### 4. Industry Moves

- **Anthropic Mythos preview surfaces: 10,000+ vulnerabilities found** — Engadget reports Anthropic claims Mythos has already discovered over 10,000 vulnerabilities, linked to "Project Glasswing." Separately, a Mythos 1 model identifier was spotted in Claude Code's internals. Release appears imminent. [Engadget](https://www.engadget.com/2180028/anthropic-claude-mythos-preview-project-glasswing-update/) | [r/singularity](https://reddit.com/r/singularity/comments/1tluzbd/mythos_1_has_been_spotted_in_claude_code/)

- **Tencent Hunyuan Hy3 preview in use as cheap agentic worker** — User reports running Hy3 (21B active params) at ~$0.18/M input tokens for bulk refactoring alongside Opus, completing 360 routine steps in under an hour. No official release post, but the model is apparently available. [r/singularity](https://reddit.com/r/singularity/comments/1tlj7ou/coding_is_basically_solved_for_the_boring_90_of/)

---

### 5. Research Highlights

- **Vision LLMs vs. OCR for long-document QA** — Benchmarked native PDF (vision LLM) against OCR pipelines on 30 image-heavy PDFs: native PDF came 5th of 6 on accuracy (52.0%) and was the most expensive ($0.2552/query). Premium OCR + full-context hit 59.6% at lower cost. Vision specifically underperformed on charts and tables. Native PDF had a 7% irrecoverable failure rate. If you're building document QA, OCR pipelines still win. [Full writeup](https://www.surfsense.com/blog/agentic-rag-vs-long-context-llms-benchmark) | [r/MachineLearning](https://reddit.com/r/MachineLearning/comments/1tm0cqg/visioncapable_llms_vs_ocr_for_longdocument/)

---

### 6. Technology Adoption

- **tts-bench: comprehensive local TTS benchmark** — Covers all major TTS engines with Windows/Mac results (Linux coming). If you're picking a local TTS solution, this saves you from running your own comparisons. [GitHub](https://github.com/5uck1ess/tts-bench) | [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tm0k2l/tts_benchmark_comparison_all_known_tts_up_until/)

- **Anthropic Cybersecurity Skills repo (754 structured skills)** — Maps to MITRE ATT&CK, NIST CSF 2.0, ATLAS, D3FEND, and NIST AI RMF. Works with Claude Code, Copilot, Cursor, and 20+ platforms. Useful if you're building security-focused agent workflows. Trending on GitHub (281 stars today). [GitHub](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)

---

### 7. Model Rankings Update

No ranking changes today. The Vision LLMs vs OCR benchmark is pipeline-level (OCR vs native PDF), not model-level — it doesn't change individual model rankings for RAG. Command A+ needs independent benchmark data from trusted sources before ranking.

---

### 8. Watchlist Updates

- **Anthropic Mythos release** — Escalating from "near future" to **likely imminent**. Model identifier "Mythos 1" spotted in Claude Code internals. Anthropic publicly claims 10,000+ vulnerabilities found during preview. Two independent signals in one day suggest days-to-weeks, not months.

- **llama.cpp MTP production readiness** — Progressing. NVFP4 + MTP now work together as of b9297, removing a key limitation. Built-in server tools also landed. MTP is getting closer to "just works" status.

- **Meta Llama license enforcement** — No new developments today.

- **Krea 2 open-source release** — No new developments today.

- **AMD Medusa Halo** — No new developments today.



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