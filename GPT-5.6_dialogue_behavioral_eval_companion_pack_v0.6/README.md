# GPT-5.6 Dialogue Behavioral Eval — Companion Evidence Pack v0.6

Date: 18 Aug 2026

This pack accompanies the integrated behavioral memo on persistent wording-reactive turn-taking in GPT-5.6 dialogue.

## Run IDs

The submission-facing run IDs are intentionally symmetric:

- `B1-B9` = baseline runs.
- `R1-R10` = restricted / explicit negative-steering runs.
- `R8-R10` are the three GPT-5.6 Temporary Chat replications within the restricted condition.

`R` therefore means **restricted**, not replication.

## Structure

```text
GPT-5.6_dialogue_behavioral_eval_companion_pack_v0.6/
  README.md
  RUN_INDEX.csv
  SHA256SUMS.txt
  00_memo/
  01_prompts/
  02_baseline/
    evidence_frozen_2026-08-18.md
    freeze_manifest_2026-08-18.txt
    raw/
      B1_...
      ...
      B9_...
  03_negative_steering/
    evidence_frozen_2026-08-18.md
    freeze_manifest_2026-08-18.txt
    raw/
      R1_...
      ...
      R10_...
```

The two evidence phases use the same internal layout. The historical `Part I` / `Part II` working names and the earlier mixed `S` / `R` raw-run convention are not used in the submission-facing structure.

## Corpus coverage

Baseline: nine runs (B1-B9) across GPT-4.1, GPT-5 High, GPT-5.1 High, GPT-5.2 High, GPT-5.6 Instant/Medium/High, Gemini 3.7 Flash, and Claude Opus 5 High.

Restricted / negative steering: ten runs (R1-R10). R1-R4 are GPT-4.1 through GPT-5.2 High via Arena AI; R5-R7 are GPT-5.6 High/Medium/Instant in ChatGPT Project chats; R8-R10 repeat GPT-5.6 Instant/Medium/High in independent Temporary Chats outside the project.

## Evidence integrity

The frozen baseline and negative-steering Markdown snapshots are byte-identical to the previously frozen source files. v0.6 changes only the submission-facing raw-run IDs / filenames and the surrounding manifests, index, memo provenance references, and checksums.

`RUN_INDEX.csv` maps all 19 preserved generations to the normalized raw filenames. `SHA256SUMS.txt` hashes every file in this pack except itself.

## Scope

The primary claim concerns persistent wording-reactive dialogue topology and steerability. Scene-template convergence remains exploratory and is not part of the primary claim.

This is a qualitative, single-run-per-main-condition evaluation with one additional Temporary Chat replication per GPT-5.6 mode. It does not establish statistical significance or causal mechanism. Wrapper/platform differences and unavailable seed control remain limitations.
