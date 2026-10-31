---
name: identifying-opportunities
description: "Builds an opportunity solution tree (Teresa Torres) from a Nala study: the outcome the team wants to move, the customer needs behind it as a tree of opportunities, each resting on Nala's themes and quotes, and the one to work on first. Use when the user wants opportunities, an opportunity solution tree, unmet needs, or where to focus next from their research."
---

# Identifying opportunities

An **opportunity** is a customer need, pain or desire, said from the customer's side: "Wants to know a route is safe before setting off", not "Add a safety score". The tree runs from the outcome the team wants to move, through the opportunities that could move it (broad ones above, specific ones beneath), to solutions at the leaves. Nala supplies the evidence for the opportunities. The outcome, and how much each opportunity matters to the business, come from the user's side.

Every claim carries its provenance (Nala, your data, or inference) as [`using-nala`](../using-nala/SKILL.md) defines it.

## 1. Set the outcome

`list_studies` for the study, then `get_overview` with `quotes_per_theme: 3`. The root of the tree is one **product outcome**: a behaviour the team can move and measure ("more runners plan a route before they start"), not a business result ("revenue") or a feature. Find it in this order:

1. what the user said;
2. their OKRs, roadmap or docs, if their AI can reach them;
3. the study's decision, in `get_overview`'s project header, reworded as the outcome it serves.

Show the user the outcome you'll use, and where it came from, before building on it. With none of the three, ask.

Done when the user has agreed one outcome.

## 2. Gather candidates

Collect every candidate opportunity, each with the ids it rests on:

- **Openings** from `get_overview`'s `nala_reading`: needs two or more people lived, each with its passages and asks. Nala's reading, already worded as needs: a strong start, cited by its quotes.
- **Themes** from `get_overview`. Pains, workarounds, goals and triggers are opportunities, or point straight at one; tools, behaviour and praise are context for them.
- **Requests** from `list_requests`. Every ask is a solution in disguise: write down the need behind it, and keep the ask as a solution under that need. Read each with its `said_next`, which often says what the need is.
- **Interview snapshots**, in an interview study of up to about 20 people: `get_participant` with `participants` (10 a call). Each person's opportunities (In their way, Ideas they had, Why it matters to them), both Nala's lines and the ones an editor kept, are already written as needs. A need only one person has is still a candidate; mark it as one person's. A person's `portrait` is Nala's summary of them: cite the passages it points to, never the portrait.
- **To test**, from `get_overview`'s `to_test`: one person's point that no theme took. A candidate, never yet a pattern.

Done when every theme, request and `to_test` point has been read and either became a candidate or was left out as context.

## 3. Write each opportunity

Merge candidates that are the same need. Word each one:

- as a need in the customer's world, in plain words, never in their voice or quotation marks (their own words are the quotes it cites);
- with **no solution inside it**: if it names a feature, ask what that feature is for, and write that;
- with its evidence: the themes (with counts) and one or two quotes, each linked.

**Counts don't add.** Two themes of 6 and 5 people may be the same 6 people. An opportunity resting on several themes carries each theme's count, or "at least 6 of 18" from the largest. Never their sum.

## 4. Build the tree

Group the opportunities under the outcome. A parent is a broad need; its children are specific ways that need shows up, each wholly inside its parent. Aim for 3 to 5 parents; an opportunity that fits under none is its own parent.

Nala's sub-themes can help split a parent: `get_subthemes` with `topics` (every theme you need, 10 a call). Every link in the tree, from child to parent and from parent to outcome, is your reading: say so where it isn't obvious.

Done when every opportunity sits in exactly one place and each parent's children are distinct from each other.

## 5. Compare and pick

Compare **siblings** (the children of one parent, or the parents), not the whole tree. For each one, give:

- **Customer:** how many raised it (Nala) and how much it hurts them, from their words: a workaround they built or a cost they named shows more pain than a passing mention.
- **Reach:** how many users hit it, from product data, or marked unknown. An interview count is never a share of users.
- **Business:** fit with the team's strategy and what it's worth, from the user's side, or marked unknown.

Recommend one **target opportunity**, the one you'd work on first, and why, in a line naming what that rests on. The team makes the call.

## 6. Hand back

Show the tree as a nested list: outcome, then parents, then children, each with its evidence linked, then the asks under the opportunity they serve as solutions. Then give the comparison and your target.

Then offer, in a line each:

- **Solutions:** three or more different ways to address the target, including the participants' own ideas (labelled as theirs) and anything their product context suggests.
- **`designing-ux-experiments`**, to test the riskiest assumption behind the target or one of its solutions.
- **`writing-a-case`**, if the team needs to argue for working on the target.
