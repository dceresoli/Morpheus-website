+++
date = "2016-12-26T10:25:35+01:00"
title = "Queuing system"
categories = [ "queuing system" ]
tags = [ "document" ]
+++
### Introduction
Morpheus uses the <code>slurm</code> queuing system with a PBS compatibility plugin, so that you have
the choice of using the legacy PBS commands (<code>qsub, qstat, qdel, ...</code>) or the SLURM commands
(<code>sbatch, squeue, scancel, ...</code>)

### SLURM job management
```
sbatch job_script                     submit a job
squeue                                show the queue status
scancel job_id                        delete a job
sview                                 open GUI with cluster status
```

### PBS job managmement
```
qsub job_script                       submit a job
qstat                                 show the queue status
qdel job_id                           delete a job
sview                                 open GUI with cluster status
```

### Current queue configuration
- debug: 1 hour, max 1 CPU, running on the master node
- parallel: 7 days, max 4 CPUs
- calcolo: **reserved** 7 days, max 4 CPUs
- samsung: **reserved** 7 days, max 8 CPUs

