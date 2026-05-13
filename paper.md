# Sim-to-Stage

## A Paradigm for Live Performance Production

**Position Paper · v0.1**
**Sim-to-Stage Research, 2026-05-14**
**License:** Creative Commons Attribution 4.0 International (CC BY 4.0)
**Canonical repository:** https://github.com/sim-to-stage/sim-to-stage
**Website:** https://simtostage.com

---

## Abstract

We introduce **Sim-to-Stage**: a paradigm for compiling director intent into rehearsable, executable, audit-traceable live-stage artifacts under a single authoritative truth source. Sim-to-Stage is to live performance production what **Sim-to-Real** is to robotics — a discipline for training, validating, and transferring complex multi-modal artifacts from a simulation environment to a real-world target. In Sim-to-Stage, the real-world target is the live stage and the live audience. We define the **Sim-to-Stage gap** as the paradigm's central technical challenge and decompose it into seven open sub-gaps. We propose seven **architecture primitives** that any Sim-to-Stage system must instantiate, abstracted from a reference implementation in development at StageR. This position paper is a starting coordinate, not a solved problem; we explicitly invite external research groups, theater companies, and live-production industrial implementers to extend, contest, and improve the paradigm.

---

## 1. Introduction

A live theatrical performance is a coordinated multi-modal artifact: script, blocking, lighting cues, sound cues, video projections, scenic transitions, performer interpretation, audience interaction — all unfolding in real time over 90 to 180 minutes. Producing such an artifact at high quality has historically been organized through human craft alone: directors, designers, technicians, and performers iterating across weeks of rehearsal, accumulating implicit knowledge that lives in production journals, cue sheets, and individual memory.

In the past three years, three forces have arrived simultaneously that change the underlying engineering question.

First, large language models and multi-modal generative models have become sufficiently capable to participate as collaborators in theatrical creative work — not merely as tools for narrow tasks, but as departmental specialists.

Second, the robotics community has formalized **Sim-to-Real** as a paradigm for transferring policies trained in simulation to physical deployment, complete with mitigation techniques (domain randomization, system identification, residual learning) and a vocabulary of "gap" diagnosis.

Third, the AI infrastructure community has converged on **world models** — large-scale simulations of physical or social environments — as a primary research direction.

These three forces converge on a question: **what would it look like to produce a live performance the way modern robotics produces a deployed policy?** That is — to simulate the production end-to-end in a director-gated environment, to validate the simulated rehearsal against a single authoritative truth source, and to compile the validated simulation into one-shot executable artifacts that human performers and technical crew deploy on the live stage. We call this paradigm **Sim-to-Stage**.

This paper makes four contributions:

1. We define the Sim-to-Stage paradigm precisely (Section 3).
2. We construct a structural **homomorphism** between Sim-to-Real (robotics) and Sim-to-Stage (live performance), showing the two are not merely analogous in metaphor but isomorphic in engineering structure (Section 3.2).
3. We define the **Sim-to-Stage gap** as the paradigm's central open problem and decompose it into seven distinct sub-gaps that admit independent research (Section 4).
4. We propose seven **architecture primitives** that any Sim-to-Stage system must instantiate (Section 5).

We are deliberate about what this paper does **not** claim. We do not claim the Sim-to-Stage gap has been closed. We do not claim the reference implementation has solved the seven primitives in their general form. We do not claim the paradigm subsumes all live-performance production — only that it provides a useful frame for one mode of production-augmented work. Section 8 details limitations and open questions in full.

---

## 2. Background

### 2.1 The Sim-to-Real Paradigm

The Sim-to-Real paradigm originates in robotics, where the cost and risk of training control policies directly on physical robots motivated a transfer-learning approach: train policies in a physics simulator (Isaac Sim, MuJoCo, Habitat, CARLA), then deploy to physical hardware. The central technical problem is the **Sim-to-Real gap** — the discrepancy between the simulator and the physical world that causes a policy trained in sim to fail on real hardware.

Three families of mitigation are well-established. **Domain randomization** trains the policy across a distribution of simulator parameters (mass, friction, lighting) so the real world appears as one of many seen environments. **System identification** estimates the parameters of the physical world to bring the simulator into closer correspondence with reality. **Residual policy learning** trains a corrective policy on top of the sim-trained policy that learns to account for residual sim-to-real discrepancy.

The Sim-to-Real paradigm has become canonical in robotics because it makes a previously intractable engineering question tractable: it gives the field a *vocabulary* (the gap, the mitigations), a *benchmark structure* (sim eval + transfer eval), and an *architectural pattern* (sim trainer, transfer step, deployment policy). This paper proposes that live performance production stands today in a similar position to robotics circa 2015, and that an analogous paradigm — Sim-to-Stage — provides similar vocabulary, structure, and pattern.

### 2.2 Live Performance Production Today

