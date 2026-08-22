---
status: complete
date: 2026-08-16
version: 1.0
phase: F2
tests: H1 (primary), H3 and H4 (secondary)
replaces: docs/discovery/experiments/e1-position-post.md (not runnable by maintainer)
---

# E1-alt — Passive listening

## What was done
E1 (public position post) could not be run. Substitute: read an existing
high-volume discussion where the target audience debates this exact problem
unprompted. Primary source: the Hacker News thread on "I deleted my second
brain" (598 points, 348 comments, June 2025), plus surrounding commentary.

**Weaker than E1, and here is why:** nobody in the thread was asked the actual
question. They discussed *whether to keep notes*, not *whether they would accept
a tool that removes configuration*. Everything below is inference from adjacent
behaviour. E1 remains the better test if it ever becomes runnable.

## H1 — verdict: weakened, not falsified

### The supporting signal
The pain is real, widely felt, and described in the project's own terms. One
commenter framed the choice sharply: reorganising what you have is an
unpleasant task today, while starting a new knowledge base is fun today, on the
bet that a future self will maintain it. That is O1 stated by a stranger.

Several described the maintainer's exact arc — falling into over-analysing where
each note belongs, feeling the mental burden accumulate, and pulling back.
Another described PKM turning into procrastination and deliberately cutting to
the bare minimum. Another said the whole second-brain industry felt like too
much and that complex rules never stuck.

**So: the problem O1/O2 describes is confirmed again, by a fresh population.**

### The damaging signal — and it is the one that matters
**Every one of those people solved it themselves, inside the flexible tool.**

- One reduced to keeping almost everything in a single folder and writing notes
  only in three specific situations — reporting a vault that stayed small and
  searchable after a year.
- One collapsed down to one large work note plus disposable small ones.
- One kept a simple hyperlinked system and stopped worrying about method.

Nobody asked for a tool that would impose this. Nobody said their tool's
flexibility was the enemy. They applied discipline and moved on — which is
precisely the falsification signal defined in advance in the E1 design:
*"the problem is real but the tool is not the answer."*

Worse for the thesis: one commenter had built their own notes app; another
restarted a vault under PARA and used an LLM to decide where things go. This
population's instinct when unhappy is to **build or automate**, not to adopt
someone else's constraints.

**Interpretation.** The problem is validated; the *solution shape* is not. The
remaining bet is narrower and harder than stated in `vision.md`: not "people
want fewer options" but **"people who have already solved this with discipline
would rather not have to spend the discipline."** That is a real product, but
it competes against a free alternative — self-restraint — that costs nothing to
adopt and that this audience has demonstrably already found.

## H3 (start clean) — verdict: further weakened

Two independent hits against it:

- One commenter described the organisational version directly: teams that
  declare the knowledge base a mess, start a fresh one, watch the new one decay
  the same way, and end up searching *two* bad knowledge bases. Applied to this
  product: "no import" does not produce a clean start, it produces a second
  system alongside the old one.
- Regret is documented. One person described discarding old notebooks as
  destroying a part of themselves. Several argued the cheap hedge is to archive
  rather than delete — one recommending zipping the old material somewhere out
  of the way, on the grounds that it is far harder to regret.

**This is the second body of evidence pointing the same way.** H3 should now be
treated as probably wrong. The archive-don't-delete hedge appears twice,
unprompted, and matches the hedge already sketched for F3: no import, but a
read-only way to reach the old vault.

## H4 (capture less) — verdict: contested, and it splits the audience

A substantial group is entirely at peace with write-only notes. One described
keeping infrequent how-tos, project state and maintenance logs, mostly never
re-read, with roughly one in a hundred proving valuable years later — explicitly
comparing the practice to a written rubber duck. Others value old notes as a
record of a former self rather than as retrievable information.

**Implication for O2.2.** "Capturing what you will never re-read" is not
inherently a pain. It becomes one when capture is *aspirational* — quotes and
insights filed against a future self who will process them. Logs are fine;
homework for a future self is not. F3 should target the aspirational kind, not
volume in general. This meaningfully sharpens O2.2 and is the most useful
finding here.

## What this changes

1. **H1 is now an explicit, weakened bet.** Record it as such in `vision.md`
   rather than as a premise. The competitor is not Obsidian; it is
   self-discipline inside Obsidian.
2. **H3 should be reversed or hedged in F3.** Two independent bodies of evidence
   now oppose "start clean".
3. **O2.2 is re-scoped:** the target is aspirational capture, not all capture.
4. **A new risk:** this audience responds to friction by building their own tool
   or wiring an LLM to it. Add to the register.

## Method note
This is inference from a discussion that was not about the product's premise.
It cannot confirm H1, only fail to support it — which is what happened. If the
maintainer ever gains the ability to post publicly, E1 remains worth running.