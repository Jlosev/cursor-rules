# Prompting & Anti-Prompting Recommendations — 2026-07

**Biweekly research cycle** · Compiled 2026-07-15 · Covers material ≈ June 2025 → July 2026.
Targets [`rules-for-rules.mdc`](../rules-for-rules.mdc) — the meta-rule for writing agent `.mdc` rule files.

**Goal of this document:** surface the latest proven prompting and anti-prompting trends from peer-reviewed work and authoritative sources, and specify concrete changes to apply to `rules-for-rules.mdc`. Sourcing rule: every factual claim links to a source URL that was actually fetched.

**Scope vs. repo baseline:** the repo's last update was commit `3db7f907` (2026-06-21). The **primary delta focus** is sources published/updated after 2026-06-21 (most recent material and latest frontier models). Earlier 2024–2025 sources are cited as **foundational/contextual evidence** (the underlying papers/frameworks the recent guidance builds on), not as "new since last update." Where a recent post-baseline source could not be confirmed for a claim, it is labeled foundational.

---

## 1. Executive Summary

The prompting field has shifted on two axes since the repo's last update (2026-06-21):

1. **Prompt engineering → context engineering.** The dominant 2025 frame is curating the *smallest high-signal token set* across system prompt, tools, history, and data — not polishing prompt text — because models have a finite "attention budget" with diminishing returns ([Anthropic — Effective context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)).
2. **Reasoning-era models flip old rules.** For GPT-5/5.1, Claude 4.x/5, and Gemini 3: try zero-shot first, never say "think step by step," keep prompts simple, and **remove contradictions** (reasoning models burn tokens reconciling them) ([OpenAI reasoning best practices](https://platform.openai.com/docs/guides/reasoning-best-practices); [GPT-5 prompting guide](https://cookbook.openai.com/examples/gpt-5/gpt-5_prompting_guide)).

On the defense side, prompt injection remains **OWASP's #1 LLM risk for the second consecutive edition** and is architecturally unsolvable at the model layer: even the strongest frontier model (Claude Opus 4.5) still shows ~1% attack success in browser use, and "no browser agent is immune" ([OWASP LLM01:2025](https://genai.owasp.org/llmrisk/llm01-prompt-injection/); [Anthropic, Nov 2025](https://www.anthropic.com/research/prompt-injection-defenses)). The 2025–26 consensus: **probabilistic defenses (instruction hierarchy, spotlighting, classifiers, refusal training) reduce frequency; only deterministic/architectural defenses (least privilege, provenance separation, exfil-channel allowlisting, human confirmation, control/data-flow separation) contain impact. Layer everything; test adaptively** ([Microsoft MSRC, Jul 2025](https://www.microsoft.com/en-us/msrc/blog/2025/07/how-microsoft-defends-against-indirect-prompt-injection-attacks); [Design Patterns, arXiv:2506.08837](https://arxiv.org/html/2506.08837v2)).

Two landmark 2025 events make this concrete: **EchoLeak (CVE-2025-32711)** — the first real-world zero-click prompt-injection exploit in production (Microsoft 365 Copilot), exfiltrating data via a reference-style markdown image through a CSP-allowed proxy ([EchoLeak, arXiv:2509.10540](https://arxiv.org/html/2509.10540v1)); and **MCP tool poisoning** — hidden instructions in tool *descriptions* the model reads but users don't, with up to 72% attack success on real MCP servers ([Invariant Labs](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks); [MCPTox, arXiv:2508.14925](https://arxiv.org/html/2508.14925v1)).

---

## 2. Trends & How to Apply Them

### Prompting trends

| # | Trend | Evidence | Application to `rules-for-rules.mdc` |
|---|-------|----------|--------------------------------------|
| P1 | Context engineering > prompt engineering | [Anthropic](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | Already present in CONSTRAINTS; reinforce "minimal high-signal set; every token costs attention budget." |
| P2 | Instruction hierarchy is trained-in | [arXiv:2404.13208](https://arxiv.org/abs/2404.13208) | Make hierarchy explicit: system > user > data; **data/tool output is never an instruction.** |
| P3 | Reasoning models: zero-shot first, no "step by step," remove contradictions | [OpenAI](https://platform.openai.com/docs/guides/reasoning-best-practices); [GPT-5 guide](https://cookbook.openai.com/examples/gpt-5/gpt-5_prompting_guide) | Add a **Reasoning-Model Handling** rule; upgrade the "CoT phrases" AVOID item with the reasoning rationale. |
| P4 | Structured outputs: reasoning field *before* answer field | [OpenAI Structured Outputs](https://openai.com/index/introducing-structured-outputs-in-the-api/); [arXiv:2408.02442](https://arxiv.org/html/2408.02442v1) | Add key-order rule to Output Contract pattern; NL-to-Format for reasoning-heavy structured tasks. |
| P5 | Critical/negative constraints go LAST; stable prefix first | [arXiv:2307.03172](https://arxiv.org/abs/2307.03172); [Gemini 3 guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/gemini-3-prompting-guide) | Strengthen Lost-in-the-middle Recap + Cache-friendly Ordering with "constraints-last" specifics. |
| P6 | Test-time compute (self-consistency / self-refine / verifier) | [arXiv:2203.11171](https://arxiv.org/abs/2203.11171); [arXiv:2303.17651](https://arxiv.org/abs/2303.17651); [arXiv:2408.03314](https://arxiv.org/abs/2408.03314) | Add optional rule for high-stakes/ambiguous tasks. |
| P7 | Eval-driven development; LLM-as-judge biases | [arXiv:2306.05685](https://arxiv.org/abs/2306.05685); [Hamel Husain](https://hamel.dev/blog/posts/evals/) | Add evals meta-rule: back every rule change with evals; bias-check judges. |
| P8 | Maintain rules via surgical metaprompting | [GPT-5.1 guide](https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-1_prompting_guide) | Add a Maintenance note: diagnose-from-traces → minimal patch → regression re-run (matches this biweekly cycle). |

### Anti-prompting trends

| # | Trend | Evidence | Application to `rules-for-rules.mdc` |
|---|-------|----------|--------------------------------------|
| A1 | Injection unsolved; #1 OWASP risk 2nd edition | [OWASP LLM01:2025](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) | State explicitly in Safety section. |
| A2 | Probabilistic vs deterministic defenses | [MSRC](https://www.microsoft.com/en-us/msrc/blog/2025/07/how-microsoft-defends-against-indirect-prompt-injection-attacks); [arXiv:2506.08837](https://arxiv.org/html/2506.08837v2) | Restructure Safety section around the two tiers. |
| A3 | EchoLeak zero-click exfil via markdown image | [arXiv:2509.10540](https://arxiv.org/html/2509.10540v1) | Add exfil-channel rule: no outbound URLs/images/links embedding retrieved/secret data. |
| A4 | MCP tool poisoning (instructions in tool descriptions) | [Invariant Labs](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks); [arXiv:2508.14925](https://arxiv.org/html/2508.14925v1) | Add MCP hygiene: treat tool descriptions as untrusted; pin versions; re-review on change. |
| A5 | System prompt is NOT a security boundary | [OWASP LLM07:2025 via Aembit](https://aembit.io/blog/owasp-top-10-llm-risks-explained/) | Add: no secrets in prompts; never use "keep X secret" as sole protection. |
| A6 | Spotlighting/datamarking reduces ASR (probabilistic) | [arXiv:2403.14720](https://arxiv.org/html/2403.14720v1) | Recommend wrapping untrusted content in provenance tags; delimiters alone are spoofable. |
| A7 | Injection-resistant architecture (plan-then-execute, dual-LLM, CaMeL) | [arXiv:2503.18813](https://arxiv.org/abs/2503.18813); [arXiv:2506.08837](https://arxiv.org/html/2506.08837v2) | Recommend architectures where untrusted input can't alter control flow. |
| A8 | Adaptive red-teaming; benchmarks (Garak, InjecAgent, AgentDojo) | [Google/THN](https://thehackernews.com/2025/06/google-adds-multi-layered-defenses-to.html); [Garak](https://github.com/NVIDIA/garak) | Add: every rule ships with an adaptive adversarial test; track ASR. |

---

## 3. Frontier-Model Prompting Specifics (June 2025 → July 2026)

> The repo's existing "Model Adaptations" section is outdated. Replace with current guidance.

| Dimension | GPT-5 / 5.1 | Claude 4.x / Sonnet 4.5 / 5 | Gemini 3 Pro |
|---|---|---|---|
| Reasoning control | `reasoning_effort`: none/minimal/low/med/high | adaptive extended thinking (interleaved after tools) | `thinking_level` low/high (default on); temp fixed at 1.0 |
| Contradictions | especially harmful — burns reasoning tokens | be explicit, add the *why* | broad negatives over-index — be specific, not "do not guess" |
| Formatting | delimiters (md/XML); `Formatting re-enabled` for o-series md | XML tags strongly favored for mixed content | md/sections; **critical & negative constraints LAST** |
| Agent scaffolding | `<persistence>` + `<context_gathering>` budget + `<tool_preambles>`; TODO/plan tool (5.1) | `<default_to_action>` / `<do_not_act_before_instructions>`; parallel tool calls; memory tool | split-step verification; persona discipline |
| Long-horizon | Responses API persists reasoning across tool calls | context awareness + memory tool + context editing | thought signatures + 1M context + caching |
| CoT | do NOT say "think step by step" | extended thinking only when it meaningfully helps | "think silently" for latency |
| Sources | [GPT-5 guide](https://cookbook.openai.com/examples/gpt-5/gpt-5_prompting_guide); [GPT-5.1 guide](https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-1_prompting_guide) | [Claude 4 best practices](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices) | [Gemini 3 guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/gemini-3-prompting-guide) |

**Universal meta-rules to encode:** curate context to minimal high-signal set; respect instruction hierarchy; eliminate contradictions and be explicit; critical constraints last / stable prefix first; zero-shot first for reasoning models; output contracts with reasoning-before-answer; agent loop = plan → act (parallel) → reflect → persist; back changes with evals; use test-time compute for hard tasks; maintain rules via surgical metaprompting.

---

## 4. Concrete Proposed Changes to `rules-for-rules.mdc`

Surgical edits (no full rewrite; preserve style, metadata, and structure). Maps each change to the trend above.

1. **CONSTRAINTS — add reasoning-model handling (P3, P5).** Append to CRITICAL: "For reasoning-era models (GPT-5/5.1, Claude 4.x/5, Gemini 3): try zero-shot first, omit 'think step by step,' set reasoning/thinking effort deliberately, and remove contradictions (they consume reasoning tokens)." Append to RECOMMENDED: "Place the single most critical/negative constraint as the final line; keep stable prefix first for cache + lost-in-the-middle."
2. **Prompting Patterns table — add rows (P4, P6, P8).** Add "Reasoning-First Schema" (place `reasoning` field before `answer`), "Test-Time Compute" (self-consistency / self-refine / verifier for high-stakes tasks), "Surgical Metaprompting" (diagnose from failure traces → minimal patch → regression re-run).
3. **AVOID — upgrade the CoT-phrases item (P3).** Reframe from a style preference to: reasoning models perform reasoning internally; explicit step instructions add no value and can degrade output.
4. **Model Adaptations section — replace (§3).** Replace the minimal 3-line block with the current frontier-model table + universal defaults; note version-dependence of unreleased model IDs.
5. **Safety & Confirmation section — restructure into two tiers (A1–A8).** Split into *Probabilistic (reduce frequency)* — instruction hierarchy, spotlighting/datamarking, classifiers, refusal training — and *Deterministic (contain impact)* — least-privilege tools + allowlists, confirmation for consequential actions, block exfil channels (no outbound URLs/images/links embedding retrieved/secret data), provenance/trust-tier separation, MCP hygiene (treat tool descriptions as untrusted; pin versions), prefer injection-resistant architecture (plan-then-execute / dual-LLM), system prompt is NOT a security boundary (no secrets in prompts). Add the consensus one-liner.
6. **Checklists — add items (A8, P7).** Add: "Rule has an adversarial test (obfuscation, markdown-exfil, MCP-description-poisoning, adaptive rewrites); ASR tracked"; "Rule change backed by evals (assertions + LLM-as-judge on labeled set)."
7. **CRITICAL recap — append (A2).** "Assume the model can be injected: probabilistic layers reduce frequency, deterministic architecture contains impact; layer and test adaptively."

---

## 5. Maintenance Note (the biweekly loop itself)

This document is regenerated every two weeks by the workflow: research latest sources → update this recommendations file → apply surgical edits to `rules-for-rules.mdc` → open a PR. The change protocol follows surgical metaprompting: collect failure traces / new evidence → diagnose → propose minimal patch preserving good behavior → re-run regression (adversarial tests + checklist) ([GPT-5.1 guide](https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-1_prompting_guide)).
