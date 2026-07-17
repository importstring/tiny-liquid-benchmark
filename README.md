# tiny-liquid-benchmark

A small benchmark for testing a simple question:

> Under a tight compute and memory budget, when do tiny liquid / state-space style models beat tiny transformers on sequence tasks?

This repo is an early prototype. The goal is not to reproduce frontier-scale Liquid results. The goal is to build a small, fair, reproducible benchmark that compares two model families under the same constraints.

## Current idea

The benchmark will compare:

- a tiny transformer
- a tiny liquid / state-space style model

Both models should be matched as closely as possible on:

- parameter count
- training budget
- hardware setting
- sequence task setup

I care about more than just accuracy. I also want to look at:

- CPU latency
- memory use
- robustness to noise / missing inputs / small shifts

## Why this exists

A lot of model comparisons happen at scales that are far beyond what I can run locally. I want something smaller and cleaner:

- small enough to run on modest hardware
- structured enough to be a fair comparison
- simple enough that the results are interpretable

The main hypothesis is that liquid / state-space style models may be strongest not at giant scale, but in constrained sequential settings where compute, memory, and latency actually matter.

## Planned structure

```text
.
├── README.md
├── .gitignore
├── prototype.ipynb
├── configs/
├── tasks/
├── models/
├── train.py
├── eval.py
└── results/
```

`prototype.ipynb` will be the place where I sketch things quickly before deciding what deserves to become actual code.

## First benchmark version

Initial plan:

1. Pick 1 synthetic sequence task.
2. Optionally add 1 small real dataset.
3. Define fairness constraints before building too much model code.
4. Implement a tiny transformer baseline.
5. Implement a tiny liquid / SSM-style baseline.
6. Compare error, latency, memory, and robustness.

## Fairness constraints

This part matters a lot.

Before tuning models too much, I want to lock down things like:

- max parameter count
- fixed training steps / epochs
- sequence length
- batch size
- optimizer settings or tuning rules
- hardware target for latency measurement

Otherwise the comparison gets muddy fast.

## Status

Very early.

Right now this repo is mostly for:

- scoping the benchmark cleanly
- prototyping tasks and baselines
- figuring out what “fair” should mean here

## Notes to self

Questions that still need sharper answers:

- What task best stresses sequential structure without becoming huge?
- What is the cleanest tiny liquid / SSM baseline to start from?
- Should “fixed compute” mean params, FLOPs, wall-clock, or some combination?
- What robustness test is actually worth running in version 1?

## Rough week plan

1. Define tasks, pipeline, and fairness constraints.
2. Build tiny transformer and liquid / state-space baselines.
3. Run matched experiments.
4. Add robustness tests.
5. Analyze results.
6. Clean up repo and write a short note.

## Goal

Build a benchmark that is small, honest, and informative.