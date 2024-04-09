# Installing and setup path variable for miniconda:
https://docs.anaconda.com/free/miniconda/

```Bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
```
then add this install to your path directory

```Bash
cd ~/miniconda3/bin/
./conda init
```

restart 
```Bash
exit
```

Check your version 
```Bash
conda -V
```

If it is >=24 you are good! 



We will need conda to install packages to use on Jupyter notebook.

```Bash
conda create -n <myenv> python=3.9 
```

```Bash
source activate <myenv>
conda install pip
conda install ipykernel # or pip install ipykernel
python -m ipykernel install --user --name <myenv> --display-name "<Python (myenv)>"  
```

Now lets install some packages we will need!

```Bash
conda install mp-api # or pip install mp-api
conda install scipy 
conda install -c conda-forge pyprocar
```
