This tutorial allows you to complete the first steps with Icepack.
[**This link**](https://cice-consortium-icepack.readthedocs.io/en/main/appendices/tutorial.html) sends you to an extensive guide for installing and running Icepack on you machine provided by the CICE Consortium.
Following, you can find summarized the significant steps. If something is not clear, please have a look at the guide.


### Step 0: configuring Git and conda

Icepack will be installed through Git, therefore it is important that you have a running GitHub account and that you know its basic functionalities. If not, please follow [**this Git workflow guide**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guide) provided by the CICE consortium. Large amount of information is provided on how to interact with the main code of Icepack; some of it is useful in the context of this project, other goes beyond the scope of this tutorial. I recommend reading them to familiarize yourself with the basic terminology, and to appreciate the complexity of running and maintaining a large geophysical model. The workflow guide is oriented toward setting up CICE rather than Icepack, but the same workflow applies to Icepack standalone.

You also need conda. If you are lucky, conda is already installed in your system, either through Anaconda or Miniconda. Miniconda is a minimal installation of Anaconda, which will be enough for the scope of our project. Check if you have conda installed in your system by typing "conda".
If conda is not installed, and you are on a cluster or HPC system try module load anaconda or module avail to see if there is a conda installation available for you. If conda is still not installed, you can easily install miniconda on your platform of choice (Windows, Linux, Mac) by following [**this guide**](https://cice-consortium-icepack.readthedocs.io/en/main/user_guide/ug_running.html#porting-to-laptop-or-personal-computers). You might need to restart your shell after installing conda.


### The first steps with Icepack: creating a case stuy

- Clone the github directory from **https://github.com/CICE-Consortium/Icepack**, check step 0.
- Enter the Icepack directory, create and activate your conda environment from the .yml file provided in ~/configuration/scripts/machines/environment.yml by using the command
```
conda env create -f environment.yml
conda activate icepack
```
- If you work on linux cluster, create a case of study by running
```
./icepack.setup --case test0 --mach conda --env linux
```
  If you work on a different machine, please check the environment that suits it better in ~/configuration/scripts/machines/.
- A folder with the name of your test (test0 in this example) is created in the Icepack folder. The environmental variables are included in icepack.setting and icepack_in contains the Icepack namelist. In icepack.settings, define the folder where Icepack runs by using the variable **ICE_RUNDIR**, you will check the results of simulations there.


### Compiling and running Icepack

- Compilation of Icepack is achieved by running ./icepack_build in the case directory.
- We need forcing data to run an example of Icepack, we take the input files from the repository **https://github.com/CICE-Consortium/Icepack/wiki/Icepack-Input-Data** where you can also find their description. You can either download them from your browser or by the terminal commands
```
wget --no-check-certificate "https://zenodo.org/record/3728287/files/Icepack_data-20200326.tar.gz?download=1" -O Icepack_data-20200326.tar.gz
tar -xvzf Icepack_data-20200326.tar.gz
```
If you work from terminal, I suggest you to download the forcing data to a different directory.
- After download, go back to the testcase folder where you have compiled the model (~/Icepack/test0). Now, modify the variable *data_dir* in icepack_in file to correct the location of input data. By default, oceanic data from SHEBA expedition are selected by variable *ocn_data_type*.
- Everything is set for running the simulation. Run ./icepack.submit and, if icepack completes successfully, you can check the results in the **ICE_RUNDIR** directory.


### Built-in visualization tool

- The Icepack scripts include a script (timeseries.csh) that will generate a timeseries figure from the diagnostic output file. You can find it in the directory ~/Icepack/configuration/scripts/tests. Copy the file to your running directory.
- Run the script followed by the diagnostic output file as
```
./timeseries.csh ice_diag.full_ITD
```
A set of .png figures are created in the same directory.
- The plotting script can be run on any of the output files (icefree, slab, full_ITD, land). To generate the figures, run the timeseries.csh script as previously passing the full path to the ice_diag file as an argument.


### Bonus track: running Icepack with ERA5 forcing and getting results in NetCDF files

- To exploit the features of NetCDF files we can follow [**this subsection of the documentation**](https://cice-consortium-icepack.readthedocs.io/en/main/user_guide/ug_implementation.html#history-files). The straightforward way to complete this task is to create a new test case with the following setttings in the cloned Icepack directory as
```
./icepack.setup --case test_nc --mach conda --env linux -s histcdf,ionetcdf
```
- Aferwards, compile the model with ./icepack.build in the testcase directory. Once the compilation is successfull, download the folder with ERA5 input data from the [**main directory**](https://github.com/francescococetta/winter_school_sea-ice/tree/main/era5_forcing) of this tutorial.
- In the testcase folder, change the icepack_in namelist acoording to the input idata you want to use. In particular, the year and the features of atmospheric forcing. Ocean is still from SHEBA campaign.
- Then, submit the simulation and check the results stored in /history folder.
