# Graphene in VASP

## Making the geometry file `POSCAR` using Jupyter notebook and the following code 
We can make the input geometry using data from the materials database

```Python
from mp_api.client import MPRester
import pymatgen

# Your Materials Project API key
API_KEY = "insert_your_API"

# The ID of the material 
# Material_id = "mp-626143" # this is ?
material_id = "mp-1040425" # this is graphene


# Create an instance of MPRester
with MPRester(API_KEY) as mpr:
    material_data = mpr.materials.summary.search(material_ids=[str(material_id)])
    structure = mpr.get_structure_by_material_id(str(material_id))
    
    structure.make_supercell((5,5,1))
    from pymatgen.io.ase import AseAtomsAdaptor

# Convert pymatgen structure to ASE Atoms
adaptor = AseAtomsAdaptor()
atoms = adaptor.get_atoms(structure)
from ase import io
import ase
import numpy as np
from ase.visualize import view
import matplotlib.pyplot as plt
from ase.visualize.plot import plot_atoms

# access the cell of the atoms object
cell=atoms.cell
print("the cell of the atoms object:")
print(cell)

# create a,b,c values to correspond to the unit cell
a, b, c = cell.lengths()
print("cell dimensions (length of vectors):")
print("a = {}, b = {}, c = {}".format(a,b,c)) 

fig, ax = plt.subplots()
plot_atoms(atoms, ax, radii=0.9,rotation=('0x,0y,0z'))
fig, ax = plt.subplots()
plot_atoms(atoms, ax, radii=0.9,rotation=('0x,90y,90z'))
fig, ax = plt.subplots()
plot_atoms(atoms, ax, radii=0.9,rotation=('180x,90y,0z'))
print('total number of atoms origionally = ',len(atoms))

# Delete atoms 267 to 270
# atoms_removed = atoms.copy()
# del atoms_removed[len(atoms)-4:len(atoms)]


atoms.write('POSCAR', format='vasp', direct=True)
len(atoms)
```

The contents of the poscar file:

```Fortran
 C 
 1.0000000000000000
     6.1700750000000006  -10.6868850000000002    0.0000000000000000
     6.1700750000000006   10.6868850000000002    0.0000000000000000
     0.0000000000000000    0.0000000000000000   19.9982930000000003
 C  
  50
Direct
  0.0666666000000000  0.1333334000000000  0.0000000000000000
  0.0666666000000000  0.3333334000000000  0.0000000000000000
  0.0666666000000000  0.5333334000000001  0.0000000000000000
  0.0666666000000000  0.7333334000000001  0.0000000000000000
  0.0666666000000000  0.9333334000000001  0.0000000000000000
  0.2666666000000000  0.1333334000000000  0.0000000000000000
  0.2666666000000000  0.3333334000000001  0.0000000000000000
  0.2666666000000000  0.5333334000000001  0.0000000000000000
  0.2666666000000001  0.7333334000000002  0.0000000000000000
  0.2666666000000001  0.9333334000000001  0.0000000000000000
  0.4666666000000001  0.1333334000000000  0.0000000000000000
  0.4666666000000001  0.3333334000000001  0.0000000000000000
  0.4666666000000002  0.5333334000000001  0.0000000000000000
  0.4666666000000001  0.7333334000000001  0.0000000000000000
  0.4666666000000001  0.9333334000000000  0.0000000000000000
  0.6666666000000001  0.1333334000000000  0.0000000000000000
  0.6666666000000002  0.3333334000000001  0.0000000000000000
  0.6666666000000001  0.5333334000000001  0.0000000000000000
  0.6666666000000000  0.7333333999999999  0.0000000000000000
  0.6666666000000000  0.9333333999999999  0.0000000000000000
  0.8666666000000002  0.1333334000000000  0.0000000000000000
  0.8666666000000002  0.3333334000000001  0.0000000000000000
  0.8666666000000000  0.5333334000000001  0.0000000000000000
  0.8666666000000002  0.7333334000000001  0.0000000000000000
  0.8666666000000000  0.9333334000000000  0.0000000000000000
  0.1333334000000000  0.0666666000000000  0.0000000000000000
  0.1333334000000000  0.2666666000000000  0.0000000000000000
  0.1333334000000000  0.4666666000000001  0.0000000000000000
  0.1333334000000000  0.6666666000000002  0.0000000000000000
  0.1333334000000000  0.8666666000000002  0.0000000000000000
  0.3333334000000000  0.0666666000000000  0.0000000000000000
  0.3333334000000001  0.2666666000000000  0.0000000000000000
  0.3333334000000000  0.4666666000000000  0.0000000000000000
  0.3333334000000001  0.6666666000000001  0.0000000000000000
  0.3333334000000001  0.8666666000000002  0.0000000000000000
  0.5333334000000001  0.0666666000000000  0.0000000000000000
  0.5333334000000001  0.2666666000000000  0.0000000000000000
  0.5333334000000002  0.4666666000000001  0.0000000000000000
  0.5333334000000001  0.6666666000000001  0.0000000000000000
  0.5333334000000001  0.8666666000000001  0.0000000000000000
  0.7333334000000001  0.0666666000000000  0.0000000000000000
  0.7333334000000000  0.2666666000000000  0.0000000000000000
  0.7333334000000001  0.4666666000000000  0.0000000000000000
  0.7333334000000000  0.6666665999999999  0.0000000000000000
  0.7333333999999999  0.8666666000000000  0.0000000000000000
  0.9333334000000001  0.0666666000000001  0.0000000000000000
  0.9333334000000001  0.2666665999999999  0.0000000000000000
  0.9333334000000001  0.4666666000000000  0.0000000000000000
  0.9333334000000003  0.6666666000000001  0.0000000000000000
  0.9333334000000001  0.8666666000000000  0.0000000000000000
```

