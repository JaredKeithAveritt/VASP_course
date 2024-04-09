# Setting up miniconda:

```
mkdir -p ~/miniconda3
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
```


https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

We will need conda to install packages to use on Jupyter notebook.
```Bash
source activate <myenv>
python -m ipykernel install --user --name <myenv> --display-name "<Python (myenv)>"  
```
(Note. You may need to install ipykernel:  conda install ipykernel)
