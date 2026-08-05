# SOTAC — Special Operations Tactical Command

A squad tactical simulation. You write the plan; you don't drive the soldiers.

Lay out routes, pick a way in, set contingencies and loadouts, then hit execute and
watch eight men try to carry it out. Every decision they make is scored and written
to a log in plain language, so when something goes wrong you can read *why* rather
than guess.

SOCOM-inspired. Single HTML file, no build step, no dependencies.

**Play it: (https://lodestaraptitude.github.io/sotac/)**

---

## What you're actually doing

You are not commanding individual soldiers. You are writing orders and watching them
meet reality.

1. **Pick an operation** — six of them, across four biomes, from a single-objective
   grab to a five-task sprawl.
2. **Plan** — draw waypoints on the map, choose a way in (gate, wall breach, culvert,
   roof), set tempo, coordination, contingencies and each man's weapon and kit.
3. **Execute** — and then you're a spectator. Element leads improvise when the plan
   stops working, and every improvisation costs you score.

The score is *outcome minus how much your leads had to save you.* A clean plan needs
few deviations. Graded S through F.

## Reading the log

The log is the point of the game. Filter it with the buttons above it.

- **DECISION** — an individual's choice, with the runner-up option and the score gap.
  Close calls show a bar so you can see how nearly he did something else.
- **LEAD** — an element lead's call: halting on a sentry, splitting the squad,
  detailing a man to work an objective.
- **DEVIATION** — the plan stopped working and someone improvised. These cost score.
  They are the most useful thing in the log.
- **CONTACT / CASUALTY / PHASE** — what happened and when.

## How to give feedback

**Export the log.** Button at the top of the log panel. It writes a text file with the
full plan, the seed, every soldier's traits and loadout, the garrison, and every scored
decision. Attach it to an issue.

Without the log a report is very hard to act on. With it, most bugs are findable in
minutes — the log has caught men shooting through walls, squads walking to the wrong
entry, and a whole feature that was silently doing nothing.

Open an issue and say what looked wrong. "They bunched up and it ruined the firefight"
is a perfectly good bug report.

## Known rough edges

Honest list, as of this build:

- **Line of sight vs. drawn tracers.** Sightlines are sampled along the true firing
  line, but a round can still graze the exact corner of a wall block. About 2% of
  tracers. Fixing it properly means giving walls real thickness.
- **Cohesion is over-engineered.** Several overlapping systems keep an element
  together (formation slots, catch-up, lead ease-off, bounding limits). They no longer
  fight each other, but it is more machinery than the problem needs.
- **The stealth layer barely runs.** Roughly 28% of mission time is pre-alarm, so the
  lead's quiet decisions — hold for a patrol, bypass, silent takedown — fire rarely.
- **One squad on a 3+ task operation is brutal.** Flagged in the mission brief. It is
  meant to be hard, but it is *very* hard.
- **Numbers move between runs.** Same plan, different seed, very different mission.
  Judge behaviour, not one result.

## Tuning it yourself

Everything balance-related is in one `CFG` block near the top of `index.html` — about
110 named constants with comments: movement speeds, detection rates, hit chance curve,
suppression, timings, scoring. Change a number, reload, play.

`CFG` throws loudly on an undefined key rather than silently producing `NaN`, which is
a lesson learned the hard way — a missing key once disabled enemy fire entirely and
every mission came back looking perfect.

## Running locally

It's one file. Open `index.html` in a browser. That's it.

Everything is generated from the seed — terrain, buildings, patrol routes, soldier
traits, every dice roll. Same seed plus same plan gives the same mission, so you can
change one order and see exactly what it changed.
