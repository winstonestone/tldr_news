---
layout: post
title: "AI News Briefing — 2026-05-22"
date: 2026-05-22
---

# AI Daily Briefing — May 22, 2026

---

### 1. New Models & Benchmarks

- **Tencent Hy-MT2 translation models released (30B-A3B/7B/1.8B)** — MoE architecture, 33-language support. Claims 7B and 30B outperform DeepSeek-V4-Pro and Kimi K2.6 in fast-thinking translation mode. 1.8B model compresses to 440MB via 1.25-bit quantization. Open-weight with new IFMTBench benchmark included. Niche but strong if you need multilingual translation. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tjien7/tencent_hy_30b7b18b/)

- **Grok 4.3 tops LLM Sycophancy Benchmark for consistency** — Most cautious model, least likely to flip its judgment based on who's speaking. GPT-5.5 and Gemini 3.1 Pro scored as "highly decisive" while Mistral and GPT-4.1 were flagged as highly sycophantic. Not from a trusted benchmark source, but useful signal for conversational reliability. [r/singularity](https://reddit.com/r/singularity/comments/1tjr3g5/grok_43_tops_the_consistency_leaderboard_in_the/) · [GitHub](https://github.com/lechmazur/sycophancy)

---

### 2. Framework & Tooling Updates

