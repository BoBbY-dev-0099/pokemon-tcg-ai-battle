# alakazam_v12_code_deck_soft_bossguard

**Canonical combined candidate** for post-convergence upload consideration (supersedes `alakazam_v12_code_deck_soft` for Boss/Brock priority).

Base: `alakazam_v12_code_deck_soft` (soft-into-threat + opening-Abra + −1 Enhanced Hammer / +1 Brock's Scouting).

## Extra patch

**Boss-over-Brock Supporter guard:** when `target_use_boss and target_can_kill` (same lethal / near-lethal bench-KO predicate the Alakazam scorer already uses) and Boss's Orders is in hand, Brock's Scouting score is capped to `boss_kill - 1` so Boss wins the Supporter slot. Does not raise Boss above setup plays (Rare Candy / Poffin / etc.).

Pre-guard baseline kept at: `outputs/submission_candidates/alakazam_v12_code_deck_soft/`

No ladder upload until convergence clears. See `outputs/alakazam_boss_over_brock_guard.md`.
