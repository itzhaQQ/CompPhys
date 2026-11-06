To create the conda environment with the used packages:
`conda env create -f environment.yml`
The environment will be called 'physics' and can be activated in VSCode or in the Terminal with
`conda activate physics`
New packages can be installed via conda with
`conda install -n physics package-name `
or if the package isnt available through conda
`python -m pip install package-name`
