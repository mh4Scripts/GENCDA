# GENCDA

> **Disclaimer — Dependency & Code Update (March 2026)**
>
> This fork has been updated to work with modern versions of its dependencies.
> The original project ([marti5ini/GENCDA](https://github.com/marti5ini/GENCDA)) was built with packages that are now deprecated or no longer supported.
> Below is a summary of the changes made:
>
> **Deprecated Module Fixes**
> | Module | Change | Reason |
> |--------|--------|--------|
> | NetworkX | `from_numpy_matrix()` → `from_numpy_array()` | Removed in NetworkX 3.0+ |
> | scikit-learn | `mean_squared_error(squared=False)` → `root_mean_squared_error()` | Deprecated in scikit-learn 1.4+ |
> | SDV | `sdv.tabular.CTGAN/TVAE` → `sdv.single_table.CTGANSynthesizer/TVAESynthesizer` | API changed in SDV 1.x |
> | KMeans | Added explicit `n_init=10` | Default changed to `"auto"` in scikit-learn 1.4+ |
> | PyFIM | Install via `conda-forge` or build from source | PyPI wheels only support Python ≤3.7; no pre-built wheels for 3.9+ |
>
> **Code Quality Improvements**
> - Fixed mutable default arguments in `CausalDataFrame`, `RelatedDataframe`, and `Distribution`
> - Removed duplicate `model.fit()` call in `hoyer.py`
> - Added missing `import pandas as pd` in `correlations.py` and `ncda.py`
> - Added missing `__init__.py` for `apriori/` and `baselines/` packages
> - Fixed typo `thresold` → `threshold` in `correlations.py`
> - Removed duplicate `networkx` import alias in `utils.py`
> - Cleaned up unnecessary `.keys()` calls and trailing semicolons
> - Added `kneed` to `requirements.txt` (was used but not listed)
> - Updated all dependency versions in `requirements.txt`

Welcome to the complete beginner's guide to **GENCDA**, a **GE**nerative method based on **N**onlinear **C**ausal **D**iscovery with **A**priori! If you're looking for a comprehensive guide to our approach, then you've come to the right place.

# Tutorial

For example usage of:

* [NCDA](https://github.com/marti5ini/GENCDA/blob/master/tutorials/ncda.ipynb)
* [GENCDA](https://github.com/marti5ini/GENCDA/blob/master/tutorials/gencda.ipynb)
* [CausalDataframe](https://github.com/marti5ini/GENCDA/blob/master/tutorials/causalDataframe.ipynb)

## Running the Tutorials

Make sure you have completed the [Setup](#setup) steps first, then launch Jupyter:

```bash
pip install jupyter
jupyter notebook tutorials/
```

### 1. CausalDataframe (`tutorials/causalDataframe.ipynb`)

Demonstrates how to generate synthetic datasets with known causal structures.

**Steps:**
1. Import `CausalDataFrame` from the `causalDataframe` module
2. Define a DAG (Directed Acyclic Graph) by specifying edges and isolated nodes
3. Generate synthetic data — source nodes are sampled independently, dependent variables are created by combining parent variables with nonlinear functions (sin, cos, sqrt, log, tan)
4. Generate random DAGs using `randomDag()`
5. Visualize graphs with `show_graph()`

### 2. NCDA (`tutorials/ncda.ipynb`)

Demonstrates Nonlinear Causal Discovery with Additive Noise Models and the NCDA (with Apriori) method.

**Steps:**
1. **Bivariate case** — Load the *abalone* dataset, create a `NonlinearANM` object, test independence between two variables, fit nonlinear regression in both directions (x→y and y→x), and determine the causal direction from residual independence
2. **Multivariate case** — Create synthetic data with a known causal structure (`w→x, w→y, x→z, y→z`), use `NCDApriori` to mine frequent itemsets via Apriori, then apply nonlinear causal discovery on filtered variable pairs
3. Evaluate results with precision, recall, accuracy, and F1-score

### 3. GENCDA (`tutorials/gencda.ipynb`)

Demonstrates the full GENCDA pipeline: discover causal structure, then generate synthetic data respecting it.

**Steps:**
1. Load a dataset (e.g., *diabetes* from sklearn, or CSV files from `datasets/`)
2. Construct or discover the DAG using `NCDApriori` (fitApriori → fitNCD)
3. Generate synthetic data with `RelatedDataframe`, preserving the discovered causal relationships
4. Compare against baselines: random generation, CTGAN, and TVAE
5. Evaluate quality using KDE-based metrics (SSE, RMSE) and Local Outlier Factor (LOF)
6. Visualize KDE plots comparing original vs. generated distributions

### Available Datasets

The `datasets/` folder contains ready-to-use CSV files:

| Dataset | File | Ground Truth DAG |
|---------|------|-----------------|
| Abalone | `abalone.csv` | Rings → Length |
| Diabetes | `diabetes.csv` | bmi → si, bmi → bp, si → bp |
| Old Faithful | `faithful.csv` | Time Interval → Duration |
| Climate | `climate.csv` | Altitude → Temperature |
| UN Data | `undata.csv` | Female Age ← Latitude |
| Synthetic | `synthetic.csv` | w → x, w → y, x → z, y → z |


# Setup

The packages requires a python version >=3.9, as well as some libraries listed in requirements file. For some additional functionalities, more libraries are needed for these extra functions and options to become available. 

```
git clone https://github.com/marti5ini/GENCDA.git
cd GENCDA
```

Dependencies are listed in requirements.txt, a virtual environment is advised:

```
python3 -m venv ./venv # optional but recommended
pip install -r requirements.txt
```

### Installing PyFIM

The `pyfim` package (Christian Borgelt's Frequent Item Set Mining) is required but **not available via pip for Python 3.9+** (the PyPI wheels only cover Python ≤3.7).

**Option A — conda-forge (recommended):**
```bash
conda install conda-forge::pyfim
```

**Option B — Build from source:**
```bash
# Requires gcc and python3-dev (Debian/Ubuntu: sudo apt install python3-dev build-essential)
pip install git+https://github.com/csinva/pyfim-clone
```

**Option C — Manual download:**
Download the shared object for your Python version from https://borgelt.net/pyfim.html and place it on your `PYTHONPATH`.

# Citing this work

```
@inproceedings{cinquini2021boosting,
  title={Boosting synthetic data generation with effective nonlinear causal discovery},
  author={Cinquini, Martina and Giannotti, Fosca and Guidotti, Riccardo},
  booktitle={2021 IEEE Third International Conference on Cognitive Machine Intelligence (CogMI)},
  pages={54--63},
  year={2021},
  organization={IEEE}
}
```



