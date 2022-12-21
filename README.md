# genomic-data-visualization-tools

## Conda environment

Create a Conda environment on Quest as follows: 

```
module purge all
module load python-miniconda3/4.12.0

# enable bioconda channels
conda config --add channels bioconda
conda config --add channels conda-forge

# create new environment in your projects folder of type p00000
conda create -c conda-forge --prefix /projects/p00000/bioinfo jupyterlab python=3.8 --yes
source activate /projects/p00000/bioinfo
pip install bio --upgrade

wget https://raw.githubusercontent.com/ritika-giri/genomic-data-visualization-tools/main/biotools.txt | xargs conda install -y
conda clean --all # remove all temporary install and cache files that take up space

# check installs
mkdir -p ~/bin
curl -s http://data.biostarhandbook.com/install/doctor.py > ~/bin/doctor.py
chmod +x ~/bin/doctor.py
~/bin/doctor.py

# load any modules required
module load bcftools/1.10.1
module load  sratoolkit/3.0.0
vdb-config --interactive # save and exit VDB to set up SRAtools one time
module load bowtie/1.2.2  # for short reads < 50bp
module load deeptools/3.5.1


# install required packages
conda install deeptools
conda install -c bioconda coolbox
pip install dna_features_viewer numpydoc statsmodels voila svgutils pybbi fire # imports for coolbox

# enable browser widget on jupyter notebook
conda install -c conda-forge nodejs
pip install npm
pip install jupyterlab_widgets
jupyter nbextension enable --py widgetsnbextension

# enable browser widget on jupyterlab
jupyter labextension install @jupyter-widgets/jupyterlab-manager
jupyter labextension list
jupyter labextension update --all

# optional troubleshooting if above doesn't work
jupyter lab clean
jupyter labextension install @jupyter-widgets/jupyterlab-manager

```

