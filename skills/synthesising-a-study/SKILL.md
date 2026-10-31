---
name: synthesising-a-study
description: "Writes up a Nala study's findings in the chat: each research question answered with its themes, counts and quotes, the rest of the themes by kind, what people ask for, where people differ, what to test next, and what bears on the team's decision. Use when the user wants a synthesis, a findings brief, a summary or a readout of their interviews or feedback in Nala."
---

# Synthesising a study

A synthesis says what a study found, for a reader who wasn't in the interviews, in an order they can act on: the team's own questions first, then everything else that matters. Nala has done the counting; you write it up. Follow [`using-nala`](../using-nala/SKILL.md) for counts, citations and provenance.

If the user wants the synthesis kept in Nala, or has a case open there, use `writing-a-case` instead: it lands in the case as suggestions they review.

## 1. Read the study

1. `list_studies` for the study. If the user named one batch of interviews (an import) or a slice ("only the enterprise customers"), use it as `filters` on every call below and name the slice at the top.
2. `get_overview` with `quotes_per_theme: 3`. Note the project's `decision`, the `research_questions` (each with `nala_answer`), `small_sample`, `nala_reading`, `to_test`, and each theme's `n`, `of`, `raised_by` and `not_raised_by`.
3. `get_topic` with `topics` (`limit: 5`) for the themes whose `top_quotes` don't carry them: `by_person` has one quote from each person who raised it.
4. `list_requests`. Keep asks marked `hypothetical_only` ("I'd use it if…") apart from asks made outright. Read each with its `said_next`, which often finishes it.

Done when you've read every theme 2 or more people raised, and every request.

## 2. Find who lived each ask

An ask is a solution someone imagined; the evidence is the people who lived the problem it would fix. For each ask, `search_evidence` with `queries` (one per ask, up to 10 a call), each the problem in plain words rather than the ask's. Keep only quotes where someone describes that problem happening to them. If you find none, say only that you found none, never that nobody has the problem.

## 3. Write it

In this order, skipping a section with nothing in it:

1. **The sample.** With `small_sample`, one line near the top: what a study this size can and can't show.
2. **The questions**, when the study has research questions, in their order, one section each, its title linked: the answer in a sentence, then the themes behind it with their counts, and one or two quotes. Start from `nala_answer`'s lead and points, and say it in your words; cite the points' quotes. A question asking what people want with no themes behind it is answered from the requests. Only where a question has nothing behind it at all, say nothing in the study answers it yet.
3. **The rest of the themes**: every theme 2 or more people raised that no question section covered, under these headings:
   - Goals (what people are trying to achieve, and why): goal, motivation
   - Pains and workarounds: pain, workaround
   - Triggers (the moments that set things off): trigger
   - Tools and alternatives: tool
   - How the work happens: behaviour, context, decision
   - What they value: praise

   With no research questions, open this with **Key findings**: the three to five themes most people raised, strongest first.
4. **What people ask for**: each ask under its theme (where Nala gave it none, with the theme whose problem it would fix, saying Nala didn't place it there), with who asked and the people from step 2 who lived the problem.
5. **Where people differ.** With 5 or more people, from `not_raised_by`: the themes everyone but one person raised, and who that was. With fewer, where people's own words on a theme pull in opposite directions, each side quoted.
6. **To test**: from `to_test` and asks made by one person, what to take to more people next, most important first, each worded as a question with who said it and their words. These are leads, never patterns.
7. **For the decision**, when the project has one: quote it, then which themes bear on it and how, each linked with its count. Nala doesn't record which way a theme points: if you sort them for and against, say the sorting is yours. The team makes the call.

Done when every theme 2 or more people raised appears in one section, every claim is linked, and nothing says more than its count.

## 4. Hand back

After the synthesis, offer in a line each:

- `writing-a-case`, to argue for a decision from it, in Nala;
- `planning-the-next-round`, to turn To test into the next round's interview guide;
- `identifying-opportunities`, to build the needs into an opportunity tree.
