---
name: planning-the-next-round
description: "Plans the next round of research from a Nala study: the questions to test that one person raised and no theme took, the research questions still unanswered, who to talk to next, and an interview guide of story-based questions. Use when the user wants questions to test, what to ask next, who to interview next, a discussion guide, or to close gaps in their research."
---

# Planning the next round

A study answers some questions and opens others. This skill finds the **gaps** (what one person said that nobody else was asked about, research questions with thin answers, people the themes leave out) and turns them into the next round: what to find out, who from, and the questions that get stories rather than opinions. Follow [`using-nala`](../using-nala/SKILL.md) for counts, citations and provenance.

## 1. Read the study

1. `list_studies`, then `get_overview` with `quotes_per_theme: 3`. Note the `decision`, `research_questions` with their `nala_answer`, `to_test`, `people`, `small_sample`, and each theme's `n`, `of` and `not_raised_by`.
2. `list_requests`, and keep the asks made by one person and those marked `hypothetical_only`.
3. In an interview study of up to about 20 people, `get_participant` with no participant for the list, then with `participants` (10 a call) for the people whose interviews look thin or unusual.

Done when you've read `to_test`, every research question's answer, and every request.

## 2. Find the gaps

Collect every gap, each with what it rests on:

- **One person's point:** each `to_test` entry, and each ask made by one person. Something nobody else was asked about, not something others disagreed with. A `to_test` entry's `modality` says whether it happened to them (`actual`), is how things usually are (`habitual`), or is something they imagined (`hypothetical`): a hypothetical point needs a question about what they did.
- **A thin answer:** a research question whose `nala_answer` has no points, or points that few people make. Say how many.
- **A conditional ask:** a `hypothetical_only` request. It shows interest, not behaviour; the next round asks about what they did.
- **A split:** a theme where people's own words pull in opposite directions (`search_evidence` for the other side).
- **Who's missing:** themes from one kind of person, or a decision that rests on a group the study barely heard from. Name the group from the study's own people and filters; the user's data says whether that group matters.

Rank them by what would change the team's call, if the project has a decision; otherwise by how much a theme rests on them. Keep the top five to eight.

Done when each gap you keep names what it rests on, with its link.

## 3. Word the questions to test

Write each gap as a **question to test**: a question about the world, answerable by more interviews, with who raised it and their words. "Do other runners leave their phone at home? (P3: "Because I often don't run with my phone.")". These are leads: never count them as patterns, and never as findings.

## 4. Write the interview guide

For the people the next round should reach, a guide of story-based questions, one block per question to test:

- **Ask for a specific time:** "Tell me about the last time you…", then follow the story: what happened next, what they did, what they used. Past behaviour, not predictions.
- **Leave the answer out of the question.** "How did you decide where to run?", not "Do you worry about safety when you pick a route?"
- **Ask what they did, not what they'd use.** A conditional ask in step 2 becomes a question about what they did the last time the problem came up.
- One or two follow-ups each, and what an answer would tell the team.

Open with a short warm-up and close with "Is there anything I should have asked?".

## 5. Hand back

In the chat:

1. **Questions to test**, ranked, each linked to its evidence.
2. **Who to talk to:** the groups, and why each, marking which came from Nala and which from the user's data or your inference.
3. **The interview guide.**

Then offer `designing-ux-experiments` for any question an experiment would answer faster than interviews (a question about how many, or about behaviour the product can measure), and say which.