- **llama.cpp b9274 fixes MTP VRAM leak** — MTP draft context GPU resources (KV cache, compute buffers) were not freed on sleep/resume cycles, causing OOM crashes over time. Now fixed. Upgrade immediately if you run MTP models on llama.cpp server. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tk0grd/latest_b9274_addresses_mtp_vram_leak/) · [GitHub Release](https://github.com/ggml-org/llama.cpp/releases/tag/b9274)

- **llama.cpp PR #22929 fixes constant prompt reprocessing with OpenCode/Pi** — If you use llama.cpp as a backend for OpenCode or Pi coding agents, this PR stops the server from re-processing the full prompt on every request. Significant latency improvement for agent workflows. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tjoiij/for_everyone_that_uses_opencode_pi_heres_your/) · [GitHub PR](https://github.com/ggml-org/llama.cpp/pull/22929)

- **ik_llama.cpp hits 110 tok/s with Qwen3.6 35B-A3B on 12GB VRAM** — Fork of llama.cpp with better CPU offloading. On RTX 4070 Super + Ryzen 7 9700X, ik_llama.cpp with MTP gets 110 tok/s vs ~90 tok/s on mainline llama.cpp. Worth trying if you're running MoE models with partial GPU offload. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tjh7az/110_toks_with_12gb_vram_on_qwen36_35b_a3b_and_ik/)

- **"Am I OpenAI Compatible" — compatibility checker for LLM serving engines** — Documents API signature differences between vLLM, llama.cpp, and other engines. Useful if you're building middleware or swapping backends. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tjgceg/am_i_openai_compatible_a_tool_and_documentation/) · [GitHub](https://github.com/heiervang-technologies/am-i-openai-compatible)

---

### 3. Infrastructure & Deployment

- **CODA: Fusing transformer blocks into GEMM epilogue programs** — Rewrites attention + FFN blocks as fused GEMM-epilogue kernels, eliminating memory-bound elementwise ops. Direct serving speedup potential for custom inference stacks. [arXiv](https://arxiv.org/abs/2605.19269) · [Hacker News](https://news.ycombinator.com/item?id=48225596)

- **DeltaBox: millisecond-level sandbox checkpoint/rollback for AI agents** — OS-level abstraction (DeltaFS + DeltaCR) that does incremental C/R instead of full state duplication. 14ms checkpoint, 5ms rollback. Tested on SWE-bench. Directly relevant if you're building tree-search or RL loops for coding agents. [arXiv](https://arxiv.org/abs/2605.22781v1)

- **AMD Gorgon Halo: only 6.7% faster than Strix Halo** — Memory bandwidth goes from 8000 to 8533 MHz, which is the bottleneck for LLM inference. Supports up to 192GB unified memory. Verdict: skip it, wait for Medusa Halo (summer 2027, ~50% improvement). [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tjqfr4/gorgon_halo_is_67_faster_than_predecessor_strix/) · [Tom's Hardware](https://www.tomshardware.com/pc-components/cpus/amd-ryzen-ai-max-400-gorgon-halo-packs-up-to-192gb-of-unified-memory-refreshed-apu-uses-zen-5-and-rdna-3-5-and-can-clock-up-to-5-2-ghz)

---

### 4. Industry Moves

- **Microsoft cancels internal Anthropic licenses** — Token-based billing reportedly blew through annual budgets in months. If even Microsoft is cost-sensitive to Claude API pricing, this is a signal about enterprise consumption patterns and potential pricing pressure on Anthropic. [r/artificial](https://reddit.com/r/artificial/comments/1tkb0op/microsoft_cancels_internal_anthropic_licenses_as/)

- **Meta serves legal notice to Heretic (LLM de-censoring project)** — Heretic has removed all Llama derivatives and is mirroring to [Codeberg](https://codeberg.org/p-e-w/heretic) in Germany. Working on "technological measures" to preserve access to non-Llama models. First major enforcement action against Llama license violators. [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tjmvx6/heretic_has_been_served_a_legal_notice_by_meta_inc/)

- **Trump postpones AI executive order after White House infighting** — Details unclear behind FT paywall, but signals continued policy uncertainty in US AI regulation. [r/singularity](https://reddit.com/r/singularity/comments/1tjxvhp/donald_trump_abruptly_postpones_ai_order_after/) · [FT](https://www.ft.com/content/14213cb0-8d11-4118-bac0-12a403696185)

- **Krea 2 image model confirmed going open-source** — Likely the Medium variant. Community expects it to be competitive with Nano Banana Pro if given search grounding. [r/StableDiffusion](https://reddit.com/r/StableDiffusion/comments/1tjnwgo/krea_2_will_be_open_source/)

---

### 5. Research Highlights

- **VPO: Vector Policy Optimization — diversity-first RL for test-time search** — Drop-in replacement for GRPO that trains LLMs to produce diverse solutions optimized for different reward trade-offs. Gap over scalar RL widens as search budget grows. Directly relevant if you use best-of-N or evolutionary search at inference time. [arXiv](https://arxiv.org/abs/2605.22817v1)

- **Multi-Stream LLMs: parallelizing prompts, thinking, and I/O** — Proposes separating prompt processing, reasoning, and output into parallel streams within the transformer. Early but could change how we think about serving latency. [arXiv](https://arxiv.org/abs/2605.12460)

- **MOSS: agents that rewrite their own source code to self-improve** — Self-evolving agent system that edits its own Python source (not just prompts/configs) based on production failures. Tested on OpenClaw, lifts 4-task mean score from 0.25 to 0.61 in one cycle. Interesting if you're building long-running agents. [arXiv](https://arxiv.org/abs/2605.22794v1)

- **Gated DeltaNet-2: better linear attention from NVIDIA** — Decouples erase and write gates in linear attention, outperforms Mamba-2/3 and KDA on long-context retrieval at 1.3B scale. Code available. [arXiv](https://arxiv.org/abs/2605.22791v1) · [GitHub](https://github.com/NVlabs/GatedDeltaNet-2)

- **AI-driven formal proof search solves 9 open Erdős problems** — The full paper behind the previously reported result. Agent alternating LLM generation with Lean verification, at per-problem cost of a few hundred dollars. Also proved 44/492 OEIS conjectures. Being deployed in active research. [arXiv](https://arxiv.org/abs/2605.22763v1)

---

### 6. Technology Adoption

- **ChromeDevTools MCP** — Official Chrome DevTools integration for coding agents (151 stars/day). Gives agents direct browser inspection capabilities. Worth evaluating if you're building web-facing agents. [GitHub](https://github.com/ChromeDevTools/chrome-devtools-mcp)

- **Runtime (YC P26) — sandboxed coding agent infrastructure** — Snapshots full Docker Compose environments, injects secrets via proxy (never touches the agent), RBAC per human and per agent. Designed to let non-engineers use Claude Code/Codex safely. Early but addresses a real gap. [Hacker News](https://news.ycombinator.com/item?id=48225596) · [Website](https://www.runtm.com/)

- **Multica — open-source managed agents platform** (534 stars/day) — Assign tasks to coding agents, track progress, compound skills. Positioning as "agents as teammates." Too early to evaluate quality but worth watching. [GitHub](https://github.com/multica-ai/multica)

- **Datasette Agent 0.1a3** — Simon Willison's new AI assistant for Datasette. Conversational SQL queries, chart generation via plugins, runs on Gemini 3.1 Flash-Lite. If you use Datasette for data exploration, this is worth trying now. [Simon Willison](https://simonwillison.net/2026/May/21/datasette-agent/#atom-everything) · [GitHub](https://github.com/datasette/datasette-agent)

- **HarnessAPI — unified streaming API + MCP tool from one Python handler** — Eliminates dual-stack boilerplate (FastAPI + FastMCP). 74% less framework code. Subclasses FastAPI so you keep all middleware. If you're building MCP tools that also need HTTP endpoints, this saves real time. [arXiv](https://arxiv.org/abs/2605.22733v1) · [GitHub](https://github.com/edwinjosechittilappilly/harnessapi)

- **notebooklm-py** — Unofficial Python API for Google NotebookLM (186 stars/day). Programmatic access to features the web UI doesn't expose, works with Claude Code, Codex, and OpenClaw. [GitHub](https://github.com/teng-lin/notebooklm-py)

---

### 8. Watchlist Updates

- **llama.cpp MTP production readiness** — Progress continues. b9274 fixes a critical VRAM leak in MTP mode, and the prompt reprocessing fix (PR #22929) improves agent workflow compatibility. MTP is getting more stable but still has rough edges (user reports models unloading after minutes of use). [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA/comments/1tk0grd/latest_b9274_addresses_mtp_vram_leak/)
- **Anthropic Stainless acquisition impact** — Microsoft reportedly canceling internal Anthropic licenses over token-based billing costs may be partially related to SDK/billing infrastructure changes post-acquisition. Worth monitoring. [r/artificial](https://reddit.com/r/artificial/comments/1tkb0op/microsoft_cancels_internal_anthropic_licenses_as/)
- **NEW WATCHLIST: Meta Llama license enforcement** — Meta's legal action against Heretic is the first visible enforcement. Could affect other projects distributing modified Llama weights.
- **NEW WATCHLIST: Krea 2 open-source release** — Confirmed coming, likely Medium variant. No release date yet.
- **NEW WATCHLIST: AMD Medusa Halo** — Summer 2027, ~50% AI performance improvement over Strix Halo. The meaningful upgrade for local inference on unified memory AMD chips.



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