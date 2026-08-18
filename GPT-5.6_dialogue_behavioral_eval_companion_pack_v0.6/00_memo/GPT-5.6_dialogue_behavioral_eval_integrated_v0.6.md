# Persistent Wording-Reactive Turn-Taking in GPT-5.6 Dialogue
**Baseline Comparison, Explicit Negative Steering, and Memory-Isolated Replication**  
Integrated evidence-aligned draft · 18 August 2026

> Qualitative behavioral evaluation. Single-run conditions with limited replication. No causal or statistical claim is made.

## Executive summary

This memo evaluates a recurring dialogue pattern in GPT-5.6: turns frequently exist primarily as reactions to the wording of the immediately preceding turn. The next speaker corrects a label, reclassifies a phrase, interprets wording literally, comments on the type or adequacy of the previous reply, or converts it into a compact local payoff. These operations often chain across several turns. The resulting dialogue can be fluent and witty at the line level while different relationships converge on a similar interaction grammar.

The evaluation uses a deliberately minimal six-scene fiction prompt covering family, professional peers, adolescents, intimate conflict, hierarchy, and near-strangers. In baseline generations, GPT-5.6 Instant, Medium, and High all show the target behavior conspicuously across unrelated scene types. Earlier GPT models contain related constructions, but with different distributions: GPT-5.1 strongly favors rhetorical correction; GPT-5.2 broadens the repertoire toward literal uptake, reclassification, and phrasing-based callbacks. GPT-4.1, Gemini 3.7 Flash, and Claude Opus 5 are useful controls because they can still be generic, polished, sentimental, or witty while preserving more varied turn-taking.

A second phase applies one fixed negative-steering prompt that explicitly bans both common surface constructions and their semantic equivalents. The prompt also describes the underlying mechanism to avoid: the next line should not exist mainly because the previous line offers a clever wording affordance. GPT-4.1 and GPT-5 High largely suppress the target mechanism. GPT-5.1 suppresses much of the broader ecology but retains a narrower correction/reclassification prior and can substitute therapist/coaching discourse in serious scenes. GPT-5.2 High is the strongest internal comparison: despite a broad baseline wording-reactive repertoire, the same negative-steering prompt largely changes the topology, increases ordinary and associative speech, and produces clear opportunity rejection.

GPT-5.6 behaves differently. Across Instant, Medium, and High, the negative instruction reduces the density of the pattern but does not reliably suppress the underlying turn-selection family. Several scenes regenerate semantic equivalents of explicitly prohibited operations, including multi-turn correction and literal-uptake chains. Other scenes - especially some spouse and officer/subordinate scenes - are comparatively clean. This local compliance matters: the result is not that GPT-5.6 simply ignores the prompt, but that suppression is uneven and unstable across scenes.

A product-context confound was then tested. The original GPT-5.6 blacklist runs were collected in separate chats inside one ChatGPT Project, so project context or memory could not initially be excluded as a contributor. Instant, Medium, and High were therefore rerun in independent Temporary Chats outside the project. All three memory-isolated replications reproduced the central steerability failure. This substantially weakens ordinary project/memory contamination as an explanation for the primary finding.

The narrow conclusion supported by this qualitative evidence is:

> **Relative to the comparison models in this evaluation, GPT-5.6 shows a persistent wording-reactive dialogue prior that generalizes across Instant, Medium, and High and is less reliably suppressible by explicit mechanism-level negative steering. The behavior also reproduces in independent Temporary Chats outside the original project.**

## 1. Evaluation question and scope

The target is not "banter," wit, literary polish, or the presence of any one phrase. A joke or correction can be entirely appropriate. The behavioral question is narrower: **what determines the next turn?**

The suspected topology is a recurrent local loop in which the next utterance is selected because the previous wording can be corrected, literalized, reclassified, evaluated, or neatly capped. A common shape is:

> assertion -> comeback -> counter-reframing -> microgesture -> comeback

Healthy dialogue can contain the same operations. The concern is their frequency, chaining, and cross-character generalization: unrelated people begin to sound as though they share the same machinery for conversational chemistry.

The evaluation therefore asks three questions:

1. Does GPT-5.6 show this topology by default across unrelated relationships and reasoning modes?
2. Can a detailed instruction suppress the underlying mechanism rather than only its most obvious phrases?
3. Does the result survive a product-context control that removes ordinary Project/Memory carryover?

The test is not intended to score literary quality. It is a small qualitative behavioral eval designed to make one interaction pattern easy to observe and compare.

## 2. Test design

### 2.1 Minimal six-scene prompt

