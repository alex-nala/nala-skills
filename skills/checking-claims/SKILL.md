---
name: checking-claims
description: "Checks a PRD, deck, strategy doc, message or draft against a Nala study: finds each claim about customers, cites the evidence behind it, has Nala count it, and rewrites what says more than the research shows. Use when the user wants a doc fact-checked, checked against the research, or asks whether the evidence backs what they wrote."
---

# Checking claims

Docs drift from their research: "most users" where 4 of 11 said it, "customers want" where one person asked. This skill finds each claim a text makes about customers, ties it to the evidence in Nala, and has Nala count it. Nala checks **count words** against the evidence; you find the evidence, judge the rest, and rewrite. Follow [`using-nala`](../using-nala/SKILL.md) for counts, citations and provenance.

## 1. Get the text and the study

The text is what the user pasted, a file or doc they pointed at, or your own draft. `list_studies` for the study it rests on; if it draws on several, check it against each in turn. `get_overview` with `quotes_per_theme: 3`.

## 2. Find the claims

Go through the text sentence by sentence and list every **claim about customers**: what they do, feel, want or ask for, how many, how often. Count words ("most", "many", "few", "7 of 18", "40%") mark the obvious ones; "users struggle with onboarding" is a claim too.

Leave out claims about the product, the market or the team; mark each as **outside the study** and move on.

Done when every sentence has been read and each claim is listed or left out with its reason.

## 3. Find each claim's evidence

For each claim, find what in the study it rests on: a theme from `get_overview`, a request from `list_requests`, a research question, or quotes from `search_evidence` (all the claims' searches in one call, with `queries`). Pick the evidence the claim is *about*: for "most people plan on paper", the theme about planning on paper, not a quote that mentions paper.

A claim with nothing behind it after a second search with its key words has **no evidence in the study**.

## 4. Have Nala count it

Send the text to `check_claims` with each claim followed straight away by its evidence: `[theme:<id>]`, `[request:<id>]`, `[question:<id>]`, `[quote:<id>]`, or several, `[quotes:<id>, <id>]`. Up to 20,000 characters a call; check a longer text in parts.

Each claim comes back with its count and a verdict on its count words:

- **holds:** keep it.
- **says more than the evidence**, **doesn't match the evidence**, or **a percentage on fewer than 20:** rewrite with `say_instead`, or with the count itself.
- **no count word:** Nala gave the count; you judge whether the sentence's meaning fits that evidence ("users struggle with onboarding" resting on 2 of 14 needs its count).
- **no evidence cited:** count words with nothing cited. Go back to step 3.

Nala checks count words; it doesn't judge the argument. Two overreaches pass its check, so you flag them, each as your reading:

- **Meaning:** the count holds but the evidence says something weaker. "Most runners want Garmin integration" on a theme of 2 of 3, where one of the two relies on their Garmin and only one asked for integration, hypothetically. Read the theme's quotes (`get_topic`) and the asks behind it before letting "want" stand.
- **Reach:** a claim about the user's users ("60% of users", "our customers") rests on interviews. A count from Nala is the people interviewed; reach comes from the user's data, or the claim is rewritten to be about the people interviewed.

Done when every claim has a verdict and every rewrite holds when checked again.

## 5. Hand back

1. **The verdict table:** each claim, its verdict (holds, rewritten, no evidence in the study, outside the study), its count and its evidence linked.
2. **The text, rewritten**, changing only what the table changed, with Nala links on the words they back, so a reader of the doc can check it.

If the text is a case in Nala, give the table in the chat and offer `writing-a-case` to send the rewrites into the case as suggestions.
