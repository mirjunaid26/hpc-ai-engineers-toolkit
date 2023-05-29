# **Supercomputing Center, Ecole Centrale Nantes**




![bg left:40% 80%](https://supercomputing.ec-nantes.fr/wp-content/uploads/2017/12/IMG_6830-1024x683.jpg)


## HPC Toolkit


        _   _ ____   ____   _____      _             _       _
       | | | |  _ \ / ___| |_   _|   _| |_ ___  _ __(_) __ _| |___
       | |_| | |_) | |       | || | | | __/ _ \| '__| |/ _` | / __|
       |  _  |  __/| |___    | || |_| | || (_) | |  | | (_| | \__ \
       |_| |_|_|    \____|   |_| \__,_|\__\___/|_|  |_|\__,_|_|___/

               Copyright (c) 2023-2023 Supercomputing Center ECN


CONTENTS

1. Connect by SSH
2. Basic Linux Commands
3. SLURM/CLAM
4. Jupyter Notebook/JupyterLab/Google Colab
5. Apptainer/Singularity Containerization
6. Parallel Programming(CUDA Python/Numba/C++)
7. HPC for AI

### 1. Connect to SUPERCOMPUTER via SSH


To access the Supercomputer, you will need an SSH (secure shell) client, a piece of software for establishing secure connections to remote machines.

On MacOS and Linux, the default terminal application has such a client built-in.

On Windows 10 machines, there is also an SSH-enabled client. You might need to download and configure some things.

If you have already requested for an account, you will find your username in the account creation confirmation email. If not get in touch cnsc-tech@ec-nantes.fr

Open a terminal and SSH as shown below

```
ssh username@liger-ec-nantes.fr
```
--------------------------------------------------------------------------------------------------------------------------------------
### 3. SLURM

SLURM (Simple Linux Utility for Resource Management) is a popular job scheduling and workload management system used in many high-performance computing environments. SLURM allows users to submit and manage jobs on a cluster of computers. It provides a framework for allocating resources (such as CPU cores, memory, and GPUs) and scheduling jobs efficiently.
- Logging in: To use SLURM, you need access to a cluster where SLURM is installed. Log in to the cluster using SSH or any other method provided by your system administrator.
- Job Script: Create a job script that describes the resources required for your job and the commands to be executed. A typical SLURM job script is a shell script with special directives recognized by SLURM. Here's an example job script:
```
#!/bin/bash
#SBATCH --job-name=myjob
#SBATCH --output=output.txt
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=4

# Commands to run
echo "Hello, World!"

```
In this example, the job script specifies the job name, the output file name, the number of nodes, and the number of tasks per node. The last line is a sample command to print "Hello, World!".

- Submitting a Job: Use the sbatch command to submit your job script to SLURM:
```
sbatch job_script.sh

```
This will submit your job to the SLURM scheduler for execution.

- Checking Job Status: You can check the status of your jobs using the squeue command:
```
squeue -u your_username
```
This will display information about your jobs, such as job ID, job name, status, and other details.

- Managing Jobs: You can cancel a running job using the scancel command followed by the job ID:
```
scancel job_id
```

- To view detailed information about a specific job, including its resource usage, use the scontrol command:
```
scontrol show job job_id
```

- Job Output: By default, SLURM captures the standard output and standard error of your job in a file. In the job script example, the output is redirected to output.txt. After the job finishes, you can examine this file to see the job's output.
-----------------------------------------------------------------------------------------------------------------------------------------------

### 4. CLAM
--------------------------------------------------------------------------------------------------------------------------------------
### 5. Apptainer/Singularity Containers

Live Demonstration on the New Cluster(90 minutes session)

1. What are containers and why do we need them?
2. Downloading and using and already existing conatiner.
3. Creating a container from scratch.
4. How to use containers for reproducible research?
5. Record the video and share on Glicid platform/docs.

### 6. JupyterLab and Jupyter Notebook Tutorial
--------------------------------------------------------------------------------------------------------------------------------------

### 7. Parallel Programming (CUDA Python/Numba/C++)


# Matrix Multiplication

```
import numpy
def dot(a, b):
    """Multiply the matrix a with the matrxi b.
    
    Parameters
    ----------
    a: ndarray
        left matrxi
    b: ndarray
        right matrix
        
    Return
    ------
    c: ndarray
        result matrix
    """
    c = numpy.zeros((a.shape[0], b.shape[1]))
    for i in range(a.shape[0]):
        for j in range(b.shape[1]):
            for k in range(a.shape[1]):
                c[i, j] += a [i, k] * b[k, j]
    return c

```
# Let's two small matrices and see how long the above function takes to conpute matrix multiplication.
```
n = 256
a = numpy.random.random((n, n))
b = numpy.random.random((n, n))

t_dot = %timeit -o dot(a, b)
```

# A matrix multiplication of two n by n matrices performs 2n^3 operations. The dot function achieves
```
print("%.3f GFLOP/s" % (2e-9 * n**3 / t_dot.best))
```

That's why they tell is Python is slower.

Luckily, we have Numba, an open source JIT compiler that translates a subset of Python and NumPy code into fast machine code.

Numba makes Python code fast.
```
from numba import jit
jdot = jit(dot)

t_jit = %timeit -o jdot(a, b)

print("%.3f GFLOP/s" % (2e-9 * n**3 / t_jit.best))
```
--------------------------------------------------------------------------------------------------------------------------------------


# Debugging

While working as AI/HPC Research Engineer, there are number of errors and bugs that I encounter on daily basis related to Linux, HPC tools, Containers, and Python programming. I have decided to pen them down on a git repo with the respective solutions...

## LINUX
**L1**. To deactivate `auto_autoactivate_conda` which displays `(base)` infront of the username.

```
conda config --set auto_activate_base False
source ~/.bashrc
```


**L2**. Configuring ssh config file
An ssh config file is a text file that contains all of your ssh connection information. This includes the hostname of the server you’re connecting to, the username you’re using to connect, the port number, and the protocol you want to use. You can also specify a key file to use for authentication, as well as other options.
```
vi .ssh/config
```
## SINGULARITY

## APPTAINER: THE CONTAINER SYSTEM FOR HIGH PERFORMANCE COMPUTING
Apptainer/Singularity is the most widely used container system for HPC. It is designed to execute applications at bare-metal performance while being secure, portable, and 100% reproducible. Apptainer is an open-source project with a friendly community of developers and users. The user base continues to expand, with Apptainer/Singularity now used across industry and academia in many areas of work.

## CONDA
### Conda Basics
**C1**. Verify conda is installed, check version number
```
conda info
```
**C2**. Update conda to the current version
```
conda update conda
```
**C3**. Install a package included in Anaconda
```
conda install PACKAGENAME
```
## PYTHON
