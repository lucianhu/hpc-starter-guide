# Slurm commands

| Command                  | Example                          | Description                                           |
|--------------------------|----------------------------------|-------------------------------------------------------|
| my-accounts              | `$ my-accounts`                  | Show your Slurm accounts.                             |
| sacct                    | `$ sacct`                        | Show details about your recent jobs.                  |
| sbatch                   | `$ sbatch slurm_script.sh`       | Submit a batch job.                                   |
| scancel                  | `$ scancel --me` (all jobs)      | Cancel all jobs                                       |
|                          | `$ scancel <jobID>` (single job) | Cancel a single job.                                  |
| scontrol                 | `$ scontrol --help` (all options)| Show all options for scontrol.                        |
|                          | `$ scontrol show job <jobID>`    | Show details of a specific job.                       |
| sinfo                    | `$ sinfo` (general)              | Show general information about the cluster.           |
|                          | `$ sinfo -o '%11P %5D %22N %4c %21G %7m %11l'` | Show detailed information about the cluster.  |
| sinteractive             | `$ sinteractive` (CPU only)     | Submit an interactive job (CPU only).                 |
|                          | `$ sinteractive --gres=gpu:<numGPUs>` | Submit an interactive job with GPUs.           |
| squeue                   | `$ squeue` (all jobs)            | Monitor all jobs.                                     |
|                          | `$ squeue --me` (your jobs)      | Monitor your jobs.                                    |
| time-until-maintenance   | `$ time-until-maintenance`       | Show upcoming maintenance windows.                    |

