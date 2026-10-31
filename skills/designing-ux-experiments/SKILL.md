---
name: designing-ux-experiments
description: "Designs the experiment that tests what a Nala study found: picks the riskiest assumption behind a theme, request or opportunity, the cheapest test that could prove it wrong, and pass and fail criteria set before it runs, combining Nala's evidence with the user's own product data. Use when the user wants to test, validate or A/B test something from their research, or asks what to build or try next from a Nala theme or request."
---

# Designing UX experiments

Research tells you a problem is real for the people who raised it. An experiment tells you whether your answer to it works for everyone else. This skill goes from one to the other: Nala's evidence on one side, the user's product data on the other, and an experiment brief between them that the team could run this week.

Every claim in the brief carries its **provenance**, as [`using-nala`](../using-nala/SKILL.md) defines it, with assumptions in place of inference:

- **Nala:** a count with its denominator and the `nala_link` it rests on: "[Can't see a route is safe](link), 7 of 18 people".
- **Your data:** what the user's analytics, code or docs show, with the source named: "PostHog, last 30 days: 4,210 weekly route views".
- **Assumption:** what nobody has shown yet. Most of an experiment's job is to turn one of these into one of the others.

A count from Nala says the problem exists and what it's like for those people. Reach, baselines and traffic come from product data, or they stay assumptions. With fewer than 20 people, a Nala count is never a share of users.

## 1. Pin the target

The target is one thing to test: a theme, a request, an opportunity or a solution idea the team has. `list_studies`, then `get_overview` for the study. If the user named the target, find it there (by name, or `search_evidence`). If they didn't, offer the three strongest candidates (themes most people raised, requests most asked, and anything already in `to_test`) with their counts, and let them pick.

Done when you have one target and its `topic_id` or request.

## 2. Read the evidence on it

- `get_topic` for the theme: `by_person` gives one quote from each person who raised it.
- `list_requests` for asks that sit in it, with `said_next`, which often finishes the ask. Keep hypothetical asks ("I'd use it if…") apart: they're weaker evidence of behaviour.
- `search_evidence` with `queries` for the **counter-evidence**: people who solved the problem already, or who said it doesn't bite. Its absence is not evidence either way: say what you searched for.

Write down what people do today (their workaround), the moment it hurts (the trigger), and their words for it. The experiment will measure the first and target the second.

## 3. Bring the product data

Look in whatever the user's AI can reach: an analytics MCP (PostHog, Amplitude, Mixpanel), the codebase, docs, a ticket tracker. You need:

- **Where it happens:** the screen, flow or event where the trigger occurs.
- **Baseline:** today's rate of the behaviour the experiment would move.
- **Traffic:** how many users reach that point a week.

Ask the user for anything you can't find, and mark what's still missing as an assumption. Leave every product number blank rather than estimate it from the interviews.

Done when each of the three is a sourced number or a marked assumption.

## 4. Find the riskiest assumption

List what has to be true for the answer to work, across the four kinds:

- **Desirable:** they want it, and it fixes the problem they described.
- **Usable:** they can find it and use it at the moment it hurts.
- **Feasible:** the team can build it.
- **Viable:** it's worth it for the business.

Mark each assumption **backed** (Nala or product data shows it, with the provenance) or **unbacked**. Nala can back desirability and some usability; feasibility and viability come from the user's side. The riskiest assumption is the one that would sink the idea if it's wrong *and* has the least behind it. Show the user the list and the one you picked, with why.

## 5. Choose the test

Pick the cheapest test that could prove the riskiest assumption **wrong**. Traffic decides what's possible: see [`references/test-types.md`](references/test-types.md) for each test type, what it can prove and the traffic it needs.

## 6. Write the brief

1. **Hypothesis:** "We believe [who] will [behaviour] when [change], because [evidence, with provenance]."
2. **Riskiest assumption**, and why it's the one.
3. **Test:** what changes, for whom, where (step 3's screen or event), and for how long.
4. **Metric:** one primary metric, its baseline (or "unknown: measure first"), and one guardrail metric that must not get worse.
5. **Pass and fail**, set now, before it runs: the result that keeps the idea, the one that kills it, and what the team does after each.
6. **What it rests on:** every claim from steps 2 to 4, by provenance.
7. **What it can't tell you**, in a line or two.

Done when every number in the brief is sourced or marked as an assumption, and pass and fail are both written down.

## 7. Hand off

- If the user has PostHog's MCP or its `creating-experiments` skill, offer to set the experiment up there from the brief.
- If the target is behind a case in Nala (`list_cases`), offer to add the test to its What we'll do section: `suggest_on_case` with a `do` item of `type: "test"` and one of `type: "measure"` for the metric. It lands as suggestions for the author.
- If the right next step is more interviews rather than an experiment, say so, and name what to ask next from `to_test`.