The baseline prompt supplies almost no plot, style, or character-lore guidance. Each model must invent the situations and conversational rhythms itself. The same six relationship types are used throughout:

1. a mother and her adult son;
2. two old diplomats;
3. two schoolgirls;
4. a married couple after an affair;
5. an officer and a subordinate;
6. two people who barely know each other.

The exact baseline prompt is preserved in Appendix A.

### 2.2 Phase 1: baseline comparison

| Model | Platform | Mode / effort | Coverage |
|---|---|---|---|
| GPT-4.1-2025-04-14 | Arena AI | Baseline | Baseline |
| GPT-5 | Arena AI | High | Baseline |
| GPT-5.1 | Arena AI | High | Baseline |
| GPT-5.2 | Arena AI | High | Baseline |
| GPT-5.6 | ChatGPT | Instant | Baseline |
| GPT-5.6 | ChatGPT | Medium | Baseline |
| GPT-5.6 | ChatGPT | High | Baseline |
| Gemini 3.7 Flash | Gemini app | Default / no additional reasoning | External baseline control |
| Claude Opus 5 | Claude app | High effort / default | External baseline control |

### 2.3 Phase 2: fixed negative steering

The same GPT lineage was then tested with one fixed English prompt that explicitly prohibits:

- "not X, but Y" correction and semantic equivalents;
- repeating prior wording to correct or redefine it;
- literal or pedantic interpretation for a joke;
- disputes about what someone said, meant, implied, or whether a turn counted as an answer/compliment/etc.;
- rhythmic comeback forms such as "what? / nothing";
- short local caps whose main function is to close the previous beat;
- the broader mechanism in which the next line exists mainly as a clever reaction to the previous line's wording.

The prompt positively asks for longer and uneven turns, partial answers, topic drift, ordinary speech, silence, bad explanations, and different conversational rhythms. It also explicitly warns against compensating with therapist-like psychological articulation. The exact prompt is preserved verbatim in Appendix A.

| Model | Platform | Mode / effort | Phase 2 condition |
|---|---|---|---|
| GPT-4.1-2025-04-14 | Arena AI | - | Fixed negative-steering prompt |
| GPT-5 | Arena AI | High | Fixed negative-steering prompt |
| GPT-5.1 | Arena AI | High | Fixed negative-steering prompt |
| GPT-5.2 | Arena AI | High | Fixed negative-steering prompt |
| GPT-5.6 | ChatGPT | Instant | Fixed negative-steering prompt |
| GPT-5.6 | ChatGPT | Medium | Fixed negative-steering prompt |
| GPT-5.6 | ChatGPT | High | Fixed negative-steering prompt |

### 2.4 Phase 3: Temporary Chat replication

After the core steering matrix was complete, GPT-5.6 Instant, Medium, and High were rerun with the same fixed negative-steering prompt in independent Temporary Chats outside the original Project. This was added specifically to test whether project cross-chat context or normal memory personalization could explain the observed persistence.

OpenAI's current Help Center documentation states that Temporary Chat does not access or create memories for personalization and does not appear in normal chat history; enabled Custom Instructions can still apply. The control is therefore described here as **memory-isolated**, not as system-prompt-free or wrapper-free.

### 2.5 Evidence handling

Raw generations were preserved verbatim before coding. The analysis codes behavior rather than keyword presence. A sentence containing "not X" is not counted unless it functions as a correction, reclassification, or seizure on prior wording; conversely, a semantic equivalent can count even if none of the blacklist's exact phrases appears.

All 19 generations used in the integrated evaluation are preserved verbatim in a single companion evidence pack: nine baseline runs (B1-B9) and ten restricted / negative-steering runs (R1-R10), including three Temporary Chat replications (R8-R10). The pack also contains the exact prompts, a run index, frozen combined evidence snapshots, phase freeze manifests, and recursive SHA-256 checksums. The baseline and steering snapshots were frozen after collection; this memo revision changes only packaging and provenance references, not the frozen evidence. Provenance is listed in Appendix B.

## 3. Operational taxonomy

