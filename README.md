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
- Easy!
- Now we can install the jupyter notebook and ipykernel packages
```
#pipenv install jupyter notebook ipykernel
```