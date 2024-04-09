Lets start with the atoms and molecules tutorials from the vasp website : https://www.vasp.at/tutorials/latest/molecules/


Lets first download all the files from the vasp site:
```Bash
mkdir -p ~/first_VASP
cd ~/first_VASP
curl -O https://www.vasp.at/tutorials/latest/molecules-part1.zip
unzip molecules-part1.zip
```

VASP is already installed at `/nas/longleaf/home/manojw/VASP/vasp.6.3.2/bin` and we need to assign the path variable for the VASP executable. 
And do the same for the location of our tutorial files we downloaded
```Bash
export PATH=$PATH:/nas/longleaf/home/manojw/VASP/vasp.6.3.2/bin
export TUTORIALS="~/first_VASP"
```

lets test the TUTORIALS variable:
```Bash
cd $TUTORIALS/molecules
```

