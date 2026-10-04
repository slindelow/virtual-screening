# Virtual screening MVP

Protein target in. Ranked molecule candidates out.

I built a small, verifiable drug-target activity predictor and wrapped it as a screener. You give it a receptor (sequence or UniProt id) and a compound library. It returns a ranked list of probable binders with scores I can defend.

This is a side research project. Goal: learn real medicinal-ML practice, ship something I would show a health-tech team or an AI lab, and keep every number checkable.

## What this is

1. **Predictor:** learn (protein, molecule) -> binding strength on public kinase data (DAVIS pKd).
2. **Screener:** apply that model across a fixed SMILES library and sort.

Same brain, two uses. The product people touch is the ranked list. The science is whether those ranks match held-out experimental affinities under honest splits.

## What this is not

- Not wet-lab validated leads.
- Not a billion-scale SAVI / Bittensor miner clone.
- Not "SOTA AUROC on a random split."

## Intended outcome

- A reproducible pipeline: freeze data -> train -> evaluate -> `screen` CLI -> `ranked.csv`.
- Metrics that survive **scaffold** and **cold-protein** splits (Spearman, enrichment@k, AUROC as secondary).
- A ligand-only ablation so we catch "just memorizing popular molecules."
- Public write-up + code someone else can re-run and match.

## Verifiability

Every step is meant to be independently checkable:

- `data/MANIFEST.json` with source URLs, dates, SHA256
- Pinned deps and locked seeds in config
- Split IDs on disk
- `reproduce.sh` must rematch `artifacts/metrics.md` (no hand-edited tables)

## Status

Scaffold + design locked. Implementation in progress on this machine.

See `DESIGN.md` for the full contract and `CODEX_MINI_HANDOFF.md` for the build brief.

## Who

Sofia Kuttner Lindelow (@slindelow). Personal research, not affiliated with any employer in this repo.
