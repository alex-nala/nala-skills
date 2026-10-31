# Test types

Ordered roughly cheapest first. Pick the first one that can prove the riskiest assumption wrong.

| Test | Proves | Traffic needed | Use when |
| --- | --- | --- | --- |
| **More interviews** | The problem exists beyond the first few people, and what it's like | None: 5 to 8 more people | Nala's count is 1 or 2 people, or the theme comes from `to_test`. Ask about past behaviour, not the idea. |
| **Prototype test** | Usable: people find it and complete the task at the moment it hurts | None: 5 users | The risk is usability. Give a task built on the trigger, then watch. Leave the solution unexplained. |
| **Fake door** | Desirable: people reach for it in the real product | ~100+ users reaching the entry point a week | The risk is "will they want it". Show an entry point, measure clicks, and tell the people who click it's coming. |
| **Concierge / Wizard of Oz** | Desirable and valuable: the outcome is worth it, before building | A handful of real users | The value is uncertain and building is expensive. Deliver it by hand behind a real interface. |
| **Survey to a wider sample** | How common the problem is across users | Enough users to reach 100+ answers | The question is reach, and the problem is easy to recognise in a sentence. Word the question from people's own quotes. |
| **A/B test** | The change moves behaviour, at scale | Enough for the minimum effect you care about (below) | The answer is built or cheap to build, and there's traffic. |

## A/B traffic check

Rough users needed **per variant** to detect a change in a conversion rate, at 95% confidence and 80% power:

`n ≈ 16 × p × (1 − p) / d²`

where `p` is the baseline rate and `d` is the absolute change worth detecting. Baseline 20%, detecting +4 points: `16 × 0.2 × 0.8 / 0.04² = 1,600` per variant. Divide by weekly traffic for the run time. If it's over about four weeks, choose a test higher up the table, or test a bigger change.

When the baseline is unknown, the first step is measuring it.
