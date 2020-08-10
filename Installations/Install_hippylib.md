First install the FEniCS.

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
