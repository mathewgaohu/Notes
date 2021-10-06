# a clean conda environment with common packages and good jupyter notebook extensions. 
```
conda create -n nb -c conda-forge matplotlib numpy scipy pandas jupyterlab jupyter_contrib_nbextensions 
conda activate nb
conda config --env --add channels conda-forge
```
