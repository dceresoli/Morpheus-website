+++
date = "2016-12-26T10:25:35+01:00"
title = "Modules"
categories = [ "software" ]
tags = [ "document" ]
+++
### Introduction
A number of compilers, libraries and software is available through the
<code>module</code> command. A sequence of module commands can be
included in your <code>.bash_profile</code> and in job submission
scripts.

### <code>module avail</code>: list available modules
```bash
$ module avail
------------ /opt/modules/compilers ------------ 
intel/xe2011         openmpi/1.10.3-gnu   openmpi/2.0.1-intel  
intel/xe2015         openmpi/1.10.3-intel openmpi/2.0.1-pgi    
intel/xe2016         openmpi/1.8.3-gnu    pgi/2016             
intel/xe2017         openmpi/1.8.3-intel  
openmpi/1.10.1-gnu   openmpi/2.0.1-gnu    
------------ /opt/modules/software ------------ 
abinit/7.10.4      exciting/5         julia/0.5.0        siesta/4.0         
anaconda2          g09/A.01           lammps/20150815    siesta/4.1-b1      
bader/0.95         g09/C.01           molpro/2010.1-8    siesta/4.1-b3      
casino/2.12.1      g09/D.01           openmx/3.8         siesta/ldau-308    
critic/2           g09/E.01           orca/3.0.3         siesta/smeagol-1.2 
crystal/13         gamess/2014R1      qbox/1.63.2        siesta/trunk-462   
crystal/13+16      gulp/4.0           qe/5.1.2           tinker/7.1.3       
crystal/14         inelastica/351     qe/5.2.0           uspex/9.4.4        
elk/3.0.18         julia/0.3.11       qe/5.2.1           vasp/5.3.3         
elk/3.1.12         julia/0.4.2        qe/5.3.0           xd/2006            
elk/3.3.17         julia/0.4.6        siesta/3.2-pl5     yambo/3.4.1-rev61  
```

#### <code>module list</code>: list currently loaded modules
```bash
$ module list
Currently Loaded Modulefiles:
 1) intel/xe2011         2) openmpi/1.8.3-intel 
```

### <code>module load</code>, <code>module unload</code>: load or unload a module
This command will report conflicting modules:
```bash
$ module unload intel/xe2011 openmpi/1.8.3-intel
$ module load openmpi/1.8.3-gnu
$ module load openmpi/1.8.3-intel
WARNING: openmpi/1.8.3-intel cannot be loaded due to a conflict.
HINT: Might try "module unload openmpi" first.
```

### <code>module display</code>: display details of a module
```bash
$ module display openmpi/1.8.3-gnu
-------------------------------------------------------------------
/opt/modules/openmpi/1.8.3-gnu:

conflict	openmpi
prepend-path	PATH	/opt/openmpi-1.8.3-gnu/bin	:
prepend-path	LD_LIBRARY_PATH	/opt/openmpi-1.8.3-gnu/lib	:
prepend-path	MANPATH	/opt/openmpi-1.8.3-gnu/share/man	:
-------------------------------------------------------------------
```

### <code>module purge</code>: clean the list of loaded modules
```bash
$ module purge
```
