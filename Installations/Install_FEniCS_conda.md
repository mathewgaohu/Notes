# Install FEniCS

You can find multiple ways in the [FEniCS website](https://fenicsproject.org/download/)

Here I share the 'Anaconda' way with MacBook. Which can work with PyCharm.

## 1. Download and install [Anaconda](https://www.anaconda.com/products/individual)


## 2. Install FEniCS in Anaconda

Run in the terminal 
```
conda create -n fenicsproject -c conda-forge fenics
source activate fenicsproject
```


## 3. Use FEniCS

In the terminal, you can use 
```
conda activate fenicsproject
```
to open fenics, and use 
```
conda deactivate fenicsproject
```
to close it.

After activating fencisproject, you can use 
```
python
```
to open a python shell, or use 
```
jupyter notebook
```
to open Jupyter Notebook. (maybe need jupyter notebook installed in anaconda)


## 4. Install hippylib

After activating fencisproject, use
```
pip install hippylib
```
to install hippylib.

## Remark

I recommend using PyCharm which is better for debugging. 
First you need to install [PyCharm](https://www.jetbrains.com/pycharm/download/#section=mac). 
The free version is OK to go. 



