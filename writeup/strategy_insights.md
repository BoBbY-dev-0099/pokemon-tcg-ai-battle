# Strategy Insights (Writeup Notes)

Last updated: 2026-07-26

Durable notes for the competition writeup — not a Codex/prompt file.

---

## 2026-07-26 — Slot pollution & upload fix

### Pattern: slot pollution

Observed ladder damage from a polluted Day-2 slot:

1. Rocket / Day2 Lucario occupied the Day-2 submission slot.
2. Follow-on uploads (bossguard + Spidops) then stacked on that polluted slot.
3. Result: the live pair no longer matched the intended Day1 Lucario + Day2 Alakazam core.

**Takeaway:** Once Day2 is wrong, later “fixes” on the same slot can amplify the mismatch instead of recovering the baseline pair.

### Fix (accepted upload pair)

Ship the plain (non-bossguard) pair:

| Order | Artifact | Role |
|------:|----------|------|
| 1 | `Day2_alakazam_v12.tar.gz` | Day-2 agent (plain v12) |
| 2 | `DAY1_mega_lucario_rule_core.tar.gz` | Day-1 agent |

Canonical local paths (submission candidates):

- `outputs/submission_candidates/Day2_alakazam_v12.tar.gz`
- `outputs/submission_candidates/DAY1_mega_lucario_rule_core.tar.gz`

(Also present under `outputs/recovery/` for Lucario; prefer `submission_candidates/` for uploads.)

### Bossguard 659 vs v12 812 — offline ≠ ladder

- Bossguard tagged offline ~**13/15** on a small tagged corpus.
- Plain v12 ladder / eval signal sat around **812** vs bossguard ~**659**.
- **Interpretation:** a 13/15 offline tagged win rate does **not** equal the full ladder loss distribution. The tagged set is a narrow slice; ladder losses include matchups and failure modes the corpus never stressed.

### Research park: bossguard

- Park bossguard research for the writeup narrative (interesting negative result / distribution mismatch).
- **Do not ship** bossguard (or bossguard+Spidops) without **re-mining the full recent ladder loss set** and validating that the patch still helps under that distribution.

### Baseline tradeoffs (accepted)

- **Hilda / Xerosic vs Boss:** keep as an accepted baseline tradeoff — intentional, not an open bug for this submission cycle.
- **Brock:** needed an **explicit guard** as a **new card** (distinct from the parked bossguard line of work). Call this out in the writeup as a card-specific defensive addition, not as “ship the full bossguard package.”

---

## Repo recommendation (GitHub for submissions + decks)

Suggested layout if/when you init a public or private GitHub repo for this project:

```text
/
  README.md                 # high-level: what ships, how to rebuild tarballs
  decks/                    # deck lists, card manifests (small text/JSON)
  agents/                   # agent code / rules that produce submissions
  scripts/                  # pack, validate, tag-corpus eval helpers
  docs/writeup/             # strategy notes, figures for the writeup
  outputs/                  # local only — see .gitignore
```

### Commit

- Agent/rule source that rebuilds Day1 / Day2 archives
- Deck definitions and small config (card lists, version tags)
- Eval scripts and a **small** tagged corpus (or pointers + hashes)
- Writeup markdown / figures that are intentionally public
- A short `SUBMISSION.md` with upload order and artifact names

### Do **not** commit

- Secrets: Kaggle tokens, API keys, `.env`, credential JSON
- Huge episode dumps / full ladder replay corpora (GB-scale)
- Generated tarballs if they are rebuildable (`*.tar.gz` under `outputs/`)
- Large scratch under `outputs/`, `recovery/`, scrape caches — keep local or release as versioned artifacts elsewhere

### Practical `.gitignore` starters

```gitignore
.env
*.pem
**/credentials*.json
outputs/**
!outputs/writeup/
!outputs/writeup/**
*.tar.gz
**/episodes/**
**/replays/**
**/ladder_dumps/**
```

---

## Git status (workspace root)

As of 2026-07-26: **no `.git` at workspace root.** Do not init casually unless you only want a tiny docs/scripts repo; if initializing, start with the structure above and ignore `outputs/` bulk + secrets.

---

## Upload checklist (current)

1. Confirm files exist under `outputs/submission_candidates/`.
2. Upload **Day2** `Day2_alakazam_v12.tar.gz` (plain v12 — not bossguard).
3. Upload **Day1** `DAY1_mega_lucario_rule_core.tar.gz`.
4. Verify the live pair matches this order; avoid stacking Rocket/Lucario or bossguard/Spidops into Day2 without a fresh full-ladder loss remine.
