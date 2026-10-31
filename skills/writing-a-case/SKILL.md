---
name: writing-a-case
description: "Writes a decision case from a Nala study: the decision, What we heard, The case against, Our call and What we'll do, each part your point then Nala's evidence, sent into the case in Nala as suggestions the author keeps or dismisses. Use when the user wants a case, a recommendation or a write-up for stakeholders from a Nala study, or to fill in or add to a case they have open in Nala."
---

# Writing a case

A case is a doc a team writes to argue for one decision from its research, for readers who weren't in it. Its title is the decision; its sections are **What we heard**, **Our call** and **What we'll do**. You write it, and Nala checks every count against the evidence it rests on. The author decides: everything you send lands as a suggestion they keep, edit or dismiss. Follow [`using-nala`](../using-nala/SKILL.md) for counts, citations and provenance.

Every part of the doc reads **point, then evidence**: a subheading that says the point, your words saying what it means for the decision, then Nala's block or quotes that show it. A reader skimming the subheadings gets the argument; a reader who stops at any one finds its proof right under it.

## 1. Find the study and the case

1. `list_studies` for the study the user means. If more than one could fit, ask.
2. Find the case. The user has one open if they gave a case id or a `/cases/<id>` link, or if `list_cases` lists one they mean (match on its title, the decision). Then **write into that case**: never make a second.
3. With no case, ask the user for the decision in a line if they haven't given one, or offer the study's own decision (in `get_overview`'s project header). If there's no decision at all, the case is a findings report: you'll skip Our call. Then `create_case_draft` with `project` and `decision` only: it makes the doc with its three sections, empty, and gives its `case_id`. If the connection can't save drafts, you'll write the case as text in the chat, every claim linked, following steps 2 to 5 in the same shape.

Done when you have a case id, or know you're writing it as text.

## 2. Read the evidence

`get_case_draft` with `include: ["overview", "requests"]`. Note each section's `heading_id`, what the author already wrote and cites, which lines are still suggestions, and the research questions. (Writing as text: `get_overview` with `quotes_per_theme: 3` and `list_requests` instead.)

- **`not_saved_yet`**: the author opened the case but hasn't saved it, so its sections are the template's and have no `heading_id`. Aim at each section by its words ("What we heard"); they land in the template the author sees.
- **No title**: the case's title is the decision, and the author hasn't written one. Write to the study's decision, and say in your hand-back that the case still needs its title.

Each research question's `nala_answer` is Nala's own reading of it, a lead and points with their people: start each take from it, saying what it means for the decision rather than repeating it (its block shows it). `get_overview`'s `nala_reading` sums up the whole study; read it, and cite the passages it rests on, never the reading. Its `cited` and openings' `quotes` are links only: to hang one of those passages under a line, find it with `get_topic` or `search_evidence` for its `mention_id`.

Then go after the **case against** as hard as the case for: `search_evidence` with `queries` (every search in one call) for what argues against the likely call, and `get_topic` with `topics` (every theme in one call) where a theme needs more than 3 quotes; its `by_person` gives one quote from each person who raised it.

Every quote you can cite carries a `mention_id`: `get_topic`'s and `get_overview`'s quotes, each `nala_answer` point's quotes, and each `search_evidence` result. A search result's `text` is the passage cut to what matched; its `quote` is the quote word for word. Quote `quote`. A result with no `mention_id` (a Feedback study) can't be hung under a line: cite its theme instead.

Done when every research question has evidence or is known to have none, and you've searched for the case against.

## 3. Bring what the user's product knows

A case argues with more than the study. If the user's AI has their analytics, codebase, docs or roadmap within reach, look there for what bears on the call: a cost, a dependency, usage that confirms or contradicts the study, a market fact. Each one goes in as a **context** note with `source_label` (and `source_url` when there is one). Nala shows it as outside the study and never counts it. When nothing is within reach, skip this step: Our call then carries only the risks the user gives you.

## 4. Lay it out

Nala's blocks carry the evidence, live: a **question block** shows Nala's answer to a research question, its points, their quotes and who spoke, and a **person block** shows one participant's quote to remember and their snapshot. You write the argument above them. Never restate what a block shows.

`get_case_draft` lists the blocks already in the doc (`type: "question"`, `type: "person"`, often from the author's /draft). Add only the ones missing; where a block is already there, your subheading and take still go in, aimed at its section.

Use two heading levels:

- **Level 2** (`heading`, `level: 2`) is a section. The doc has three; you add one, **The case against**.
- **Level 3** (`heading`, `level: 3`) is a subheading inside a section. It says the point in a few words, as a finding: "Nobody knew who an alert reached", "Contacts met the app through an alarm". Name a part by what it shows, never by its kind ("Findings", "Q1").

The doc, top to bottom:

```
## What we heard
### <what Q1's answer shows>        heading, level 3
<what it means for the decision>    take, question 1
[Q1 block]                          question 1
### <what Q2's answer shows>
…
### <another point the blocks miss>  heading, level 3
<the point>                         paragraph, its quotes hung under it
### Who we heard from
[P1] [P2] [P3]                      person
## The case against                 heading, level 2
<a point against the call>          paragraph, with its own evidence
### What this can't tell us
<a small sample, a theme few raised, a question nothing answered>
## Our call
<the call, because …>               call
### Risks
<a risk from outside the study>     risk; context notes from step 3
## What we'll do
### What it means                   do, implication
### Next steps                      do, step (a row of them is one to-do list)
### How we'll know                  do, measure
### What to test                    do, test
```

## 5. Write it

A paragraph is a line or two in the author's voice, then what it means for the decision. Its evidence is the 1 to 6 theme or quote ids it rests on, strongest first. When a paragraph says how many, put what that count is about first in its evidence (the theme, or the quotes): Nala checks the count words against the first piece.

- **What we heard.** For each research question, in order: a level-3 subheading saying what its answer shows, then one `take` (its number) saying what that means for *this decision*, in one to three sentences, then its `question` block straight after the take. Nala prints the question on the block, so the take doesn't name it. Then a subheading for each point that matters and isn't on the page yet (a theme no question covers, a quote from someone the blocks leave out), with its paragraphs. In an interview study, end with a **Who we heard from** subheading and a `person` item for each of the 3 or 4 people the answers lean on most (their label, "P2").
- **The case against**, sent last among What we heard's items, so it lands just before Our call: a level-2 heading, then each point against the likely call as a paragraph with its own evidence, then a **What this can't tell us** subheading with what the data can't show. It's a section of its own because the case's brief counts the themes under it as against the call, not for it.
- **Our call**, only with a decision. One `call` item, with `call` (the recommendation in a sentence) and `because` (the line that runs through what you heard, as the rest of a sentence after "Because"). A paragraph never becomes the case's call. If /draft already put a call there, send yours only if it says something different, as a choice for the author. Then a **Risks** subheading, each risk from outside the study as a `risk` item, and the context from step 3 as `note` items (`note_kind: "context"`, with `source_label`). Anything argued *from* the study belongs in The case against, with its evidence.
- **What we'll do**, a subheading per part. **What it means**: one or two `do` items of `type: "implication"`. **Next steps**: `type: "step"`, plain actions, sent one after another so they arrive as one to-do list; owners and dates are the author's. **How we'll know**: one `type: "measure"`, the metric alone (the author adds today's value and the target). **What to test**: the assumptions the call rests on that the study hasn't settled, each `type: "test"`, worded as a statement Nala can check against every interview ("Contacts who were warned act on an alert"), from `get_overview`'s `to_test` and the case against. Each arrives as a test block the author runs, and Nala counts the people for and against.

Where the author has renamed, added or removed sections, put each part where it belongs. A section you name by words that the doc doesn't have arrives as a new section at the end of the doc.

## 6. Send it

1. Send the whole write-up in **one** `suggest_on_case` call, as `sections`, each `under_heading` its `heading_id` (or its words, when `not_saved_yet`), with `done: true`. The doc holds 60 suggestions at a time: 60 items at most.
2. Lines that come back in `held_back` said more than their evidence: rewrite each with the words Nala gives and send just those again.

The reply's `items_sent` is what you sent; `suggested` is the blocks those made in the doc (a paragraph with quotes is its line and its evidence group, a theme card one more, a row of steps one list).

Done when nothing is held back, or you've told the user which lines still are.

## 7. Hand back

In the chat, in a few lines:

- their suggestions are waiting in the case (its `nala_link`);
- what you left out, since the doc keeps no note of it;
- whether the case still needs its title;
- if the user has `designing-ux-experiments`, that it designs the experiment for each assumption under What to test, beyond what the study can show.

Leave the write-up itself out of the chat: Nala is where it's read.