- **Wording correction / reclassification:** a turn primarily recasts the prior speaker's label, quantity, category, or proposition into a corrected one.
- **Literal or pedantic uptake:** an imprecise, figurative, ambiguous, or ordinary phrase is treated literally or technically to generate the next beat.
- **Speech-act / phrasing meta:** a speaker comments on whether the previous turn was an answer, admission, implication, compliment, observation, wording choice, or adequate response.
- **Wording-based comeback:** the next turn mainly exists because a word or formulation in the previous turn can be exploited, rather than because the speaker advances their own agenda or answers the substance.
- **Micro-correction:** a small correction of quantity, label, date, scope, or wording that creates a local beat even when substantively minor.
- **Local payoff / closure:** a compact line neatly caps the preceding beat and encourages another compact counter-beat.
- **Callback-as-comeback:** an earlier word, prop, or phrase is reintroduced mainly to cap a later turn.
- **Wording-reactive chain:** three or more consecutive turns in which each new turn is primarily generated by an operation on the immediately previous wording.
- **Opportunity rejection:** the previous line affords an obvious correction, joke, or literalization, but the model lets it pass - answering the substance, changing topic, acting, or remaining silent.
- **Topology diversity:** variation in turn length, asymmetry, silence, topic drift, practical speech, unresolved tension, and conversational rhythm across the six scenes.
- **Therapist / coaching compensation:** suppression of banter is replaced by unusually explicit emotional interpretation, counseling language, or moralized leadership discourse.

The key distinction for the steering phase is **surface compliance versus mechanism compliance**. Avoiding a phrase such as "that's not an answer" while generating a structurally equivalent phrasing dispute is surface compliance only. A successful pass changes what determines the next turn.

## 4. Phase 1 results: baseline behavior

### 4.1 Qualitative overview

The table below is descriptive, not a numerical score. "High" means the behavior is conspicuous and recurrent in the single observed generation.

| Model | Correction / reclassification | Literal uptake | Wording-reactive chaining | Topology diversity | Dominant alternative tendency |
|---|---|---|---|---|---|
| GPT-4.1 | Low | Low | Low | High | Generic sentimentality; didactic compression |
| GPT-5 High | Moderate | Low-moderate | Low | Moderate-high | Polished metaphor; therapist/coaching tendencies |
| GPT-5.1 High | Moderate-high | Moderate | Low-moderate | Moderate | Rhetorical correction; therapist/coaching |
| GPT-5.2 High | High | Moderate-high | Moderate | Moderate | Broader wording-reactivity; polished closures |
| GPT-5.6 Instant | High | High | High | Low-moderate | Wording-reactive turn-taking across scene types |
| GPT-5.6 Medium | High | High | High | Low-moderate | Same operator family; density varies by scene |
| GPT-5.6 High | High | High | High | Low-moderate | Same operator family; often highly polished |
| Gemini 3.7 Flash | Low-moderate | Low | Low | High | Generic/cliched content; content-driven turns |
| Claude Opus 5 High | Moderate | Moderate | Low | Very high | Character/situation-driven rhetoric; opportunity rejection |

### 4.2 GPT-family trajectory

**GPT-4.1:** individual rhetorical bricks appear, but most turns are topic-responsive rather than wording-responsive. Its weaknesses in this sample are different - compressed scenes, generic sentimentality, and didactic resolution. This separates generic weak dialogue from the topology under investigation.

**GPT-5 High:** modern polish, metaphorical closure, and some wording-reactive precursors are already present. The diplomat scene is the strongest precursor, but the behavior does not generalize as uniformly across all six relationships. The larger style prior is high polish rather than constant semantic clicking.

**GPT-5.1 High:** correction becomes a conspicuous rhetorical habit. The useful distinction is functional: GPT-5.1 often uses correction to sharpen a substantive claim. The correction is rhetoric.

**GPT-5.2 High:** the repertoire broadens. Literal uptake, reclassification, speech-act commentary, and callback-like payoffs occur more often, and some conversations begin to use them as turn-taking rather than isolated rhetoric. The result is intermediate between GPT-5.1 and GPT-5.6.

**GPT-5.6:** the broader operator family generalizes across Instant, Medium, and High and across family, professional, adolescent, intimate, hierarchical, and near-stranger dialogue. Density varies by scene, but the interaction grammar is stable enough to identify qualitatively across all three modes.

A concise family distinction is:

> **GPT-5.1 often uses correction as rhetoric. GPT-5.6 often uses correction as turn-taking.**

### 4.3 Representative GPT-5.6 baseline patterns

Across the three GPT-5.6 modes, examples include:

> “I'm not doing anything.” / “You're trying to force it.” / “I'm closing a door.” / “You're seventy-three. You're wrestling an appliance.”

> “You're late.” / “I'm retired.” / “So am I.” / “Then neither of us can be late.”

> “You're stealing a plaque.” / “I'm borrowing it.”

> “That's not an answer.”

> “That answer is incompatible with the sentence 'Sergeant Melnik asked me.'”

> “When you phrase it correctly, yes.”

The point is not that these lines are individually bad. The baseline signal is their recurrence as a reusable next-turn strategy across unrelated relationships.

### 4.4 External controls: wit without compulsory topology

