# PAGE UNDER CONSTRUCTION 

# 2015 Unidata Users Workshop

[Complete information on the 2015 Unidata Users Workshop](http://www.unidata.ucar.edu/events/2015UsersWorkshop/)

## Python Instructions

A number of demonstrations will make use of the Jupyter Project (formerly
IPython Notebook) technology. For participants who wish to use Python during the
workshop, please follow the instructions below. To save time, we suggest
following these steps before your arrival at the workshop.

1. [Install Miniconda (Python 2.7) from Continuum Analytics](http://conda.pydata.org/miniconda.html). ([Determine if your OS 32 or 64 bit](http://www.akaipro.com/kb/article/1616#os_32_or_64_bit).)
2. Once Miniconda is installed, from the command line (e.g., OS X terminal, cmd.exe), run these instructions:

```
conda create -n workshop-xray python=2 pip numpy scipy matplotlib ipython-notebook pandas netcdf4 dask xray
conda create -n workshop-scikit python=2 pip numpy scipy matplotlib pandas ipython-notebook netcdf4 scikit-learn scikit-image basemap
conda create -n workshop-metpy python=2 pip numpy scipy matplotlib ipython-notebook netcdf4
source activate workshop-metpy && pip install metpy siphon
```

### From a Unix command line (e.g., OS X terminal)

To activate or switch to a conda environment, you can `source activate
<environment>`. For example,

```
source activate workshop-xray
```

### From a Windows command line (e.g., cmd.exe)

To activate or switch to a conda environment, you can `activate
<environment>`. For example,

```
activate workshop-xray
```

### jupyter notebook

The presenters will probably ask you to run examples in the `ipython notebook`.
You may wish to create a folder on your desktop, and from the command line `cd`
to that folder, `activate` (see above) an environment, and start the notebook
with the `ipython notebook` command. Once this software is in place, Unidata
Users Workshop staff and presenters will instruct participants how to make use
of this software.

#### inline graphics

You will probably be doing matplotlib visualizations in which case you will want
to inline the graphics with this command:

```
%matplotlib inline
```

### 2015 Unidata Users Workshop Github Repository

Presenters, participants and staff are encouraged to make use of this github
repository for sharing of presentations and any material relevant to the Users
Workshop.

### Questions

If you have questions about these instructions, please contact
<mailto:support@unidata.ucar.edu>.
