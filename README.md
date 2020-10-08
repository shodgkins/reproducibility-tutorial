# reproducibility-tutorial
This is a tutorial for FOSS 2020.

## Computer Setup

### Clone the GitHub repository into /scratch
    cd /scratch
    git clone https://github.com/shodgkins/reproducibility-tutorial.git
    ls

### Install MiniConda
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    bash Miniconda3-latest-Linux-x86_64.sh -b -p /opt/conda

#### Make sure all conda packages will be in path by symbolic links to /bin (this step is a bit of a hack)
    ln -s /opt/conda/pkgs/*/bin/* /bin
    ln -s /opt/conda/pkgs/*/lib/* /usr/lib

### Install and test Jupyter

#### Install Jupyter, bash kernel, and dependencies using conda
    /opt/conda/bin/conda install -c conda-forge -y jupyterlab=1.2.3
    /opt/conda/bin/conda install -c conda-forge -y nodejs=10.13.0
    /opt/conda/bin/pip install bash_kernel
    /opt/conda/bin/pip install ipykernel
    /opt/conda/bin/python3 -m bash_kernel.install

#### Examples of searching for available packages
    /opt/conda/bin/conda search bowtie
    /opt/conda/bin/conda search -c bioconda bowtie

#### Start Jupyterlab server
    /opt/conda/bin/jupyter lab --no-browser --allow-root --ip=0.0.0.0 --NotebookApp.token='' --NotebookApp.password='' --notebook-dir='/scratch/reproducibility-tutorial/'

### Install and test snakemake

#### See what snakemake versions are available
    /opt/conda/bin/conda search -c bioconda snakemake

#### Install version 5.8.1
    /opt/conda/bin/conda install -c bioconda -c conda-forge -y snakemake=5.8.1

#### Make sure conda packages will be in path again
    ln -s /opt/conda/bin/* /bin
    ln -s /opt/conda/lib/* /usr/lib

#### Verify the installation
    snakemake --version

### Install and test Docker

#### Update ubuntu apt-get package manager, and install some needed packages
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common

#### Add the Docker key
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

#### Add the repository
    sudo add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
     $(lsb_release -cs) \
     stable"

#### Update apt-get with new repository information
    sudo apt-get update

#### Install Docker
    sudo apt-get install -y docker-ce docker-ce-cli containerd.io

#### Test Docker
    docker run hello-world

### Set up local filesystem

#### Change into the repository directory
    cd /scratch/reproducibility-tutorial/

#### Save the software installation to README.md (this file), and then verify it's saved
    history >>README.md
    cat README.md

