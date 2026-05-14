---
title: CTF4Nuclear MSFR
layout: default
---

<p class="lead">
CTF4Nuclear is a NeurIPS 2026 competition for evaluating machine-learning surrogates of nuclear-reactor multiphysics simulations. The first challenge in the series scores models on the <strong>Molten Salt Fast Reactor (MSFR)</strong> — a Generation-IV reactor concept whose liquid-fuel design couples neutronics, thermal-hydraulics, and salt transport in ways that make full-physics simulations expensive. Models are evaluated on twelve standardised experiments covering short- and long-time forecasting, denoising, limited-data, and parametric generalisation; the public [Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard) runs continuously on Hugging Face compute.
</p>

<div class="button-row">
<a href="https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard">▶ Live leaderboard</a>
<a href="https://huggingface.co/datasets/ctf4science/ctf4nuclear-msfr">Dataset</a>
<a href="https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard/blob/main/baselines/baseline_last.ipynb">Starter notebook</a>
<a href="https://github.com/CTF-for-Science/ctf4science"><code>ctf4science</code> package</a>
</div>

## The challenge

Nuclear fission and fusion reactors are among the most safety-critical
dynamical systems ever engineered. Their safe operation demands
continuous, real-time knowledge of the full multi-physics state of the
reactor core — neutron flux distributions, fuel and coolant
temperatures, coolant velocity fields, and delayed-neutron precursor
concentrations. In next-generation reactor concepts — Generation-IV
fission designs such as molten salt reactors and micro-reactors, and
magnetic-confinement fusion devices — extreme environments make in-core
instrumentation nearly impossible: sensors are physically confined to
core boundaries or external shielding structures.

**Competition task.** Reconstruct the spatially resolved, multi-field
state of the reactor core given only sparse point measurements of a
single observable field. This setting is fundamentally different
from standard time-series forecasting and has no analogue in existing
ML benchmarks. The first challenge in the CTF4Nuclear series targets
the Molten Salt Fast Reactor: five coupled fields — prompt fission
power, decay heat, temperature, and two velocity components — on a
3 880-node mesh, evaluated across twelve experiments that probe
short- and long-time forecasting, denoising, limited-data, and
parametric generalisation.

**Why it matters.** Digital twins capable of real-time state estimation
from sparse sensors are a prerequisite for autonomous reactor control,
predictive maintenance, and rapid accident prognosis. The IAEA has
identified AI-enabled digital twins as a strategic priority for nuclear
safety, and the OECD Nuclear Energy Agency has called for standardised
ML benchmarks in this domain. The underlying inverse problem —
recovering a high-dimensional multi-physics state from partial,
indirect observations — also arises in climate modelling, industrial
process control, and biomedical monitoring, making algorithmic
advances broadly transferable.

## Tentative timeline

The launch date and the NeurIPS Competition Workshop date are fixed.
All other dates below are tentative and will be finalised at competition
launch.

| Date | Milestone |
|---|---|
| **June 2026** | Competition opens — public [Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard) accepts submissions |
| August 2026 | Mid-competition mini-talks (top participants present their approaches) |
| Mid-October 2026 | Public [Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard) closes; final phase begins (top submissions re-evaluated on organiser hardware against a held-out parametric regime) |
| November 2026 | Winners announced; PMLR proceedings write-ups invited |
| **11–12 December 2026** | NeurIPS Competition Workshop, Sydney |

## How to participate

1. Create a Hugging Face account (if you don't have one).
2. Clone the [`ctf4science`](https://github.com/CTF-for-Science/ctf4science) package and `pip install -e .`.
3. Download the training data from [`ctf4science/ctf4nuclear-msfr`](https://huggingface.co/datasets/ctf4science/ctf4nuclear-msfr).
4. Generate a 9 500-row predictions Parquet (or run the
   [starter notebook](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard/blob/main/baselines/baseline_last.ipynb)
   to get a working *Baseline Last* submission).
5. Push the Parquet to your own public Hugging Face dataset repository.
6. Submit via the **Submit** tab on the [Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard) — scores appear within minutes.

The [starter notebook](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard/blob/main/baselines/baseline_last.ipynb)
completes steps 2–6 end-to-end in under ten minutes on a free Colab CPU
instance.

## Rules

The competition rules are tentative and still being finalised. Winning
entries are released under an OSI-approved open-source license, and
winning teams are invited to contribute a short write-up to the PMLR
competition-track proceedings volume.

Full official rules — including submission caps, allowed external data
and tools, and the final re-evaluation procedure — will be published on
the
[Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard)
before competition launch.

## Frequently asked questions

**Who can participate?** Anyone with a Hugging Face account.

**Do I need a GPU?** Not necessarily. Submissions are prediction files,
not training code, and the [Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard) scoring runs entirely on
Hugging Face compute — no resources are required from you to submit.
However, most deep-learning approaches will still need a GPU to train
your model. The reference
[*Baseline Last*](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard/blob/main/baselines/baseline_last.ipynb)
is pure NumPy and runs in under ten minutes on a free Colab CPU
instance.

**Where is the training data?** Public mirror at
[`huggingface.co/datasets/ctf4science/ctf4nuclear-msfr`](https://huggingface.co/datasets/ctf4science/ctf4nuclear-msfr).
Backup tarball at [OSF](https://osf.io/6rzhm/).

**What format is the submission?** A single Parquet file with 9 500 rows
and columns `id, pair_id, timestep, f1, …, f19400`. Schema and
per-pair row layout: see the **Submission Format** tab on the
[Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard).

**How is my score computed?** Twelve metrics across forecasting,
denoising, and parametric generalisation, each clipped to
[−100, 100], averaged into *AvgScore*. Formal definitions:
[ctf4science documentation](https://ctf-for-science.github.io/ctf4science/).

**Can I submit multiple times?** Yes — the per-day and final-submission
limits will be set in the official rules published before launch.

**Is there a private leaderboard?** Yes. After the public phase closes,
top finishers are re-evaluated on organiser hardware against a held-out
parametric regime; the private scores are the official final rankings.

**How do I cite this benchmark?** A reference paper *"CTF4Nuclear: A
Common Task Framework for Nuclear Fission and Fusion Models"* is
under review at NeurIPS 2026; a citation will be added here on
publication.

**Where can I ask questions?** Use the
[Community tab](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard/discussions)
on the [Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard). For email, write to
[alexeyy@uw.edu](mailto:alexeyy@uw.edu) for technical questions
(submission, scoring, data) or to
[kutz@uw.edu](mailto:kutz@uw.edu) for general questions about the
competition.

## Lead organisation and sponsors

<div class="sponsor-banners">
<a href="https://dynamicsai.org/"><img class="ai-institute" src="assets/ai-institute-banner.png" alt="AI Institute in Dynamic Systems"></a>
<a href="https://huggingscience.co/"><img class="huggingscience" src="assets/huggingscience-logo.svg" alt="Hugging Science"></a>
<a href="https://huggingface.co/"><img class="huggingface" src="assets/huggingface-logo.svg" alt="Hugging Face"></a>
</div>

The CTF4Nuclear competition is led by the
[AI Institute in Dynamic Systems](https://dynamicsai.org/), with
co-organisers across the University of Washington, Columbia University,
Politecnico di Milano, MIT, American University of Beirut, University
of Cambridge, Autodesk Research, Distyl AI, and SURF; the full
organising team is listed in the companion paper.
[Hugging Face](https://huggingscience.co/) sponsors all
submission-evaluation compute and hosts the public
[Hugging Face leaderboard](https://huggingface.co/spaces/ctf4science/ctf4nuclear-msfr-leaderboard).

