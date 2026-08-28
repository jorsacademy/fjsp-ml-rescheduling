# FJSP ML Rescheduler

Research-inspired Python implementation of flexible job-shop scheduling and rescheduling for Industry 4.0 scenarios.

The project combines:

- Flexible Job-Shop Scheduling Problem (FJSP) modeling
- Sequence-dependent machine setup times
- Limited setup-worker resources
- Genetic Algorithm scheduling
- Random Forest rescheduling decisions
- Processing-time variation scenarios
- ML-based vs. periodic rescheduling comparison

## Important note

This is a simplified, research-inspired implementation based on the concepts described in Li et al. (2019), *Integration of Machine Learning and Optimization Techniques for Flexible Job-Shop Rescheduling in Industry 4.0*. It is not a line-by-line reproduction of the paper.

The current classifier-training formulation is demonstrative: processing-time variation is included in the feature vector, but the rescheduling label is still based on comparing GA-generated schedules on the same base instance. For research-grade experiments, the disruption should also be propagated into the optimization state/objective and the unfinished portion of the schedule should be rescheduled explicitly.

## Fixes applied

Compared with the initial draft, this version:

- fixes setup-worker state mutation during candidate-machine evaluation;
- supports `num_workers > 1` with independent setup-worker availability clocks;
- validates machine configurations, compatible machines, and chromosome job IDs;
- prevents crossover failure for very short chromosomes;
- prevents division by zero in rescheduling-benefit evaluation;
- handles invalid one-class datasets before Random Forest/AUC evaluation;
- removes the inaccurate claim that Tabu Search is implemented.

## Installation

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\\Scripts\\activate
pip install -r requirements.txt
```

## Run

```bash
python fjsp_ml_rescheduler.py
```

The default experiment trains a Random Forest classifier and compares ML-triggered rescheduling with periodic P-2, P-4, and P-7 strategies.

## Requirements

- Python 3.10+
- NumPy
- scikit-learn

## Project status

Educational/research prototype. For publication-level benchmarking, add benchmark FJSP instances, explicit dynamic schedule-state propagation, repeated seeded experiments, confidence intervals, and stronger baselines.
