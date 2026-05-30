# High ROP (Restart Often Protocol)
Rooted in the "Commit early, commit often" philosophy, ROP is for working with Coding Agents.

## Basic ROP Workflow
- Agent and/or User saves state continuously to repo.
  - a main TASK.md file
  - a collection of Packets as individual ###.packet.md files
- Packet 1 is when Agent and/or User splits the task into 9 packets.
- After every packet is done, User restarts in new session.
- Or User restarts anytime they want!

## Example
- Task: A complex codebase change with testing and deployment
- 10 packets
- 1 packet = 100,000 tokens
- 1m tokens = $10

## ROP Costs Savings

| Packet | NO ROP     |        |         | 50% ROP  |        |        | 100% ROP |        |        |
|--------|------------|--------|---------|----------|--------|--------|----------|--------|--------|
|        | Tokens     | Cost   | Total   | Tokens   | Cost   | Total  | Tokens   | Cost   | Total  |
| 1      | 100,000    | $1.00  | $1.00   | 100,000  | $1.00  | $1.00  | 100,000  | $1.00  | $1.00  |
| 2      | 200,000    | $2.00  | $3.00   | 200,000  | $2.00  | $3.00  | 100,000  | $1.00  | $2.00  |
| 3      | 300,000    | $3.00  | $6.00   | 100,000  | $1.00  | $4.00  | 100,000  | $1.00  | $3.00  |
| 4      | 400,000    | $4.00  | $10.00  | 200,000  | $2.00  | $6.00  | 100,000  | $1.00  | $4.00  |
| 5      | 500,000    | $5.00  | $15.00  | 100,000  | $1.00  | $7.00  | 100,000  | $1.00  | $5.00  |
| 6      | 600,000    | $6.00  | $21.00  | 200,000  | $2.00  | $9.00  | 100,000  | $1.00  | $6.00  |
| 7      | 700,000    | $7.00  | $28.00  | 100,000  | $1.00  | $10.00 | 100,000  | $1.00  | $7.00  |
| 8      | 800,000    | $8.00  | $36.00  | 200,000  | $2.00  | $12.00 | 100,000  | $1.00  | $8.00  |
| 9      | 900,000    | $9.00  | $45.00  | 100,000  | $1.00  | $13.00 | 100,000  | $1.00  | $9.00  |
| 10     | 1,000,000  | $10.00 | $55.00  | 200,000  | $2.00  | $15.00 | 100,000  | $1.00  | $10.00 |

- ROP reduces the total cost

|          |   Cost | Save |
|:---------|-------:|-----:|
| ROP      | $10.00 |  82% |
| 50% ROP  | $15.00 |  73% |
| NO ROP   | $55.00 |   0% |

## ROP Agent Performance

| Packet |    NO ROP |          |       | 50% ROP |          |       | 100% ROP |          |       |
|--------|----------:|:--------:|------:|---------|:--------:|------:|---------:|:--------:|------:|
|        |   Context | Success  | Total | Context | Success  | Total |  Context | Success  | Total |
| 1      |   100,000 |   80%    |   80% | 100,000 |   80%    |   80% |  100,000 |   80%    |   80% |
| 2      |   200,000 |   75%    | 77.5% | 200,000 |   75%    | 77.5% |  100,000 |   80%    |   80% |
| 3      |   300,000 |   70%    |   75% | 100,000 |   80%    | 78.3% |  100,000 |   80%    |   80% |
| 4      |   400,000 |   65%    | 72.5% | 200,000 |   75%    | 77.5% |  100,000 |   80%    |   80% |
| 5      |   500,000 |   60%    |   70% | 100,000 |   80%    |   78% |  100,000 |   80%    |   80% |
| 6      |   600,000 |   55%    | 67.5% | 200,000 |   75%    | 77.5% |  100,000 |   80%    |   80% |
| 7      |   700,000 |   50%    |   65% | 100,000 |   80%    | 77.9% |  100,000 |   80%    |   80% |
| 8      |   800,000 |   45%    | 62.5% | 200,000 |   75%    | 77.5% |  100,000 |   80%    |   80% |
| 9      |   900,000 |   40%    |   60% | 100,000 |   80%    | 77.8% |  100,000 |   80%    |   80% |
| 10     | 1,000,000 |   35%    | 57.5% | 200,000 |   75%    | 77.5% |  100,000 |   80%    |   80% |

- Assumption: Baseline agent with 80% success rate.
- Assumption: Larger contexts cause increased chance of agent performance degradation.

- ROP improves agent performance

|          | Success | Save |
|:---------|--------:|-----:|
| ROP      |   80.0% |  39% |
| 50% ROP  |   77.5% |  35% |
| NO ROP   |   57.5% |   0% |
