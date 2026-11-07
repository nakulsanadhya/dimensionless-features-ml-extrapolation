# Can dimensional analysis make ML models extrapolate?

An educational Jupyter notebook on **input representation vs model choice under distribution shift**, written for PGE 383 (Subsurface Machine Learning, Prof. Michael Pyrcz) at The University of Texas at Austin.

Raw, log-transformed and dimensionless inputs are compared with linear regression, a random forest and a neural network. The test case is 2,900 simulations of 1D consolidation of a layered soil column. Each model is tested in range and on two shifts:
- larger absolute scales
- a fluid-solid coupling beyond its training range

The notebook also covers grouped cross-validation, data leakage, inductive bias and permutation importance.

## Contents

| Path | What |
|---|---|
| `dimensionless_extrapolation.ipynb` | the notebook |
| `data/train.csv`, `test.csv`, `ood_scale.csv`, `ood_coupling.csv` | 2,000 / 300 / 300 / 300 simulations, one row each: `sim_id`, 10 inputs (`H_m`, `sigma0_Pa`, `M_Pa`, `alpha`, `k1_m2`-`k3_m2`, `Mc1_Pa`-`Mc3_Pa`), 41 output times `t_00`-`t_40` [s] and settlements `s_00`-`s_40` [m] |

The data come from a layered finite-volume solver extended from the reference solver in [poroConsolidationFoam](https://github.com/nakulsanadhya/poroConsolidationFoam), which is verified against the exact Terzaghi solution.

## Running it

- Requirements: Python 3 with numpy, pandas, matplotlib, scikit-learn and Jupyter.
- The notebook reads the CSVs from this repository's GitHub URL. To read the local `data/` folder instead, set `LOCAL = True` in the Load Data cell.
- It runs top to bottom in about 3.5 minutes on a laptop CPU. Seeds are fixed, so a rerun in the same environment gives identical results.
- Tested with Python 3.12.7, numpy 1.26.4, pandas 2.2.2, scikit-learn 1.7.1 and matplotlib 3.9.2 (Anaconda).
- The exact numbers need scikit-learn 1.7.1. Newer versions run without errors, but they assign the grouped cross-validation folds differently and build slightly different random forests, so the cross-validation and random-forest scores shift; the linear and neural-network test scores are unchanged.

## License

MIT, see [LICENSE](LICENSE). The notebook cites the course e-book (Pyrcz, *Applied Machine Learning in Python*, CC BY-NC-ND 4.0) by chapter. No code from the e-book is included.
