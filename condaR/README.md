# Building Installers with Conda Constructor

[Conda Constructor](https://github.com/conda/constructor) is a tool that builds an installer for a collection of conda packages. This is the same tool used to build Anaconda installers that you can use to build custom installations.

This tutorial shows how to build an installer with custom R environment and Jupyter Notebook Jupyter.

## Prerequisites

This tutorial requires the following :
* git

  (To install" `conda install git`)

* conda 4.7.10 or greater 

  (either by installing the latest version of [Anaconda Distribution](https://www.anaconda.com/distribution/) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or by upgrading `conda upgrade conda`)

## Getting Started

Clone the project.
```
git clone https://github.com/spara/condaR
```

If necessary check the conda version and update conda to the latest version, in the Anaconda prompt:
```
(base) $ conda --version
conda 4.7.5
(base) $ conda upgrade conda
```

Install conda constructor:
```
conda install constructor
Collecting package metadata (repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /Users/sparafina/condar

  added / updated specs:
    - constructor


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    constructor-3.0.0          |           py37_0         9.1 MB
    ------------------------------------------------------------
                                           Total:         9.1 MB

The following NEW packages will be INSTALLED:

  constructor        pkgs/main/osx-64::constructor-3.0.0-py37_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
constructor-3.0.0    | 9.1 MB    | ################################################################################ | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done

(base) $ constructor --version
constructor 3.0.0
```

## Constructor Basics

Constructor uses a YAML file to configure the build. The default file name for the configuration file is `construct.yaml` The only mandatory elements are the name and version, but to create an environment you will need to specify the channels and the packages to be installed. This is an example file that creates an installer with just python and conda:
```
name: myBase
version: 0.1

channels:
  - https://repo.anaconda.com/pkgs/main/
 

specs:
  - python
  - conda
```
To build this installer
```
(base) $ constructor .
```

If you run this command in macOS, constructor will create an installer named myBase-0.1-MacOSX-x86_64.sh. By default, the installer uses name-version-OS as the naming convention if a name is not specified. If you want create a .pkg installer named `myBase_Belong_To_Us` add the `installer_type` and `installer_filename` keys to construct.yaml

```
installer_filename: myBase_Belong_To_Us.pkg
installer_type: pkg  [osx]
```

The keys available to customise the installer are listed on the [constructor github repository](https://github.com/conda/constructor/blob/master/CONSTRUCT.md).

## Building Operating System Specific Installers

Building an installer is relatively simple but there are a few operating system specific characteristics. For that reason, the rest of the tutorial has been split up by operating system.

* [macOS](./macOS/build.md)
* [linux](./linux/build.md)
* [windows](./windows/build.md)




