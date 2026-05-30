# Packet 02 — Overview & Framework

# Restart Often Protocol

**Stop carrying the past. Start scaling the future.**

> ROP is a context-management discipline for multi-packet LLM workflows. Instead of feeding every prior token back into each new prompt, ROP quantifies how much context you *drop* between steps — converting quadratic cost blow-up into predictable, linear spend. The higher your ROP score, the leaner your architecture, and the further your compute budget stretches.

---

## § 01 — What is ROP?

### The Core Idea

Every time an LLM processes a new step in a multi-turn workflow, you face a choice: carry forward all previous context, some of it, or none. Naive "append everything" approaches balloon your token count at a rate proportional to *n²* — making long pipelines financially unviable at scale.

ROP (Restart Often Protocol) names and quantifies the degree to which a system sheds prior context between execution packets. An ROP of **0%** means full context carry-forward. An ROP of **100%** means each packet runs entirely stateless. Most production systems live somewhere in between.

> **The ROP insight:** Engineering ROI in multi-packet workflows is almost never found in making individual packets faster — it's found in pushing the system rightward on the ROP spectrum as far as accuracy allows.

---

## § 02 — The Math

### Cost Formula

For a sequence of *n* packets each with base size *s*, and ROP factor *r*, total token volume *T* is:

`T = n * s + [n(n - 1) / 2] * s * (1 - r)`

- **n** = packet count
- **s** = base packet size
- **r** = ROP% (0.0 → 1.0)

At baseline (*n* = 10, *s* = 100k tokens, $10/M):

| ROP % | Total Tokens | Cost | vs 0% | Savings |
| :--- | :--- | :--- | :--- | :--- |
| 0% | 5.5M | $55.00 | baseline | — |
| 20% | 4.6M | $46.00 | −16% | $9.00 |
| 40% | 3.7M | $37.00 | −33% | $18.00 |
| 60% | 2.8M | $28.00 | −49% | $27.00 |
| 80% | 1.9M | $19.00 | −65% | $36.00 |
| **100%** | **1.0M** | **$10.00** | **−82%** | **$45.00** |

*Linear step-down: every 20% ROP increase = −0.9M tokens = −$9.00*

---

## § 03 — Architectural Mapping

### The Continuum

Each point on the ROP spectrum corresponds to a distinct engineering pattern. Higher ROP demands more deliberate state design but pays back in efficiency and scalability.

**0% — Full Context | 50% — Hybrid | 100% — Stateless**

| ROP % | Architecture | Trade-off |
| :--- | :--- | :--- |
| **0%** | Naive Append | Perfect recall, quadratic cost |
| **20%** | Sliding Window | Good short-term memory, loses older context |
| **40%** | Recursive Summarization | Balanced — themes retained, micro-details at risk |
| **60%** | Vector DB / RAG | Targeted retrieval, adds lookup latency |
| **80%** | Skeleton / State Vars | Minimal overhead, strict schema dependency |
| **100%** | Pure Stateless | Linear cost, requires fully decomposable tasks |

---

## § 04 — Strategy

### Key Takeaways

*   **T-01: The r-Factor is your primary lever.** Speeding up individual packets gives marginal returns. Moving rightward on the ROP spectrum restructures your cost curve entirely.
*   **T-02: Scale inversion at high n.** As pipeline length grows, 0% ROP scales as O(n²) — financially unviable for long workflows. High ROP converts this to O(n): predictable, budgetable, linear.
*   **T-03: The sweet spot is 60%.** RAG or graph-memory architectures cut the operational deficit nearly in half while still passing critical semantic state forward. Most production systems should target this range first.
*   **T-04: 100% ROP requires task decomposability.** Fully stateless execution demands upfront architectural investment in defining clean packet boundaries. It's not free — it's a design trade-off.

---

**ROP FRAMEWORK — PACKET 02**
**RESTART OFTEN PROTOCOL**
