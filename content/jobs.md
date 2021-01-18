+++
date = "2016-12-26T10:25:35+01:00"
title = "Job scripts"
categories = [ "queuing system" ]
tags = [ "document" ]
+++
### Using SLURM
Example job script asking for 4 CPUs on the parallel queue:
```bash
#!/bin/bash --login
#======================================================================
#SBATCH -J job_name
#SBATCH --nodes=1 --ntasks=4
#SBATCH --time=00:30:00
#SBATCH --partition parallel
#======================================================================
module load ...
mpirun ...
```

### Using PBS
Example job script asking for 4 CPUs on the parallel queue:
```bash
#!/bin/bash --login
#======================================================================
#PBS -N job_name
#PBS -l nodes=1:ppn=4
#PBS -l walltime=00:30:00
#PBS -q parallel
#======================================================================
# don't cd $PBS_O_WORKDIR!!
module load ...
mpirun ...
```
Note that in other cluster you need to <code>cd $PBS_O_WORKDIR</code>. On
morpheus it is unnecessary.
