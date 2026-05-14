---
title: CTF4Nuclear MSFR
layout: default
---

# A NeurIPS 2026 benchmark for nuclear scientific ML

CTF4Nuclear is a Common Task Framework for evaluating machine-learning
surrogates of nuclear-reactor multiphysics simulations. The first
challenge in the series scores models on the **Molten Salt Fast Reactor
(MSFR)** — a Generation-IV reactor concept whose liquid-fuel design
couples neutronics, thermal-hydraulics, and salt transport in ways that
make full-physics simulations expensive. Models are evaluated on twelve
standardised experiments covering short- and long-time forecasting,
denoising, limited-data, and parametric generalisation; the public
leaderboard runs continuously on Hugging Face compute.

[**▶ Live leaderboard**](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard) &nbsp;·&nbsp;
[**Dataset**](https://huggingface.co/datasets/ctf4science/ctf4nuclear-msfr) &nbsp;·&nbsp;
[**Starter notebook (Colab)**](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard/blob/main/baselines/baseline_last.ipynb) &nbsp;·&nbsp;
[**`ctf4science` package**](https://github.com/CTF-for-Science/ctf4science)

## What you'll be modelling

Five physical fields — prompt fission power, decay heat, temperature,
axial velocity, and vertical velocity — on a 3 880-node mesh, sampled
every 0.05 s. Nine evaluation pairs produce twelve normalised scores
**E1–E12**, aggregated into a single composite **AvgScore**. As of
proposal time, the current published leader is *PyKoopman* at
**AvgScore = 70.97**; the strongest deterministic baseline
(*Baseline Last* — repeat the last training state across the forecast
horizon) sits at **62.67**.

## Timeline

| Date | Milestone |
|---|---|
| 16 June 2026 | Competition opens — public leaderboard accepts submissions |
| 1 August 2026 | Mid-competition mini-talks (top participants present) |
| 17 October 2026 | Public leaderboard closes; final-phase begins |
| 24 October 2026 | Final-phase submissions close; private re-evaluation begins |
| Late November 2026 | Winners announced |
| 11–12 December 2026 | NeurIPS Competition Workshop, San Diego |

## How to participate

1. Create a Hugging Face account (if you don't have one).
2. Clone the [`ctf4science`](https://github.com/CTF-for-Science/ctf4science) package and `pip install -e .`.
3. Download the training data from [`ctf4science/ctf4nuclear-msfr`](https://huggingface.co/datasets/ctf4science/ctf4nuclear-msfr).
4. Generate a 9 500-row predictions Parquet (or run the
   [starter notebook](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard/blob/main/baselines/baseline_last.ipynb)
   to get a working *Baseline Last* submission).
5. Push the Parquet to your own public Hugging Face dataset repository.
6. Submit via the **Submit** tab on the leaderboard — scores appear within minutes.

The starter notebook completes steps 2–6 end-to-end in under ten minutes
on a free Colab CPU instance. No GPU is required at any point.

## Prizes

- **1st place:** \$500
- **2nd place:** \$300
- **3rd place:** \$200

All winning entries are released under an OSI-approved open-source
license. Winning teams are also invited to contribute a short write-up
to the PMLR competition-track proceedings volume.

## Rules at a glance

- Maximum team size: **5**.
- Up to **5 submissions per day**; up to **2 final submissions** selected for ranking.
- **No external training data** and **no pre-trained models**.
- Same model across all metrics in a single submission (no per-metric tuning).
- LLMs are permitted as a development tool.
- The **top 10** finishers on the public leaderboard are re-evaluated on organiser hardware against a held-out parametric regime; the private re-evaluation produces the official final rankings.

Full official rules and prize terms: see the
[**Rules** tab on the leaderboard Space](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard).

## Frequently asked questions

**Who can participate?** Anyone with a Hugging Face account, subject to
the eligibility rules. Employees of the Competition Sponsor and Hugging
Face may compete but are not eligible to win prizes.

**Do I need a GPU?** No. Submissions are prediction files, not training
code; you only need enough compute to fit your own model. The reference
*Baseline Last* runs in under ten minutes on a free Colab CPU instance.

**Where is the training data?** Public mirror at
[`huggingface.co/datasets/ctf4science/ctf4nuclear-msfr`](https://huggingface.co/datasets/ctf4science/ctf4nuclear-msfr).
Backup tarball at [OSF](https://osf.io/6rzhm/).

**What format is the submission?** A single Parquet file with 9 500 rows
and columns `id, pair_id, timestep, f1, …, f19400`. Schema and
per-pair row layout: see the **Submission Format** tab on the
leaderboard Space.

**How is my score computed?** Twelve metrics across forecasting,
denoising, and parametric generalisation, each clipped to
[−100, 100], averaged into *AvgScore*. Formal definitions:
[ctf4science documentation](https://ctf-for-science.github.io/ctf4science/).

**Can I submit multiple times?** Yes — up to five per day. Pick up to
two for final ranking.

**Is there a private leaderboard?** Yes. After the public phase closes,
the top ten by public *AvgScore* are re-evaluated on organiser hardware
against a held-out parametric regime; the private scores are the
official final rankings.

**Will the test data ever be released?** Yes, after the competition
concludes, to support reproducible follow-up research.

**How do I cite this benchmark?** A reference paper *"CTF4Nuclear: A
Common Task Framework for Nuclear Fission and Fusion Models"* is
under review at NeurIPS 2026; a citation will be added here on
publication.

**Where can I ask questions?** Use the
[Community tab](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard/discussions)
on the leaderboard Space, or email
`ctf4nuclear@[INSTITUTION]` (forthcoming).

## Organisers

This benchmark is led by the
[AI Institute in Dynamic Systems](https://dynamicsai.org/), with
co-organisers across the University of Washington, Columbia University,
Politecnico di Milano, MIT, American University of Beirut, University
of Cambridge, Autodesk Research, Distyl AI, and SURF. The full
organising team is listed in the companion paper.

---

_Last updated: May 2026._
