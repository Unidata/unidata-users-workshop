# Goal

Showcase some of the ideas behind Big Weather Web (BWW). In particular:

  * Curated VM images that are "ready to go".
  * Dataset Management
  * Big Data infrastructure

# The Docker Image

This docker image contains:

  * miniconda
  * Sample NetCDF files
  * python packages [`xray`], [`dask`], [`netcdf4`] and its 
    dependencies.

# Prerequisites

 1. A working installation of Docker. We recommend 
    [`boot2docker`](http://boot2docker.io).

    **NOTE**: For windows users, we recommend using the provided CLI 
    (accessed by clicking on `Start -> Docker -> Boot2Docker Start`).

 2. Download the image that corresponds to our hands-on experience:

    ```bash
    docker pull ivotron/unidata2015uw
    ```

 3. Corroborate that we can instantiate containers that correspond to 
    this image.

    ```bash
    docker run -ti --rm ivotron/unidata2015uw
    ```

    A bash terminal should appear. Then type inside the terminal:

    ```bash
    conda list
    ```

    That should display something like the following:

    ```bash
    root@0c5b54cf5ff3:/# conda list
    # packages in environment at /opt/conda:
    #
    chest                     0.2.2                    py27_0
    conda                     3.13.0                   py27_0
    conda-env                 2.2.1                    py27_0
    curl                      7.38.0                        0
    dask                      0.5.0                np19py27_0
    dill                      0.2.2                    py27_0
    hdf5                      1.8.14                        0
    heapdict                  1.0.0                    py27_0
    libnetcdf                 4.3.2                         1
    libsodium                 0.4.5                         0
    netcdf4                   1.1.8                np19py27_0
    numpy                     1.9.2                    py27_0
    openssl                   1.0.1k                        1
    pandas                    0.16.1               np19py27_0
    pip                       7.0.3                    py27_0
    psutil                    2.2.1                    py27_0
    pycosat                   0.6.1                    py27_0
    python                    2.7.10                        0
    python-dateutil           2.4.2                    py27_0
    pytz                      2015.4                   py27_0
    pyyaml                    3.11                     py27_0
    pyzmq                     14.6.0                   py27_0
    readline                  6.2                           2
    requests                  2.7.0                    py27_0
    setuptools                17.0                     py27_0
    six                       1.9.0                    py27_0
    sqlite                    3.8.4.1                       1
    system                    5.8                           2
    tk                        8.5.18                        0
    toolz                     0.7.2                    py27_0
    xray                      0.5.0                np19py27_0
    yaml                      0.1.4                         0
    zeromq                    4.0.5                         0
    zlib                      1.2.8                         0
    ```

# Experience 1

We show how a curated docker image that contains all the necessary 
software/configuration allows climate scientists to get stuff done 
quickly. Also, we showcase the common cataloging methodology of BWW. 
In concrete, in this exercise we see how to obtain and combine two 
datasets that come from distinct servers.

## Steps

**NOTE**: the first part (steps 1-5) consists of proof-of-concept code 
that illustrates what a python package for the BWW project would 
offer. Our goal is to give users an idea of how it would work and to 
get feedback from them.

 1. Launch a container, change to root directory within the container 
    and then invoke the python terminal:

    ```bash
    docker run -ti --rm ivotron/unidata2015uw

    root@af:$ cd /root
    root@af:/root:$ python
    Python 2.7.10 |Continuum Analytics, Inc.| (default, May 28 2015, 17:02:03)
    [GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    Anaconda is brought to you by Continuum Analytics.
    Please check out: http://continuum.io/thanks and https://binstar.org
    >>>
    ```

    Once inside the python terminal, we first import the Big Weather 
    Web python module and connect to one of the central metadata 
    repositories:

    ```python
    import bww

    bww.connect()
    ```

 2. We then show the summary of the available datasets:

    ```python
    bww.summary()
    ```

 3. Show the available datasets:

    ```python
    bww.datasets()
    ```

 4. Get the URL of a dataset:

    ```python
    bww.get_url('cldc_mean')
    ```

 5. Using this info of where these datasets are located, we then open 
    each dataset using the 
    [`xray.open_dataset()`](xray.readthedocs.org/en/latest/generated/xray.open_dataset.html) 
    function:

    ```python
    import xray

    d1 = xray.open_dataset(cldc_url)
    d2 = xray.open_dataset(lflx_url)

    d1

    d2
    ```

 6. We then combine the two datasets and operate on the resulting 
    dataest.

    ```python
    c = xray.auto_combine([d1,d2])

    c

    c.cldc * c.lflx
    ```

    See the 
    [`auto_combine()`](xray.readthedocs.org/en/latest/generated/xray.auto_combine.html) 
    documentation for detailed info on how it operates.

<!--
    ```python
    # cldc_url = 'http://noaa_server/dap/data/nc/cldcdmean.nc?geogrid(cldc,62,206,56,210,"19722<time<19755")'
    # lflx_url = 'http://nasa_server/dap/data/nc/lflxmean.nc?geogrid(lflx,62,206,56,210,"19722<time<19755")'
    cldc_url = 'cldc.mean.nc'
    lflx_url = 'lflx.mean.nc'
    ```
-->

# Experience 2

One of the aspects of Big Weather Web (BWW) is the distributed dataset 
management characteristics, which take care of recording metadata 
about what datasets are available on all the distinct (BWW) sites, 
creating a unified catalog of weather data, while at the same time 
keeping track of the what datasets are replicated among sites of the 
BWW network. Having multiple copies of a dataset distributed in 
different sites not only helps ensure the reproducibility of published 
results but it also allows to optimize the execution of an analytic 
task. In this experience we exemplify the latter.

For this experience, we have multiple [NetCDF 
files](http://motherlode.ucar.edu/thredds/catalog/station/metar/catalog.html) 
that, for the purposes of the demonstration, reside locally inside the 
container. Every file corresponds to a chunk of the same dataset and, 
in practice, each chunk would reside on a distinct server (and would 
be orders of magnitude larger).

We first show that the container can't handle all the files on its 
own, due to imposed restrictions on the available memory. In other 
words, the container doesn't have enough memory to handle all the 
chunks of the dataset.

 1. We first launch a container with restricted memory:

    ```bash
    docker run -m="50m" --memory-swap="50m" -ti --rm ivotron/unidata2015uw
    ```

    The above creates a container with only 50 MB of RAM available to 
    it. This is just for illustration purposes.

 2. Inside the container, we then again change to the `/root` 
    directory, launch a python terminal and:

    ```python
    import xray

    d1 = xray.open_dataset('Surface_METAR_20150604_0000.nc')
    d2 = xray.open_dataset('Surface_METAR_20150605_0000.nc')
    ```

    we then want to combine the datasets as in Experience 1, to obtain 
    the mean value of a variable:

    ```python
    d = xray.auto_combine([d1,d2])

    d.air_temperature.mean()
    ```

    At the line where we combine, the container gets killed since it 
    violates the memory limits that we explicitly imposed on it. This 
    is the analogous of having to execute some computation on a single 
    server over a large dataset (by "large" we mean larger than the 
    available RAM). The analogy we make here is that one single site 
    can't handle large datasets, or if it does it does it 
    inefficiently. We can take advantage of the fact that BWW has 
    knowledge about multiple copies of the same dataset that reside in 
    multiple sites. Given this, we can execute the same computation in 
    a distributed fashion, taking advantage of the compute 
    capabilities of each site's backend.

 3. In order to illustrate the distributed execution of a computation, 
    we execute an out-of-core computation by (1) lazily loading each 
    chunk (file) into memory and (2) aggregating each chunk 
    independently. This is done via the [`xray`] and [`dask`] python 
    packages in particular the `open_mfdataset()` function.

    ```python
    import xray

    d = xray.open_mfdataset('Surface*.nc')

    d

    # the above loads a file in each chunk (50MB each)
    d.chunks

    # this executes an out-of-core max() function
    # in other words, goes chunk by chunk
    m = d.air_temperature.max()

    # the previous operation wasn't actually executed since they
    # are lazily evaluated. We show this by executing:
    m

    # getting the results triggers the actual execution
    m.values
    ```

    The BWW project will handle and optimize the distributed execution 
    of analytic tasks such as the one shown above.

[`xray`]: http://xray.readthedocs.org/en/latest/generated/xray.open_dataset.html
[`dask`]: https://github.com/ContinuumIO/dask
[`netcdf4`]: https://github.com/Unidata/netcdf4-python
