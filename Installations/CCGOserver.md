# CCGO servers

First you need to ssh ccgo1.

## 0. Rules
* Create a directory under `/workspace`. Do not create any files or folders in the root directory.

## 1. To use conda
```
source /workspace/anaconda3/etc/profile.d/conda.sh
conda activate fenics
```

You can also put the source command in your `.bashrc` file so it runs automatically when you ssh in. First do
```
vim ~/.bashrc
```
this file indicates the commands that you want to run when you log in. So, add the `source` command here. You are all set. 

Even more you can add the `conda activate` command there. Then you will start will fenics environment when you log in .

## 2. To run faster
use following three commands in terminal
```
export OMP_NUM_THREADS=1
export OPENBLAS_NUM_THREADS=1
export OPENMP_NUM_THREADS=1
```
or, equivalently, following in python script.
```
import os
os.environ['OMP_NUM_THREADS'] = '1'
os.environ['OPENBLAS_NUM_THREADS'] = '1'
os.environ['OPENMP_NUM_THREADS'] = '1'
```
Don't know why. Just use it. 
