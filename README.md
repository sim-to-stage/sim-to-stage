# Sim-to-Stage

> A paradigm for compiling director intent into rehearsable, executable,
> audit-traceable live-stage artifacts under a single authoritative truth source.

**Status:** Position paper v0.1 published 2026-05-14 — see [`paper.md`](paper.md)
**Site:** [simtostage.com](https://simtostage.com)
**Canonical home:** [github.com/sim-to-stage/sim-to-stage](https://github.com/sim-to-stage/sim-to-stage)

---

## TL;DR

Sim-to-Stage is to live performance production what **Sim-to-Real** is to robotics:
a paradigm for training, validating, and producing complex multi-modal artifacts
in a simulation environment, then transferring them to a real-world target — in
this case, the live stage.

A live performance is a coordinated multi-modal artifact: script, blocking,
lighting, sound, video, scenic, cueing. Producing it well requires the same
discipline robotics applies to producing a robot policy: simulate, validate,
gate, transfer. The Sim-to-Stage paradigm formalizes that discipline.

## What is in this repository

This repository is the canonical home of the Sim-to-Stage paradigm. It hosts:

- ✅ The **Position Paper** ([`paper.md`](paper.md)) — full definition,
  Sim-to-Real ↔ Sim-to-Stage homomorphism, Sim-to-Stage gap decomposition
  (seven sub-gaps), and seven architecture primitives. Published 2026-05-14
  as v0.1.
- ⏳ The Sim-to-Stage Benchmark proposal (`benchmark.md`) — task definitions
  and evaluation metrics. Target Q4 2026.
- ✅ Citation ([`CITATION.cff`](CITATION.cff)), license ([`LICENSE`](LICENSE)),
  and contribution guidelines.

## Roadmap

- [x] Domain registered: `simtostage.com`
- [x] Canonical GitHub home: `sim-to-stage/sim-to-stage`
- [x] **Position Paper v0.1 published 2026-05-14** — see [`paper.md`](paper.md)
- [ ] Sim-to-Stage Benchmark proposal v0.1 (target: Q4 2026)
- [ ] First external co-author / reviewer engagement
- [ ] Reference implementation public preview

## Citation

If you reference the term "Sim-to-Stage" or this paradigm in academic or
industrial work, please cite:

```bibtex
@misc{simtostage2026,
  title  = {Sim-to-Stage: A Paradigm for Live Performance Production},
  author = {{Sim-to-Stage Research}},
  year   = {2026},
  url    = {https://simtostage.com},
  note   = {Position paper v0.1, published 2026-05-14.
            Canonical repository: https://github.com/sim-to-stage/sim-to-stage}
}
```

A machine-readable `CITATION.cff` is provided in the repository root and powers
GitHub's "Cite this repository" auto-export.

## License

The text and figures in this repository are licensed under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE).
You may use, share, adapt, and translate the material freely with attribution.

## Reference implementation

An early reference implementation of the Sim-to-Stage paradigm is
[StageR](https://simtostage.com), a director-gated multi-agent stage simulation
environment. StageR is currently in incubation and shares no operational
control with this paradigm repository — the paradigm is intended to be larger
than any single implementation.

## Contact

For paradigm-level inquiries, academic collaboration, translation, or media:
see [simtostage.com](https://simtostage.com).

---

## 中文版

### TL;DR（中文）

**Sim-to-Stage** 与现场演出制作的关系，等同于 **Sim-to-Real** 与机器人的关系——
都是一种"先在仿真环境里训练、校验、产出复合制品，再迁移到真实目标"的范式。
对机器人，真实目标是物理世界；对 Sim-to-Stage，真实目标是现场舞台。

一场现场演出本身就是一份复合的多模态制品：剧本、调度、灯光、声音、视频、舞美、提示信号。
要把它做好，需要与机器人相同的工程纪律——仿真、校验、设门、迁移。
Sim-to-Stage 范式正式化了这套纪律。

### 本仓库放什么

本仓库是 Sim-to-Stage 范式的官方权威坐标。即将容纳：

- ✅ **Position Paper**（[`paper.md`](paper.md)）—— 范式完整定义、
  Sim-to-Real ↔ Sim-to-Stage 同构对照、Sim-to-Stage gap 分解（7 个子 gap）、
  7 个架构 primitives。2026-05-14 已发布 v0.1。
- ⏳ Sim-to-Stage Benchmark 提案（`benchmark.md`）—— 评估任务定义与指标。目标 Q4 2026。
- ✅ 引用规范、协议、贡献指南。

### 引用本工作

请使用上方 BibTeX 区块，或点击仓库主页 "Cite this repository" 按钮自动导出。

### 参考实现

Sim-to-Stage 范式的一个早期参考实现是 [StageR](https://simtostage.com) ——
一个导演裁决型多智能体舞台仿真环境。StageR 目前在孵化中，与本范式仓库不共享运营控制权：
范式的存续应大于任何单一实现。
