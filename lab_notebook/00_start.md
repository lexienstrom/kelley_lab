# Notes for getting started

[Markdown cheatsheet](https://www.markdownguide.org/cheat-sheet/)

Configure remote git repo (in home directory /hb/home/aenstrom): 
~~~
git clone https://github.com/lexienstrom/kelley_lab.git
git config user.name "lexienstrom"
git config user.email "aenstrom@ucsc.edu" 
git remote set-url origin https://{personal-access-token}@github.com/lexienstrom/kelley_lab.git
~~~

## Slurm on [Hummingbird](https://hummingbird.ucsc.edu/) 

`ssh aenstrom@hb.ucsc.edu`

`cd /hb/groups/kelley_training/lexi`

- running jobs: [tutorial](https://hummingbird.ucsc.edu/documentation/creating-scripts-to-run-jobs/)
    - SLURM template for #SBATCH directives
    ```bash
    #!/bin/bash

    #SBATCH --job-name=JOB_NAME    # Job name
    #SBATCH --partition=128x24
    #SBATCH --mail-type=ALL               # Mail events (NONE, BEGIN, END, FAIL, ALL)
    #SBATCH --mail-user=aenstrom@ucsc.edu   # Where to send mail	
    #SBATCH --nodes=1                    # Use one node
    #SBATCH --ntasks=1                    # Run a single task 
    #SBATCH --cpus-per-task=1           # Number of CPU cores per task
    #SBATCH --time=24:00:00               # Time limit hrs:min:sec (you may not want this)
    #SBATCH --output=./logs/job_%j.out    # Standard output and error log
    #SBATCH --error=./logs/job_%j.err     # Standard output and error log
    #SBATCH --mem=1G                    # Allocate memory for the job.
    ``` 
- interactive job:
    ```bash
    salloc --partition=128x24 --time=02:00:00 --mem=1G --ntasks=1 --cpus-per-task=1
    ssh $SLURM_NODELIST
    # run stuff
    exit
    exit
    ```
- data transfer:
    - type in terminal on personal computer `sftp aenstrom@hb.ucsc.edu`
        - To transfer file from home directory on personal computer to Hummingbird
            - `put filename` or `get filename`
            - `get -r folder_name`
              
### Loading modules:

`module load miniconda3`

`module load fastqc`

`module load star`

`module load agat`

# Conda Environments
## Making a conda environment

~~~
# To create an environment:
conda create --name <my-env>

# To create an environment with a specific version of Python:
conda create -n myenv python=3.9

# Create the environment from the environment.yml file
conda env create -f environment.yml

# Verify that the new environment was installed correctly:
conda env list
~~~

## Installing software with conda:

`conda install -c bioconda orthofinder`
- orthofinder conda package came with the wrong version of diamond, so manually installed diamond and replaced the executable in the conda env directory

~~~
wget http://github.com/bbuchfink/diamond/releases/download/v2.1.8/diamond-linux64.tar.gz
tar xzf diamond-linux64.tar.gz
cp diamond /hb/home/aenstrom/.conda/envs/orthofinder/bin/
~~~

`conda install -c conda-forge ncbi-datasets-cli`

`conda install -c conda-forge biopython`

`conda install -c bioconda subread` (featureCounts)

`conda install -c bioconda agat` (GFF/GTF tools)

### Installing other software to home directory
dir: /hb/home/aenstrom/bin

seqtoolkit
~~~
wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/3.0.7/sratoolkit.3.0.7-ubuntu64.tar.gz
tar xzf sratoolkit.3.0.7-ubuntu64.tar.gz
~~~

# GitHub 
## Initialize Git inside your folder
```bash
cd /path/to/directory
git init
git clone git@github.com:your-username/bear_phylogenetics.git
cd repository
```
## commit and push your files:
```bash
git add .
git commit -m "Initial commit"
git push -u origin main
```
