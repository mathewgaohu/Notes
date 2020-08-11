# Install FEniCS

You can find multiple ways in the [FEniCS website](https://fenicsproject.org/download/)

Here I share the 'docker' way with MacBook. 

## 1. Download and install [docker](https://www.docker.com/products/docker-desktop)

(Play with docker: you can enter 'docker' in terminal and you will find all commands that you can try.
Some commands are useful, such as 'ps -a', 'rm', 'images', 'start', 'stop'.)


## 2. Install FEniCS in docker

The fenics website provided a code to install fencis.

```
docker run -ti -p 127.0.0.1:8000:8000 -v $(pwd):/home/fenics/shared -w /home/fenics/shared quay.io/fenicsproject/stable:current
```

But I recommend a better one, and I will explain it.

```
docker run --name fenics -w /home -v $(pwd):/home/Local quay.io/fenicsproject/stable -d -p 127.0.0.1:8888:8888 'jupyter-notebook --ip=0.0.0.0'
```

Explaination:

(a) `docker run` it means you want to build a container.

(b) `--name fenics` it means the name of the container is fenics. Of course you can use other names as you like.

(c) `-w /home` it means the working directory (the directory when you open jupyter) is `/home`. 
I think it is better to set it as the root directory as I did, because then you can find all files in the container. 

(d) `-v $(pwd):/home/Local` it mirrors you files in the `$(pwd)` to the directory `/home/Local`. 
It allows you to open local files in the container, in case when you want to have some external files run in the container. 
Here `$(pwd)` is your current path. You can change it with command `cd` before you create the container. 
Here `/home/Local` wasn't there, so docker will create a folder named 'Local' in the directory `/home`.

(e) `quay.io/fenicsproject/stable` this is the image they provided online. 
If you want to install some previous version, you can find the tag in [their website](quay.io/fenicsproject/) and use it by e.g. `quay.io/fenicsproject/stable:2017.2.0`

(f) `-d` it means the container will run background.

(g) `-p 127.0.0.1:8888:8888` publish a container's port to the host. `127.0.0.1:8888` is your (host) port. `8888` is the container's port.

(h) `'jupyter-notebook --ip=0.0.0.0'` this is to run the code inside quotes. So it will run jupyter-notebook.


## 3. Open FEniCS in Jupyter Notebook.

To open the files we first enter in the terminal:  

```
docker logs fenics  
```

Then you can find, at the bottom, the link and token you can use to open in a browser.


## 4. Install hippylib

It is quite easy to install hippylib with FEniCS installed in docker.

1. Download the latest version [hippylib package](https://hippylib.github.io/download/)

2. Unzip it, and rename the folder as 'hippylib'.

3. Copy the folder to the container with the `docker cp` command. First use `cd` to set `pwd` to the directory where hippylib lies. Then

```
docker cp $(pwd)/hippylib /home/fenics
```

It copies the folder hippylib into under the folder fenics in the container.

You can find explainations [here](https://docs.docker.com/engine/reference/commandline/cp/)

4. When you run anything using hippylib, remember to include following codes to add hippylib to the path

```python
# To work with hippylib
import sys
import os
HIPPYLIB_BASE_DIR = "/home/fenics/hippylib"
sys.path.append( HIPPYLIB_BASE_DIR )
from hippylib import *
```
