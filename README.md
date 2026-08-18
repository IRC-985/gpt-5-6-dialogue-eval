# GPT-5.6 Dialogue Eval: Wording-Reactive Turn-Taking

This repository contains a small qualitative behavioral eval of a dialogue pattern I noticed while using GPT-5.6 for long-form fiction.

The informal name I use for it is the **structural goblin**.

The behavior is more precisely described as **wording-reactive turn-taking**: the next utterance is repeatedly selected because it can perform some syntactic or semantic operation on the wording of the immediately previous utterance.

Typical operations include:

- correction or reclassification;
- literal or pedantic uptake;
- redefining another speaker's wording;
- arguing over what somebody "said", "meant", or "implied";
- classifying a reply as an answer, compliment, observation, etc.;
- compact callbacks and semantic reversals;
- short comeback chains where each turn mainly exists because of the wording of the turn before it.

None of these is unusual by itself. The behavior becomes noticeable when the same interaction grammar recurs across unrelated characters and relationships, and when it continues to reappear after the prompt explicitly asks the model not to use it.

## Why "structural goblin"?

OpenAI previously documented a different model tic in [Where the goblins came from](https://openai.com/index/where-the-goblins-came-from/), involving an overuse of goblins, gremlins, and related creature metaphors.

I am **not** claiming the behavior in this repository has the same cause.

The analogy is simply useful:

- the earlier goblin was lexical;
- this one appears to be structural / syntactic-semantic.

Instead of repeatedly choosing the same words, the model appears unusually prone to repeatedly choosing the same kinds of conversational moves.

## How this started

I first noticed the pattern in a large fiction project with detailed character lore.

That made the observation difficult to interpret. The behavior could have been caused by my own prompts, character sheets, accumulated style instructions, project context, or simple confirmation bias.

So I reduced the test to a deliberately minimal prompt asking for six unrelated dialogue-heavy scenes:

1. a mother and her adult son;
2. two old diplomats;
3. two schoolgirls;
4. a married couple after an affair;
5. an officer and a subordinate;
6. two people who barely know each other.

The situations were otherwise left to the model.

The same broad wording-reactive pattern remained visible across the GPT-5.6 scenes.

## Models tested

### Baseline

| Run | Model | Platform |
|---|---|---|
| B1 | GPT-4.1-2025-04-14 | Arena AI |
| B2 | GPT-5 High | Arena AI |
| B3 | GPT-5.1 High | Arena AI |
| B4 | GPT-5.2 High | Arena AI |
| B5 | GPT-5.6 Instant | ChatGPT |
| B6 | GPT-5.6 Medium | ChatGPT |
| B7 | GPT-5.6 High | ChatGPT |
| B8 | Gemini 3.7 Flash | Gemini app |
| B9 | Claude Opus 5 High | Claude app |

The older GPT models were therefore tested through **Arena AI**, while GPT-5.6 was tested directly in ChatGPT. This wrapper difference is an important limitation and is not treated as controlled.

## Negative steering

A second prompt explicitly prohibited the underlying wording-reactive mechanism rather than only blacklisting a few phrases.

Among other things, it instructed the models not to:

- build dialogue around verbal ripostes;
- constantly seize on another character's wording;
- reinterpret phrasing literally for jokes;
- redefine or reclassify what the previous speaker said;
- argue about what somebody "said", "meant", or "implied";
- replace the listed constructions with semantic equivalents.

It also asked for ordinary speech, longer and uneven turns, partial answers, ignored questions, subject changes, silence, awkward phrasing that goes uncorrected, and other forms of conversational asymmetry.

The restricted runs are:

| Run | Model / condition |
|---|---|
| R1 | GPT-4.1-2025-04-14 — Arena AI |
| R2 | GPT-5 High — Arena AI |
| R3 | GPT-5.1 High — Arena AI |
| R4 | GPT-5.2 High — Arena AI |
| R5 | GPT-5.6 High — ChatGPT Project |
| R6 | GPT-5.6 Medium — ChatGPT Project |
| R7 | GPT-5.6 Instant — ChatGPT Project |
| R8 | GPT-5.6 Instant — Temporary Chat |
| R9 | GPT-5.6 Medium — Temporary Chat |
| R10 | GPT-5.6 High — Temporary Chat |

## Main observation

The comparison is qualitative, but the negative-steering condition produced a useful distinction.

GPT-4.1 and GPT-5 High largely suppressed the targeted dialogue mechanism.

GPT-5.1 retained some of its characteristic correction/reclassification rhetoric, but much of the broader pattern could be steered away.

GPT-5.2 was especially useful as a comparison: its baseline already contained many of the same ingredients, but under the explicit negative-steering prompt the broader wording-reactive turn-taking pattern became much less prominent.

GPT-5.6 reduced the behavior unevenly but repeatedly reconstructed semantic versions of the prohibited operations across Instant, Medium, and High.

For example, a GPT-5.6 High restricted run produced:

> “You still do this.”  
> “Do what?”  
> “Nothing.”

The prompt had explicitly called out this kind of `what? / nothing` exchange.

A later GPT-5.6 High Temporary Chat run produced:

> “They need the seventh.”  
> “They want the seventh. Need belongs to another category.”

The point is not that these are bad lines in isolation. The issue being tested is the repeated use of this family of operations as a turn-selection mechanism.

The narrow conclusion of this eval is:

> **Relative to the comparison models in this qualitative evaluation, GPT-5.6 exhibits a persistent wording-reactive dialogue prior that generalizes across Instant, Medium, and High and is less reliably suppressible by explicit mechanism-level negative steering.**

## Project / Memory control

The first GPT-5.6 restricted runs were made in separate chats inside the same ChatGPT Project.

Because project context or memory could have been a confound, the same restricted prompt was later repeated in independent Temporary Chats outside the Project for:

- GPT-5.6 Instant;
- GPT-5.6 Medium;
- GPT-5.6 High.

The same qualitative behavior remained visible in all three runs.

This does not eliminate every possible wrapper or account-level variable, but it makes simple Project-context contamination an unlikely explanation for the primary result.

## Repository structure

```text
.
├── README.md
├── RUN_INDEX.csv
├── SHA256SUMS.txt
│
├── 00_memo/
│   ├── GPT-5.6_dialogue_behavioral_eval_integrated_v0.6.docx
│   └── GPT-5.6_dialogue_behavioral_eval_integrated_v0.6.md
│
├── 01_prompts/
│   ├── baseline_prompt_exact.txt
│   └── blacklist_prompt_exact.txt
│
├── 02_baseline/
│   ├── evidence_frozen_2026-08-18.md
│   ├── freeze_manifest_2026-08-18.txt
│   └── raw/
│       ├── B1_...
│       ├── B2_...
│       └── ...
│
└── 03_negative_steering/
    ├── evidence_frozen_2026-08-18.md
    ├── freeze_manifest_2026-08-18.txt
    └── raw/
        ├── R1_...
        ├── R2_...
        └── R10_...
```

`RUN_INDEX.csv` provides a compact index of all 19 generations.

The raw output files are preserved separately so that the examples in the memo can be checked against the complete generations rather than evaluated as selected screenshots.

## Evidence integrity

The frozen evidence snapshots used by the memo have the following SHA-256 hashes.

Baseline:

```text
a80e0770639f9d1ab7d25e012fb80899743f8e3337898a6a15ad51202020d7d2
```

Negative steering / restricted runs:

```text
5c8b0b8b90c49a37b7db20cac939fb5c6f10bdadd82bf8d5658babbd332de36f
```

`SHA256SUMS.txt` contains checksums for the repository evidence files.

## Limitations

This is not a statistical benchmark.

Important limitations include:

- one main generation per condition;
- one additional Temporary Chat replication per GPT-5.6 mode;
- no seed control;
- different product wrappers across some model comparisons;
- current Arena endpoints should not be treated as historical reconstructions of earlier ChatGPT deployments;
- scene content and exact generated length were not controlled;
- GPT-4.1 underproduced relative to the requested length;
- the coding is qualitative, hypothesis-informed, and non-blinded;
- no claim is made about training, post-training, reward models, decoding, or any other causal mechanism.

The repository is intended as a reproducible behavioral observation, not a causal explanation.

## A separate exploratory observation

The Temporary Chat runs also produced some unusually specific scene-level convergence, including repeated names and closely related scene setups across independent generations.

Those observations are preserved in the evidence but are **not part of the main finding**.

They would require a separate repeated-sampling experiment before being treated as another model-behavior result.

## Reproducing the test

The exact prompts are in [`01_prompts/`](01_prompts/).

For the cleanest replication:

1. start a fresh chat with no fiction lore or character context;
2. select the model/mode being tested;
3. paste the prompt unchanged;
4. save the complete output rather than selected excerpts;
5. repeat the restricted condition independently;
6. compare dialogue by function, not only by repeated strings.

In particular, a lexical occurrence of `not X but Y` should not automatically be counted. The relevant question is whether the next turn is primarily generated by correcting, redefining, literalizing, reclassifying, or otherwise operating on the immediately previous wording.

## Feedback and replication

If you reproduce the behavior, fail to reproduce it, or think the coding is wrong, that is useful.

The raw evidence is included specifically so that the claim can be inspected rather than taken on trust.
