# The Multi-Assumption Architecture and Testbed (MAAT) modelling system. #



### MAAT Version 1.0 ###

The multi-assumption architecture and testbed (MAAT) is a modelling framework designed to facilitate simple and rapid comparison of multiple modelling hypotheses and assumptions, i.e. ways in which to represent processes, in a systems context.
MAAT is designed to easily specify and run large ensembles of simulations.
Ensembles can vary in process representation, parameter values, and environmental conditions.
Built in sensitivity analysis and uncertainty quantification (SA/UQ) can be used to assess variability in model caused output by multiple ways in which to represent processes. 

The MAAT framework is a model wrapper and a model coding syntax that can be used to define a model of a system.
The wrapper and the model system are separated and the syntax allows the wrapper to pass system-model specific information to the model without any system-model specific information contained in the wrapper. 
All system-model specific information is contained within the system model and initialisation files. 
This separation of wrapper and system model allows rapid development of new system models and system model components (e.g. process representations) withou the need to edit the wrapper.

Current systems models that come packaged with the MAAT are a leaf-scale model of photosynthesis, a simple ground-water model detailed in Dai et al (2017 WRR), and a simple 'Hello World' type example and template for building new system models. 

MAAT is written in R and uses the object oriented programming package 'proto' to develop the wrapper and model objects. 
MAAT has been developed on Linux Ubuntu 16.04 and is designed to be run from the command line (and in some instances from within the R console or IDE like Rstudio).



### MAAT set up ###

* Fork this repo and then clone your fork to your local machine. 


*All bash commands below are run from within the highest level maat source code directory* 

* Install R package dependencies ('proto', 'XML', 'xtable', 'randtoolbox'), from the command line (or manually run the script within the R console):
```bash 
Rscript install_dependencies.R
```


* Run unit tests (not necessary but will help confirm code is running on your system). 
Change directory to the system model source directory and open unit\_testing.R in RStudio or similar.
Make sure RStudio is closed before openning the unit testing script as this will allow the R to be opened in the correct working directory. 
```bash 
cd ./src/system_models/<modelobject>/
rstudio unit_testing.R
```
where `<modelobject>` is the name of the system model to be tested.
The unit testing script can be run line by line to run a number of tests of the model objects. 
An example from the leaf model object `unit_testing.R` script to run an ACi curve: 
```R 
source('leaf_object.R')
leaf_object$.test_aci(leaf.ca_conc=seq(0.1,2000,50))
```
The MAAT wrapper can also be tested. 
```bash 
cd ./src/
rstudio unit_testing.R
```


* Set up a MAAT project:
```bash 
./run_scripts/setup_MAAT_project.bs <modelobject> <projectpath>
```
where `<modelobject>` is the name of the system model to be used in the project and `<projectpath>` is the full path of where the project is to be set up.
The lowest level directory in the path will be created if it does not already exist.
Run the above command with `leaf` as `<modelobject>` and your prefered path to set up the MAAT project. 
Change directory to the project directory and a simple instance of MAAT can be run:  
```bash
cd <projectpath>
Rscript run_MAAT.R
```  
This should provide a simple simulation of Aci curves with three different electron transport functions. 


* Initialisation files. 
Once the above steps have been completed and MAAT is working without error, the next step is to customise the run. 
Fundamentally a MAAT ensemble is defined by the process representations, parameter values, and environmental variables. 
These can be defined as static variables, i.e. variables that are invariant across the whole ensemble, or dynamic variables, i.e. variables that are varied across the ensemble. 
The values of the static variables and dynamic variables are defined by the user as either lists in an R script `init_MAAT.R` or as separate XML files `init_user_static.xml` and `init_user_dynamic.xml`. 
These are expected to be found in the highest level project directory. So that multiple simulations can be run from within the same project, these initialisation file names and be appended with `_<runid>` where `<runid>` is a character string that identifies the particular ensemble. 


* Options.
MAAT can be configured in many different ways. 
Alternative command line options, their names, and how to specify them on the command line can be found on lines 33 - 110 of `run_MAAT.R`.

 
* Meteorological data files. 




### Contribution guidelines ###

* For development please fork this repo, create your own dev branch, and then [use the pull request functionality on BitBucket](https://confluence.atlassian.com/bitbucket/fork-a-teammate-s-repository-774243391.html). 
Before making a pull request please ensure that your development branch code is up-to-date by [comparing your forked repo with the 'master' branch in the original repo](https://confluence.atlassian.com/bitbucket/create-a-pull-request-774243413.html) and checking your code has not deviated too far from the updates in master.
 
* Code review - by walkeranthonyp and anyone else that has the time 

* Other guidelines - none



### Please direct questions to ###

Anthony Walker (walkerap@ornl.gov)
