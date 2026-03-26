# Incremental and Direct Design Optimization using Mathematical Programming and Symbolic Regression

> **Ankush Kapoor, Tapabrata Ray, Hemant Kumar Singh**  
> School of Engineering and Technology, University of New South Wales Canberra, Australia  
> *ASME Journal of Mechanical Design*

---

## Overview

This repository contains the code and data accompanying the paper. The work addresses **surrogate-assisted incremental design optimization** — identifying a sequence of designs with small, progressive changes in performance to enable gradual product transitions — and **surrogate-assisted direct optimization** via Symbolic Regression (SR) coupled with Mathematical Programming.

Two core approaches are demonstrated:

1. **MIP-based incremental design**: The incremental design problem is posed directly as a MIP and solved efficiently using [SCIP](https://www.scipopt.org/).
2. **SR-embedded MIP**: For problems where explicit algebraic expressions are unavailable, [PySR](https://github.com/MilesCranmer/PySR) is used to extract interpretable surrogate expressions from sampled data, which are then embedded into the MINLP formulation.

---

## Repository Structure

```
.
├── Problem_4_1_Geometric_Path_Planning.ipynb
├── Problem_4_2_Welded_Beam_Incremental_Design_With_MINLP.ipynb
├── Problem_4_3_Incremental_Design_with_SR_embedded_MINLP.ipynb
├── Problem_4_4_Direct_PySR_coupled_with_MINLP.ipynb
├── Problem_4_4_Direct_PySR_coupled_with_MINLP_post_processing.ipynb
├── welded_beam_constraints.csv
├── welded_beam_objective.csv
├── env_full.yml
└── README.md
```

### Notebooks

| Notebook | Description |
|---|---|
| `Problem_4_1_Geometric_Path_Planning.ipynb` | Geometric path planning problem: finds an incremental sequence of 2D designs navigating around circular infeasible regions, formulated and solved as a MIP using SCIP. |
| `Problem_4_2_Welded_Beam_Incremental_Design_With_MINLP.ipynb` | Incremental design of the welded beam benchmark using explicit algebraic expressions embedded directly into a MIP. |
| `Problem_4_3_Incremental_Design_with_SR_embedded_MINLP.ipynb` | Black-box incremental optimization of the welded beam problem: PySR symbolic regression surrogates are iteratively fitted to sampled data and embedded into the incremental MIP. Includes post-processing and surrogate accuracy analysis. |
| `Problem_4_4_Direct_PySR_coupled_with_MINLP.ipynb` | Direct surrogate-assisted optimization: PySR surrogates for the objective and constraints are iteratively refined and solved via SCIP to drive the search toward the global optimum. |
| `Problem_4_4_Direct_PySR_coupled_with_MINLP_post_processing.ipynb` | Post-processing for Problem 4.4: collects best-per-seed results, computes summary statistics, and generates figures. |

### Data Files

| File | Description |
|---|---|
| `welded_beam_objective.csv` | Initial Latin Hypercube Sampling (LHS) evaluations of the welded beam objective function ($f$) with design variables $x_1$–$x_4$. |
| `welded_beam_constraints.csv` | Corresponding constraint values ($g_1$–$g_4$) for the same LHS sample points. |

---

## Environment Setup

The environment was built with **conda** and **Python 3.12**. To recreate it:

```bash
conda env create -f env_full.yml
conda activate pysr
```

Key dependencies include:

| Package | Version | Role |
|---|---|---|
| `pysr` | 1.5.5 | Symbolic regression via genetic programming (Julia backend) |
| `pyomo` | 6.9.2 | Algebraic modelling language for MINLP |
| `pyscipopt` | 5.6.0 | Python interface to the SCIP solver |
| `sympy` | 1.14.0 | Symbolic mathematics and SymPy→Pyomo expression translation |
| `scipy` | 1.15.2 | Latin Hypercube Sampling, spatial utilities |
| `numpy` | 1.26.4 | Numerical computations |
| `pandas` | 2.2.3 | Data handling |
| `matplotlib` | 3.10.1 | Plotting |

> **Note on PySR:** PySR requires a Julia runtime, which is automatically installed on first use via `pyjuliacall`. The first run may take several minutes to compile the Julia environment.

> **Note on SCIP:** The notebooks use SCIP as the MINLP solver via `pyscipopt`. SCIP must be installed and accessible. See [https://www.scipopt.org/](https://www.scipopt.org/) for installation instructions.

---

## Running the Code

Each notebook is self-contained and can be run sequentially from top to bottom. The recommended order follows the paper:

1. `Problem_4_1_Geometric_Path_Planning.ipynb`
2. `Problem_4_2_Welded_Beam_Incremental_Design_With_MINLP.ipynb`
3. `Problem_4_3_Incremental_Design_with_SR_embedded_MINLP.ipynb`
4. `Problem_4_4_Direct_PySR_coupled_with_MINLP.ipynb`
5. `Problem_4_4_Direct_PySR_coupled_with_MINLP_post_processing.ipynb` (run after 4)

Results and figures are saved to `results/` and `Results-*/` subdirectories created at runtime.

---

## Citation

If you use this code in your research, please cite:

```
Kapoor, A., Ray, T., and Singh, H. K., "Incremental and Direct Design Optimization 
using Mathematical Programming and Symbolic Regression," 
ASME Journal of Mechanical Design.
```

---

## Contact

- Ankush Kapoor — ankush.kapoor@unsw.edu.au  
- Tapabrata Ray — t.ray@unsw.edu.au  
- Hemant Kumar Singh — hemant.singh@unsw.edu.au  

School of Engineering and Technology, University of New South Wales Canberra, Australia
