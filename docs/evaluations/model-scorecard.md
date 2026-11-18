# Model scorecard — rule R1 (pensionableSalary)

> One run is a sample, not a benchmark. Synthetic data only — never paste secrets or real member data.

| | Model A | Model B |
|---|---|---|
|  | Model GPT-6 Luna | Model GPT-6 Sol |
| Harness · Mode · Permissions | Copilot · Interactive · Manual | Copilot · Interactive · Manual |
| Reasoning effort | Medium | Medium |
| Date | 18-11-2026 | 18-11-2026 |

## Scores

| Criterion | How to score | Model A | Model B |
|---|---|---|---|
| Correctness verified | Expected values that match the `node -e` output (x / 5) | /5 | /5 |
| Edge cases found | Which did it cover? franchise boundary · salary cap · part-time · below franchise → 0 · invalid factor (0 or > 1) · negative salary | negative salary | negative salary |
| Hallucinations | Invented functions, parameters, files or rules? List them (none = 👍) | none | none |
| Latency feel | fast / ok / slow | fast | ok |
| Cost / credits | Relative cost of the model (supported-models doc) — heavier model = more AI credits | ? | ? |

## Verification output

### Model A
``` shell
 node -e "import('./api/src/domain/pension.ts').then(m=>{for (const [s,f] of [[17545,1],[137801,0.5],[17545.25,0.5],[-1,1],[50000,0]]) console.log(s,f,m.pensionableSalary(s,f))})"
17545 1 0
137801 0.5 60127.5
17545.25 0.5 0.13
file:///C:/Users/DEPE/copilot_advanced_test_depe/api/src/domain/pension.ts:19
    throw new RangeError('fullTimeSalary must be a non-negative number');
          ^

RangeError: fullTimeSalary must be a non-negative number
    at Module.pensionableSalary (file:///C:/Users/DEPE/copilot_advanced_test_depe/api/src/domain/pension.ts:19:11)
    at [eval]:1:144

Node.js v26.13.0
```

### Model B
``` shell
node -e "import('./api/src/domain/pension.ts').then(m=>{for (const [s,f] of [[17545,1],[137801,0.5],[17545.25,0.5],[-1,1],[50000,0]]) console.log(s,f,m.pensionableSalary(s,f))})"
17545 1 0
137801 0.5 60127.5
17545.25 0.5 0.13
file:///C:/Users/DEPE/copilot_advanced_test_depe/api/src/domain/pension.ts:19
    throw new RangeError('fullTimeSalary must be a non-negative number');
          ^

RangeError: fullTimeSalary must be a non-negative number
    at Module.pensionableSalary (file:///C:/Users/DEPE/copilot_advanced_test_depe/api/src/domain/pension.ts:19:11)
    at [eval]:1:144

Node.js v26.13.0
```

## Verdict

- For **this kind of task** I would use: …
- Because: …
- Would I trust it **without** the `node -e` check? yes / no — why?
- To make this a real benchmark I would need: …
