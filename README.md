# TextQL Design Work Sample

One workflow, seen two ways. A design work sample for TextQL.

**Live:** https://textql-design-work-sample-janhavi4.vercel.app

---

## What this is

A prototype for a workflow tool that serves both data engineers and operations
teams from a single workflow object, rather than splitting them across separate
products the way Airflow and Zapier do today.

The scenario is Fashion Week: pulling RSVP data, matching it against guest
profiles, then seating each VIP, notifying the team and confirming the guest.

## Running it

Open `index.html`. No build step, no dependencies, no server. Everything is in
one file.

Inter loads from Google Fonts, so it falls back to the system sans-serif offline.

## What to try

**The two views.** Toggle Ops and Data in the top bar. Same ten steps, drawn
two different ways, with node contents that change to suit who is asking.

**The fold.** Each view collapses the other half into one dashed node. Click it
to open the hidden half in place.

**Editing SQL redraws the graph.** In the Data view, open "Clean, join and save
the guest list" and delete the `left join profiles` line. The connector from
"Pull guest profiles" disappears. Type it back and it returns. Nobody drew those
arrows.

**Ask Ana.** Bottom right, or ⌘K. Try "stop losing guests whose emails don't
match." Ana names the three guests, asks one question about how to handle them,
then proposes a diff you accept or discard.

**The missing records.** In the Ops view, open "Assign show and seat" and the
History tab. Three guests never arrived. The panel names them and links to the
step upstream that lost them.

**Version history.** Change any field, then open the Versions tab on that step.
The edit is recorded with its old value and a one-click restore.

**Consequences before an edit.** Change a retry or error setting and a dialog
lists what the change touches and what runs after it.

## How it is built

A single `STEPS` array near the top of the file is the workflow. Both views,
the side panel, the graph edges and the source drawer are all rendered from it.
Changing one value updates everywhere, which is the entire argument of the
design.

Connectors declare their own fields, so two steps on the same connector always
show the same shape, and the only difference between them is the values someone
chose.

Styling is built on a token layer taken from a shadcn design system, using the
slate scale, Inter, and a green primary.

## Documents

Diagrams used in the writeup are in `docs/`.

| File | What it shows |
|---|---|
| `runway-problem.png` | Where a guest is lost between two disconnected tools |
| `runway-ia.png` | How one workflow record renders as two views |
| `runway-sitemap.png` | Every screen, panel and dialog in the prototype |
