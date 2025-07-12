<!-- Header: -->
<div align="center"> 
  <a href="https://anaconda.org/">
    <img align="center" src="https://anaconda.org/static/img/anaconda-symbol.svg" alt="conda" height="200" />
  </a>
  <h1> Conda Essentials </h1>
</div>

<h3 align="center"> 
  For more information, resort to the 
  <a href="https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf"> 
    Conda Cheat Sheet. 
  </a>
</h3> 
<br />

# Table of Contents

- [Installing Anaconda](#installing-anaconda)
- [Managing Conda Environments](#managing-conda-environments)
  - [Creating an Environment](#creating-an-environment)
  - [Removing an Environment](#removing-an-environment)
  - [Activating & Deactivating](#activating--deactivating)
- [Managing Packages](#managing-packages)
  - [Installing Packages](#installing-packages)
  - [Updating Packages](#updating-packages)
- [Listing Information](#listing-information)
- [Reverting, Cloning, and Exporting](#reverting-cloning-and-exporting)

# Installing Anaconda

> **Note:** text enclosed in `< >` (angle brackets) represents placeholders that should be replaced with actual values.

1. Download [Anaconda](https://www.anaconda.com/products/individual).

2. Open a terminal, navigate to the downloaded file, and grant execute permission (for [Unix-like users](../linux_essentials/README.md)): 

```bash
cd <dir_pathname> && chmod +x <filename>.sh
```

3. Run the installer (Ubuntu example):

```bash
./<filename>.sh
```  

Example installation command (check the [latest version](https://docs.anaconda.com/anaconda/install/hashes/lin-3-64/)):
```bash
cd ~/Downloads && chmod +x Anaconda3-2022.10-Linux-x86_64.sh && ./Anaconda3-2022.10-Linux-x86_64.sh
```

4. Update Conda:

```sh
conda update -yn base conda
```

<!--- ############################################################################################################################################### -->

# Managing Conda Environments

## Creating an Environment

- Create a new environment with an exact Python version (e.g., V3.13.2):

```sh
conda create -yn <env_name> python==3.13.5
```

- Add `conda-forge` as a default channel:

```sh
conda config --add channels conda-forge
```

- Create an environment from an `environment.yml` file:

```sh
conda env create -f environment.yml
```

- Create an environment from a spec file:

```sh
conda create -n <env_name> --file <filename>.txt
```

## Removing an Environment

```sh
conda env remove -n <env_name>
```
or (alternative due to issue [#3215](https://github.com/conda/conda/issues/3215))
```sh
conda remove -yn <env_name> --all
```

## Activating & Deactivating

- Activate an environment:

```sh
conda activate <env_name>
```

- Deactivate the current environment:

```sh
conda deactivate
```

<!--- ############################################################################################################################################### -->

# Managing Packages

## Installing Packages

- Install multiple packages with exact versions in a specific environment:
  
```sh
conda install -yn <env_name> <package1>==<version> <package2>==<version>
```
Note: Conda will install the latest available version if the version is not specified.

- Install a package from a different channel:
  
```sh
conda install -c <channel_name> <package_name>
```

## Updating Packages 

- Update a package in the active environment:

```sh
conda update <package_name>
```

- Update a package in a specific environment:

```sh
conda update -n <env_name> <package_name>
```

- Update the environment after modifying the environment.yml file:

```sh
conda env update -n <env_name> --file environment.yml --prune
```
or (shorthand)
```sh
conda env update -f environment.yml --prune
```

<!--- ############################################################################################################################################### -->

# Listing Information

- List available environments:

```sh
conda env list
```
or
```sh
conda info -e
```

- List configured channels:
  
```sh
conda config --show channels
```

- List package dependencies in an environment:

```sh
conda list -n <env_name>
```

- Check a specific package in an environment:

```sh
conda list -n <env_name> <package_name>
```

- Show details about the current environment:

```sh
conda info
```

- List a specific package in the current environment:

```sh
conda list <package_name>
```

- Show revision history of the current environment:

```sh
conda list --revisions
```

- Show environment directories:
  
```sh
conda config --show envs_dirs
```

<!--- ############################################################################################################################################### -->

# Reverting, Cloning, and Exporting

- Revert to a previous revision:

```sh
conda install --revision <revision_number>
```

- Clone an existing environment:

```sh
conda create -n <new_env_name> --clone <existing_env_name>
```

- Create a spec file with all dependencies:

```sh
conda list -n <env_name> > spec_list.txt
```
or (if the env. is activated)
```sh
conda list > spec_list.txt
```
or (for a spec file containing the URLs of the package dependencies)
```sh
conda list -n <env_name> --explicit > spec_list.txt
```

- Export an environment to a .yml file for [sharing](https://conda.io/projects/conda/en/latest/user-guide/concepts/environments.html#share-an-environment) between users:

```sh
conda env export > environment.yml
```

Export only installed packages with exact version specification:

```sh
conda env export --from-history -n <env_name> > environment.yml
```
