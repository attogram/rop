# Restart Often Protocol (ROP)
The Restart Often Protocol (ROP) is a method of working with AI Agents that
decreases costs and increases developer happiness.

## The Idea
Rooted in the "Commit early, commit often" philosophy, ROP is a
context-management discipline for multi-packet LLM workflows. It focuses on
shedding prior context between execution steps to convert quadratic cost
blow-up into predictable, linear spend.

## The Keyword
**ROP** - The primary keyword and name of the protocol.

## The Metric
**ROPness** - A metric measuring a system's adherence to the protocol, ranging
from 0 to 100.
- 0% ROP: Pure "append everything" approach (quadratic cost).
- 100% ROP: Pure stateless execution (linear cost).

## The Math of ROPness
The higher your ROPness, the leaner your architecture and the further your
compute budget stretches.

### Cost Formula
Total token volume (T) for a sequence of n packets each with base size s, and
ROPness factor r (0.0 to 1.0):

T = n * s + [n(n - 1) / 2] * s * (1 - r)

### ROPness Savings (n=10, s=100k, $10/M)
| ROPness % | Total Tokens | Cost | vs 0% |
| :--- | :--- | :--- | :--- |
| 0% | 5.5M | $55.00 | baseline |
| 20% | 4.6M | $46.00 | −16% |
| 40% | 3.7M | $37.00 | −33% |
| 60% | 2.8M | $28.00 | −49% |
| 80% | 1.9M | $19.00 | −65% |
| 100% | 1.0M | $10.00 | −82% |

### Agent Performance Impact
Larger contexts cause performance degradation. High ROPness keeps context lean,
maintaining higher success rates.

| ROPness % | Avg Success Rate | Total Improvement |
| :--- | :--- | :--- |
| 0% | 57.5% | baseline |
| 50% | 77.5% | +35% |
| 100% | 80.0% | +39% |

## Architectural Mapping
| ROPness % | Architecture | Trade-off |
| :--- | :--- | :--- |
| 0% | Naive Append | Perfect recall, quadratic cost |
| 20% | Sliding Window | Good short-term memory, loses older context |
| 40% | Recursive Summarization | Balanced thematic retention |
| 60% | Vector DB / RAG | Targeted retrieval, lookup latency |
| 80% | Skeleton / State Vars | Minimal overhead, strict schema |
| 100% | Pure Stateless | Linear cost, requires decomposability |
