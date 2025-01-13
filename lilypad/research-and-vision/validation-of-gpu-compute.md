---
description: Validation of GPU Computation in Decentralized, Trustless Networks
---

# Validation of GPU Compute

## Overview

The Lilypad Research team published "[Validation of GPU Computation in Decentralized, Trustless Networks](https://arxiv.org/abs/2501.05374)" diving into the complexities of validating successful compute jobs on GPUs. The investigation then explores verification methods and solutions that Lilypad can implement across the network.

Verifying computational processes in decentralized networks poses a fundamental challenge, particularly for Graphics Processing Unit (GPU) computations. The Lilypad Research team conducted an investigation revealing significant limitations in existing approaches: exact recomputation fails due to computational non-determinism across GPU nodes, Trusted Execution Environments (TEEs) require specialized hardware, and Fully Homomorphic Encryption (FHE) faces prohibitive computational costs.&#x20;

To address these challenges, this report explores three verification methodologies adapted from adjacent technical domains: model fingerprinting techniques, semantic similarity analysis, and GPU profiling. Through systematic exploration of these approaches, we develop novel probabilistic verification frameworks, including a binary reference model with trusted node verification and a ternary consensus framework that eliminates trust requirements.&#x20;

These methodologies establish a foundation for ensuring computational integrity across untrusted networks while addressing the inherent challenges of non-deterministic execution in GPU-accelerated workloads.
