# HH-DFC-OrbitMemory

**Limit-Cycle Proliferation Under Parametric Delayed Feedback in a Conductance-Based Neuron: Bifurcation Landscape, Orbit Catalog, and Capacity Analysis**

Mohammad O. Alhawarat, Ayman J. Alnsour, Mohammed A. F. Al-Husainy, Khalil M. Abdelnaby

*Entropy*, 2026. https://doi.org/10.3390/e1010000

---

## Overview

This repository contains the complete simulation code for the paper. We show that a single Hodgkinâ€“Huxley (HH) neuron with Pyragas-type delayed feedback control (DFC) can store multiple symbols as stable periodic orbits, where the specific orbit is selected by tuning the DFC gain *K* and time delay *د„*. Sweeping the (*K*, *د„*) parameter plane reveals 207 orbit types across 12 topological categories, with a read-discriminable memory capacity of 67 symbols and a fully write-validated capacity of 12 symbols.

---

## Repository Structure

```
HH-DFC-OrbitMemory/
â”œâ”€â”€ experiments/
â”‚   â”œâ”€â”€ PS0_OrbitCatalog.ipynb          # Dense (K,د„) sweep â†’ 207 orbit types
â”‚   â”œâ”€â”€ PS0b_FloquetValidation.ipynb    # Floquet multiplier validation (9 orbits)
â”‚   â”œâ”€â”€ PS0b_ExtendedFloquet.ipynb      # Extended Floquet analysis
â”‚   â”œâ”€â”€ PS0c_ThresholdSensitivity.ipynb # ISI clustering threshold sensitivity
â”‚   â”œâ”€â”€ PS1_WriteProtocol.ipynb         # Write protocol + switching matrix
â”‚   â”œâ”€â”€ PS2_ReadProtocol.ipynb          # POLD classifier + noise robustness
â”‚   â”œâ”€â”€ PS3_WriteReadErase.ipynb        # Complete Wâ€“Râ€“E memory cycle
â”‚   â”œâ”€â”€ PS4_RateCodingBaseline.ipynb    # Rate coding baseline comparison
â”‚   â”œâ”€â”€ PS5_MaximumCapacity.ipynb       # Full pairwise confusion matrix + capacity
â”‚   â”œâ”€â”€ PS7_RetentionUnderNoise.ipynb   # Retention under additive noise
â”‚   â””â”€â”€ PS8_MultiplicativeNoise.ipynb   # Ornsteinâ€“Uhlenbeck conductance noise
â”œâ”€â”€ LICENSE
â””â”€â”€ README.md
```

---

## Six-Phase Gated Pipeline (PS0â€“PS5)

The study follows a six-phase gated pipeline in which each phase has formal pass/fail criteria that must be satisfied before proceeding:

| Phase | Notebook | Description | Gate Result |
|-------|----------|-------------|-------------|
| PS0 | `PS0_OrbitCatalog.ipynb` | Dense 10,100-point (*K*,*د„*) sweep; orbit classification and cataloging | PASS (207 types, 12 categories) |
| PS1 | `PS1_WriteProtocol.ipynb` | Write protocol performance; orbit-to-orbit switching matrix | PASS (median settling 13.9 ms) |
| PS2 | `PS2_ReadProtocol.ipynb` | POLD classifier; noise and jitter robustness | PASS (100% clean accuracy) |
| PS3 | `PS3_WriteReadErase.ipynb` | Complete writeâ€“readâ€“erase cycle; retention up to 50 s | PASS (*N*\* = 12 at 100%) |
| PS4 | `PS4_RateCodingBaseline.ipynb` | Rate coding baseline comparison (*K* = 0) | PASS (2.0أ— advantage) |
| PS5 | `PS5_MaximumCapacity.ipynb` | Full pairwise confusion matrix; maximum capacity subset | PASS (*N*\* = 67, 98.2%) |

---

## Key Results

- **207 distinct orbit types** across 12 topological categories from a 10,100-point (*K*, *د„*) sweep at *I*_bias = 10.0 آµA/cmآ²
- **Write-validated capacity: 12 symbols** â€” complete writeâ€“readâ€“erase cycle at 100% read accuracy and 92% erase verification
- **Read-discriminable capacity: 67 symbols** â€” pending write-viability confirmation for the extended set
- **11.2أ— read-discriminable advantage** over rate coding in the same neuron (2.0أ— fully validated)
- **POLD classifier**: 100% accuracy from only 5 observed ISIs, no training data required
- **Passive retention**: 100% accuracy over hold durations up to 50 s without refresh

---

## Model

The HHâ€“DFC system is governed by:

```
C_m dV/dt = I_bias + K[V(tâˆ’د„) âˆ’ V(t)] âˆ’ ل¸،_Na mآ³h(Vâˆ’E_Na) âˆ’ ل¸،_K nâپ´(Vâˆ’E_K) âˆ’ ل¸،_L(Vâˆ’E_L)
```

with standard squid giant axon parameters (*C*_m = 1 آµF/cmآ²; *ل¸،*_Na = 120, *ل¸،*_K = 36, *ل¸،*_L = 0.3 mS/cmآ²; *E*_Na = 115, *E*_K = âˆ’12, *E*_L = 10.6 mV).

Control parameters:
- **K** â‰¥ 0: DFC gain (mS/cmآ²)
- **د„** > 0: time delay (ms)
- **I_bias** = 10.0 آµA/cmآ² (fixed unless stated otherwise)

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

All simulations use Numba JIT compilation and were executed on Google Colab (Intel Xeon 2.3 GHz, 13 GB RAM). A fixed random seed (seed = 42) is used throughout for reproducibility; results are verified invariant across seeds 1â€“10.

---

## Usage

Clone the repository and run the notebooks in order (PS0 â†’ PS5):

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
  volume  = {1},
  pages   = {0},
  doi     = {10.3390/e1010000}
}
```

---

## License

This project is licensed under the MIT License â€” see the [LICENSE](LICENSE) file for details.

---

## Contact

Mohammad O. Alhawarat â€” m.hawarat@ammanu.edu.jo  
Faculty of Information Technology, Al-Ahliyya Amman University, Amman 19328, Jordan
