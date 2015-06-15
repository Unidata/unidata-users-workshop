# PAGE UNDER CONSTRUCTION 

# 2015 Unidata Users Workshop

[Complete information on the 2015 Unidata Users Workshop](http://www.unidata.ucar.edu/events/2015UsersWorkshop/)

## Python Instructions

A number of demonstrations will make use of the Jupyter Project (formerly
IPython Notebook) technology. For participants who wish to use Python during the
workshop, please follow the instructions below. To save time, we suggest
following these steps before your arrival at the workshop.

1. [Install Miniconda from Continuum Analytics](http://conda.pydata.org/miniconda.html)
2. Once Miniconda is installed, from the command prompt, run these instructions:

```
conda create -n workshop-xray python=2 pip numpy scipy matplotlib ipython-notebook pandas netcdf4 dask xray
conda create -n workshop-scikit python=2 pip numpy scipy matplotlib pandas ipython-notebook netcdf4 scikit-learn scikit-image basemap
```

To activate or switch to a conda environment, you can `source activate
<environment>`. For example,

```
source activate workshop-xray
```

If you have questions about these instructions, please contact
<mailto:support@unidata.ucar.edu>.

Once this software is in place, Unidata Users Workshop staff and presenters will
instruct participants how to make use of this software.

## 2015 Unidata Users Workshop Github Repository

Presenters, participants and staff are encouraged to make use of this github
repository for sharing of presentations and any material relevant to the Users
Workshop.