We want to center all of the atoms to the middle of the box in the z-coordinate:

```Bash
vaspkit
921
cp POSCAR POSCAR_ORIGINAL
cp POSCAR_REV POSCAR
```

## Geometry Optimization (i.e. energy minimisation) , - ionic relaxation

We can use vaspkit to make the input files:
note: make sure the `POSCAR` file is in the active directory

**INCAR:**
```Bash
cd  ~/graphene_tutorial
vaspkit
101
SRD3
```

**POTCAR:**
```Bash
cd  ~/graphene_tutorial
vaspkit
103
```

**KPOINTS:**
```Bash
cd  ~/graphene_tutorial
vaspkit
102
1
0.03
```

And our SLURM file will need to look something like:
**.sh:**
```Bash
#!/bin/bash
#SBATCH -N 2
#SBATCH -p debug_queue
#SBATCH --ntasks-per-node=44
#SBATCH --time=04:00:00
#SBATCH --mail-type=BEGIN,END,FAIL
#SBATCH --mail-user=email_address_@uncg.edu

module purge
module load hdf5/1.12.1-openmpi
module list

mpirun vasp_std
```

The output files from the geometry optimization, with the above incar include the files : 

but the one I want to show is here is `OUTCAR` : 
```Fortran
 LDA part: xc-table for Pade appr. of Perdew
 POSCAR, INCAR and KPOINTS ok, starting setup
 FFT: planning ... GRIDC
 FFT: planning ... GRID_SOFT
 FFT: planning ... GRID
 WAVECAR not read
 WARNING: random wavefunctions but no delay for mixing, default for NELMDL
 entering main loop
       N       E                     dE             d eps       ncg     rms          rms(c)
DAV:   1     0.166870545281E+04    0.16687E+04   -0.72419E+04  1056   0.829E+02
DAV:   2    -0.261374835532E+03   -0.19301E+04   -0.18584E+04  1848   0.190E+02
DAV:   3    -0.488115423049E+03   -0.22674E+03   -0.22577E+03  1496   0.788E+01
DAV:   4    -0.492660633579E+03   -0.45452E+01   -0.45189E+01  1584   0.140E+01
DAV:   5    -0.492783618119E+03   -0.12298E+00   -0.12282E+00  1408   0.222E+00    0.315E+01
DAV:   6    -0.470131111980E+03    0.22653E+02   -0.19945E+01  1056   0.765E+00    0.185E+01
DAV:   7    -0.461346032174E+03    0.87851E+01   -0.27643E+01  1496   0.883E+00    0.474E+00
DAV:   8    -0.461175217235E+03    0.17081E+00   -0.67690E-01  1408   0.143E+00    0.509E-01
DAV:   9    -0.461156424646E+03    0.18793E-01   -0.24399E-02  1408   0.287E-01    0.377E-01
DAV:  10    -0.461095442979E+03    0.60982E-01   -0.67778E-02  1496   0.325E-01    0.305E-01
DAV:  11    -0.461105157138E+03   -0.97142E-02   -0.60399E-03  1320   0.124E-01    0.134E-01
DAV:  12    -0.461122172042E+03   -0.17015E-01   -0.41532E-03  1056   0.997E-02    0.972E-02
DAV:  13    -0.461128524329E+03   -0.63523E-02   -0.26013E-04  1408   0.232E-02    0.769E-02
DAV:  14    -0.461143806688E+03   -0.15282E-01   -0.24099E-03  1408   0.579E-02    0.239E-02
DAV:  15    -0.461145606808E+03   -0.18001E-02   -0.13319E-04  1144   0.185E-02    0.211E-02
DAV:  16    -0.461145914019E+03   -0.30721E-03   -0.18559E-05  1320   0.591E-03    0.574E-03
DAV:  17    -0.461146107759E+03   -0.19374E-03   -0.56668E-06  1232   0.443E-03    0.473E-03
DAV:  18    -0.461146147954E+03   -0.40195E-04   -0.92534E-08  1320   0.625E-04    0.249E-03
DAV:  19    -0.461146213060E+03   -0.65105E-04   -0.63931E-07  1144   0.167E-03    0.115E-03
DAV:  20    -0.461146219438E+03   -0.63789E-05   -0.20599E-08  1408   0.272E-04    0.426E-04
DAV:  21    -0.461146221240E+03   -0.18017E-05   -0.45062E-09  1232   0.160E-04    0.334E-04
DAV:  22    -0.461146221457E+03   -0.21660E-06    0.74161E-09  1232   0.369E-05    0.309E-04
DAV:  23    -0.461146221480E+03   -0.23327E-07    0.75058E-09  1144   0.183E-05    0.308E-04
DAV:  24    -0.461146221478E+03    0.20482E-08    0.72205E-09  1144   0.775E-06
   1 F= -.46286319E+03 E0= -.46285693E+03  d E =-.462863E+03
 curvature:   0.00 expect dE= 0.000E+00 dE for cont linesearch  0.000E+00
 trial: gam= 0.00000 g(F)=  0.488E-38 g(S)=  0.000E+00 ort = 0.000E+00 (trialstep = 0.100E+01)
 search vector abs. value=  0.100E-09
 reached required accuracy - stopping structural energy minimisation
```

