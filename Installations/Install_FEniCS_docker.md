# Install FEniCS

You can find multiple ways in the [FEniCS website](https://fenicsproject.org/download/)

Here I share the 'docker' way with MacBook. 

## 1. Download and install [docker](https://www.docker.com/products/docker-desktop)

(Play with docker: you can enter 'docker' in terminal and you will find all commands that you can try.
Some commands are useful, such as 'ps -a', 'rm', 'images', 'start', 'stop'.)


## 2. Install FEniCS in docker
The fenics website provided a code to install fencis.
```
docker run --name fenics -ti -p 127.0.0.1:8000:8000 -p 127.0.0.1:8888:8888 -v $(pwd):/home/fenics/shared -w /home/fenics quay.io/fenicsproject/stable:current
```
This is a standard way to install FEniCS, and you can execute your python files easily. 

Explaination:
* `docker run` 
it means you want to build a container.

* `--name fenics` 
it means the name of the container is fenics. Of course you can use other names as you like.

* `-p 127.0.0.1:8000:8000` 
publish a container's port to the host. 
`127.0.0.1:8000` is your (host) port. `8000` is the container's port.
When python plot something in the container, it will send the figure to its port `8000`, then you can view it in your browser with URL `127.0.0.1:8000`.

* `-p 127.0.0.1:8888:8888`
publish a container's port to the host. 
`127.0.0.1:8888` is your (host) port. `8888` is the container's port, which is for Jupyter Notebook.

* `-v $(pwd):/home/fenics/shared` 
it mirrors you files in the `$(pwd)` to the directory `/home/fenics/shared`. 
It allows you to open local files in the container, in case when you want to have some external files run in the container. 
Here `$(pwd)` is your current path. You can change it with command `cd` before you create the container. 
Here `/home/fenics/shared` is a directory in the container.

* `-w /home/fenics`
it means the working directory (the directory when enter the container and when you open jupyter) is `/home/fenics`. 

* `quay.io/fenicsproject/stable:current`
this is the image they provided online. 
If you want to install some previous version, you can find the tag in [their website](quay.io/fenicsproject/) 
and use it by, e.g., `quay.io/fenicsproject/stable:2017.2.0`.
The current version is `2019.1.0`. 
I think it's better to specify the version because when they update, we may forget what version we have.

### 2.1 Use FEniCS: Enter the container
When you create the container, you will enter it. 
You can use `pwd` and `ls` to check where you are. 

You can exit the container by `exit` or `Ctrl+D`. It will stop the container.

You can restart the container by `docker start fenics`. 
The container will be started but you are not in yet. 
You can enter the container by `docker attach fenics`. 
If nothing shows, press the `space` key and it may show.

### 2.2 Execute python files
An example is enough. 
In the container.
```
cd ~/demo/documented/poisson/python/
python3 demo_poisson.py
```

### 2.3 Edit python files
A basic way is to open python3 by 
```
python3
```
Remark: The current version of FEniCS only support `python3`, not `python`.

You can also open a Jupyter Notebook
```
jupyter notebook --ip=0.0.0.0 
```
Then we can open Jupyter Notebook with the url shown in the terminal.

QUESTION: Can we use other IDEs?

## 2' Install FEniCS together with Jupyter Notebook
Another way is recommended.
```
docker run --name fenics-nb -d -p 127.0.0.1:8888:8888 -v $(pwd):/home/fenics/shared -w /home/fenics quay.io/fenicsproject/stable:current  'jupyter-notebook --ip=0.0.0.0'
```
It is convenient if you only want to use Jupyter Notebook, and don't want to set the port of jupyter every time.
To use it, just start the container and go to the url `127.0.0.1:8888` in your browser.

Explaination:
* `-d` 
it means the container will run background.

* `'jupyter-notebook --ip=0.0.0.0'` this is to run the code inside quotes. So it will open a jupyter-notebook.


### 2'.1 Open FEniCS in Jupyter Notebook.
To open the Jupyter Notebook we use:  
```
docker logs fenics  
```
Then you can find, at the bottom, the link and token you can use to open in a browser.


## 3. Install hippylib
[Here](https://hippylib.github.io/documentation/) is a documentation of hippylib.

### 3.1 Fastest: Tom's container
This is a built container which include FEniCS and hippylib. 
The version is `hIPPYlib 2.3.0` and `FEniCS 2017.2.0`.
Just use this in the terminal.
```
docker run --name hippylib2017 -ti -p 127.0.0.1:8000:8000 -p 127.0.0.1:8888:8888 -v $(pwd):/home/fenics/shared -w /home/fenics hippylib/toms
```
and we are all set. It support both `python` and `python3`. 

### 3.2 Current Version
In a FEniCS 2019.1.0.r3 container, we can install hippylib by 
```
pip install hippylib --user
```

### 3.3 Move files manually
In Tom's container, we can see an folder named hippylib, where there tutorials and scripts of the argorithms. 
However when we install hippylib by `pip`, we cannot see this folder.
We can add it to the container manually.

1. Download the latest version [hippylib package](https://hippylib.github.io/download/)

2. Unzip it, and rename the folder as 'hippylib'.

3. Copy the folder to the container with the `docker cp` command. First use `cd` to set `pwd` to the directory where hippylib lies. Then
```
docker cp $(pwd)/hippylib fenics:/home/fenics
```

It copies the folder `hippylib` into the container `fenics`, under the folder `/home/fenics`.

You can find explainations [here](https://docs.docker.com/engine/reference/commandline/cp/)

4. If you want to use the scripts there, remember to include following codes to add hippylib to the path
```python
# To use scripts in hippylib folder
import sys
import os
HIPPYLIB_BASE_DIR = "/home/fenics/hippylib"
sys.path.append( HIPPYLIB_BASE_DIR )
from hippylib import *
```
