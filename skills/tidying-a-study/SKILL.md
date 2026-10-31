---
name: tidying-a-study
description: "Suggests the work an editor does on a Nala study's own pages: each participant's interview snapshot (Teresa Torres: opportunities, insights and the quote to remember) and names for a theme's unnamed sub-themes, every line citing its passages, landing in Nala as suggestions an editor keeps or dismisses. Use when the user wants interview snapshots, a participant's snapshot rewritten, or sub-themes named."
---

# Tidying a study

Two jobs on a study's own pages in Nala, both **suggestions** beside Nala's own lines until an editor keeps, edits or dismisses them. Pick the branch the user asked for. Follow [`using-nala`](../using-nala/SKILL.md) for citations and provenance.

## Snapshots

Teresa Torres' interview snapshot of one person: their needs, how they work, and the quote that says most about them, from their passages only.

1. `list_studies`, then `get_participant`: with their label ("P2") for one person; for everyone, with no participant for the list, then `participants` 10 at a time in interview order. Each comes back with their passages in six sections (each with its id), their snapshot so far (`by_nala`, lines an editor kept, suggestions waiting), and sometimes a portrait: Nala's summary of them, not evidence.
2. Write each person's snapshot:
   - **Opportunities:** a need of theirs as a short summary about them, "Wants to know a route is safe before setting off", never a feature. Up to 3 under each of `way` (In their way), `ideas` (Ideas they had) and `why` (Why it matters to them).
   - **Insights:** what you'd tell a teammate about how this person works, at most 1 under each of `today` (How they work today), `happened` (What happened) and `worked` (What worked).
   - **The quote to remember:** one of their passages by id, the one that says most about them, with a `reason` in a line.

   Write each line as a summary about them, in your words: their own words are the passages it cites. Every line cites the passage ids it rests on, this person's only. Skip a section their passages don't support.
3. Suggest beside Nala's lines only where you'd say it better or add what they miss; leave kept lines alone.
4. `suggest_snapshot` with the person and their lines, one person a call. A refused call names the line: fix it and send again.

Done when each person has been sent, or skipped with a reason (nothing to add to what's kept).

## Sub-theme names

Nala groups a theme's quotes into sub-themes and leaves naming them to an editor.

1. `get_overview` for the themes, then `get_subthemes` with `topics` (10 a call): the user's theme, or every theme, strongest first. Skip sub-themes that already have a name.
2. Name each for what its quotes have in common: a short finding in plain words, up to 12 words, in the participants' world, "They plan runs around daylight" rather than "Daylight". Use only the quotes `get_subthemes` returned. A sub-theme whose quotes share no idea gets no name: tell the user it may not be a real sub-theme.
3. Show the user the names by theme, each with one quote that backs it, and send them only once they agree: `suggest_subtheme_names`, one theme a call.

Done when every unnamed sub-theme has a suggested name or a reason it has none.

## Hand back

In the chat, in a few lines: what you suggested, where it's waiting (the person's or theme's `nala_link`), and what you skipped and why.