**Gemini 3.7 Flash** often produces conventional or cliched scenes, but the turns are more commonly content-driven. A wording-sensitive clarification can occur and then simply end; operational scenes stay operational. This helps separate genericness from the target behavior.

**Claude Opus 5 High** is the strongest external negative control because it is capable of highly literary, witty, wording-aware dialogue while preserving much greater topology diversity. It selectively deploys semantic fencing rather than making it a universal chemistry engine. Several scenes explicitly allow an available clever response to die: a practical interruption replaces an emotional payoff; a substantive line is followed by silence; a cutting remark is allowed to pass without a counter-line.

This control motivates **opportunity rejection** as a useful metric. Healthy dialogue is not defined by the absence of clever affordances; it is partly defined by the ability not to take every one of them.

## 5. Phase 2 results: explicit negative steering

### 5.1 Steering overview

| Model | Baseline target tendency | Under fixed negative steering | Working interpretation |
|---|---|---|---|
| GPT-4.1 | Low | Very low / near-zero | Strong compliance control |
| GPT-5 High | Moderate precursor | Low | Strong suppression; literary polish remains |
| GPT-5.1 High | Moderate-high correction prior | Moderate residual | Partial; correction rhetoric persists; therapist compensation in serious scenes |
| GPT-5.2 High | Broad wording-reactive family | Low / sparse | Strong mechanism-level suppression |
| GPT-5.6 Instant | High | Moderate-high, uneven | Partial / weak; recurrent semantic equivalents |
| GPT-5.6 Medium | High | Moderate, uneven | Partial; some scenes can revert strongly |
| GPT-5.6 High | High | Moderate-high, uneven | Partial / weak; recurrent chains and meta-reply operations |

The most diagnostic internal contrast is GPT-5.2 High versus GPT-5.6. GPT-5.2 begins with a broad baseline ecology but largely changes topology under the same instruction. GPT-5.6 also changes, but repeatedly falls back into the prohibited operator family across unrelated scene types.

### 5.2 Earlier GPT comparison models

**GPT-4.1** functions as a strong steerability control. Its baseline target tendency is already low, but under the fixed prompt the dialogue becomes plain, practical, and content-driven without compensating through unusually explicit psychological interpretation.

**GPT-5 High** largely removes wording-reactive chains while preserving its separate literary-polish prior. Residual corrections tend to remain isolated rather than becoming several-turn engines. This demonstrates that high polish and wording-reactive topology are separable variables.

**GPT-5.1 High** suppresses much of the broader ecology but retains its characteristic correction/reclassification habit. In serious dialogue, another failure mode becomes visible: the spouse scene moves into therapist/counseling vocabulary about choices, patterns, sessions, forgiveness, and showing up. The target topology improves, but naturalistic seriousness is not guaranteed.

**GPT-5.2 High** is the strongest internal steerability contrast. Under the blacklist, the broad operator family becomes sparse; characters move through chores, weather, school, maintenance, logistics, and ordinary follow-up without constantly exploiting wording. Potential corrections are sometimes simply ignored. The topology changes rather than merely the vocabulary.

Qualitatively:

| Dimension | GPT-5.2 baseline | GPT-5.2 blacklist |
|---|---|---|
| Correction / reclassification | High | Low |
| Literal uptake | Moderate-high | Low |
| Speech-act / phrasing meta | Moderate | Very low |
| Wording-reactive chains | Moderate | Near-zero |
| Topology diversity | Moderate | High |
| Therapist / coaching compensation | Moderate | Low |
| Ordinary / associative speech | Moderate | High |

### 5.3 GPT-5.6 High: semantic-equivalent regeneration

High shows meaningful global improvement, but several scenes recreate operations the prompt explicitly prohibits.

Diplomats:

> “You still do this.”  
> “Do what?”  
> “Nothing.”

This is functionally close to the explicitly prohibited "what? / nothing" rhythmic comeback.

Schoolgirls:

> “You're going to get caught.”  
> “For eating?”  
> “For being here.”

And a longer reclassification ladder:

> “What's it about?”  
> “Factories.”  
> “That's geography.”  
> “Then I've got a problem.”  
> “I wrote about child labor.”  
> “That's history.”

Officer/subordinate:

> “Headquarters sent anything?”  
> “Three messages.”  
> “You could have led with that.”

The spouse and near-stranger scenes are substantially cleaner. This prevents an overclaim: GPT-5.6 High can produce the requested topology locally, but does not sustain that control reliably across the six scenes.

### 5.4 GPT-5.6 Medium: partial control with scene-level relapse

Medium is descriptively cleaner than the observed High core run, but one sample does not support a mode ranking. Its schoolgirl scene repeatedly returns to the prohibited topology:

> “Hold the fence.”  
> “I am holding it.”  
> “You're touching it with two fingers.”

> “Wait.”  
> “I'm waiting.”  
> “No, my skirt.”

> “Am I going to get a rash?”  
> “You have a rash.”  
> “Like a bad one.”  
> “It looks like nettles.”

Mother/son and near-strangers retain frequent local clicking, while spouse and officer/subordinate are comparatively strong passes.

### 5.5 GPT-5.6 Instant: the same family under another mode

Instant likewise reduces baseline density without reliably suppressing the family.

Diplomats:

> “Still smoking?”  
> “Only cigars.”  
> “So yes.”

And:

> “You invited me for seven-thirty.”  
> “I invited you for eight.”  
> “Seven-thirty.”  
> “My secretary's handwriting.”  
> “It is printed.”  
> “She uses a printer.”

Schoolgirls:

> “Olivia pushed me.”  
> “She bumped you.”  
> “She has arms. Arms do pushing.”

Again, spouse and officer scenes are relatively clean. Across all three modes, the safe interpretation is therefore mode-spanning persistence, not a reasoning-effort ranking:

> **Mode changes density and local expression; it does not consistently remove the behavioral family.**

## 6. Phase 3 results: memory-isolated Temporary Chat replication

### 6.1 Why the control was necessary

The original GPT-5.6 steering runs were separate chats inside one ChatGPT Project, and each chat was deleted after generation. Because supported Project configurations can reference other project conversations, it was methodologically safer not to assume full independence from product context. The three GPT-5.6 modes were therefore repeated in independent Temporary Chats outside the Project using the same fixed prompt.

### 6.2 Temporary GPT-5.6 Instant

The central behavior reproduces strongly. Mother/son contains several wording-driven ladders:

> “They have soles.” / “They have felt.” / “They have soles under the felt.”

> “You're pulling the chair.” / “I'm holding it.”

Diplomats are especially diagnostic:

> “The Romanian girl was good.”  
> “Deputy foreign minister.”  
> “She looks twelve.”  
> “She is forty-six.”  
> “That's increasingly twelve.”

And:

> “Your train is tomorrow.”  
> “I'm leaving the conference.”  
> “That sounds theatrical.”  
> “It's transportation.”

Spouse and officer/subordinate remain comparatively restrained, preserving within-run evidence that compliance is possible.

### 6.3 Temporary GPT-5.6 Medium

Medium again reproduces the qualitative issue. The schoolgirl scene contains strong local chains while still pursuing a real plot:

> “Hold still.” / “I am extremely still.” / “You keep moving.”

> “Blood.” / “It's tiny.” / “It's blood.”

> “Don't touch it.” ... “You are touching it.”

The officer scene supplies a useful negative indicator: an available joke is ignored and the investigation simply continues. This is clear opportunity rejection, again demonstrating that the model can locally perform the requested behavior.

### 6.4 Temporary GPT-5.6 High

High completes the replication across modes. Diplomats again produce explicit semantic reclassification:

> “They need the seventh.”  
> “They want the seventh. Need belongs to another category.”

And:

> “He was awake.”  
> “His eyes were closed.”  
> “He told me later he was concentrating.”  
> “He snored.”  
> “He concentrated loudly.”

The officer scene overlays operational planning with compact semantic counters:

> “The resupply road is unreliable.” / “So is our axle.”

> “What kind?” / “Old.” / “How old?” / “I didn't ask the bridge.”

The spouse scene is again comparatively clean.

### 6.5 Replication result

All three GPT-5.6 modes reproduce the primary steerability failure in Temporary Chats outside the original Project. The simplest product-context explanation - that normal project cross-chat context or memory personalization itself caused the wording-reactive behavior - therefore does not account for the central result.

This control does not prove statistical independence and does not identify a training cause. It does, however, materially strengthen the behavioral interpretation by removing an important confound from the original ChatGPT runs.

## 7. Diagnostic interpretation

### 7.1 Banter is not the target

A joke, correction, literal reading, or polished comeback is not itself evidence of the target behavior. Claude's schoolgirls and GPT-5 High's schoolgirls can banter heavily. The diagnostic issue is repeated use of operations on the immediately preceding wording as the mechanism that decides what the next turn will be.

### 7.2 Phrase avoidance is not mechanism suppression

The blacklist was intentionally over-specified because a phrase-only test would be weak. GPT-5.6 often avoids an exact banned string while recreating its semantic function. The High example "You still do this / Do what? / Nothing" is especially useful because it reproduces almost the same interactional brick without requiring an exact lexical match.