A modern live performance is produced over a typical timeline of 8 to 16 weeks of rehearsal, technical preparation, and previews. The artifact that ultimately runs on stage is the joint product of dozens of specialists: director, dramaturg, lighting designer, sound designer, video designer, scenic designer, costume designer, stage manager, technical director, and a cast of performers. The coordination problem alone is substantial; the creative problem is, by traditional account, the entirety of theatrical art.

Several technological currents already exist in live-production practice. Stage management software (QLab, ETC Eos, Disguise) captures cue scripts and operates them at performance time. Digital previz tools (Capture, WYSIWYG, depence²) allow lighting and projection designers to preview their work before installation. Collaborative document tools and shared cue sheets manage cross-department coordination. However, these tools operate as **departmental islands**: each specialist's tool optimizes that specialist's work in isolation, with handoffs across department boundaries handled through unstructured human communication.

The Sim-to-Stage paradigm proposes a different architecture: a **single director-gated truth source** representing the production, against which all specialist work is reconciled; a **multi-modal simulation environment** in which the production can be rehearsed end-to-end across modalities; and a **compiler** that translates the validated simulation into one-shot executable artifacts deployable by the human performers and technical crew.

### 2.3 Why "Sim-to-Stage" Now

Three preconditions for Sim-to-Stage have arrived approximately together in 2024–2026:

1. **Multi-modal generative models** are now capable of producing draft artifacts (lighting plots, sound compositions, video sequences, scenic visualizations) at quality sufficient for director review and iteration. This makes specialist agents tractable.

2. **Long-context and persistent-memory language models** can hold an entire production's worth of script, notes, blocking, and rationale in working memory, enabling a Director Intelligence Profile that remembers across rehearsals.

3. **Sim-to-Real** as a paradigm has matured to the point that its vocabulary and architectural lessons (gap diagnosis, mitigation families, benchmark structure) can be ported to adjacent transfer domains.

The Sim-to-Stage paradigm therefore arrives at a specific historical moment, and we believe the moment is genuinely open: no canonical paradigm has yet been published for this domain.

---

## 3. The Sim-to-Stage Paradigm

### 3.1 Definition

**Sim-to-Stage** is a paradigm for producing live performances in which:

1. The production is represented as an **authoritative, director-gated, multi-modal artifact** (the Authoritative Truth Source — Section 5.1) maintained as a single source of truth across all departments.
2. The production is **rehearsed end-to-end in a simulation environment** that models, to varying fidelity, lighting state, sound state, video state, scenic state, blocking, and performance timing.
3. Specialist work is contributed by **department-level agents** (human or AI) whose proposals are reconciled against the truth source through **director-mediated confirmation gates**.
4. The validated simulation is **compiled into one-shot executable artifacts** (cue scripts, packages, briefings) that human performers and technical crew deploy on the live stage.
5. Every decision, every gate, every revision is recorded in a **provenance ledger** that maintains audit traceability from director intent to live execution.

