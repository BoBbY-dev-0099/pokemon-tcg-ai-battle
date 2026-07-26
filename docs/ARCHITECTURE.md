# Architecture (short)

## What ships to Kaggle

Each submission archive is a small agent package:

- `main.py` — agent policy / rules
- `deck.csv` — 60-card list
- `cg/` — competition game engine (native libs + Python bindings)
- `LICENSES/` — competition-use license text

Rebuild or re-upload using the `.tar.gz` under `submissions/*/`.

## Active pair

- **Day 2:** Alakazam v12 (plain — not bossguard)
- **Day 1:** Mega Lucario rule-core

## Local lab layout (not all committed)

| Path | Purpose |
|------|---------|
| `outputs/submission_candidates/` | Canonical upload candidates + extracts |
| `outputs/challengers/` | Experimental agent packages |
| `outputs/kaggle_episodes/` | Ladder replay dumps (large; gitignored) |
| `outputs/writeup/` | Working writeup notes (mirrored to `writeup/`) |
| `tools/` | Local analysis scripts |
| `data/` | Official competition data zips / card CSVs |

## Validation sketch

1. Confirm tarball contains `main.py`, `deck.csv`, and `cg/`.
2. Smoke-eval locally if your environment has the competition sim.
3. Upload in the order listed in `submissions/README.md` so Day-1 / Day-2 slots match the intended pair.
