This tutorial allows you to complete the first steps with Icepack.
[**This link**](https://cice-consortium-icepack.readthedocs.io/en/main/appendices/tutorial.html) sends you to an extensive guide for installing and running Icepack on you machine provided by the CICE Consortium.
Following, you can find summarized the significant steps. If something is not clear, please have a look to the guide.

### The first steps with Icepack

- Clone the github directory from https://github.com/CICE-Consortium/Icepack
- Create a conda environment from the .yml file provided in ~/Icepack/configuration/scripts/machines/environment.yml
- Create a case of study by running
      ./icepack.setup --case test0 --mach conda --env linux
- A folder with the name of your test is created in ~/Icepack/. The environmental variables are included in icepack.setting and icepack_in contains the Icepack namelist. In the first file, define the folder where you want to run Icepack through the variable ICE_RUNDIR.
- Compilation of Icepack is achieved by running ./icepack_build in the case directory, and ./icepack_submit runs the models.
- We need forcing data to run an example of Icepack, we take the input files from the repository https://github.com/CICE-Consortium/Icepack/wiki/Icepack-Input-Data. The commands for doing that are wget --no-check-certificate "https://zenodo.org/record/3728287/files/Icepack_data-20200326.tar.gz?download=1" -O Icepack_data-20200326.tar.gz and tar -xvzf Icepack_data-20200326.tar.gz, the latter unzip the downloaded folder.
- After download, modify the icepack.settings file to correct the input data folder and run ./icepack_submit. If Icepack runs, you can check the results in the testcase directory.

### Running Icepack with ERA5 forcing and getting results in NetCDF files
- To exploit the features of NetCDF files we can follow [**this subsection of the documentation**](https://cice-consortium-icepack.readthedocs.io/en/main/user_guide/ug_implementation.html#history-files). The straightforward way to complete this task is to create a new test case with the settings histcdf,ionetcdf. For example, ./icepack.setup --case test_nc --mach conda --env linux -s histcdf,ionetcdf. Then, compile the model with ./icepack_build.
- Download the folder with ERA5 input data from the github directory of this tutorial
- Change the icepack_in namelist acoording to the data you want to use and run the code. In particular, the year and the features of atmospheric forcing.
- Check the results, cheers


<br>
<br>
<br>
<br>
This tutorial is founded by<br>
<br>
<img src="https://www.imt-atlantique.fr/sites/default/files/styles/w292noagrandissement/public/projetderecherche/Edito%20Model-Lab.png?itok=ClyZaNrX" width="300">
Grant agreement No 101093293
<br>
<br>
<br>
<br>

<img src="https://s3.amazonaws.com/resumator/customer_20200915130155_8HA19PA6VHIGHXM4/logos/20201001134925_CMCCorizzontaleCOLORE_BLU.png" width="200">

