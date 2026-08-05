# SOTAC

**Special Operations Tactical Command**

## ▶ [Play it](https://lodestaraptitude.github.io/sotac/)

A squad tactical simulation. You write the plan. You don't drive the soldiers.

Lay out routes, pick a way in, set contingencies and loadouts, then hit execute and
watch eight men try to carry it out. Every decision they make is scored and written to
a log in plain language, so when something goes wrong you can read why instead of
guessing.

SOCOM inspired. Single HTML file, no build step, no dependencies.

---

## What you're actually doing

You are not commanding individual soldiers. You are writing orders and watching them
meet reality.

1. **Pick an operation.** Six of them across four biomes, from a single objective grab
   to a five task sprawl.
2. **Plan.** Draw waypoints on the map, choose a way in (gate, wall breach, culvert,
   roof), set tempo, coordination, contingencies, and each man's weapon and kit.
3. **Execute.** Now you're a spectator. Element leads improvise when the plan stops
   working, and every improvisation costs you score.

Your score is the outcome minus how much your leads had to save you. A good plan needs
few deviations. Graded S down to F.

## Reading the log

The log is the point of the game. Filter it with the buttons above it.

**DECISION** is an individual's choice, showing the runner up option and the score gap.
Close calls draw a bar so you can see how nearly he did something else.

**LEAD** is an element lead's call. Halting on a sentry, splitting the squad, detailing
a man to work an objective.

**DEVIATION** means the plan stopped working and someone improvised. These cost score,
and they are the most useful line in the log.

**CONTACT**, **CASUALTY** and **PHASE** cover what happened and when.

## How to give feedback

**Export the log.** The button sits at the top of the log panel. It writes a text file
with the full plan, the seed, every soldier's traits and loadout, the garrison, and
every scored decision. Attach it to an issue.

Without the log a report is very hard to act on. With it, most bugs turn up in minutes.
The log has already caught men shooting through walls, squads walking to the wrong
entry point, and a whole feature that was silently doing nothing at all.

Open an issue and say what looked wrong. "They bunched up and it ruined the firefight"
is a perfectly good bug report.

## Known rough edges

An honest list as of this build:

**Sightlines versus drawn tracers.** Shots are checked along the true firing line, but a
round can still graze the exact corner of a wall block. Roughly 2% of tracers. Fixing it
properly means giving walls real thickness.

**Cohesion is over engineered.** Several overlapping systems keep an element together:
formation slots, catch up speed, lead ease off, bounding limits. They no longer fight
each other, but it's more machinery than the problem needs.

**The stealth layer barely runs.** Only about 28% of mission time happens before the
alarm, so the lead's quiet decisions (hold for a patrol, bypass, silent takedown) fire
rarely.

**One squad on a three plus task operation is brutal.** The mission brief flags it. It's
meant to be hard, but it is *very* hard.

**Results swing between runs.** Same plan, different seed, very different mission. Judge
the behaviour, not one result.

## Tuning it yourself

Everything balance related lives in one `CFG` block near the top of `index.html`. About
110 named constants with comments covering movement speeds, detection rates, the hit
chance curve, suppression, timings and scoring. Change a number, reload, play.

`CFG` throws loudly on an undefined key instead of quietly producing `NaN`. That one is
a lesson learned the hard way: a missing key once disabled enemy fire entirely and every
mission came back looking perfect.

## Running locally

It's one file. Open `index.html` in a browser. That's it.

Everything is generated from the seed: terrain, buildings, patrol routes, soldier traits,
and every dice roll. The same seed with the same plan gives the same mission, so you can
change a single order and see exactly what it changed.
