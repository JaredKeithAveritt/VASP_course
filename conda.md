# Setting up miniconda:

```
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
```

Check your version 
```
conda -V
```


https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

We will need conda to install packages to use on Jupyter notebook.
```Bash
source activate <myenv>
python -m ipykernel install --user --name <myenv> --display-name "<Python (myenv)>"  
```
(Note. You may need to install ipykernel:  conda install ipykernel)
