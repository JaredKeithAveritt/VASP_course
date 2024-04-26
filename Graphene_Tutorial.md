# Graphene in VASP

## Making the geometry file
We can make the input geometry using data from the materials database
```

```

## Geometry Optimization (i.e. energy minimisation)

We can use vaspkit to make the input files:
note: make sure the `POSCAR` file is in the active directory

**INCAR:**
```
cd  ~/graphene_tutorial
vaspkit
101
SRD3
```

**POTCAR:**
```
cd  ~/graphene_tutorial
vaspkit
103
```

**KPOINTS:**
```
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
```
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

anot
