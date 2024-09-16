# notebook-pipenv
An example setup of a project with a Pipfile / Pipenv managed jupyter notebook kernel.
1. Pipenv : https://github.com/pypa/pipenv :  This system manages pip requirements, virtual environments, python versions and has a dependency solver and locking.
2. Jupyter notebook - we all know and love
3. Ipython Kernel - a package which lets jupyter notebook operate inside a given virtual environment as the jupyter kernel.

##Supporting cast:
pyenv -> tracks and installs python versions, is used by pipenv for enforcing python version for the environment.


# Installation steps:
1. setup pyenv and pipenv for your machine.
2. initialize pipenv inside the project directory
```
#pipenv install
Creating a virtualenv for this project...
Pipfile: /Users/rybczym/PycharmProjects/test-notebook-pipenv/Pipfile
Using default python from /Users/rybczym/.local/pipx/venvs/pipenv/bin/python (3.9.18) to create virtualenv...
...
```
- this will initialize an empty Pipfile with your default python version, check that it is what was intended.
```
#cat Pipfile
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]

[dev-packages]

[requires]
python_version = "3.9"
```

- WHOOPS!   I had python 3.9 as the default, but really we want 3.11.  Let's fix that.
```
#pipenv --rm # remove the wrong virtual environment
## edit the Pipfile, change python_version to 3.11, rerun pipenv install
#pipenv install 
python --version
Python 3.9
# whoops!  We're still in system env, we need to be INSIDE the pipenv shell environment
pipenv shell
python --version
Python 3.11.9
```
- Easy!   We can add the waterAI private repo to the source section to install packages from there (like forecast library)
3. Now we can install the jupyter notebook and ipykernel packages
```
#pipenv install jupyter notebook ipykernel
Installing jupyter...
Resolving jupyter...
Added jupyter to Pipfile's [packages] ...
✔ Installation Succeeded
Added notebook to Pipfile's [packages] ...
✔ Installation Succeeded
Added ipykernel to Pipfile's [packages] ...
✔ Installation Succeeded
Pipfile.lock (51d3e4) out of date, updating to (361b8e)...
Locking [packages] dependencies...
✔ Success!
Locking [dev-packages] dependencies...
Updated Pipfile.lock (b46ed13dbda2e15ce5b3a7c3d3e47845334480f8e96a2cafeb02abc627361b8e)!
Installing dependencies from Pipfile.lock (361b8e)...
```
- this did a few things - each package was installed from the pypi repo, and their dependent packages, added to the virtual environment managed by this pipenv, and the Pipfile.lock was updated to the exact versions that were installed just NOW.  (they may change as new versions are released... hence the lock file)

4. Now we can setup jupyter to have a kernel available that is this virtual environment (managed by pipenv)
```
#python -m ipykernel install --user --name=test-notebook-pipenv
and let's run a notebook:
jupyter notebook
```
- this will open a browser window with the jupyter notebook interface, and you can create a new notebook, and select the kernel that was just installed.  This will ensure that the notebook is running in the virtual environment, and has access to the packages that were installed there.
- File -> New (select test-notebook-pipenv as the kernel for the new file)
'''
import numpy as np:
'''