# Self Consistent Field (SCF) Calculation (electronic-opt)
the electron density is energy minimized 

The `CONTCAR` contains the ionic relaxed positions from the last optimization step

```Bash
cd ~/graphene_tutorial
mkdir SCF
cd SCF

cp ../OPT/CONTCAR POSCAR
cp ../OPT/run_job.sh ../OPT/POTCAR ../OPT/KPOINTS .

vaspkit
101
STD3
```

check parameters of `ENCUT` and `PREC` from the `/OPT/INCAR` vs. `/SCF/INCAR` is the same.

Also make sure that `ISMEAR = 1`

# Density of States Calculation (DOS) - post dft analysis
```Bash
~/graphene_tutorial
mkdir DOS
cd DOS
cp ../SCF/CHGCAR ../SCF/WAVECAR ../SCF/run_job.sh ../SCF/POSCAR ../SCF/POTCAR ../SCF/KPOINTS .

vaspkit
101
STD3
```

The `INCAR` file needs to be changes a little

uncomment the lines
```Fortran
ENCUT = 520
ICHARGE = 11
```

and change 
```Fortran
ISMEAR = 5 
```
so it looks like: 
```Fortran
Global Parameters
ISTART =  1            (Read existing wavefunction, if there)
ISPIN  =  1            (Non-Spin polarised DFT)
# ICHARG =  11         (Non-self-consistent: GGA/LDA band structures)
LREAL  = .FALSE.       (Projection operators: automatic)
ENCUT  =  520        (Cut-off energy for plane wave basis set, in eV)
# PREC   =  Accurate   (Precision level: Normal or Accurate, set Accurate when perform struct$
LWAVE  = .TRUE.        (Write WAVECAR or not)
LCHARG = .TRUE.        (Write CHGCAR or not)
ADDGRID= .TRUE.        (Increase grid, helps GGA convergence)
# LVTOT  = .TRUE.      (Write total electrostatic potential into LOCPOT or not)
# LVHAR  = .TRUE.      (Write ionic + Hartree electrostatic potential into LOCPOT or not)
# NELECT =             (No. of electrons: charged cells, be careful)
# LPLANE = .TRUE.      (Real space distribution, supercells)
# NWRITE = 2           (Medium-level output)
# KPAR   = 2           (Divides k-grid into separate groups)
# NGXF    = 300        (FFT grid mesh density for nice charge/potential plots)
# NGYF    = 300        (FFT grid mesh density for nice charge/potential plots)
# NGZF    = 300        (FFT grid mesh density for nice charge/potential plots)

Static Calculation
ISMEAR =  0           (gaussian smearing method)
SIGMA  =  0.02         (please check the width of the smearing)
LORBIT =  11           (PAW radii for projected DOS)
NEDOS  =  2001         (DOSCAR points)
NELM   =  60           (Max electronic SCF steps)
EDIFF  =  1E-06        (SCF energy convergence, in eV)

DFT-D3 Correction
IVDW   =  12           (DFT-D3 method of method with no damping)
```

