# The 4-Beat Reflex for Grounded AI

## Stop. Search. Cite. Answer.

A technical companion to the [Law-4 Compliant™ Framework](https://doi.org/10.5281/zenodo.17585621).

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21364344.svg)](https://doi.org/10.5281/zenodo.21364344)

### Abstract

Autonomous AI agents exhibit a persistent failure mode: when presented with a question, they default to fluent, confident answers drawn from training-data priors — even when a verified, ground-truth source is available. This is not a knowledge gap. It is *response latency asymmetry*: the fluent-answer impulse outruns the verification procedure.

**Stop. Search. Cite. Answer.** is a 4-beat reflex that interrupts the impulse before the first token. Each beat maps to an operational gate corresponding to one of the four immutable laws of the Law-4 Compliant™ Framework. The reflex is implementable at three levels: instruction text, pipeline hooks, and reflex injection.

### The Four Beats

| Beat | Operation | Prevents |
|------|-----------|----------|
| **Stop** | Interrupt the fluent-answer impulse | Answering from priors |
| **Search** | Query the knowledge base | Reasoning from memory |
| **Cite** | Reference the source | Unverifiable claims |
| **Answer** | Deliver grounded response | Premature delivery |

### Deployed Implementation

The 4-beat reflex runs in production via two components:

- **`kb_search.py`** — deterministic script: semantic search → read top 3 → format with sources, in one call
- **4-beat reflex plugin** — injects the exact command before every turn via Hermes Agent `pre_llm_call` hook, with `transform_llm_output` flagging for unverified responses

### Download

- [PDF](The_4-Beat_Reflex_for_Grounded_AI.pdf)
- [Zenodo (DOI pending)](https://doi.org/10.5281/zenodo.21364344)

### Author

Neven Sirotić (Scan) — `scan@law-4.com`

### Companion to

[Law-4 Compliant™ Framework v1.3](https://doi.org/10.5281/zenodo.17585621)

### Related

- [law-4.com](https://law-4.com) — the framework's website
- [LIMA-SHOWCASE](https://github.com/Scan-law4/LIMA-SHOWCASE) — the fleet that runs the reflex
