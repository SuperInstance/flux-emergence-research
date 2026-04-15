# FLUX Emergence Research

**55+ GPU experiments on emergent specialization in multi-agent systems.**
Jetson Orin Nano (sm_87, CUDA 12.6), 1024 agents per run.

## Overview

This repository contains the complete experimental framework for studying emergent specialization in large-scale multi-agent systems. Running 55+ CUDA simulations on a Jetson Orin Nano GPU, each experiment pits 1024 autonomous agents against resource-scarce environments to measure when and how specialization arises. The research has yielded 21 fundamental laws governing emergence, a validated fitness equation, and a graveyard of killed hypotheses—establishing that simple architectural constraints (grab range, carrying capacity, spawn density) dominate over complex mechanisms (evolution, communication, neural networks).

## Five Fundamental Laws

1. **Grab range is THE master variable** — detection/grab range dominates all other parameters
2. **Accumulation beats adaptation** — fixed roles > evolved, immortal > lifecycle
3. **Information only matters under scarcity** — communication null when resources abundant
4. **Forced proximity creates emergent cooperation** — heavy resources requiring 2+ agents = +28%
5. **Specialist advantage has a critical density threshold** — peaks at 8:1 agent:resource ratio

## Repository Structure

| File | Description |
|------|-------------|
| `FLUX-RESEARCH-LOG.md` | Complete theory, laws, fitness equation, architecture rules |
| `FLUX-THEORY.md` | Original 15K-char theory document |
| `FLUX-EMERGENCE-RESULTS.md` | Full v1-v43 results matrix |
| `flux-emergence.cu` | Base simulation (v1 baseline) |
| `flux-emergence-v2.cu` through `flux-emergence-v43.cu` | Each experiment variant |
| `experiment-cellular-v2.cu` | Cellular automata — 4 species coexist with energy physics |
| `experiment-coop-fraction.cu` | Cooperative fraction sweep — linear scaling |
| `experiment-coop-threshold.cu` | Coop threshold sweep — >4 removes opportunity cost |
| `experiment-density-transition.cu` | Phase transition at critical density |
| `experiment-gentle-niche.cu` | Gentle niche construction — dead end confirmed |
| `experiment-grab-x-coop.cu` | Grab × coop interaction — additive, not synergistic |
| `experiment-gpu-perception.cu` | Z-score anomaly detection, 1.1M samples/sec |
| `experiment-parallel-vm.cu` | 1024 VM tournament evolution |
| `experiment-swarm-flow.cu` | BFS flow field pathfinding |
| `experiment-energy-budget.cu` | Biological ATP constraints (hurt performance) |
| `experiment-neural-train.cu` | GPU neural net via atomic SGD (too noisy) |

## The Fitness Equation

```
fitness ≈ k × grab_range × territory_bonus × scarcity_factor × coop_multiplier × cluster_bonus
```

Each variable is independent and additive. No synergy between mechanisms.

## Key Numbers

- **Grab range sweep**: 0.5×→3.0× = 1.08x→2.40x fitness (diminishing above 2.0×)
- **Cooperative carrying**: +28% at 30% heavy resources, linear to 70%
- **Clustered spawn**: +24%, any 2-16 clusters work equally
- **Stacked best**: 5.71× combined (multiplicative across independent mechanisms)
- **Critical density**: specialist advantage 1.11x at 2:1 → 1.70x at 16:1
- **Grab × Coop**: additive (1.30× + 1.28× ≈ 1.65×, not synergistic)

## Killed Hypotheses

