# SPHY Framework - RDTSC & Chaos Stress Validation Suite

This repository provides the official empirical validation script for the **SPHY Framework**. The purpose of this utility is to audit high-precision atomic datasets generated under extreme stochastic stress conditions, proving the stability and phase coherence of the manifold without exposing the proprietary logic of the underlying kernel.

---

## What This Validator Does

The `sphy_validator_rdtsc.py` script performs a strict, read-only scan of the generated dataset (`sphy_ghz_chaos_rdtsc_dataset.csv`), executing the following integrity checks across 12,000 execution frames:

1. **Coherence and Variance Audit:** Validates that the manifold maintains 100.00% phase coherence and zero global variance ($0.00$), even under maximum chaos injection.
2. **Thermal Noise and Bit-Flip Stress ($P = 1.0$):** Confirms that the system absorbs and neutralizes stochastic perturbations and simulated bit inversions in hardware[cite: 1, 2].
3. **Memory Invariance:** Ensures that memory consumption remains static and restricted to the stack (`6152 KB`, with zero heap allocation), guaranteeing strict $\mathcal{O}(1)$ complexity[cite: 1, 2].
4. **Silicon Telemetry (RDTSC):** Processes processor clock cycle registers locked at 2.49 GHz and high-precision timestamps (`CLOCK_MONOTONIC_RAW`)[cite: 1, 2].

---

## System Requirements

The validator is written in pure Python and requires no complex external dependencies for basic execution.

* **Python:** Version `3.6` or higher.
* **Operating System:** Compatible with Linux environments (tested and optimized on Pop!_OS / Ubuntu)[cite: 1, 2].

---

## How to Run

1. Ensure that the generated dataset file (`sphy_ghz_chaos_rdtsc_dataset.csv`) is present in the same directory as the script[cite: 1, 2].
2. Run the validator via terminal:

```bash
python3 sphy_validator_rdtsc.py
