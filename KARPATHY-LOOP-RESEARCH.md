# The Karpathy Loop — Applications for Cinema & AI Workflows
_Autoresearch — March 2026 — 4 parallel agents, 20+ sources_

## Executive Summary

The **Karpathy Loop** (March 2026, 42k GitHub stars) is an autonomous optimization pattern with 3 primitives: editable file + scalar metric + time-boxed cycle. Karpathy achieved 11% improvement on LLM training over 700 experiments in 2 days. Shopify achieved 53% speedup on Liquid in 120 experiments. The pattern is universal.

## Core Mechanics

### The 3 Files
- `prepare.py`: fixed harness (data, tokenizer, eval). Agent NEVER touches.
- `train.py`: the only editable file. Agent modifies architecture, hyperparams, optimizer.
- `program.md`: instructions for the agent. Human iterates on this file.

### The Loop
1. Agent reads `program.md`
2. Agent modifies `train.py`  
3. Git commit on feature branch
4. Training runs for exactly 5 minutes (fixed budget)
5. Evaluate `val_bpb` (validation bits-per-byte)
6. If better → keep. If worse → revert.
7. Repeat indefinitely ("NEVER STOP" instruction)

Cadence: ~12 experiments/hour, ~100 per night.

## Real-World Adaptations

| Who | Asset | Metric | Result |
|-----|-------|--------|--------|
| **Shopify (Tobi Lütke)** | Ruby tokenizer (Liquid) | ThemeRunner benchmark | 53% faster, 61% fewer allocations, 93 commits |
| **Ole Lehmann** | Skill .md prompt | Pass/fail checklist | 56% → 92% accuracy in 4 rounds |
| **Udit Goenka** | Claude Code skill | Variable (marketing/sales/HR) | MIT framework, 608 stars |
| **P.J. Hoberman** | Hybrid search algo | Composite score | 60 experiments, Pareto ceiling at 0.72 |
| **Backbeat v0.7.0** | Source code | `npm test` exit 0 | Retry + Optimize strategies |

## Applications for Filmmakers

### 1. ComfyUI Workflow Optimization
- **Asset**: workflow JSON (cfg, steps, denoise, sampler, LoRA weight)
- **Metric**: CLIP similarity vs 5-10 hand-picked reference images
- **Cycle**: 5 min/iteration, 20 iterations overnight
- **Impact**: from "tweak → render → look → tweak" (30 min) to "define style → sleep → result"

### 2. Dialogue/Voiceover via Agent Council
- **Asset**: voiceover script for a character
- **Metric**: weighted vote from 5 filmmaker agent personas on a quality checklist
- **Cycle**: 8 rewrite iterations with scoring
- **Impact**: calibrated voiceover draft by an autonomous "filmmaker committee"

### 3. LoRA Hyperparameter Search
- **Asset**: training config (rank, learning rate, steps)
- **Metric**: ArcFace face similarity score
- **Cycle**: overnight runs on GPU
- **Impact**: automatic character likeness fine-tuning

### 4. Video Prompt Template Optimization
- **Asset**: Seedance/Krea prompt template with variables
- **Metric**: optical flow consistency between frames
- **Cycle**: API calls, 3 min per generation
- **Impact**: auto-optimized video prompts for temporal coherence

### 5. Narrative Structure Optimization
- **Asset**: scene beatsheet (durations + order)
- **Metric**: Pearson correlation between tension curve and target curve
- **Cycle**: 100+ iterations in < 2 min (pure computation)
- **Impact**: algorithmic exploration of alternative narrative structures

### 6. Bible/Script Coherence
- **Asset**: project bible markdown files
- **Metric**: contradiction count detected by LLM
- **Cycle**: 10 iterations with diff per edit
- **Impact**: auto-coherent project documentation

## Key Principle

> The filmmaker defines the goal (reference images, target curve, labeled examples).
> The loop does the search.
> The decision remains human.
> The role shifts from "parameter operator" to "creative director".

## Key Karpathy Quotes

> "The goal is to engineer your agents to make the fastest research progress indefinitely and without any of your own involvement."

> "any metric you care about that is reasonably efficient to evaluate...can be autoresearched by an agent swarm"

> "Context engineering is the delicate art and science of filling the context window with just the right information for the next step."

## Sources
- [karpathy/autoresearch](https://github.com/karpathy/autoresearch)
- [X @karpathy — launch](https://x.com/karpathy/status/2030371219518931079)
- [X @karpathy — results](https://x.com/karpathy/status/2031135152349524125)
- [X @karpathy — SETI@home](https://x.com/karpathy/status/2030705271627284816)
- [Fortune](https://fortune.com/2026/03/17/andrej-karpathy-loop-autonomous-ai-agents-future/)
- [Data Science Dojo](https://datasciencedojo.com/blog/karpathy-autoresearch-explained/)
- [The New Stack](https://thenewstack.io/karpathy-autonomous-experiment-loop/)
