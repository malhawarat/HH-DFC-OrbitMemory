# HH-DFC-OrbitMemory

**Limit-Cycle Proliferation Under Parametric Delayed Feedback in a Conductance-Based Neuron: Bifurcation Landscape, Orbit Catalog, and Capacity Analysis**

Mohammad O. Alhawarat, Ayman J. Alnsour, Mohammed A. F. Al-Husainy, Khalil M. Abdelnaby

*Entropy*, 2026. https://doi.org/TBI

---

## Overview

This repository contains the complete simulation code for the paper. We show that a single Hodgkin–Huxley (HH) neuron with Pyragas-type delayed feedback control (DFC) can store multiple symbols as stable periodic orbits, where the specific orbit is selected by tuning the DFC gain *K* and time delay *τ*. Sweeping the (*K*, *τ*) parameter plane reveals 207 orbit types across 12 topological categories, with a read-discriminable memory capacity of 67 symbols and a fully write-validated capacity of 12 symbols.

---

## Repository Structure

```
HH-DFC-OrbitMemory/
├── experiments/
│   ├── PS0_OrbitCatalog.ipynb          # Dense (K,τ) sweep → 207 orbit types
│   ├── PS0b_FloquetValidation.ipynb    # Floquet multiplier validation (9 orbits)
│   ├── PS0b_ExtendedFloquet.ipynb      # Extended Floquet analysis
│   ├── PS0c_ThresholdSensitivity.ipynb # ISI clustering threshold sensitivity
│   ├── PS1_WriteProtocol.ipynb         # Write protocol + switching matrix
│   ├── PS2_ReadProtocol.ipynb          # POLD classifier + noise robustness
│   ├── PS3_WriteReadErase.ipynb        # Complete W–R–E memory cycle
│   ├── PS4_RateCodingBaseline.ipynb    # Rate coding baseline comparison
│   ├── PS5_MaximumCapacity.ipynb       # Full pairwise confusion matrix + capacity
│   ├── PS7_RetentionUnderNoise.ipynb   # Retention under additive noise
│   └── PS8_MultiplicativeNoise.ipynb   # Ornstein–Uhlenbeck conductance noise
├── LICENSE
└── README.md
```

---

## Six-Phase Gated Pipeline (PS0–PS5)

The study follows a six-phase gated pipeline in which each phase has formal pass/fail criteria that must be satisfied before proceeding:

| Phase | Notebook | Description | Gate Result |
|-------|----------|-------------|-------------|
| PS0 | `PS0_OrbitCatalog.ipynb` | Dense 10,100-point (*K*,*τ*) sweep; orbit classification and cataloging | PASS (207 types, 12 categories) |
| PS1 | `PS1_WriteProtocol.ipynb` | Write protocol performance; orbit-to-orbit switching matrix | PASS (median settling 13.9 ms) |
| PS2 | `PS2_ReadProtocol.ipynb` | POLD classifier; noise and jitter robustness | PASS (100% clean accuracy) |
| PS3 | `PS3_WriteReadErase.ipynb` | Complete write–read–erase cycle; retention up to 50 s | PASS (*N*\* = 12 at 100%) |
| PS4 | `PS4_RateCodingBaseline.ipynb` | Rate coding baseline comparison (*K* = 0) | PASS (2.0× advantage) |
| PS5 | `PS5_MaximumCapacity.ipynb` | Full pairwise confusion matrix; maximum capacity subset | PASS (*N*\* = 67, 98.2%) |

---

## Key Results

- **207 distinct orbit types** across 12 topological categories from a 10,100-point (*K*, *τ*) sweep at *I*_bias = 10.0 µA/cm²
- **Write-validated capacity: 12 symbols** — complete write–read–erase cycle at 100% read accuracy and 92% erase verification
- **Read-discriminable capacity: 67 symbols** — pending write-viability confirmation for the extended set
- **11.2× read-discriminable advantage** over rate coding in the same neuron (2.0× fully validated)
- **POLD classifier**: 100% accuracy from only 5 observed ISIs, no training data required
- **Passive retention**: 100% accuracy over hold durations up to 50 s without refresh

---

## Model

The HH–DFC system is governed by:

```
C_m dV/dt = I_bias + K[V(t−τ) − V(t)] − ḡ_Na m³h(V−E_Na) − ḡ_K n⁴(V−E_K) − ḡ_L(V−E_L)
```

with standard squid giant axon parameters (*C*_m = 1 µF/cm²; *ḡ*_Na = 120, *ḡ*_K = 36, *ḡ*_L = 0.3 mS/cm²; *E*_Na = 115, *E*_K = −12, *E*_L = 10.6 mV).

Control parameters:
- **K** ≥ 0: DFC gain (mS/cm²)
- **τ** > 0: time delay (ms)
- **I_bias** = 10.0 µA/cm² (fixed unless stated otherwise)

---

## Requirements

```
Python 3.8+
numpy
scipy
matplotlib
numba
jupyter
```

All simulations use Numba JIT compilation and were executed on Google Colab (Intel Xeon 2.3 GHz, 13 GB RAM). A fixed random seed (seed = 42) is used throughout for reproducibility; results are verified invariant across seeds 1–10.

---

## Usage

Clone the repository and run the notebooks in order (PS0 → PS5):

```bash
git clone https://github.com/malhawarat/HH-DFC-OrbitMemory.git
cd HH-DFC-OrbitMemory/experiments
jupyter notebook
```

Each notebook is self-contained with formal pass/fail gate criteria. PS0 must be run first as subsequent phases depend on the cached orbit catalog it produces.

---

## Data Availability

The complete orbit catalog CSV and processed output data are included in the repository. Raw simulation outputs exceeding the repository size limit are available from the corresponding author upon reasonable request (m.hawarat@ammanu.edu.jo).

---

## Citation

If you use this code, please cite:

```bibtex
@article{alhawarat2026limitcycle,
  title   = {Limit-Cycle Proliferation Under Parametric Delayed Feedback in a 
             Conductance-Based Neuron: Bifurcation Landscape, Orbit Catalog, 
             and Capacity Analysis},
  author  = {Alhawarat, Mohammad O. and Alnsour, Ayman J. and 
             Al-Husainy, Mohammed A. F. and Abdelnaby, Khalil M.},
  journal = {Entropy},
  year    = {2026},
  volume  = {TBI},
  pages   = {TBI},
  doi     = {TBI}
}
```

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## Contact

Mohammad O. Alhawarat — m.hawarat@ammanu.edu.jo
Department of Data Science and AI, 
Faculty of Information Technology, 
Al-Ahliyya Amman University, Amman 19328, Jordan
