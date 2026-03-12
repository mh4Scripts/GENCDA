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

Please note that in addition to the dependencies listed in the requirements file, you also need to install a novel version of "fim" package. You can find the package and installation instructions on the following webpage: https://borgelt.net/pyfim.html

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



