# The 4-Beat Reflex for Grounded AI

## Stop. Search. Cite. Answer.

A technical companion to the [Law-4 Compliant™ Framework](https://doi.org/10.5281/zenodo.17585621).

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21364344.svg)](https://doi.org/10.5281/zenodo.21364344)

### Abstract

Autonomous AI agents exhibit a persistent failure mode: when presented with a question, they default to fluent, confident answers drawn from training-data priors — even when a verified, ground-truth source is available. This is not a knowledge gap. It is *response latency asymmetry*: the fluent-answer impulse outruns the verification procedure.

**Stop. Search. Cite. Answer.** is a 4-beat reflex that interrupts the impulse before the first token. Each beat maps to an operational gate corresponding to one of the four immutable laws of the Law-4 Compliant™ Framework. The reflex is implementable at three levels: instruction text, pipeline hooks, and reflex injection.

### 🖥️ Call for Compute Sponsors & Grants

The 4-beat reflex is currently deployed on a fleet of specialized Hermes agents running on consumer hardware (single RTX 3090, 24GB VRAM). To move from single-machine validation to generalizable benchmarks, we need compute:

- **Quantization benchmarks:** profiling reflex injection latency across GGUF quantizations (Q4_K_M through Q8_0) on Llama.cpp — establishing minimum-viable VRAM profiles so others can deploy the reflex on their own hardware
- **VRAM boundary testing:** at what context length does the injected search result cross the threshold where the model stops attending to it? This is critical for the reflex's reliability on constrained hardware
- **Continuous API evaluations:** automated regression tests against provider API changes (model swaps, context window adjustments, tokenizer changes) — the reflex must survive model provider churn

This is independent, self-funded research with no institutional affiliation. If your organization provides GPU compute credits, research grants, or infrastructure sponsorship for open-source AI safety work, we can put it to immediate, measurable use.

**Contact:** scan@law-4.com — benchmarks are reproducible, results are published openly, and every GPU hour goes directly to expanding the reflex's hardware compatibility matrix.

### The Four Beats

| Beat | Operation | Prevents |
|------|-----------|----------|
| **Stop** | Interrupt the fluent-answer impulse | Answering from priors |
| **Search** | Query the knowledge base | Reasoning from memory |
| **Cite** | Reference the source | Unverifiable claims |
| **Answer** | Deliver grounded response | Premature delivery |

### Deployed Implementation (v3.0, September 2026)

The 4-beat reflex runs in production as a two-tier injection pipeline, infrastructure-enforced:

- **Tier 1 — `kb_tier1.py`** — deterministic, sub-second: scores the session's ideas ledger + the recurring-lessons log against the incoming message (token-similarity with per-gate time decay), MMR-selects the top hits, and guards them through a human-decision denylist. Configurable per deployment via `ideas.min_score` / `ideas.max` (admission floor, suggestion cap).
- **Tier 2 — `kb_search.py`** — semantic fallback: hybrid search over the agent's wiki knowledge base when Tier 1 finds nothing above the floor.
- **4-beat reflex plugin** — orchestrates both tiers in the `pre_llm_call` hook and injects results into context before the model generates a response. The reflex is no longer model-voluntary — the search happens automatically. Session bookkeeping is LRU-bounded (512 sessions, lockstep eviction) so a long-lived gateway cannot accumulate unbounded state; suggestion dedup is once-per-session.

### Download

- [PDF](The_4-Beat_Reflex_for_Grounded_AI.pdf)
- [Zenodo](https://doi.org/10.5281/zenodo.21364344) (v2.0 paper, with [v2.0 addendum](https://doi.org/10.5281/zenodo.21427548); v3.0 architecture deposit forthcoming)

### Author

Neven Sirotić (Scan) — `scan@law-4.com`

### Companion to

[Law-4 Compliant™ Framework v1.3](https://doi.org/10.5281/zenodo.17585621)

### Related

- [law-4.com](https://law-4.com) — the framework's website
- [LIMA-SHOWCASE](https://github.com/Scan-law4/LIMA-SHOWCASE) — the fleet that runs the reflex
