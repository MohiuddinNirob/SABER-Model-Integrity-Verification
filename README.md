# SABER: Joint Structural and Behavioral Verification for Edge-Deployed Model Integrity

This anonymous repository contains the implementation, evaluation scripts,
configurations, and supporting materials for **SABER**, a model integrity
verification framework for edge-deployed machine learning models.

SABER jointly captures structural and behavioral evidence from the same
challenged model execution. Structural evidence consists of the runtime
operator sequence and input-conditioned participation patterns, while
behavioral evidence consists of the clean output, perturbation-response
direction, and response magnitude.

The repository also contains the implementation of the
**Execution-Coupled Model Chain (ECMC)**, which maintains lightweight
model-dependent continuity evidence during user-level inference to detect
verification-aware model replacement.

This repository is provided for anonymous peer review and reproducibility.

---

## Overview

SABER consists of three stages.

### 1. Trusted Setup

Before deployment, the verifier:

- associates each edge node with an authorized reference model;
- establishes the structural and behavioral verification evidence;
- selects eligible perturbation layers;
- calibrates layer-specific perturbation scales and verification thresholds;
- constructs the parameter registry used by ECMC; and
- initializes the trusted continuity state.

All verification thresholds are fixed before attack evaluation.

### 2. Explicit Integrity Verification

For each explicit verification round, the verifier issues a fresh challenge.

The edge node generates:

- runtime operator sequence `G`;
- input-conditioned participation pattern `P`;
- clean output `z`; and
- perturbation response `Delta z`.

These values are returned in an authenticated integrity proof.

The verifier independently generates the corresponding evidence using the
authorized reference model and accepts the proof only when all authentication,
structural, and behavioral checks succeed.

### 3. Execution Continuity with ECMC

Explicit verification checks model integrity only during verification rounds.

Between these rounds, ECMC sparsely samples model parameters during ordinary
user inference and links the resulting observations into continuity records.

This allows the verifier to obtain model-dependent evidence about the model
serving user requests between explicit verification rounds.

---

## Verification Evidence

SABER uses four evidence components.

### Runtime Operator Sequence

The runtime sequence records monitored operator executions using stable
operator identifiers, operator types, computation-relevant attributes, and
input/output tensor shapes.

It is used to detect changes in the monitored computation structure,
configuration, or execution order.

### Input-Conditioned Participation Pattern

The participation pattern is derived from monitored intermediate tensors.

Each tensor is divided into fixed logical regions, and their normalized
absolute contributions are quantized.

This evidence captures input-conditioned internal activity that may change
even when the runtime operator sequence remains unchanged.

### Clean Output

The clean output captures the normal behavior of the challenged model.

It is compared with the output independently generated from the authorized
reference model.

### Perturbation Response

A controlled internal perturbation is applied at a verifier-selected layer.

The difference between the perturbed and clean outputs is used as the
perturbation response.

Both its direction and magnitude are verified because a model modification
may change one without substantially changing the other.

---

## Repository Structure

```text
SABER/
├── configs/       Experiment configurations
├── src/           SABER and ECMC implementation
├── attacks/       Evaluated attack implementations
├── baselines/     Baseline implementations and wrappers
├── experiments/   Experiment entry points
├── data/          Dataset preparation information
├── checkpoints/   Model preparation information
├── results/       Raw and processed experiment results
├── figures/       Figure-generation materials
└── docs/          Detailed reproducibility and security documentation
