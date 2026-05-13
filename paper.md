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
