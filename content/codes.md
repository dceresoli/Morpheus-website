+++
date = "Thu, 23 Feb 2017 14:53:57 +0100"
title = "Installed codes"
categories = [ "software" ]
tags = [ "document" ]
+++
## Plane wave codes
### Quantum Espresso
Installed versions: 5.1.2, 5.2.0, 5.2.1, 5.3.0, 6.0. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
#scratch=/scratch/$USER/${PWD#$HOME}            # to save files on the global scratch (slow)
scratch=/local_scratch/$USER/${PWD#$HOME}       # to save files on the global scratch (fast)
mkdir -p $scratch 2>/dev/null
ln -sf $scratch ./scratch
#======================================================================
module purge
module load intel/xe2011 openmpi/1.8.3-intel qe/5.1.2
#======================================================================
mpirun pw.x <C60-scf.in >C60-scf.out
mpirun ph.x <C60-phonon.in >C60-phonon.out
```

### VASP
Installed versions: 5.3.3. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
#scratch=/scratch/$USER/${PWD#$HOME}            # to save files on the global scratch (slow)
scratch=/local_scratch/$USER/${PWD#$HOME}       # to save files on the global scratch (fast)
mkdir -p $scratch 2>/dev/null
#======================================================================
module purge
module load intel/xe2011 openmpi/1.8.3-intel vasp/5.3.3
#======================================================================
export OMP_NUM_THREADS=1
export MKL_NUM_THREADS=1
export KMP_NUM_THREADS=1
cp INCAR POSCAR POTCAR KPOINTS $scratch
pushd .
cd $scratch
vasp                                            # k-points version
#vasp_gamma                                     # Gamma-point version
#vasp_nc                                        # non-collinear and spin-orbit version
popd
cp $scratch/OUTCAR .
```

## Local basis codes
### Siesta & Transiesta (& Smeagol)
Installed versions: 3.2-pl5, trunk-462, 4.0, 4.1b1, 4.1b3, ldau308, smeagol-1.2. Example of job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module purge
module load intel/xe2011 openmpi/1.8.3-intel siesta/trunk-462
#======================================================================
mpirun siesta <C60.fdf >C60.out
```

### Gaussian 09 & Gaussview
Installed versions: A.01, C.01, D.01, E.01. Gaussiew-4.1.6 is also available. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N TEST-G09
#PBS -l walltime=1:00:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module load g09/D.01
source $g09root/g09/bsd/g09.profile
#======================================================================
g09 S01-hyper.com
```

Don't use LINDA, etc. Use only shared-memory parallelism (in the example, only 4 CPU cores):
```
 %chk=S01-hyper.chk
 %mem=500MW
 %nproc=4
 # nmr=giao upbepbe/epr-III integral=ultrafine scf=tight
 ...
```

To use Gaussview interactively:
```bash
$ module load g09/E.01
$ source $g09root/g09/bsd/g09.profile
$ gaussview -soft
```

### Crystal
Installed version: 13 (unofficial, compiled from sources), 13+some features from 2016, 14-v1.0.3,
both serial and parallel.  Example of job script:
```
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
#scratch=/scratch/$USER/${PWD#$HOME}            # to save files on the global scratch (slow)
scratch=/local_scratch/$USER/${PWD#$HOME}       # to save files on the local scratch (fast)
#======================================================================
# to use CRYSTAL14
module purge
module load intel/xe2015 openmpi/1.8.3-intel crystal/14

# to use CRYSTAL13 instead
module purge
module load intel/xe2011 openmpi/1.8.3-intel crystal/13

echo Running on node: `hostname`:$scratch
launchdir=`pwd`
mkdir -p $scratch
cp test00.d12 $scratch   # you can copy also restart files
cd $scratch

# ----- serial -----
crystal <test00.d12 >test00.out
properties <test00.d3 >test00.outprop

# ----- parallel -----
cp test00.d12 INPUT
mpirun --output-filename OUTPUT Pcrystal
cp OUTPUT.1.0 $launchdir/test00.out-para
cp test00.d3 INPUT
mpirun --output-filename OUTPUTP Pproperties
cp OUTPUTP.1.0 $launchdir/test00.outprop-para
 
echo Files on scratch:
ls -l $scratch
```

### Mopac 7
Mopac7 is present in the Debian repository. No module is needed. Mopac is a serial code.
Input file must have the .dat extension. Example:
```
run_mopac H2O
```

### Gamess-US
Installed version: 2014-12-05 R1. Example of use in a job script (rungms is limited to max 4 CPU cores!):
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module purge
module load intel/xe2011 gamess/2014R1
#======================================================================
rungms C60 00 4  >C60.out                 # C60.dat, 00=version, 4=ncpus
cp /local_scratch/$USER/C60.dat .
```

### Molpro
Installed versions: 2010.1-8. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module purge
module load molpro/2010.1-8
#======================================================================
molpro -W /local_scratch/$USER/wfu -n 4 C60.com     # on 4 CPUs
```

### Orca
Installed versions: 4.0.0. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module purge
module load openmpi/2.0.1-gnu orca/4.0.0
#======================================================================
$ORCAPATH/orca C60.inp >C60.out     # always run using $ORCAPATH!
```

## Full potential linearized augmented plane wave codes
### Exciting FLAPW
Installed version: boron (5). Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N NaCl
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module purge
module load load intel/xe2011 openmpi/1.8.3-intel exciting/5
#======================================================================
ln -s $EXCTITINGROOT/species .
mpirun $EXCITINGROOT/bin/excitingmpi              # input file is input.xml
```

### ELK FLAPW
Installed version: 3.0.18, 3.1.12, 3.3.17. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N NaCl
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module purge
module load load intel/xe2011 elk/3.0.18
#======================================================================
ln -s $ELKROOT/species .
export OMP_NUM_THREADS=$SLURM_NTASKS
elk                                               # input file is elk.in
```

## Other codes
### Yambo (GW, TDDFT for molecules and solids)
Installed versions: 3.4.1-rev61, 4.1.2-rev120. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
#scratch=/scratch/$USER/${PWD#$HOME}            # to save files on the global scratch (slow)
scratch=/local_scratch/$USER/${PWD#$HOME}       # to save files on the global scratch (fast)
#======================================================================
module purge
module load intel/xe2015 openmpi/1.8.3-intel yambo/3.4.1-rev61
#======================================================================
mpirun yambo ....
```

### MolGW (molecular GW, TDDFT and BSE)
Installed versions: 1.b. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testC60
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module purge
module load intel/xe2015 openmpi/1.8.3-intel molgw/1.b
#======================================================================
mpirun molgw h2o_gw_bse.in >h2o_gw_bse.out
```

### Casino (Quantum Monte Carlo)
Installed versions: 2.12.1. Example of use in a job script:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N testQMC
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=4
#PBS -q parallel
#======================================================================
module purge
module load intel/xe2015 openmpi/1.8.3-intel casino/2.12.1
#======================================================================
mpirun casino   # input file is 'input', 'gwfn.data', 'correlation.data'
```


**Important: do not use the `runqmc` launcher. It's not supported on morpheus**

### XD
Installed versions: 2006 and 2016.01. **XD2006 can be used only on the
master node or with the calcolo queue, in serial**. XD2016.01 can be used
on any node. Example of use in a job script (XD2006)
```bash
#!/bin/bash --login
#======================================================================
#PBS -N test_xd
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=1
#PBS -q calcolo
#======================================================================
module load xd/2006
export XD_DATADIR=$XD_ROOT/lib/xd.`cat /etc/hostname`   # don't change!
#======================================================================
xdprop CE30LT
...
```
Example of use in a job script (XD2016.01, **note the extra commands
after loading the module**):
```bash
#!/bin/bash --login
#======================================================================
#PBS -N test_xd
#PBS -l walltime=00:30:00
#PBS -l nodes=1:ppn=1
#PBS -q calcolo
#======================================================================
module load xd/2016.01
cp -r $XD_DATADIR /local_scratch/$USER                  # don't change!
export XD_DATADIR=/local_scratch/$USER/xd               # don't change!
#======================================================================
xdlsm re175
...
```


### Gollum (Quantum transport)
Installed versions: 1.1. Gollum cannot be run from within a job script
because the stupid Matlab Compiler Runtime (MCR) tries to open an X11 connection.
I'm working to find a solution.
```
module load gollum/1.1
run_gollum.sh
```
You don't need to specify the MCR path as the first argument.


### Multiwfn
Installed version: 3.4.1. **It must be run from the master node**
```
module load multiwfn
Multiwfn          # with GUI
Multiwfn-nogui    # without GUI
```