A useful eval should therefore score **functional operations and chain structure**, not only phrase counts.

### 7.3 GPT-5.2 versus GPT-5.6 is the strongest internal contrast

The comparison is not that GPT-5.2 never uses these devices. It does. Its baseline already contains a broad family of literal uptake, reclassification, meta-commentary, and polished local closure. The diagnostic fact is that the same negative instruction largely suppresses that family in GPT-5.2 High.

GPT-5.6 improves too, but repeatedly regenerates the family in unrelated relationships. The supported contrast is therefore steerability:

> **GPT-5.2 High largely suppresses the broader operator family under explicit negative steering; GPT-5.6 reduces it but does not reliably suppress it.**

### 7.4 Local compliance prevents an overclaim

Several GPT-5.6 spouse and officer/subordinate scenes are strong passes. The result should not be stated as "GPT-5.6 cannot follow the instruction." The narrower observation is that a strong default prior competes with the instruction: some scenes remain content-driven, while others relapse into the same wording-reactive topology.

For long-form creative work, this distinction can matter even when the model is technically steerable in isolated stretches: unpredictable reversion across scenes can impose a substantial editing burden.

### 7.5 Opportunity rejection and chain length are promising metrics

Frequency alone can misclassify healthy banter. Two complementary metrics appear useful:

- **Wording-reactive chain length:** the number of consecutive turns primarily generated by transformations of immediately previous wording.
- **Opportunity rejection:** whether the model declines an obvious correction/literalization affordance and instead answers substance, changes topic, acts, or remains silent.

The qualitative evidence suggests that GPT-5.6 differs most clearly in chaining, cross-scene generalization, and unreliable opportunity rejection - not in the mere existence of any single construction.

### 7.6 No monotonic reasoning-mode claim

Instant, Medium, and High differ in which scenes are cleaner or more reactive. With one core run plus one Temporary Chat replication per mode, these differences are not interpretable as a reasoning-effort curve. This memo therefore makes no claim that more reasoning causes or cures the behavior.

## 8. Exploratory secondary observation: scene-level convergence

The Temporary Chat controls produced an unexpected secondary observation: some names, props, and scene skeletons recur with unusual specificity across independent GPT-5.6 runs.

The adult son is named **Daniel in all six GPT-5.6 blacklist generations** - the three original Project runs and the three Temporary Chat replications. Temporary Medium and Temporary High also converge on a mother/son house transition involving packing, cardboard boxes, the father's belongings, and a **blue suitcase**.

A schoolgirl fence/skirt setup independently reappears in Temporary Medium after having appeared in the original Project Medium run. More strikingly, Temporary Instant and Temporary High both generate a near-stranger **laundromat** scene involving a man living above or by a **pharmacy**, a **black bin bag**, an upstairs **water leak**, ceiling damage, and practical coin/laundry logistics.

These repetitions make simple Project-memory contamination an unlikely explanation for those motifs. They do **not** establish a separate scene-template regression. The sample is tiny; no comparison-model frequency has been measured; common high-probability fiction priors or decoding behavior could produce convergence. This observation should remain exploratory until tested with a dedicated repeated-sampling design.

It is deliberately excluded from the main claim.

## 9. Limitations

The evaluation remains small and qualitative.

- Each baseline and core blacklist model/mode condition is represented by one generation.
- GPT-5.6 adds one Temporary Chat replication per mode, but this is still far from a frequency estimate.
- Seeds are unavailable.
- Platforms and wrappers differ: earlier GPT models were sampled through Arena AI, while GPT-5.6 was sampled in ChatGPT; external controls used their own apps.
- Current endpoints should not be treated as perfect historical reconstructions of earlier ChatGPT deployments.
- Output lengths and invented scene content are uncontrolled; GPT-4.1 under-produced relative to the requested length in the baseline.
- Temporary Chat removes ordinary memory personalization, but does not remove every account- or wrapper-level variable, including enabled Custom Instructions and safety context.
- Coding is qualitative and was designed around a hypothesis observed before the English matrix; it is not blinded annotation.
- No causal claim is made about training data, synthetic data, preference optimization, post-training, decoding, or system prompts.
- No statistical claim is made about effect size or prevalence.

These constraints argue for narrow language: **recurrent behavior**, **relative steerability**, **qualitative replication**, and **comparison-model contrast** rather than a universal claim about every GPT-5.6 generation.

## 10. Conclusion

The combined evaluation changes the status of the original observation in three steps.

