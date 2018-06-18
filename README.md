# 2018 Unidata Users Workshop Computing Environment

[Complete information on the 2018 Unidata Users Workshop](http://www.unidata.ucar.edu/events/2018UsersWorkshop/)

## Installing git and Python

A number of demonstrations and hands-on exercises will make use of tools written in the
Python programming language. If you want to follow along with these segments during the
workshop, you can install a Python environment on your laptop by following the instructions below. We suggest installing the Python environment before you arrive at the workshop, but there will
be time to ask questions about configuration during the first session on Monday morning.

1. [Install Miniconda (Python 3.6)](https://conda.io/miniconda.html). We'll be using the conda package manager to install dependencies, so consider installing a conda-based Python for the workshop even if you have a different version installed already. If you have trouble installing Miniconda, you might find [this video](https://www.youtube.com/watch?v=-fOfyHYpKck) useful.
1. Install the [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) distributed version control system software. (We will be using git and GitHub to distribute code.)
1. Once git and Miniconda are installed, from the command line (e.g., OS X terminal, or cmd.exe on Windows), run these instructions:

```
git clone https://github.com/Unidata/unidata-users-workshop

cd unidata-users-workshop

conda env create -f environment.yml
```

Note that the `conda env create` command installs numerous dependencies and may take a while to complete. If you're interested in learning more about Conda environments, try [this video](https://www.youtube.com/watch?v=15DNH25UCi0).

### From a Unix command line (e.g., OS X terminal)

If your default shell is NOT bash, first type `bash`. To activate or
switch to a conda environment, you can `source activate <environment>`.
For example,

```shell
source activate users-workshop
```

To switch and/or deactivate environments:

```shell
source deactivate
source activate <environment>
```

### From a Windows command line (e.g., `cmd.exe`)

To activate or switch to a conda environment, you can `activate <environment>`.
For example,

```shell
activate users-workshop
```

To switch and/or deactivate environments:

```shell
deactivate
activate <environment>
```

## Updating the Workshop Environment

If we need to update the Python package dependencies during the workshop, change to the `unidata-users-workshop` directory and do the following:

```shell
deactivate users-workshop             # Windows systems
   or
source deactivate users-workshop      # Unix-like systems

git pull origin master                # update the local files from the workshop repository

conda env update -f environment.yml   # update the Python environment
```

Updating the environment after the initial creation *should* be fairly speedy.

## Other Resources

If you're new to using Python, you might find some of the resources available in
Unidata's [Online Python Training](http://unidata.github.io/online-python-training/)
pages useful.

Similarly, the materials for the Unidata
[Python Training Workshops](https://unidata.github.io/unidata-python-workshop/) we run
at the Unidata Program Center and various university sites may help you get started.
