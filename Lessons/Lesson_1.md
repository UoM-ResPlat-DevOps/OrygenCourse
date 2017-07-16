-- *Slide* --
### Part 0: Goals for today
* Part 1: Supercomputers, Spartan, and Accounts.
* Part 2: Environment Modules and Job submission system.
* Part 3: Slurm Sample Jobs and Command Summary
* Part 4: Workshopping Your Examples
-- *Slide End* --

-- *Slide* --
### Part 0: Slide Respository
* A copy of the slides and same code is available at: https://github.com/UoM-ResPlat-DevOps/OrygenCouse
* A copy of information about HPC at the University of Melbourne is available at https://dashboard.hpc.unimelb.edu.au
* Also see `man spartan` on the cluster and the `/usr/local/common/` directories - more on that later.
-- *Slide End* --

-- *Slide* --
### Part I: Helpdesk
* If a user has problems with submitting a job, needs a new application or extension to an existing application installed, if their submissions are generated unexpected errors etc., an email can be sent to: `hpc­-support@unimelb.edu.au`. 
* Do not email individual sysadmins. Be informative about the error or issue.
-- *Slide End* --

-- *Slide* --
### Part 1: Supercomputers and High Performance Computers
* A "supercomputer" means any single computer system that has exceptional processing power for its time. 
* One popular metric (LINPACK) is the number of floating­ point operations per second (FLOPS) such a system can carry out (http://top500.org). HPC Challenge is a broader, more interesting metric.
* High Performance Computer (HPC) is any computer system whose architecture allows for above average performance.
-- *Slide End* --

-- *Slide* --
### Part 1: More on High Performance Computing 
* The command­ line interface provides a great deal more power and is very resource efficient. 
* GNU/Linux scales and does so with stability and efficiency.
* The operating system and many applications are provided as "free and open source" which are better placed to improve, optimize and maintain.
* Application software is typically installed from sourcecode.
-- *Slide End* --

-- *Slide* --
### Part 1: Clusters and Scientific Computing
* Clustered computing is when two or more computers serve a single resource. This improves performance and provides redundancy in case of failure system. Typically commodity systems with a high-speed local network.
* Scientific (or research) computing is the software applications used by the scientific community to aid research. Does not necessarily equate with high performance computing, or the use of clusters.­ It is whatever scientists use and do. Not issues of producibility and environments.
-- *Slide End* --

-- *Slide* --
### Part 1: Parallel Computing
* Cluster computing with data parallelism: The horse and cart example.
* With a cluster architecture, applications can be more easily parallelised across them. Parallel computing refers to the submission of jobs or processes over multiple processors and by splitting up the data or tasks between them.
* Further examples of serial versus parallel; random number generation, driving a car, weather forecasting, aerodynamic design, fluid mechanics, radiation modelling, molecullar dynamics, CGI rendering for popular movies, etc. Reality is a parallel system!
-- *Slide End* --

-- *Slide* --
### Part 1: Generic HPC Cluster Design
<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanIntro/master/Images/genericcluster.png" />
-- *Slide End* --

-- *Slide* --
### Part 1: What's Different About Spartan?
* New system is Spartan (not Æthelstan or Ælfweard).
* Recommended solution was to make use of existing NeCTAR Research cloud with an expansion of general cloud compute provisioning and use of a smaller "true HPC" system on bare metal nodes.
* Also uses departmental and project specific partitions, plus a special transfer node for data.
-- *Slide End* --

-- *Slide* --
### Part 1: Spartan Design
<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanIntro/master/Images/spartanlayout.png" />
-- *Slide End* --

-- *Slide* --
### Part I: Logging In
* Spartan uses an authentication that is tied to the university Security Assertion Markup Language (SAML). The login URL is `https://dashboard.hpc.unimelb.edu.au/karaage`
* Users on Spartan must belong to a project. Projects must be led by a University of Melbourne researcher (the "Principal Investigator") and are subject to approval by the Head of Research Compute Services. 
* Participants in a project can be researchers or research support staff from anywhere.
-- *Slide End* --

-- *Slide* --
### Part I: Logging In
* To log on to a HPC system, you will need a user account and password and a Secure Shell (ssh) client. Linux distributions almost always include SSH as part of the default installation as does 
Mac OS 10.x. For MS-­Windows users, the free PuTTY client is recommended (http://putty.org). 
* To transfer files use scp, WinSCP, Filezilla (https://filezilla-project.org/), or rsync.
* Example login: `lev@spartan.hpc.unimelb.edu.au`
* Consider using an `.ssh/config` flile!
-- *Slide End* --

-- *Slide* --
### Part I: SSH Keys, Config, Data Transfers
* SSH Keys will make your life easier. Follow the instructions here: `http://www.linuxproblem.org/art_9.html`
* An `.ssh/config` flile will make your life easier too!
* Both useful for data transfers. c.f., `https://dashboard.hpc.unimelb.edu.au/managing_data/` 
-- *Slide End* --

-- *Slide* --
### Part 2: Environment Modules I
* Environment modules provide for the dynamic modification of the user's environment via module files, such as the location of the application's executables, its manual path, the library path, and so forth
* Modulefiles also have the advantages of being shared on many users on a system (such as an HPC system) and easily allowing multiple installations of the same application but with different versions and compilation options.
-- *Slide End* --

-- *Slide* --
### Part 2: Environment Modules  II
* The are two implementations of environment modules. The classic modules system is available on the Edward HPC, and the newer Lmod is on Spartan. LMod is considered superior for hierarchies of modules.
-- *Slide End* --

-- *Slide* --
### Part 2: Module Commands I
| Command                       | Explanation                                            |
|-------------------------------|:------------------------------------------------------:|
| `module avail`                | Lists all the modules which are available to be loaded.|
| `module display <modulefile>` | Display paths etc for modulefile                       |
| `module load <modulefile>`    | Loads paths etc to user's environment                  |
| `module unload <modulefile>`  | Unloads paths etc from user's environment.             |
| `module list`                 | lists all the modules currently loaded.                |
| `module purge`		| Remove all existing modules				 |
-- *Slide End* --

-- *Slide* --
### Part 2: Module Commands II
* Modules load other other modules; try `module purge; module load module load MRtrix/0.3.14-intel-2016.u3-Python-2.7.11; module avail`
* There is also the `module switch <modulefile1> <modulefile2>`, which unloads one modulefile (modulefile1) and loads another (modulefile2).
* On Spartan there is also the lmod-specific `module spider modulename`, which traverses through the system for modules available for the user to load.
-- *Slide End* --

-- *Slide* --
### Part 2: Portable Batch System
* The Portable Batch System (or simply PBS) is a utility software that performs job scheduling by assigning unattended background tasks expressed as batch jobs, among the available resources.
* Originally developed by MRJ Technology Solutions under contract to NASA in the early 1990s. Released as an open-source product as OpenPBS. Forked by Adaptive Computing as TORQUE (Terascale Open-source Resource and QUEue Manager). Many of the original engineering team now part of Altair Engineering who have their own commercial version, PBSPro. TORQUE is used on the old UniMelb Edward HPC system.
-- *Slide End* --

-- *Slide* --
### Part 2: Slurm
* Slurm, used on Spartan, began development as a collaborative effort primarily by Lawrence Livermore National Laboratory, SchedMD, Linux NetworX, Hewlett-Packard, and Groupe Bull as a Free Software resource manager. As of November 2015, TOP500 list of most powerful computers in the world indicates that Slurm is the workload manager on six of the top ten systems. Slurm's design is very modular with about 100 optional plugins.
* There is a repository for converting PBS to SLURM: https://github.com/bjpop/pbs2slurm
-- *Slide End* --

-- *Slide* --
### Part 2: Job Submission Principles
* The steps for job submission are (a) setup and launch., (b) monitor., and (c) retrieve results and analysis. 
* Jobs are launched from the login node with resource requests and, when the job scheduler decides, run on compute nodes. Some directories (e.g.,. user home or project directories) are shared across the entire cluster so output is accessible.
* A cluster is a shared environment thus a a resource requesting system. Policies ensure that everyone has a "fair share" to the resources (e.g., user processor limits).
-- *Slide End* --

-- *Slide* --
### Part 2: DON'T RUN JOBS ON THE LOGIN NODE!
* The login node is a **particularly** shared resource. All users will access the login node in order to check their files, submit jobs etc. If one or more users start to run computationally or I/O intensive tasks on the login node (such as forwarding of graphics, copying large files, running multicore jobs), then that will make operations difficult for everyone.
-- *Slide End* --

-- *Slide* --
<img src="http://levlafayette.com/files/rabbitjobs.png" width="100%" height="100%" title="Job submission using rabbits" />
* From the IBM 'Red Book' on Job Submission.
-- *Slide End* --

-- *Slide* --
### Part 2: Partitions and Queues
* Setup and launch consists of writing a short script that initially makes resource requests 
(walltime, processors, memory, queues) and then commands (loading modules, changing 
directories, running executables against datasets etc), and optionally checking queueing system.
* Core command for checking paritions is `sinfo -s`, or `sinfo -p` for partition and node status.
* Core command for checking queue `squeue` or `showq` (on Spartan).
-- *Slide End* --

-- *Slide* --
### Part 2: Job Status
* Core command for job submission `sbatch [jobscript]` 
* Core command for checking job `squeue -j [jobid]`, detailed command `scontrol show job [jobid]` (SLURM), or all user's jobs `squeue -u [username]`.
* Core command for deleting job `scancel [jobid]`
-- *Slide End* --

-- *Slide* --
### Part 3: Single Core Job
`#!/bin/bash`<br />
`#SBATCH -­p cloud`<br />
`#SBATCH ­­--time=01:00:00`<br />
`#SBATCH ­­--ntasks=1`<br />
`module load my­app­compiler/version`<br />
`my­app data`<br />
* Examples at `/usr/local/common/MATLAB` and `/usr/local/common/R`; note that the job can call other scripts.
-- *Slide End* --

-- *Slide* --
### Part 3 : Multicore and Multithreaded Jobs
* In Slurm, `ntasks` means number of tasks, whereas `cpus-per-task` allocates processor cores. In most jobs (serial, MPI) this is 1 by default.
* With shared-memory multithreaded jobs on (e.g., OpenMP), modify the `--cpus-per-task` to a maximum of 8, which is the maximum number of cores on a single cloud VM (or 12 for physical).<br />
`#SBATCH ­­--cpus-­per-­task=8`
* See examples at `/usr/local/common/FSL/`
-- *Slide End* --

-- *Slide* --
### Part 3 : Multinode Jobs I
* For distributed-memory multicore job using message passing, the multinode partition has to be 
invoked and the resource requests altered e.g.,
`#!/bin/bash`<br />
`#SBATCH -­p physical`<br />
`#SBATCH ­­--nodes=2`<br />
`#SBATCH ­­--ntasks-per-node=8`<br />
`module load my­app­compiler/version`<br />
`srun my­mpi­app`

### Part 3 : Multinode Jobs II
* Multinodes jobs should be run on the `physical` partition which has the higher interconnect speed.
* Multinode jobs on Spartan may be slower if they have a lot of interprocess communication and they cross compute nodes.
* This said, multinodes jobs can also request total tasks/cores rather than allocating them per node. e.g., `#SBATCH ­­--ntasks=16`<br />
* See examples at `/usr/local/common/Python`
-- *Slide End* --

-- *Slide* --
### Part 3 : Job/Batch Arrays
* With a job or batch array the same batch script, and therefore the same resource requests, is used multiple  times to launch subjobs. A typical example is to apply the same task across multiple datasets. An array task range is set, which established a Slurm variable which can be invoked into filenames etc.
* Examples at `/usr/local/common/array` and `/usr/local/common/Octave`
-- *Slide End* --

-- *Slide* --
### Part 3 : Job/Batch Dependencies
* A dependency condition is established on which the launching of a batch script depends, creating a conditional pipeline. The dependency directives consist of `after`, `afterok`, `afternotok`, `before`, `beforeok`, `beforenotok`. A typical use case is where the output of one job is required as the input of the next job.<br />
`#SBATCH ­­dependency=afterok:myfirstjobid mysecondjob`
* Examples at `/usr/local/common/depend/`
-- *Slide End* --

-- *Slide* --
### Part 3: Interactive Jobs
* An interactive job, based on the resource requests made on the command  line, puts the user on to a compute node. This is typically done if they user wants to run a  large script (and shouldn't do it on the login node), or wants to test or debug a job. The  following command would launch one node with two processors for twenty minutes.<br />
`sinteractive ­­nodes=1 ­­ntasks­per­node=2 ­­time=0:10:0`
* Handy for x-windows forwarding; go to login node with `-Y` (secure) and follow example at `/usr/local/common/interact`. See also FreeSufer example at `/usr/local/common/FreeSurfer` 
-- *Slide End* --

-- *Slide* --
### Part 3: Slurm User Commands

| User Commad    | Slurm Command           | 
|----------------|------------------------:|
|Job submission  |sbatch [script_file]     |
|Job delete      |scancel [job_id]         |
|Job status      |squeue [job_id]          |
|Job status      |squeue -u [user_name]    |
|Node list       |sinfo -N                 |
|Queue list      |squeue                   |
|Cluster status  |sinfo               	   |
-- *Slide End* --

-- *Slide* --
### Part 3: Slurm Job Job Commands
| Job Specification     | Slurm Command              | 
|-----------------------|---------------------------:|
|Script directive       |`#SBATCH`                   |
|Queue                  |`-p [queue]`                |
|Job Name               |`--job-name=[name]`         |
|Nodes                  |`-N [min[-max]]`            |
|CPU Count              |`-n [count]`                |
|Wall Clock Limit       |`-t [days-hh:mm:ss]`        |
|Event Address          |`--mail-user=[address]`     |
|Event Notification     |`--mail-type=[events]`      |
|Memory Size            |`--mem=[mem][M|G|T]`        |
|Proc Memory Size       |`--mem-per-cpu=[mem][M|G|T]`|
-- *Slide End* --

-- *Slide* --
### Part 3: Slurm Environment Commands
| Environment Command   | Slurm (Command)         | 
|-----------------------|------------------------:|
|Job ID                 |`$SLURM_JOBID`           |
|Submit Directory       |`$SLURM_SUBMIT_DIR`      |
|Submit Host            |`$SLURM_SUBMIT_HOST`     |
|Node List              |`$SLURM_JOB_NODELIST`    |
|Job Array Index        |`$SLURM_ARRAY_TASK_ID`   |
-- *Slide End* --

-- *Slide* --
<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanIntro/master/Images/hypnotoad.png" width="150%" height="150%" />
-- *Slide End* --
