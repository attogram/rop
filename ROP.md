# Restart Often Protocol (ROP)
ROP is a context-management discipline for multi-packet LLM workflows. Instead
of feeding every prior token back into each new prompt, ROP quantifies how much
context you drop between steps. This converts quadratic cost blow-up into
predictable, linear spend. The higher your ROP score, the leaner your
architecture, and the further your compute budget stretches.

See [HROP.md](HROP.md) for an Opinionated High ROP Workflow used in this repo.

## What is ROP?
Every time an LLM processes a new step in a multi-turn workflow, you face a
choice: carry forward all previous context, some of it, or none. Naive "append
everything" approaches balloon your token count at a rate proportional to n^2.
This makes long pipelines financially unviable at scale.

ROP (Restart Often Protocol) names and quantifies the degree to which a system
sheds prior context between execution packets. An ROP of 0% means full context
carry-forward. An ROP of 100% means each packet runs entirely stateless. Most
production systems live somewhere in between.

The ROP insight: Engineering ROI in multi-packet workflows is almost never
found in making individual packets faster. It is found in pushing the system
rightward on the ROP spectrum as far as accuracy allows.

## The Math
### Cost Formula
For a sequence of n packets each with base size s, and ROP factor r, total
token volume T is:

T = n * s + [n(n - 1) / 2] * s * (1 - r)

- n = packet count
- s = base packet size
- r = ROP% (0.0 → 1.0)

At baseline (n = 10, s = 100k tokens, $10/M):

| ROP % | Total Tokens | Cost | vs 0% | Savings |
| :--- | :--- | :--- | :--- | :--- |
| 0% | 5.5M | $55.00 | baseline | — |
| 20% | 4.6M | $46.00 | −16% | $9.00 |
| 40% | 3.7M | $37.00 | −33% | $18.00 |
| 60% | 2.8M | $28.00 | −49% | $27.00 |
| 80% | 1.9M | $19.00 | −65% | $36.00 |
| 100% | 1.0M | $10.00 | −82% | $45.00 |

Linear step-down: every 20% ROP increase = −0.9M tokens = −$9.00

### ROP Costs Savings (Detailed Example)
Example task: 10 packets, 100k tokens per packet, $10/M tokens.

| Packet | NO ROP | | | 50% ROP | | | 100% ROP | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | Tokens | Cost | Total | Tokens | Cost | Total | Tokens | Cost | Total |
| 1 | 100,000 | $1.00 | $1.00 | 100,000 | $1.00 | $1.00 | 100,000 | $1.00 | $1.00 |
| 2 | 200,000 | $2.00 | $3.00 | 200,000 | $2.00 | $3.00 | 100,000 | $1.00 | $2.00 |
| 3 | 300,000 | $3.00 | $6.00 | 100,000 | $1.00 | $4.00 | 100,000 | $1.00 | $3.00 |
| 4 | 400,000 | $4.00 | $10.00 | 200,000 | $2.00 | $6.00 | 100,000 | $1.00 | $4.00 |
| 5 | 500,000 | $5.00 | $15.00 | 100,000 | $1.00 | $7.00 | 100,000 | $1.00 | $5.00 |
| 6 | 600,000 | $6.00 | $21.00 | 200,000 | $2.00 | $9.00 | 100,000 | $1.00 | $6.00 |
| 7 | 700,000 | $7.00 | $28.00 | 100,000 | $1.00 | $10.00 | 100,000 | $1.00 | $7.00 |
| 8 | 800,000 | $8.00 | $36.00 | 200,000 | $2.00 | $12.00 | 100,000 | $1.00 | $8.00 |
| 9 | 900,000 | $9.00 | $45.00 | 100,000 | $1.00 | $13.00 | 100,000 | $1.00 | $9.00 |
| 10 | 1,000,000 | $10.00 | $55.00 | 200,000 | $2.00 | $15.00 | 100,000 | $1.00 | $10.00 |

Total Savings:

| | Cost | Save |
| :--- | :--- | :--- |
| 100% ROP | $10.00 | 82% |
| 50% ROP | $15.00 | 73% |
| NO ROP | $55.00 | 0% |

## Agent Performance
Larger contexts cause an increased chance of agent performance degradation. ROP
improves agent performance by keeping context lean.

### ROP Agent Performance Table
| Packet | NO ROP | | | 50% ROP | | | 100% ROP | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | Context | Success | Total | Context | Success | Total | Context | Success | Total |
| 1 | 100,000 | 80% | 80% | 100,000 | 80% | 80% | 100,000 | 80% | 80% |
| 2 | 200,000 | 75% | 77.5% | 200,000 | 75% | 77.5% | 100,000 | 80% | 80% |
| 3 | 300,000 | 70% | 75% | 100,000 | 80% | 78.3% | 100,000 | 80% | 80% |
| 4 | 400,000 | 65% | 72.5% | 200,000 | 75% | 77.5% | 100,000 | 80% | 80% |
| 5 | 500,000 | 60% | 70% | 100,000 | 80% | 78% | 100,000 | 80% | 80% |
| 6 | 600,000 | 55% | 67.5% | 200,000 | 75% | 77.5% | 100,000 | 80% | 80% |
| 7 | 700,000 | 50% | 65% | 100,000 | 80% | 77.9% | 100,000 | 80% | 80% |
| 8 | 800,000 | 45% | 62.5% | 200,000 | 75% | 77.5% | 100,000 | 80% | 80% |
| 9 | 900,000 | 40% | 60% | 100,000 | 80% | 77.8% | 100,000 | 80% | 80% |
| 10 | 1,000,000 | 35% | 57.5% | 200,000 | 75% | 77.5% | 100,000 | 80% | 80% |

Assumption: Baseline agent with 80% success rate. Performance drops as context
grows.

Total Success Gains:

| | Success | Improvement |
| :--- | :--- | :--- |
| 100% ROP | 80.0% | +39% |
| 50% ROP | 77.5% | +35% |
| NO ROP | 57.5% | 0% |

## Architectural Mapping
Each point on the ROP spectrum corresponds to a distinct engineering pattern.
Higher ROP demands more deliberate state design but pays back in efficiency
and scalability.

| ROP % | Architecture | Trade-off |
| :--- | :--- | :--- |
| 0% | Naive Append | Perfect recall, quadratic cost |
| 20% | Sliding Window | Good short-term memory, loses older context |
| 40% | Recursive Summarization | Balanced — themes retained, micro-details at risk |
| 60% | Vector DB / RAG | Targeted retrieval, adds lookup latency |
| 80% | Skeleton / State Vars | Minimal overhead, strict schema dependency |
| 100% | Pure Stateless | Linear cost, requires fully decomposable tasks |

## Strategy
- T-01: The r-Factor is your primary lever. Speeding up individual packets
  gives marginal returns. Moving rightward on the ROP spectrum restructures
  your cost curve entirely.
- T-02: Scale inversion at high n. As pipeline length grows, 0% ROP scales
  as O(n²) — financially unviable for long workflows. High ROP converts
  this to O(n): predictable, budgetable, linear.
- T-03: The sweet spot is 60%. RAG or graph-memory architectures cut the
  operational deficit nearly in half while still passing critical semantic
  state forward. Most production systems should target this range first.
- T-04: 100% ROP requires task decomposability. Fully stateless execution
  demands upfront architectural investment in defining clean packet
  boundaries. It is not free — it is a design trade-off.