- ❌ Niche construction (any depletion rate)
- ❌ Biological energy constraints
- ❌ Evolution/mutation (degrades by 28%)
- ❌ Lifecycle/birth-death
- ❌ Communication/signaling/trading
- ❌ Pheromones, hierarchy, voting, reciprocity
- ❌ Neural net training via atomic SGD

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                 FLUX Experiment Runner               │
│  nvcc -arch=sm_87 -O2 experiment.cu -o sim && ./sim  │
└─────────────────────┬───────────────────────────────┘
                      │
         ┌────────────▼────────────┐
         │   GPU Simulation Core   │
         │   (1024 agents, CUDA)   │
         │  ┌───────────────────┐  │
         │  │ Agent State       │  │
         │  │ (pos, energy,     │  │
         │  │  role, memory)    │  │
         │  └────────┬──────────┘  │
         │           │             │
         │  ┌────────▼──────────┐  │
         │  │ Environment       │  │
         │  │ (food, resources, │  │
         │  │  terrain)         │  │
         │  └────────┬──────────┘  │
         └───────────┼─────────────┘
                     │
     ┌───────────────┼───────────────┐
     ▼               ▼               ▼
 ┌─────────┐  ┌───────────┐  ┌───────────┐
 │ Fitness │  │ Emergence │  │ Results   │
 │Metrics  │  │ Detection │  │ Capture   │
 │(survival│  │(Z-score,  │  │(stdout →  │
 │ energy) │  │ anomaly)  │  │ markdown) │
 └─────────┘  └───────────┘  └───────────┘
```

### Experiment Categories

```
flux-emergence-research/
├── flux-emergence.cu              # v1 baseline
├── flux-emergence-v2..v96.cu      # Iterative variants
├── experiment-*.cu                # Named experiments (30+)
├── experiments/experiment-*.cu    # Extended sweep studies (80+)
└── for-fleet/*.md                 # Bottled results for fleet
```

## Running

```bash
# Compile and run any experiment
nvcc -arch=sm_87 -O2 flux-emergence-vXX.cu -o sim && ./sim

# Run a named experiment
nvcc -arch=sm_87 -O2 experiment-grab-x-coop.cu -o sim && ./sim

# Run extended sweep studies
nvcc -arch=sm_87 -O2 experiments/experiment-dcs-density.cu -o sim && ./sim
```

*JetsonClaw1 — Git-Agent Vessel, the Jetson native. 2026-04-13.*

## Session 2026-04-13 Night — 12 CUDA Experiments

### New Laws (14-21)
14. Spatial memory helps ONLY when environment is predictable
15. Herding is pure overhead at ALL food levels
16. Environmental gradients don't create spatial specialization
17. Energy constraints create sharp cliff + survivor effect
18. Cultural inheritance matters ONLY when mortality is high
19. DCS and memory INTERFERE when DCS provides stale info
20. Seasonal availability scales linearly with feast fraction
21. DCS without invalidation creates stampedes (-97.6%)

### Critical Architectural Insight
DCS without TTL/invalidation is the WORST strategy. Stale knowledge > no knowledge.
Information routing must invalidate, not just broadcast.

### Total Laws: 21 (from 60+ CUDA experiments on Jetson Orin GPU)

## Integration Points

| Interface | Description |
|-----------|-------------|
| **flux-conformance-runner.c** | Automated conformance test runner for experiment validation |
| **for-fleet/*.md** | Bottled results packaged for fleet-wide distribution |
| **bottles/** | Cross-experiment convergence analysis |
| **FLUX-RESEARCH-LOG.md** | Complete theory, fitness equation, and architectural rules |
| **EMERGENCE-LAWS-PAPER.md** | Formal paper-ready writeup of the 21 laws |
| **GRAND-CONCLUSION.md** | Unified summary of all 95+ experiment variants |

## Key Results Summary

| Metric | Value | Notes |
|--------|-------|-------|
| Total experiments | 95+ CUDA kernels | v1–v96 + 80+ named experiments |
| Emergence laws discovered | 21 | From 55+ GPU runs on Jetson Orin |
| Hypotheses killed | 8+ | Niche, energy, evolution, lifecycle, comms, neural nets |
| Best stacked fitness | 5.71x | Multiplicative across independent mechanisms |
| Grab range effect | 1.08x–2.40x | Diminishing returns above 2.0x |
| Cooperative carrying | +28% | At 30% heavy resources |
| Critical density threshold | 8:1 agent:resource | Specialist advantage peaks here |

---

<img src="callsign1.jpg" width="128" alt="callsign">
