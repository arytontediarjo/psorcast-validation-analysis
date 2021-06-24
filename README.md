# Sage Bionetworks - Psorcast Validation Analysis
<img alt="GitHub pull requests" src="https://img.shields.io/github/issues-pr/Sage-Bionetworks/psorcast-validation-analysis">  <img alt="GitHub issues" src="https://img.shields.io/github/issues/Sage-Bionetworks/psorcast-validation-analysis">  <img alt="Docker Cloud Build Status" src="https://img.shields.io/docker/cloud/build/arytontediarjo/psorcast-validation-analysis">

Welcome to Psorcast Validation Analysis Github Repository, this repository is purposed to be the analytical pipeline for Psorcast Validation Study.

## File Directories:
- <b>curate_tables</b>: Folder for storing all scripts related to curating tables from Bridge to Validation Analysis Project
- <b>feature_extraction</b>: Folder for storing all scripts related to extracting key features from previously extracted Synapse Tables
- <b>analysis</b>: Folder for storing analysis codes and notebooks

## How to run
To run this repository, you will be required to have several credentials:
- A Github Token Credentials for fetching github urls
- A .synapseConfig File for getting your credentials to synapse
- A .synapseCache Folder for caching synapse files I/O

### How to run:
We will be using docker for reproducing this analysis, we will require your Synapse/Github credentials (in file location) to be placed in .env so that as we build the container, it will contain all the required credentials.

#### a. Using Docker:
```zsh
docker pull arytontediarjo/psorcast-validation-analysis

docker run -v <SYNAPSE_CONFIG_PATH>:/root/.synapseConfig\ 
            -v <SYNAPSE_CACHE_PATH>:/root/.synapseCache\
            -v <GIT_TOKEN_PATH>:/git_token.txt\
            -d arytontediarjo/psorcast-validation-analysis

docker exec <CONTAINER_ID> make pipeline
```
#### b. Contributing Using Local RStudio (Local):

##### i. Git Clone
```zsh
git clone git clone https://github.com/Sage-Bionetworks/psorcast-validation-analysis.git
```

#### ii. Create Python Virtual Environment
Some of the steps of the pipeline will use python and will be using R renv library for managing it (https://rstudio.github.io/renv/articles/python.html)
```zsh
bash init_py_env.sh
```

##### iii. Restore Libraries 
```R
renv::init(bare = T)
renv::restore()
renv::use_python(name = "env", type = "virtualenv") # parse in python location with installed packages from requirements.txt
```