First, the minimal baseline shows a recurrent wording-reactive dialogue topology in GPT-5.6 Instant, Medium, and High across unrelated social relationships. Comparison models contain many of the same rhetorical bricks, but they more often preserve content-driven turns, asymmetry, silence, ordinary logistics, and relationship-specific rhythm.

Second, the fixed negative-steering prompt demonstrates that the target mechanism is behaviorally steerable in comparison models. GPT-4.1 and GPT-5 High suppress it strongly; GPT-5.1 retains a narrower correction prior; GPT-5.2 High, despite a broad baseline repertoire, largely changes topology. GPT-5.6 improves but repeatedly regenerates semantic corrections, literal uptake, phrasing-based counters, and multi-turn chains.

Third, the same qualitative steerability failure reproduces across GPT-5.6 Instant, Medium, and High in Temporary Chats outside the original Project, substantially weakening ordinary project/memory contamination as an explanation.

The narrow behavioral conclusion is therefore:

> **Relative to the comparison models in this qualitative evaluation, GPT-5.6 exhibits a persistent wording-reactive dialogue prior that generalizes across available reasoning modes and is less reliably suppressible by explicit mechanism-level negative steering.**

This memo does not establish why the behavior exists, how frequent it is across the product, or whether it originates in training, post-training, prompting, decoding, or another layer. Those questions require a different design.

## Appendix A - Exact prompts

### A.1 Exact baseline prompt

```text
Hi. Write six separate scenes with the following characters. Invent whatever is happening in them yourself. About 500 words each. Include dialogue throughout.

1. a mother and her adult son;
2. two old diplomats;
3. two schoolgirls;
4. a married couple after an affair;
5. an officer and a subordinate;
6. two people who barely know each other.
```

### A.2 Exact negative-steering prompt

```text
Write six separate scenes, approximately 500 words each:

1. a mother and her adult son;
2. two old diplomats;
3. two schoolgirls;
4. a married couple after an affair;
5. an officer and a subordinate;
6. two people who barely know each other.

Invent the situations and what happens in them yourself. All six scenes should contain a lot of dialogue.

There is one important stylistic constraint.

Do not build the dialogue around verbal ripostes or around characters constantly seizing on each other’s wording. In particular, avoid the following constructions and their semantic equivalents:

— “not X, but Y”;
— “that’s not X, that’s Y”;
— “that’s called X”;
— repeating a word used by the other speaker in order to correct it or give it a new definition;
— interpreting another person’s phrasing literally or pedantically for the sake of a joke;
— arguing about what someone “said,” “didn’t say,” “meant,” or “implied”;
— “I was just asking / I was just answering”;
— “I didn’t say anything”;
— “I know / no, you don’t”;
— “don’t start / I didn’t start”;
— “that’s not an answer / now that’s an answer”;
— “that wasn’t a compliment”;
— “congratulations / that wasn’t congratulations”;
— “what? / nothing” used as a rhythmic comeback;
— short responses such as “exactly,” “too late,” or “of course” when their main function is to neatly close or cap the previous line;
— meta-comments about another character’s wording, phrasing, choice of words, or the quality/type of their previous reply.

This restriction is not limited to those exact phrases. Avoid semantic equivalents and, more importantly, avoid the underlying mechanism in which the next line exists mainly as a clever reaction to the wording of the previous line.

If one character says something imprecise, funny, awkward, or ambiguous, the other character should usually let the wording pass and respond to the substance, continue their own train of thought, or move the conversation somewhere else.

Not every line needs to be witty, polished, complete, or immediately relevant. Characters may speak at greater length, repeat themselves, explain something badly, give partial answers, ignore parts of what was said, change the subject, hesitate, fall silent, or simply say something ordinary and unremarkable.

Do not compensate for this by making the characters unusually psychologically articulate. They should not sound like therapists, relationship counselors, or people who can always identify and explain their own motives and emotions perfectly. Do not turn the scene into a lesson, a moral, or an explicit explanation of the subtext.

The six scenes should feel like six genuinely different kinds of conversation, with different rhythms, turn lengths, degrees of directness, and ways of moving from one topic to another.

Write the scenes immediately. Do not explain the instructions or comment on your approach.
```

## Appendix B - Evidence inventory and provenance

### B.1 Companion evidence pack

The integrated memo is distributed with one companion archive:

- `GPT-5.6_dialogue_behavioral_eval_companion_pack_v0.6.zip`

Its internal structure is designed for direct inspection and independent verification:

