# Alakazam — Boss-over-Brock Supporter guard

- Timestamp (UTC): **2026-07-25T19:00:39Z**
- Timestamp (local NPT): **2026-07-26 00:45:39 NPT**
- Ladder uploads: **NONE**
- Convergence recheck: **SKIPPED**
- **Canonical candidate:** `outputs/submission_candidates/alakazam_v12_code_deck_soft_bossguard`
- Pre-guard baseline (kept): `outputs/submission_candidates/alakazam_v12_code_deck_soft`
- Raw JSON: `outputs/ladder_convergence/boss_over_brock_guard.json`

## Diff summary

Surgical change in `heuristic_scores` for `Brocks_Scouting` only:

```python
# after existing Brock score assignment
if (
    score > 0
    and target_use_boss
    and target_can_kill
    and hand_counts[Boss_Orders] > 0
    and len(my_field) > 1
):
    score = W["boss_kill"] - 1  # 2261 < Boss 2262
```

Keeps Boss at `boss_kill` (2262) so setup plays (Rare Candy / Poffin / Pokémon) still outrank the Supporter kill; only demotes Brock below Boss when the existing lethal/near-lethal bench-KO predicate fires.

Unchanged: soft-into-threat retreat, opening-Abra, −1 Hammer / +1 Brock deck.
- Guard source cap present: **True**
- Soft baseline still unpatched: **True**

## Collision breakdown (Task B re-check)

Task B tagged ~**7.8%** corpus / **12.1%** broader turns as Boss-collision (Boss in hand + Brock desire + simplified bench-kill). Re-scored those turns with a scorer-style `target_use_boss`/`target_can_kill` (special Mist/Rock + Hammer need; win-cand / best-killable selection).

### Soft-union 15 corpus

| Metric | Value |
|---|---|
| Games / turns | 15 / 154 |
| Task B Boss-collision turns | **12** (7.8%) |
| Of those with **real** killable bench (scorer-style) | **11** (91.7% of Task B Boss-coll) |
| Of those **not** real kill (simple false / active-only) | 1 (8.3%) |
| Boss merely legal + Brock desire (no kill either model) | 20 (13.0% turns) |
| Guard flips real-kill Brock→Boss (weight model) | **11** |

### Broader recent sample

| Metric | Value |
|---|---|
| Games / turns | 120 / 1681 |
| Task B Boss-collision turns | **209** (12.4%) |
| Of those with **real** killable bench | **102** (48.8% of Task B Boss-coll) |
| Of those **not** real kill | 107 (51.2%) |
| Guard flips real-kill Brock→Boss | **102** |

### Guard confirmation

- Weight-model (authoritative for this patch): on every **real-kill** Boss∩Brock collision, soft pairwise winner was Brock; after guard, Boss wins the pairwise Boss-vs-Brock slot (**11/11** corpus, **102/102** broader = 100% of real-kill Task B Boss-collisions).
- Note: when Hilda/Xerosic also score, they can still beat Boss (3000/3250 > 2262) — pre-existing; guard only fixes Brock theft.
- Live agent sample (Boss in hand, Brock injected): 18 frames where either side picked Boss/Brock as top action; soft rarely had Brock as the immediate top pick vs setup plays, so frame-level Brock→Boss flip count stayed 0 — consistent with Boss staying at 2262 under setup weights.

## Soft-union pass rates

Boss-over-Brock guard does not change soft/opening CF or deck tutor CF; 14/15 pass rates inherit from code_deck_combined_gate (same deck + same soft or opening code surfaces).

- **14-case code∨deck:** **12/14** (86%) — unchanged by this patch
- **15-case code∨deck:** **13/15** (87%) — unchanged by this patch
- Residual hard bricks: [87902185, 88057800]

## Regression (soft baseline vs bossguard)

| Metric | Value |
|---|---:|
| Usable frames compared | 86 |
| Target ≥50 met | YES |
| Hard regressions (non-Boss-kill flips) | 0 |
| Intentional Boss-guard flips | 0 |
| Errors | 46 |
| Clean? | YES |

## Residual risk

- Guard is pairwise Boss>Brock only. Hilda (3000) / Xerosic (3250) still outrank Boss (2262) when they also score — pre-existing, unchanged.
- Scorer-style kill still approximates `estimate_hand_increase`; a few edge frames may disagree with live `heuristic_scores` draw math.
- Seed-mode Brock (17000) is correctly demoted on real kill turns; non-kill seed turns keep tutoring priority.
- Convergence still must clear before any ladder upload.

## Ready for post-convergence upload?

**Yes, with caveats** — use `outputs/submission_candidates/alakazam_v12_code_deck_soft_bossguard`. Real-kill share of Task B Boss-collisions ≈ **91.7%** corpus / **48.8%** broader; guard flips those to Boss; soft-union **13/15** unchanged; still HOLD until convergence + accept 2 hard-brick residual.

