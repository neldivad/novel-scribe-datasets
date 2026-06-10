# office-drama — benchmark results

What the controlled set found when run through novel-scribe (`ingest-nvs → extract → resolve →
resolve-threads → aggregate → questlog / revelations`), scored against [`ground-truth.md`](ground-truth.md).

> **Caveat — not a blind recall test.** These T2 extractions were produced by a Claude Code session that
> *knew the plot*, so the thread layer measures **representational adequacy** (can the schema hold the
> planted plot?) and the **deterministic reductions** (status folding, questlog, significance, revelations)
> — not the LLM's blind reading. A blind run (a fresh session via
> [the extraction-loop recipe](../../novel-scribe/docs/recipes/t2-extraction-loop.md), no answer key) is
> the next measurement.

## Scorecard — what the system got right

| Check | Result |
|---|---|
| **Threads** | **8/8 planted represented**; final statuses match the design — `layoff` open via resolve→**reopen** (cliffhanger, 16 beats), `payments_suite_broken` open/1-beat (the planted dropped hole), the other 6 resolved. Status-folding + defeasible closure hold. |
| **Distractor rejection** | **0 leaked.** Entities = 11 real cast + 2 real locations (Polsia, Halcyon). Offsite, branzino, Henderson, the bad-news font — none became an object or thread. |
| **Significance vs the presence trap** | **Passed.** Ann (the keystone) is near-bottom by appearances (2/24 scenes) yet computed `major` — the T2-signal weighting (goals/pov/arc) overrode raw counts, exactly resisting the bias the story is about. |
| **Twist stored** | `lore_updates: ai_authored_layoff (major)` + the `layoff` reopen. |

## Gaps found → revisions

### novel-scribe (library)
1. ~~`revelations.detect()` misses the actual twist.~~ **FIXED.** It was too narrow (death-reversal + `lore_retcon` only). Broadened (and made read-only — it's a reduction, no table) to also emit `major_reveal` (a `major` lore-bomb) and `reopened_closure` (a thread resolved then reopened). Office now surfaces both the `ai_authored_layoff` twist and the `layoff` sequel-hook reopen.
2. ~~The authority-breach check was never exercised / needs authority wired.~~ **CORRECTED — it works.** Running the T3 coherence diff on Opus flags the breach as `contradiction / high` (declared `not authorised to alter the ranking` vs observed `altered it`). `authority` **is** surfaced to the diff (`read_declared` returns the full frontmatter). The only real gotcha: `diff-bundle`'s default `nvs_path` is `data/derived/<game>/nvs`, wrong for an externally-sourced work — pass `--nvs-path <nvs root>` or the declared side comes back empty.
3. **Significance over-assigns `major` (7/11)** on a 24-scene work — declared *supporting* characters all came out `major`. Calibration question for short works.
4. **(Subtle) significance masks an "underwritten protagonist" signal.** Ann is declared a keystone but appears in 2/24 scenes; boosting her to `major` hides the legitimate "central character barely on the page" note a writer might want.

### office-drama (dataset)
5. **`ground-truth.md` conflates two kinds of plant.** The "keystone contradiction" (Ann central vs ranked 18.40) is an **in-world plot irony** (GPT's mis-rank), which NVS correctly treats as plot (threads), **not** author drift — yet the key calls it a coherence finding NVS should flag. → tag each plant as *NVS-checkable* vs *in-narrative irony*. The truly NVS-checkable contradiction is the **authority breach**.
6. The twist is correctly a `major` lore-bomb (not a `retcon`) — so the fix is library-side (#1); the dataset should **not** bend to the detector's current shape.

## Update — after running every pass (windows → quest-verdict → coherence diff)
- **Authority breach: caught** (`coherence_findings`: contradiction/high) once the diff is run with `--nvs-path`. (See corrected #2.)
- **Cliffhanger vs hole: classified** by the quest-verdict pass — `layoff → sequel_hook`, `payments_suite_broken → hole`. (The deterministic questlog can't distinguish them; `quest-ingest` can.)
- **The lore-bomb twist IS now surfaced** — `revelations.detect()` was broadened (and made read-only): it emits `major_reveal` (the `ai_authored_layoff` disclosure at S20) and `reopened_closure` (the `layoff` resolve→reopen at S24). Finding #1 **closed**.
- **Dropped orphan tables** (migration 007): `entity_profiles`, `revelation_events`, `dialog_branches` — reductions (compute-on-demand) or an unbuilt feature.

## One-line takeaway
The *structural* layer is solid and even clever, and **every reader-facing check now fires** — surface-the-twist (`major_reveal` + `reopened_closure`), the authority breach, and cliffhanger-vs-hole. The earlier "doesn't fire" was *passes not run* + a wrong default `nvs_path` + one too-narrow detector — all addressed, none a missing capability.

## Method
DB `office`. `ingest-nvs` → per-chapter `extract-bundle`/`extract-ingest` (×4) → `resolve` → `resolve-threads`
→ `aggregate` → `questlog` / `revelations`. Inspection notebook:
[`novel-scribe/notebooks/office-drama-nb.ipynb`](../../novel-scribe/notebooks/office-drama-nb.ipynb).
