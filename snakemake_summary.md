# A Summary of Snakemake workflow

It's defined by specifying rules in a snakefile. These rules  decompose the workflow into smaller steps by specifying how to create sets of output files from sets of input files.
 Dependencies between rules are determined automatically.

# Features

_Readability_

With Snakemake, data analysis workflows are defined via an easy to read, adaptable, yet powerful specification language on top of Python. 

_Portability_

 Integration with the  Conda package manager  and  container virtualization  , all software dependencies of each workflow step are automatically deployed upon execution.

_Modularization_

Rapidly implement analysis steps via direct  script  and  jupyter notebook  integration. Easily create and employ  re-useable tool wrappers  and split your data analysis into well-separated modules.

_Transparency_

Automatic, interactive, self-contained reports ensure full transparency from results down to used steps, parameters, code, and software.

_Scalability_

Workflows scale seamlessly from single to multicore, clusters or the cloud, without modification of the workflow definition and automatic avoidance of redundant computations.

# Consider...

Some Bioinformatic tools, 20% of them, are impossible to install due to the large amount of data and software dependancies it contains and requires to be installed.
Thus, we employ the use of Package managers for easy in Portability and execution of the software.

**For example;**

_Bioconda_ is a channel for the conda package manager specializing in bioinformatics software
Integration with such channels allows for ease in installation and execution of some Bioinformatic tools and softwares. [Read more](https://bioconda.github.io/)

Explore the code below that creates a conda environment to house your softwares, activates your environment, installs your software (for our example; Snakemake), exports the environment and allows for its importation.

   `$ conda create -n angeltony`

  Creates a new environment named _angeltony_ 
  
  `$ conda activate angeltony`
  
  Activates the Environment
  
  `$ conda install -c snakemake`
  
  Installs all packages
  
  `$ conda env export > environment.yml`
  
  Exports the environment

  `$  conda env create -f environment.yml`

  Imports the environment


# Strengths of Snakemake:

• Suitable for complex jobs and dependency structures, including wildcards

• Built-in methods to visualize task graph

• Can run tasks in parallel

• Built-in methods to keep track of finished and pending tasks

• Easy on SLURM (when Cluster execution is not used)


# Disadvantages of Snakemake

• Snakemake is complex and requires time to learn

• Works in two modes: single node or cluster mode,   it is strongly suggest that Snakemake be used for single node jobs. 

• Users who need multinode jobs should use another tool such as Parsl, Taskfarmer, or Fireworks.



            
