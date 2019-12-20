# aas_workshop_2020_winter
Workshop resources for winter AAS meeting 2020

# Configuring Python Environment
These directions walk through installing miniconda, a lightweight distribution of the python package installer conda, and then creating a custom environment for the NAVO workshop. If you already have a conda distribution installed skip to section 2. If you have python installed, but not conda, and do not wish to install conda, skip to section 3. (Everyone else can skip section 3).
## Section 1: Installing miniconda
### Command­-line instructions for Mac and Linux
First, download the appropriate installation script by running the following commands **in a bash shell**:

**Mac**

    wget --no-check-certificate https://repo.continuum.io/miniconda/Miniconda3-latest-MacOSX-x86_64.sh -O conda_latest.sh

**Linux**

    wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O conda_latest.sh

To install miniconda globally, run the following commands (this assumes you have permission to install in system directories):

    bash conda_latest.sh
    rm conda_latest.sh

To install miniconda locally, run the following commands in the directory you wish to install it in (no special permissions are required for this method):

    bash conda_latest.sh -b -p $PWD/conda
    rm conda_latest.sh
    export PATH=$PWD/conda/bin:$PATH

*If you want to add conda to your path permanently you will need to add the export PATH line to your ~/.profile or ~/.bashrc file (with $PWD replaced by the actual path to your conda installation).
### Instructions for Windows
* Download a Python 3.6 installer:
  * https://repo.continuum.io/miniconda/Miniconda3-latest-Windows-x86_64.exe (64-bit)
  * https://repo.continuum.io/miniconda/Miniconda3-latest-Windows-x86.exe (32-bit)
* Double click the .exe files and follow the instructions on the screen.
* To access conda and Python you will use the "Anaconda Prompt" which you can find by opening the start menu and searching.

## Section 2. Install the workshop environment
Within a suitable Python environment such as one installed in Section 1, 
Python code and notebooks at the top level can easily import and run the utility code.  This is the recommended way to set up such an environment:
```
conda env create -f environment.yml
conda activate navo-workshop
```

# Updating development versions
The environment may include some development versions. To update to the latest:
```
conda env update --file environment.yml --prune
```

# Starting Jupyterlab
From the directory containing the notebooks:
```
jupyter lab
```

# Demo in Binder
This badge opens Jupyterlab session on Binder which can be used to run the workshop notebooks.
Note that the session will disapper after being left unattended for several minutes.

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/NASA-NAVO/aas_workshop_2020_winter/master?urlpath=lab)
