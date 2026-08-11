# SOTAC

**Special Operations Tactical Command**

## ▶ [Play it](https://lodestaraptitude.github.io/sotac/)

A squad tactical simulation. You write the plan. You don't drive the soldiers.

Lay out routes, pick a way in, set contingencies and loadouts, then hit execute and
watch eight men try to carry it out. Every decision they make is scored and written to
a log in plain language, so when something goes wrong you can read why instead of
guessing.

Single HTML file, no build step, no dependencies.

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

## The men

Four soldiers per element, generated from the seed. Four traits, none of them cosmetic:

| | |
|---|---|
| **Aggression** | how readily he closes and shoots rather than waiting |
| **Discipline** | how closely he holds to the plan under pressure |
| **Marksmanship** | his chance of hitting what he aims at |
| **Nerve** | how much fire he takes before he breaks |

**Balanced** (the default) guarantees each element has a marksman, someone who holds
under fire, someone who will go first, and a lead who keeps the plan together. The rest
of each man is still rolled, so you will still get a Dunn with nerve 2. **As they come**
rolls them straight; about one element in ten then has nobody who can shoot.

The dice are deliberately worth less than the plan. Marksmanship swings a shot by about
13 points; getting the enemy out of cover is worth about 22. A poor shot is a liability
to work around, not a mission you have already lost.

## Map events

A wildfire, lava, meteorites, a flood or a landslide can start mid mission, between
T+45s and T+150s. It rewrites the ground permanently and does not care whose side anyone
is on. Each has its own pace and reach:

| | pace | takes |
|---|---|---|
| **Landslide** | all at once | a hillside, instantly |
| **Meteorite** | 23 small impacts over about a minute | craters and rubble |
| **Wildfire** | crawls, then does not stop | up to a third of the map |
| **Flash flood** | slow to start, then wide | the low ground |
| **Lava flow** | barely moves, never gives anything back | a third of the map, permanently |

An event will never bury an outstanding objective, but it will close the way to one. If
the last route in goes, the lead writes the task off out loud and it scores as a failure.

## Reading the log

The log is the point of the game. Filter it with the buttons above it.

**DECISION** is an individual's choice, showing the runner up option and the score gap.
Close calls draw a bar so you can see how nearly he did something else.

**LEAD** is an element lead's call. Halting on a sentry, splitting the squad, detailing
a man to work an objective.

**DEVIATION** means the plan stopped working and someone improvised. These cost score,
and they are the most useful line in the log.

**CONTACT**, **CASUALTY** and **PHASE** cover what happened and when.

The debrief also breaks down **who shot what and how it went**: rounds, hit rate, kills
and average engagement range per man per weapon. A low hit rate is not always a bad man.
An automatic rifle is scored on what it pins down, and a marksman rifle firing at four
metres is the wrong tool rather than a bad shot.

## Reference

The **Reference** button above the map opens a sheet covering every terrain type with its
real movement, concealment and sightline numbers, what each map event does and what it
does to you, and what every symbol on the map means.

It is generated from the live tuning tables when you open it, not written by hand, so it
cannot drift out of step with the game.

## How to give feedback

**Export the log.** The button sits at the top of the log panel. It writes a text file
with the full plan, the seed, the settings, which map event rolled and whether it fired,
every soldier's traits and loadout, the garrison, and every scored decision. Attach it to
an issue.

Without the log a report is very hard to act on. With it, most bugs turn up in minutes.
The log has already caught men shooting through walls, squads walking to the wrong entry
point, a whole feature that was silently doing nothing, and a crash that froze the game
every time a hostage was rescued.

If the picture ever stops updating, the game now says so in the log with the actual error
in it. That line is the useful part of the report.

Open an issue and say what looked wrong. "They bunched up and it ruined the firefight" is
a perfectly good bug report.

## Known rough edges

An honest list as of this build:

**Pathfinding failures.** About one man in ten at any moment is stuck with no path at
all, on average 46 cells short of where he is going. This is the largest outstanding
problem and the cause of most "they got caught on something" reports.

**Formation slots put men on the wrong side of walls.** Related to the above, and the
reason an element occasionally strings out around the wrong face of a building.

**Sightlines versus drawn tracers.** Shots are checked along the true firing line, but a
round can still graze the exact corner of a wall block. Roughly 2% of tracers. Fixing it
properly means giving walls real thickness.

**Cohesion is over engineered.** Several overlapping systems keep an element together:
formation slots, catch up speed, lead ease off, bounding limits. They no longer fight
each other, but it's more machinery than the problem needs.

**The stealth layer barely runs.** Only about 28% of mission time happens before the
alarm, so the lead's quiet decisions (hold for a patrol, bypass, silent takedown) fire
rarely.

**The flank option is effectively dead.** Offered a few hundred times a mission, wins
under 2% of them.

**One squad on a three plus task operation is brutal.** The mission brief flags it. It's
meant to be hard, but it is *very* hard.

**Results swing between runs.** Same plan, different seed, very different mission. Judge
the behaviour, not one result.

## Tuning it yourself

Everything balance related lives in one `CFG` block near the top of `index.html`. Around
150 named constants with comments covering movement speeds, detection rates, the hit
chance curve, suppression, map events, timings and scoring. Change a number, reload, play.

`CFG` throws loudly on an undefined key instead of quietly producing `NaN`. That one is
a lesson learned the hard way: a missing key once disabled enemy fire entirely and every
mission came back looking perfect.

## Interface

Above 1180px wide the page is a fixed frame that never scrolls: mission settings on the
left, the men beside the map, the map in the middle, the log on the right. Every panel
header collapses. Below that it stacks for phones.

Three looks are available from the **Look** switcher in the header. **Channel** is the
default, giving each section a filled header band in its own colour. **Sheet** is quieter,
with the colour as a spine down the panel edge. **Rack** treats each column as a piece of
equipment.

There is sound, synthesised in the browser with no files: rifle fire pitched differently
for your weapons and theirs, suppressed fire, men going down, breaching charges, the
alarm, objectives, and a rumble under a map event. Everything is panned by where it
happens on the map. **SOUND / MUTED** sits in the map toolbar.

Hover or tap anything in the plan for an explanation of that specific option.

## License

All rights reserved. See [LICENSE](LICENSE).

The source is public so people can play it and report what looks wrong. It is not
open source, and no permission is granted to reuse it, commercially or otherwise.

## Running locally

It's one file. Open `index.html` in a browser. That's it.

Everything is generated from the seed: terrain, buildings, patrol routes, soldier traits,
which map event you get, and every dice roll. The same seed with the same plan gives the
same mission, so you can change a single order and see exactly what it changed.
