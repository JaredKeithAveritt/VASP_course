# Setting up conda:

https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

We will need conda to install packages to use on Jupyter notebook.
```Bash
source activate <myenv>
python -m ipykernel install --user --name <myenv> --display-name "<Python (myenv)>"  
```
(Note. You may need to install ipykernel:  conda install ipykernel)
