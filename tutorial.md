There is a [**detailed tutorial**](https://cice-consortium-icepack.readthedocs.io/en/main/appendices/tutorial.html) for a basic Icepack installation provided by the CICE Consortium. I recommend you follow that guide and try to have your first Icepack simulation running on your machine.

Following, I summarize the essential steps:

- clone the github directory from https://github.com/CICE-Consortium/Icepack
- create a conda environment from the .yml file provided in ~/Icepack/configuration/scripts/machines/environment.yml
- create a case of study by running
      ./icepack.setup --case test0 --mach conda --env macos
- A folder with the name of your test is created in ~/Icepack/; icepack_in is the file containing the icepack namelist
