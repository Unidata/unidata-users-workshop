# 2018 Unidata Users Workshop

[Complete information on the 2018 Unidata Users Workshop](http://www.unidata.ucar.edu/events/2018UsersWorkshop/)

## Python Instructions

A number of demonstrations will make use of the Jupyter Project (formerly
IPython Notebook) technology. For participants who wish to use Python during the
workshop, please follow the instructions below. To save time, we suggest
following these steps before your arrival at the workshop.

1. [Install Miniconda (Python 3.6)](https://conda.io/miniconda.html).
2. Once Miniconda is installed, from the command line (e.g., OS X terminal, cmd.exe), run these instructions:

```
git clone https://github.com/Unidata/unidata-users-workshop

cd unidata-users-workshop

conda env create -f environment.yml
```

### From a Unix command line (e.g., OS X terminal)

If your default shell is NOT bash, first type `bash`. To activate or
switch to a conda environment, you can `source activate <environment>`.
For example,

```shell
source activate unidata-users-workshop
```

To switch and/or deactivate environments:

```shell
source deactivate
source activate <environment>
```

### From a Windows command line (e.g., cmd.exe)

To activate or switch to a conda environment, you can `activate <environment>`.
For example,

```shell
activate unidata-users-workshop
```

To switch and/or deactivate environments:

```shell
deactivate
activate <environment>
```