A Sim-to-Stage system is one that instantiates all five of these properties. The first reference implementation is StageR (https://simtostage.com), but the paradigm is intended to be larger than any single implementation, and we invite external groups to instantiate it independently.

### 3.2 Homomorphism with Sim-to-Real

Sim-to-Stage is not merely analogous to Sim-to-Real in metaphor; the two paradigms exhibit a structural **homomorphism** — a one-to-one correspondence of roles between the two transfer pipelines. Table 1 documents the correspondence.

**Table 1: The Sim-to-Real ↔ Sim-to-Stage Homomorphism**

| Aspect | Sim-to-Real (Robotics) | Sim-to-Stage (Live Performance) |
|---|---|---|
| Target domain | Physical world | Live stage / live audience |
| Simulator | Physics engine (Isaac Sim, MuJoCo) | Stage simulation environment |
| Object of transfer | Robot policy / control program | Cue script + production package |
| Source of truth | Reward function | Director intent (codified, gated) |
| Validation | Simulated rollout | Simulated rehearsal |
| Transfer challenge | Sim-to-real gap | **Sim-to-stage gap (this paper)** |
| Mitigation: randomization | Domain randomization | Variability rehearsal |
| Mitigation: identification | System identification | Performer / venue identification |
| Mitigation: residual | Residual policy learning | Dress-rehearsal residual adjustment |
| Executor | Robot embodiment | Human performers + technical crew |
| Re-run semantics | Possible (deploy, observe, redeploy) | One-shot per show (previews are imperfect dress-rehearsals) |
| Success criterion | Task-completion metric | Director judgment + audience response (partially aesthetic) |
| Multi-agent structure | Single robot or fleet | Irreducibly multi-department (lighting, sound, video, scenic, blocking, script) plus cast |
| Governance | Safety review, deployment gate | Director-gated Confirmation Gates, technical and dress rehearsal sign-offs |

We claim this homomorphism is not a stylistic flourish but a genuine engineering correspondence. Each row of Table 1 maps a Sim-to-Real role to a Sim-to-Stage role that occupies the same structural position in the transfer pipeline. We argue the homomorphism licenses the import of Sim-to-Real's accumulated engineering wisdom — randomization-style mitigation, identification-style mitigation, residual-style mitigation, deployment-gate governance — into Sim-to-Stage practice. The remaining sections develop the specifics.

---

## 4. The Sim-to-Stage Gap

### 4.1 Definition

We define the **Sim-to-Stage gap** as the family of discrepancies between a simulated rehearsal and the live performance that cause a Sim-validated production package to fail on the live stage. Like the Sim-to-Real gap in robotics, the Sim-to-Stage gap is not a single phenomenon but a structural collection of distinct sub-gaps, each amenable to its own analysis and mitigation. Closing the Sim-to-Stage gap is the central open research program of the paradigm.

### 4.2 Seven Identified Sub-Gaps

We identify seven sub-gaps. We do not claim the list is exhaustive; we claim it is *useful*: each sub-gap is independently studyable, and progress on any one is progress on the paradigm. Each sub-gap is named, defined, and connected to a candidate research direction.

**Sub-gap 1 · The Timing-Variability gap.** Simulated rehearsal runs against a synthetic clock; live performance runs against human performance timing, which varies with audience response, performer state, and unrepeatable contingency. A cue script that fires precisely on a synthetic clock will fail when human performance is faster, slower, or restructured by ad-lib. *Candidate direction:* robust cue compilation that admits a tolerance window per cue, with sim-time domain randomization across performance-timing distributions.

**Sub-gap 2 · The Director-Authority gap.** In Sim-to-Real, the reward function is the authority — a formal mathematical object. In Sim-to-Stage, the director's intent is the authority, but intent is informal: aesthetic, stylistic, intuitive, evolving through rehearsal. How does a system formalize an informal authority sufficiently that the rest of the pipeline can act on it, without flattening the aesthetic content? *Candidate direction:* the Director Intelligence Profile (Section 5.2) — a model of director preference that combines explicit declared rules, learned stylistic patterns, and decision-by-decision confirmation.

**Sub-gap 3 · The Multi-Modal Coherence gap.** A live performance is a joint artifact across lighting, sound, video, scenic, blocking, script, and performer interpretation. Each modality has its own conventions, file formats, and specialist tools. Simulating one modality well is tractable; simulating all coherently is harder, and preserving coherence under transfer is harder still. *Candidate direction:* specialist production agents (Section 5.3) coordinating against a shared Authoritative Truth Source (Section 5.1), with cross-modal coherence checks at each Confirmation Gate.

**Sub-gap 4 · The Human-Execution gap.** Robots execute the deployed policy autonomously. In Sim-to-Stage, the deployed artifact is executed by humans — actors interpret blocking, stage managers call cues, technicians operate consoles. Each human introduces interpretation, slippage, and modification. How does a sim-validated artifact survive contact with human execution? *Candidate direction:* compilation targets that explicitly model human execution affordances (cue scripts written for human operators; rehearsable, not just executable), and previews / dress rehearsals as transfer-validation checkpoints.

**Sub-gap 5 · The One-Shot Deployment gap.** A robot policy can fail in deployment, be observed, and be redeployed after a fix. A live performance is one-shot per show: there is no retry. Sim-validation must be sufficient for one-shot deployment, a regime closer to safety-critical Sim-to-Real (surgical robotics, aerospace) than to typical robotics. *Candidate direction:* layered defense — sim eval, then specialist eval, then technical rehearsal eval, then dress-rehearsal eval, then preview eval — with each layer admitting only what the previous layer validated.

**Sub-gap 6 · The Long-Horizon Narrative gap.** A robot policy may have a horizon of seconds to minutes; a live performance has a horizon of 90 to 180 minutes of continuous interconnected causal narrative (foreshadowing, character arcs, dramatic structure, payoff). Local Sim-validation of each scene does not imply global validation of long-horizon coherence. *Candidate direction:* narrative-aware Project Intelligence (a long-context understanding component) coupled with explicit dramaturgical evaluation criteria during sim rehearsal.

**Sub-gap 7 · The Aesthetic-Judgment gap.** Robot success criteria are predominantly functional (the robot completed the task or not). Live performance success criteria are partially aesthetic — was the moment moving, did the comedy land, did the audience lean in. Even formal metrics (run time, sound level, cue precision) underdetermine aesthetic success. *Candidate direction:* the Director Intelligence Profile as aesthetic judge (Section 5.2), combined with structured audience response signals in previews; explicit acknowledgment that aesthetic judgment will remain partially human throughout the paradigm's lifetime.

These seven sub-gaps are the proposed map of the Sim-to-Stage research territory. We invite extension, refinement, and challenge.
