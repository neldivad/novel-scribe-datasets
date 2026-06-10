# shakespeare/hamlet — benchmark (fidelity cross-examination)

Where [office-drama](../office-drama/BENCHMARK.md) is a *controlled* set scored against a planted answer
key, Hamlet tests **representational fidelity**: extract a *knowable classic* and check the result against
the canonical plot. Reference synopses:
[SparkNotes](https://www.sparknotes.com/shakespeare/hamlet/summary/) ·
[RSC act-by-act](https://www.rsc.org.uk/shakespeare-learning-zone/hamlet/story/scene-by-scene) ·
[LitCharts](https://www.litcharts.com/lit/hamlet/summary).

## Method

Ingested `shakespeare/hamlet`, extracted all five acts via the keyless
[extraction loop](../../novel-scribe/docs/recipes/t2-extraction-loop.md), reviewed with
[`work-inspection.ipynb`](../../novel-scribe/notebooks/work-inspection.ipynb) (`WORK='shakespeare-hamlet'`),
then cross-examined the extracted threads and disclosures against the canonical plot.

**Size:** 5 acts · 20 scenes · 41 characters · 1,099 lines · 16 threads · 66 beats.

## Scorecard — it succeeds

- **16 / 16 threads are real plot lines — zero hallucinations.** Every extracted thread maps to something
  that actually happens (table below).
- **All 17 `major_reveal` disclosures are genuine** — the ear-poison murder, Claudius's prayer confessing
  fratricide, Ophelia's drowning, the forged death-warrant, Rosencrantz & Guildenstern's execution. Accurate
  summaries, not invention.
- **The questlog arc matches the play's shape** — tension builds to Act IV, the Act V bloodbath closes nine
  threads, and the single deliberate loose end (Fortinbras's succession) is correctly the only thing left open.

| Canonical beat | Extracted thread |
|---|---|
| Ghost appears on the watch | `ghost_apparition` |
| Fortinbras massing on the border | `fortinbras_threat` |
| Hamlet's grief + disgust at the o'erhasty marriage | `hamlet_grief_disgust` |
| Hamlet/Ophelia romance, forbidden | `ophelia_hamlet_relationship` |
| **Ghost: Claudius murdered me — avenge it, spare your mother** | `hamlet_revenge_mandate` + `claudius_murder_secret` |
| Hamlet's feigned madness ("antic disposition") | `hamlet_antic_disposition` |
| Rosencrantz & Guildenstern sent to spy | `rosencrantz_guildenstern_spy` |
| The Mousetrap play to catch the King | `play_mousetrap` |
| Claudius ships Hamlet to England | `hamlet_sent_to_england` |
| Hamlet kills Polonius by mistake | `polonius_death_consequences` |
| Laertes returns vowing revenge | `laertes_revenge` |
| The poisoned-sword-and-cup duel plot | `poisoned_sword_plot` |
| Fortinbras inherits the throne (the open ending) | `fortinbras_claim_to_denmark` *(left open)* |

## Caveats — calibrate your trust

1. **Shakespeare is deep in the model's training data.** This validates *representational fidelity* — can
   the schema faithfully hold a known plot (yes) — **not** blind reading of unseen dialogue, since the
   producer already knows Hamlet. office-drama (original, unseen) is the truer test of *reading ability*;
   Hamlet is the test of "does the structure match a plot we can independently verify" — and it does.
2. **One coverage gap:** Ophelia's madness-and-death is captured as a *reveal* but not as its own *thread*
   (arguably it should be — a consequence of Polonius's death).

## Calibration findings (what a dense, real work exposed)

1. **`revelations` over-fires on `major_reveal` by volume — 17.** Every one is *accurate*, but "major
   disclosure" ≠ "twist": Hamlet is disclosure-dense, so flagging all 17 is a list, not an alarm. The true
   twist/fake-out signals are the **contradiction-based** kinds (`lore_retcon`, `apparent_death_overturned`,
   `reopened_closure`); `major_reveal` should live in a separate, quieter "notable disclosures" bucket — or
   get a tighter trigger. (office-drama had only *one* major lore-bomb, so this never showed.)
2. **The deterministic cliffhanger-vs-hole heuristic mislabels the ending.** `fortinbras_claim_to_denmark`
   is one beat / `last_action=open`, so beat-count reads it as a *dropped hole* — but it opens in the final
   scene and is the *intentional* ending. The heuristic needs "how late did it open?" as a factor (the
   `quest-verdict` LLM pass catches this; the shortcut doesn't).

## Reproduce

```bash
scribe ingest-nvs --path shakespeare/hamlet --work-id shakespeare-hamlet
# extraction loop — see novel-scribe/docs/recipes/t2-extraction-loop.md
scribe aggregate --game shakespeare-hamlet
# then open novel-scribe/notebooks/work-inspection.ipynb with WORK = 'shakespeare-hamlet'
```
