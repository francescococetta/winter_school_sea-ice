There is a [**detailed tutorial**](https://cice-consortium-icepack.readthedocs.io/en/main/appendices/tutorial.html) for a basic Icepack installation provided by the CICE Consortium. I recommend you follow that guide and try to have your first Icepack simulation running on your machine.

Following, I summarize the essential steps:

- clone the github directory from https://github.com/CICE-Consortium/Icepack
- create a conda environment from the .yml file provided in ~/Icepack/configuration/scripts/machines/environment.yml
- create a case of study by running
      ./icepack.setup --case test0 --mach conda --env linux
- A folder with the name of your test is created in ~/Icepack/. The environmental variables are included in icepack.setting and icepack_in contains the Icepack namelist. In the first file, define the folder where you want to run Icepack through the variable ICE_RUNDIR.
- Compilation of Icepack is achieved by running ./icepack_build in the case directory, and ./icepack_submit runs the models.
- We need forcing data to run an example of Icepack, we take the input files from the repository https://github.com/CICE-Consortium/Icepack/wiki/Icepack-Input-Data. The commands for doing that are wget --no-check-certificate "https://zenodo.org/record/3728287/files/Icepack_data-20200326.tar.gz?download=1" -O Icepack_data-20200326.tar.gz and tar -xvzf Icepack_data-20200326.tar.gz, the latter unzip the downloaded folder.
- After download, modify the icepack.settings file to correct the input data folder and run ./icepack_submit. If Icepack runs, you can check the results in the testcase directory.
