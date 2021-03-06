# Configuring the Workshop Environment
These directions walk through installing miniconda, a lightweight distribution of the python package installer conda, downloading the NAVO workshop material, then creating and testing the custom environment for the  workshop. 

This file:<br>https://github.com/NASA-NAVO/aas_workshop_2020_winter/blob/master/00_SETUP.md

## 0. Update Previously-Created Environments
If you followed these instructions prior to today, update the environment with the instruction in this step.  First time installers proceed to **Step 1**.

Within a `bash` shell (Mac and Linux), or Anaconda Prompt (Windows):
#### Get the Latest from Github

    % cd [wherever'git clone' was done]/aas_workshop_2020_winter
    % git pull

    # If that failed due to local changes, stash those changes and try again:
    % git stash
    % git pull
#### Install an updated PyVO package

    % conda activate navo-workshop  # Always remember to activate the environment!
    % pip install git+git://github.com/tomdonaldson/pyvo.git@increase_tap_timeout --upgrade
#### Skip the Installation Steps
The environment should be ready.  Skip to **Step 6** to check the environment and start Jupyter Lab.

## 1. Install Miniconda (if needed)

*Miniconda is a free minimal installer for conda. It is a small, bootstrap
version of Anaconda that includes only conda, Python, the packages they depend
on, and a small number of other useful packages, including pip, zlib and a few
others. Note, though, that if you have either Miniconda or the full Anaconda
already installed, you can skip to the next step.*

Check if Miniconda is already installed.

    % conda info

If Miniconda is not already installed, follow these instructions for your
operating system: https://docs.conda.io/en/latest/miniconda.html

On Windows, you might also need
[additional compilers](https://github.com/conda/conda-build/wiki/Windows-Compilers).

## 2. Open the conda command prompt

*Miniconda includes an environment manager called conda. Environments
allow you to have multiple sets of Python packages installed at the same
time, making reproducibility and upgrades easier. You can create,
export, list, remove, and update environments that have different versions of
Python and/or packages installed in them. For this workshop, we will configure the environment using the conda command prompt.*

On Mac or Linux, the `bash` shell will handle the conda commands.  Open your terminal and verify your shell environment:

    % echo $SHELL

If the output text does not contain `bash`, switch to the bash shell before
being able to run anything related to conda.

On Windows, open the `Anaconda Prompt` terminal app.

## 3. Install git (if needed)

At the prompt opened in the previous step, enter this command to see whether git is already installed and accessible to this shell:

    % git --version

If the output shows a git version, proceed to the next step.  Otherwise install git by entering the following command and following the prompts:

    % conda install git

## 4. Clone This Repository

Download the workshop folder using
[git](https://help.github.com/articles/set-up-git/):

    % git clone https://github.com/NASA-NAVO/aas_workshop_2020_winter.git

## 5. Create a conda environment for the workshop

*For this workshop, the python version and all needed packages are listed in the
[environment.yml](https://github.com/NASA-NAVO/aas_workshop_2020_winter/blob/master/environment.yml) file.*

Navigate to the workshop directory in the terminal. For example, if you installed
the navo-workshop directory in your home directory, you could type the
following:

    % cd aas_workshop_2020_winter

And finally, on any platform, to install and activate the aas_workshop_2020_winter
environment, type:

    % conda env create -n navo-workshop --file environment.yml
    % conda activate navo-workshop

## 6. Check Installation

The name of the new conda environment created above should be displayed next
to the terminal prompt:

    (navo-workshop) %

Run the `check_env.py` script to check the Python environment and some of the
required dependencies:

    (navo-workshop) % python check_env.py

## 7. Starting Jupyterlab
From the directory containing the notebooks:

    (navo-workshop) % jupyter lab

## Additional Resources

- [Set up git](https://help.github.com/articles/set-up-git/)
- [Conda Users Guide](https://docs.conda.io/projects/conda/en/latest/user-guide/)