# Lets plot the DOS! 

using jupyter:

```Python
import numpy as np
import matplotlib.pyplot as plt
import os
from scipy.ndimage import gaussian_filter1d


# Read data from the file
def read_pdos(file_path):
    data = np.loadtxt(file_path, skiprows=1)  # Assuming the first row contains strings

    # Extract labels from the comment line
    with open(file_path, 'r') as file:
        comment_line = file.readline().strip()

    # Remove leading '#' and split the line into labels
    labels = comment_line[1:].split()[1:]

    # Extract data columns
    energy_values = data[:, 0]  # First column as x-axis values
    pdos_values = data[:, 1:]  # Data excluding the first column

    return energy_values, pdos_values, labels


def read_doscar(file_path):
    total_dos=[]
    with open(file_path, 'r') as file:
        # Skip the first four header lines
        for _ in range(5):
            next(file)
        
        # Read the 5th line to get the desired value
        fifth_line = next(file).split()
        E_fermi_value = float(fifth_line[3])  # Extracting the fourth item
        NEDOS_value=int(fifth_line[2])
        # Initialize lists for energy values and total DOS
        energy_values = []
        total_dos = []
        int_dos = []
        
        # Initialize line counter
        line_count = 0

        # Read total DOS data from the remaining lines
        for line in file:
            # Increment line counter
            line_count += 1

            # Check if line count exceeds NEDOS_value
            if line_count > NEDOS_value:
                break

            data = line.split()
            # Ensure the line has enough elements to avoid index errors
            if len(data) >= 2:
                energy_values.append(float(data[0]))
                total_dos.append(float(data[1]))
                int_dos.append(float(data[2]))

    # Convert lists to numpy arrays for further processing
    energy_values_np = np.array(energy_values)
    total_dos_np = np.array(total_dos)
    int_dos_np= np.array(int_dos)

    energy_values_np -= E_fermi_value

    return energy_values_np, total_dos_np, int_dos_np


# Function to smooth data using Gaussian filter
def smooth_data(data, sigma=2):
    return gaussian_filter1d(data, sigma)

doscar_path_G ='/nas/longleaf/home/YOUR_ONYEN/graphene_tutorial/DOS/DOSCAR'

energy_values_G, total_dos_G , int_dos_G= read_doscar(doscar_path_G)


sigma = 0# Adjust the sigma value as needed
i=9
# Smooth total DOS data using Gaussian filter
if sigma !=0:
    total_dos_G = smooth_data(total_dos_G, sigma)

# Plot the data
plt.figure(figsize=(12, 6))

plt.plot(energy_values_G, total_dos_G, label='Total', color='blue')
plt.plot(energy_values_G, int_dos_G/7, label='Integrated', color='green')

# Setting font size and style for axis labels
plt.xlabel('Energy (eV)', fontsize=12, fontfamily='sans-serif', fontstyle='normal')
plt.ylabel('Density of States', fontsize=12, fontfamily='sans-serif', fontstyle='normal')

# Setting font size for tick labels

#plt.axhline(0, color='black', linestyle='--', linewidth=0.8)  # Horizontal line at y=0
#plt.xlim(-4,4)
#plt.ylim(0,1)
plt.legend()
plt.gca().set_yticklabels([])
#plt.grid(True)
plt.xticks(fontsize=18, fontfamily='monospace')
plt.yticks(fontsize=18, fontfamily='monospace')
plt.legend(fontsize=18)
plt.savefig('G_DOS.png', dpi=300)  # Adjust dpi value as needed for higher or lower resolution
plt.show()
```


