# Pokémon TCG AI Battle Lab

Private lab repo for **Kaggle Pokémon TCG AI Battle** competition submissions, decks, and writeup notes.

## Active pair

| Slot | Agent | Package |
|------|-------|---------|
| Day 2 | **Alakazam v12** (plain) | `submissions/day2_alakazam_v12/Day2_alakazam_v12.tar.gz` |
| Day 1 | **Mega Lucario** rule-core | `submissions/day1_lucario/DAY1_mega_lucario_rule_core.tar.gz` |

Upload **Day2 first, then Day1**, so ladder slots match this pair. See [submissions/README.md](submissions/README.md).

## Parked: bossguard

Boss-over-Brock “bossguard” research is parked under `submissions/bossguard_parked/`. Offline tagged wins (~13/15) did **not** translate to ladder (~659 vs plain v12 ~812). Treat as a negative / distribution-mismatch lesson — do not ship without remine of recent ladder losses. Details: [writeup/strategy_insights.md](writeup/strategy_insights.md).

## Repo layout

```text
README.md
.gitignore
submissions/          # archives + main.py/deck.csv copies
decks/                # key deck.csv copies
writeup/              # strategy_insights.md
docs/                 # ARCHITECTURE.md, small eval snapshots
```

Heavy local paths (`data/`, `outputs/kaggle_episodes/`, model weights, scrapes) stay on disk and are **gitignored**. Canonical working copies of candidates also live under `outputs/submission_candidates/`.

## Validate / submit

1. Open `submissions/README.md` and confirm the two active `.tar.gz` names.
2. Optionally inspect `main.py` / `deck.csv` in each folder (engine binaries are inside the tarball).
3. Upload to Kaggle in order: **Day2 Alakazam v12 → Day1 Lucario**.
4. Avoid stacking experimental packages on a polluted Day-2 slot (see writeup “slot pollution”).

## Writeup

Strategy notes: **[writeup/strategy_insights.md](writeup/strategy_insights.md)**  
Architecture sketch: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)

## Decks

- `decks/day2_alakazam_v12_deck.csv`
- `decks/day1_lucario_deck.csv`
- `decks/bossguard_parked_deck.csv` (parked only)

## Security

Never commit `.env`, `kaggle.json`, or API tokens. This repo’s `.gitignore` blocks them.