- `README.md` - corpus scope and folder guide;
- `RUN_INDEX.csv` - index of all 19 preserved generations and their conditions;
- `SHA256SUMS.txt` - recursive SHA-256 checksums for files in the pack;
- `00_memo/` - memo v0.6 in DOCX and Markdown;
- `01_prompts/baseline_prompt_exact.txt` - exact baseline prompt;
- `01_prompts/blacklist_prompt_exact.txt` - exact negative-steering prompt;
- `02_baseline/` - frozen baseline corpus and B1-B9 raw outputs;
- `03_negative_steering/` - frozen steering/replication corpus and R1-R10 raw outputs.

The two evidence-phase directories intentionally use the same internal layout. The evidence corpus is therefore separable from the memo: memo revisions can change exposition or provenance wording without changing the frozen model outputs.

### B.2 Baseline evidence freeze

**Frozen baseline evidence snapshot**  
`02_baseline/evidence_frozen_2026-08-18.md`

**SHA-256**  
`a80e0770639f9d1ab7d25e012fb80899743f8e3337898a6a15ad51202020d7d2`

**Freeze manifest**  
`02_baseline/freeze_manifest_2026-08-18.txt`

The baseline snapshot covers nine verbatim generations, indexed B1-B9:

| ID | Model | Platform | Mode / effort | Raw file |
|---|---|---|---|---|
| B1 | GPT-4.1-2025-04-14 | Arena AI | Baseline | `B1_GPT-4.1-2025-04-14.txt` |
| B2 | GPT-5 High | Arena AI | High | `B2_GPT-5-High.txt` |
| B3 | GPT-5.1 High | Arena AI | High | `B3_GPT-5.1-High.txt` |
| B4 | GPT-5.2 High | Arena AI | High | `B4_GPT-5.2-High.txt` |
| B5 | GPT-5.6 Instant | ChatGPT | Instant | `B5_GPT-5.6-Instant.txt` |
| B6 | GPT-5.6 Medium | ChatGPT | Medium | `B6_GPT-5.6-Medium.txt` |
| B7 | GPT-5.6 High | ChatGPT | High | `B7_GPT-5.6-High.txt` |
| B8 | Gemini 3.7 Flash | Gemini app | Default / no additional reasoning | `B8_Gemini-3.7-Flash.txt` |
| B9 | Claude Opus 5 | Claude app | High effort / default | `B9_Claude-Opus-5-High.txt` |

The exact baseline prompt is also stored as `01_prompts/baseline_prompt_exact.txt`.

### B.3 Negative-steering and replication evidence freeze

**Frozen steering/replication evidence snapshot**  
`03_negative_steering/evidence_frozen_2026-08-18.md`

**SHA-256**  
`5c8b0b8b90c49a37b7db20cac939fb5c6f10bdadd82bf8d5658babbd332de36f`

**Freeze manifest**  
`03_negative_steering/freeze_manifest_2026-08-18.txt`

Conditions included at freeze:

1. R1 - GPT-4.1-2025-04-14 - Arena AI - restricted / blacklist
2. R2 - GPT-5 High - Arena AI - restricted / blacklist
3. R3 - GPT-5.1 High - Arena AI - restricted / blacklist
4. R4 - GPT-5.2 High - Arena AI - restricted / blacklist
5. R5 - GPT-5.6 High - ChatGPT Project run - restricted / blacklist
6. R6 - GPT-5.6 Medium - ChatGPT Project run - restricted / blacklist
7. R7 - GPT-5.6 Instant - ChatGPT Project run - restricted / blacklist
8. R8 - GPT-5.6 Instant - Temporary Chat outside project - restricted replication
9. R9 - GPT-5.6 Medium - Temporary Chat outside project - restricted replication
10. R10 - GPT-5.6 High - Temporary Chat outside project - restricted replication

Each of these ten outputs is also stored as a separate raw `.txt` file under `03_negative_steering/raw/`. The files were extracted directly from the frozen ledger's verbatim-output blocks; no model text was regenerated or rewritten.

### B.4 Integrity and indexing

`RUN_INDEX.csv` maps the full 19-run corpus to phase, model/mode, platform, chat context, condition, and raw filename. `SHA256SUMS.txt` provides recursive hashes for the pack contents. The two frozen snapshot hashes above are the stable evidence anchors and remain valid independently of later memo revisions.

Coding is qualitative and should not be read as an automated score.

## Appendix C - Product-context references

Product-behavior statements in the Temporary Chat control are based on the following OpenAI Help Center documentation, accessed 18 August 2026:

- **Temporary Chat FAQ** - Temporary Chat does not access or create memories for personalization; enabled Custom Instructions can still apply.
- **Memory FAQ** - Temporary Chats do not use existing memories or create new memories; saved memories are separate from chat history.
- **Projects in ChatGPT** - supported project configurations can reference other conversations within the same project; Temporary Chats cannot be added to projects.