We see BUTT! 

![BAD DOS](https://github.com/JaredKeithAveritt/VASP_course/blob/main/BAD-G_DOS.png)


# Re-Run SCF

to fix it we need to go back to the SCF step first and tighten the converging criterian and increase the density of the mesh and change ISMEAR = 0, as advised by the VASP

**SCF/INCAR:**
```
IVDW = 12
ISMEAR = 0
SIGMA = 0.02
EDIFF = 1E-6
```

**SCF/KPOINTS:**
```
K-Spacing Value to Generate K-Mesh: 0.030
0
Monkhorst-Pack
   13   13   1
0.0  0.0  0.0
```

re-run job, when job is done, we can calculate the DOS again.

# Re-Run DOS

```
cd ~/graphene_tutorial
rm -r DOS
mkdir DOS
cd DOS
cp ../SCF/CHGCAR ../SCF/WAVECAR ../SCF/run_job.sh ../SCF/POSCAR ../SCF/POTCAR ../SCF/KPOINTS ../SCF/INCAR .
```

edit the following lines in the `DOS/INCAR` to:
```FORTRAN
ICHARG = 11
LWAVE  =  .FALSE.
LCHARGE = .FALSE.
IVDW = 12
ISMEAR = -5
LORBIT = 11
NEDOS = 3001
```

Other Considerations: 
K-Points Density:
A k-points grid of 33x33x1 is quite high and should generally give a well-converged DOS. However, in certain cases, such as band structures involving Dirac points, a different density or grid might yield better results.
Try slightly reducing the k-point density to a value like 21x21x1 or 27x27x1 to check if the high noise levels are a result of an excessively dense grid.
Smearing Method:
You have ISMEAR = -5, which is suitable for accurate DOS calculations. Ensure that the chosen SIGMA value (0.02 eV) is appropriate for the system by experimenting with other values like 0.05 or 0.1.
If you are not observing clear features even after adjusting SIGMA, consider switching to ISMEAR = 0 (Gaussian) for metallic systems or testing other methods.
Projected DOS:
The parameter LORBIT = 11 is necessary for projected DOS but could potentially add extra noise depending on orbital contributions. You can try LORBIT = 10 to reduce noise while still generating reasonable projections.
NEDOS Points:
Having NEDOS = 3001 should generally provide sufficient resolution. Try varying the value between 1000 and 4000 to see how this affects the appearance of the DOS plot.
Non-Self-Consistent Calculation (ICHARG = 11):
Using ICHARG = 11 for DOS calculation is appropriate, but ensure that the input charge density file (CHGCAR) is from a fully converged SCF calculation.
Check Wavefunction Consistency:
If you are using an old wavefunction (WAVECAR) from another calculation, consider regenerating the wavefunction using an SCF calculation before performing the DOS.
Check Data Processing:
Ensure your data extraction and plotting process is consistent and not introducing artificial noise. If you're using a custom script, try validating the output with another plotting tool.
Other Functional or Correction Parameters:
The DFT-D3 correction (IVDW = 12) can affect the DOS shape subtly. Verify that this method is appropriate for your system, or consider testing the calculation without dispersion correction to see if it improves the DOS plot.

