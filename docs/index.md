# Getting Started with Lulu Supercomputers (HPC)

Supercomputers offer immense computing power for demanding tasks, but using them requires some understanding. This guide breaks down the key steps:

## 1. Accessing HPC

* Registration or Proposal Submission: Depending on the specific supercomputer, register for a user account or submit a project proposal for computing resources.
* Logging In: Utilizes SSH to access Login Nodes, typically reserved for users.
* SSH (Secure Shell) keys: Enhances the authentication and security of your SSH connection.
* Moving Data: Common tools include `rsync` for mirroring directories, `scp` for transferring individual files or folders.

## 2. Running Jobs

* Batch Schedulers: HPCuse schedulers to allocate resources for user jobs. These jobs consist of a script detailing commands and required resources (time, memory, processors).
* Job Scripts: Write a job script specifying the tasks (commands) and the resources your application needs. Supercomputer documentation or support resources can help with this.
* Submission and Execution: Submit your job script to the scheduler. It waits for available resources and then runs your job on the allocated hardware. This may involve a delay depending on other users' jobs.

!!! warning 
    Oops! Lulu's system will update sections 3 and 4 soon.

## 3. Modules

* Managing Software: The Module System allows loading specific software packages (compilers, libraries) without manual installation. 
* Module Commands: Use commands like `module list`, `module avail`, `module load/unload`, and `module switch` to interact with the Module System.

## 4. Parallel Programming

* Beyond Single Cores: Modern HPCrely on parallel programming techniques like [OpenMP](https://hpc-wiki.info/hpc/OpenMP) and [MPI](https://hpc-wiki.info/hpc/MPI) to distribute tasks across multiple processors, significantly accelerating execution.

