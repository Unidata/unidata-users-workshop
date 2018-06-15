# Before the Workshop

Planning on attending the workshop or going through this material on your own?
We recommend getting setup ahead of time to avoid any bandwidth issues at the
venue. In this short guide, we'll get your environment setup and running.

## Miniconda
We'll be using the conda package manager. So if you don't already have
Anaconda or Miniconda installed, that's the first step.

1. Head over to [https://conda.io/miniconda.html](https://conda.io/miniconda.html)
   and download the Python 3 installation for your operating system.
1. On Windows, run and follow the graphical installer. On Max/Linux, open a
   command prompt and run the command line installer:
   `bash Miniconda3-latest-MacOSX-x86_64.sh` (or whatever the filename of the
    script you downloaded is).
1. Restart your terminal on Mac/Linux.
1. Open a terminal on Mac/Linux or open the Anaconda Prompt on Windows.
1. Run `conda --version` and make sure that you are running at least conda
   4.5.X

If you're having issues, checkout the video tutorial below on installing conda.

<iframe width="560" height="315" src="https://www.youtube.com/embed/-fOfyHYpKck"
 frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

We'll also be using packages from the conda-forge channel. The environment file
will use that channel for us during installation, but you can add it to your
default channel list with `conda config --add channels conda-forge` in the
terminal (Mac/Linux) or Anaconda Prompt (Windows). To learn more about
conda forge, checkout the video below.

<iframe width="560" height="315" src="https://www.youtube.com/embed/G3AF-nhNyDk"
 frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Environment
We've created and environment that has the dependencies we'll use during this
tutorial. It's in the repository for the tutorial, so we'll need to clone that
repository, then setup the environment. You'll be setting up your own repository
during the tutorial, so no need to fork this one, we just need some of the
content.

1. Clone the repository or download the ZIP file. On Windows we recommend
   using git bash. On Mac ensure that XCode is installed for easy access to
   git. Linux users should install with their relevant package manager.
   [https://github.com/Unidata/unidata-users-workshop](https://github.com/Unidata/unidata-users-workshop)
1. Open a terminal (or Anaconda Prompt) and `cd` into the repository.
1. Create the environment with `conda env create` in the terminal/Anaconda
   prompt.
1. The instructions following installation completion tell you how to activate
   and deactivate the environment.

To learn more about conda environments, checkout the following video.
<iframe width="560" height="315" src="https://www.youtube.com/embed/15DNH25UCi0"
 frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Other Requirements
There are a just a couple of other things you'll want to do:
1. If you don't already have a GitHub account, sign up for one (free).
1. Make sure you are familiar with the git workflow. Checkout some of
   [these](https://try.github.io/) free resources.
