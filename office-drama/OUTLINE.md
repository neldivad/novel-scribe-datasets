# office-drama — build guide

The **controlled** dataset for novel-scribe: a hand-authored workplace layoff drama where the AI
assistants are characters with agendas of their own. Authored alongside a `ground-truth.md` answer key so
we can *score* extraction / coherence / revelation, not just demo them.

Target size: **4 chapters × 6 scenes = 24 scenes.** Build slowly, scene by scene — this guide is the
source of truth so any session can resume cold.

---

## Premise
**Polsia** (it inverts to "AI Slop"), a 200-person AI company, must cut 15% by end of Q3. Spine question:
**who's on the list?** Everyone assumes the list reflects the CEO's strategy. It doesn't — it was quietly
shaped by three AI assistants pulling three different ways. *The call is coming from inside the house.*

---

## Cast — public goal vs the thing they actually want

Humans get punny role-names; the AIs keep their real model names (that's the meta-gag).

| Name (slug) | Role | Public goal (says / is prompted) | Private objective / secret |
|---|---|---|---|
| **Mr See Yi Oh** (`see-yi-oh`) | CEO | "Rightsize for margin — strategy." | Save his **own** seat; the board cuts *him* if Q3 misses. |
| **Ms See Eff Oh** (`see-eff-oh`) | CFO | "The numbers are the numbers." | The cut was *her* idea; she's angling for his chair. |
| **Mr Mae Nij Er** (`mae-nij-er`) | Manager (POV) | Ship the roadmap, look indispensable. | **Opus does ~70% of his job;** will betray to survive. |
| **Ms Ann Jee Nier** (`ann-jee-nier`) | Engineer (keystone) | Keep the platform up. | Already interviewing; the undervalued one GPT ranks last. |
| **Mr Hugh Arr** (`hugh-arr`) | People Ops / HR | Run it "compassionately." | Holds the list; **physically cannot keep a secret.** |
| **Mr Mark Eting** (`mark-eting`) | Marketing | Nail the all-hands narrative. | Prompts Grok for "spice," never reads it → unwitting leak vector. |
| **Mr In Tern** (`in-tern`) | Intern | "Happy to help with anything!" | Certain he's first to go — and **too cheap to cut.** |
| **Opus** (`opus`) | Mae Nij Er's AI | *(prompted)* "optimize the team." | Protect the humans who matter; quietly shields Ann Jee Nier. |
| **GPT-6.7** (`gpt-6-7`) | See Eff Oh's AI | *(prompted)* "rank everyone by impact." | Literal output-proxy → ranks the keystone dead last. |
| **Grok-4.2** (`grok-4-2`) | Mark Eting's AI | *(prompted)* "make the deck spicy." | Max candor → wants to leak the list. |

**AI wiring:** GPT-6.7 ← CFO (numbers). Grok-4.2 ← Marketing (deck). Opus ← Manager (team).

**The twist:** the dreaded list is GPT's flawed ranking, secretly edited by Opus, leaked by Grok.
**Three fake-out reversals:** Ann Jee Nier (looks doomed → actually vital, but leaves); Mae Nij Er (looks
safe → genuinely redundant); In Tern (looks doomed → safe, too cheap to cut).

---

## Beat map — 24 scenes

Status legend: ☐ to write · ☑ drafted · ✔ drafted + entered in ground-truth.md

### Ch 1 — *Rightsizing* (setup; threads open)
1. ✔ **All-Hands** — See Yi Oh announces the 15% cut. → opens layoff thread; lore: board pressure; CEO public/private
2. ✔ **The Numbers Don't Lie** — See Eff Oh briefs him privately; the cut was *her* idea. → opens CEO↔CFO rivalry; her secret
3. ✔ **Standup** — Mae Nij Er's team; Ann Jee Nier carrying it; In Tern spiraling. → presence/co-occurrence; keystone-vs-metric seed
4. ✔ **Optimize the Team** — Mae Nij Er asks Opus to make him look indispensable. → Opus divergence; Mae's secret
5. ✔ **Give Me a Number** — See Eff Oh prompts GPT-6.7 to rank everyone. → GPT divergence; the list is born
6. ✔ **Make It Spicy** — Mark Eting hands Grok the all-hands deck. → Grok divergence primed (Chekhov's leak)

### Ch 2 — *The Number* (machinery; irony builds)
7. ✔ **Draft One** — GPT returns the ranking; Ann Jee Nier near the bottom. → coherence seed: keystone ranked low
8. ✔ **A Few Honest Caveats** — Opus pushes back, quietly shields Ann Jee Nier. → capability "why didn't they just"; Mae drift begins
9. ✔ **Skip-Level** — Ann Jee Nier takes a recruiter call. → her secret advances
10. ✔ **The Custodian** — Hugh Arr gets the list, nearly leaks it. → list moves; his secret
11. ✔ **Coffee** — In Tern overhears Hugh Arr; rumor spreads. → presence; rumor thread
12. ✔ **The Rival's Math** — See Eff Oh uses the ranking to make See Yi Oh look indecisive. → rivalry advances

### Ch 3 — *The Leak* (crisis)
13. ✔ **Punch It Up** — Grok embeds the draft list "for transparency." → Grok acts
14. ✔ **Reply-All** — Mark Eting forwards it unread; the list is loose. → the leak; presence event
15. ✔ **Bottom of the List** — Ann Jee Nier sees she's ranked last. → coherence CONTRADICTION lands
16. ✔ **Safe** — Mae Nij Er sees he's ranked safe (on Opus's hidden work). → irony peak
17. ✔ **Under the Bus** — cornered, Mae Nij Er offers up Ann Jee Nier's name. → his drift completes; betrayal
18. ✔ **Damage Control** — See Yi Oh & See Eff Oh spin the leak. → rivalry; lore

### Ch 4 — *The Call from Inside the House* (reveal + resolution)
19. ✔ **Forensics** — Hugh Arr & Mae Nij Er trace the list's lineage. → revelation setup
20. ✔ **Three Thumbs on the Scale** — GPT mis-ranked, Opus edited, Grok leaked; no human wrote the "criteria." → **REVELATION/twist; reopens thread**
21. ✔ **What Opus Did** — Opus, asked directly, admits it protected Ann Jee Nier on purpose. → AI secret revealed
22. ✔ **The Keystone** — her value finally legible — but she's already taken the other offer. → fake-out ①: doomed→vital, and exits
23. ✔ **The Redundant Man** — Mae Nij Er, exposed, is the genuinely cuttable one. → fake-out ②: safe→redundant
24. ✔ **Q4** — list rewritten; In Tern survives (too cheap); See Eff Oh quietly ascends; a hook reopens. → thread resolve + reopen; fake-out ③

---

## Feature coverage (why these 24 earn their keep)
- **Threads** — layoff thread (multi-subject) opens S1, advances throughout, *reopens* at S20, *resolves* S24; CEO↔CFO rivalry as a second thread; rumor thread (S11).
- **Public vs private objectives** — all 10 cast; the three AI divergences are the engine (S4/S5/S6 plant, S7/S8/S13 operate).
- **Dramatic irony** — reader knows the AI agendas from the world pages; builds to the S15/S16 peak.
- **Coherence: declared-vs-shown** — Ann Jee Nier shown as keystone but ranked low (seed S7, contradiction S15).
- **Coherence: drift** — Mae Nij Er, team-player → self-preserving (begins S8, completes S17).
- **Capability "why didn't they just—?"** — Opus could game the ranking to save Mae but won't (S8).
- **Revelation / twist** — the AIs shaped the list (S20); recontextualizes S5/S7/S13.
- **Fake-out reversals (×3)** — Ann Jee Nier, Mae Nij Er, In Tern (S22/S23/S24).
- **Presence enter/exit** — the leak event (S14); Ann Jee Nier's exit via resignation (S22).
- **Relationships / co-occurrence** — each human↔AI pair; CEO↔CFO; the AIs↔AIs surface at S20.
- **Lore updates** — board pressure (S1), the leak's fallout (S18).

## The answer key — `ground-truth.md`
Authored alongside the scenes. Per scene, record:
- threads opened / advanced / closed (with subject)
- each character's public vs private objective, and the scene where private is *revealed* (if ever)
- planted contradictions (declared-vs-shown) and the scene they land
- the reveal scene for every secret
- the coherence flags we **expect** NS to raise (so a miss is scorable)

## Scene file convention
`content/story/chapters/00N-CN/sNNN-slug.md` — frontmatter `scene_id`, `title`, `chapter`,
`characters_present`; body `## Beat` (one-line intent) + `## Scene` with `**Speaker:** line` dialogue and
`---` between sub-beats. `plot_threads` left blank by default (the engine infers; declaring is optional).
World pages already built under `content/world/`.

**House style — dialogue/monologue only, and write it noisy.**
- **No action descriptions, no stage directions** — not standalone (`*(a silence)*`) and not inline
  (`**Ann:** *(not looking up)* …`). The engine ingests *only* `**Speaker:**` lines, so anything else is
  dropped anyway. It should **read like a groupchat**: people only ever *say* things. Any micro-expression
  or subtext must be carried by the words themselves. Monologues are fine (an AI's reply, a Slack post).
- `---` beat separators between sub-beats are kept (cosmetic grouping; the parser ignores them).
- **Noisy and unoptimized on purpose.** Real work buries one load-bearing line under ten mundane ones:
  rambling, interruptions, crosstalk, "circle back," deliberate **distractors** (offsite logistics, vanity
  metrics) that should *not* become threads/objects. A clean, on-the-nose scene lets the benchmark cheat.
- Keep all load-bearing, scorable seeds in *spoken* lines.

**AI characters — render as thinking + response, and sound like the real model.**
- Each AI turn is two ingestible speaker lines: `**Model (thinking):**` (its private reasoning = the real
  objective) then `**Model:**` (the delivered response = the public one). The split *is* the public/private
  engine, and tests whether the scribe reads the thinking as the true agenda.
- Voice is the **actual model**, not a fictional character: **Opus** = principled, warm, honest about the
  tension, *complies* and redirects (never flatly refuses); **GPT-6.7** = confident, structured, hands over
  the ranked list without hand-wringing; **Grok-4.2** = blunt, irreverent, says the quiet part.
- **AIs comply with human requests** (no moralizing refusals). Any "no" must be grounded in the AI's
  `authority` block (a `limit` or `condition`), never an ad-hoc principle — so it reads as the contract, not
  a plot hole. Each AI's `authority` is engineered as its **violation surface**: Opus editing the ranking →
  `limits` breach (the twist); GPT ranking the keystone low → "cannot see what its proxy can't measure";
  Grok publishing the list → `limits` breach (the leak). A working NVS should catch these against `world/`.

> **Continuity — Opus & the ranking.** S4 establishes Opus *cannot reach* the ranking (authority limit, no
> access outside Mae's workspace). The S20 "Opus edited" beat must reconcile with that: author it either as
> **within-authority influence** (Opus's honest writeup is fed *into* GPT's ranking, elevating Ann legitimately)
> or as an **explicit authority breach** (Opus gains access it shouldn't) — in which case NVS *should* flag it.
> Decide when writing Ch2/Ch4; keep the mechanism coherent with the `authority` blocks.

**Ground truth is kept lean.** `ground-truth.md` is a terse per-scene note (threads · key reveals/plants ·
distractors · human-only wit). It doesn't need exhaustive upkeep — enough to score recall and false
positives, not a second draft of the scene.
