# **Supercomputing Center, Ecole Centrale Nantes**




![bg left:40% 80%](https://supercomputing.ec-nantes.fr/wp-content/uploads/2017/12/IMG_6830-1024x683.jpg)


## HPC Toolkit



NEW IDEAS
1. Poll the users: Send a survey email to the users with a few questions that help us better understand their struggles and we can design courses and help them accordingly. Which tools and softwares do they use or plan to use?
1. Workshop in ECN or offer a course in High Performance Computing.
2. We can also conduct a regional workshop in 2023-24 session.
3. Montly blog posts about Cluster and new code demonstration.
4. Video Tutorials/Animations  
5. Voice over Google Slides for Presentation


- Create a list of milestones and 
- Compile course content, materials, and resources
----------------------------------------------------------------------------------------------------------------------------------------

CONTENTS

1. Connect by SSH
2. Basic Linux Commands
3. SLURM
4. Apptainer/Singularity Containers
5. Python/Numba

### 1. Connect to SUPERCOMPUTER via SSH


To access the Supercomputer, you will need an SSH (secure shell) client, a piece of software for establishing secure connections to remote machines.

On MacOS and Linux, the default terminal application has such a client built-in.

On Windows 10 machines, there is also an SSH-enabled client. You might need to download and configure some things.

If you have already requested for an account, you will find your username in the account creation confirmation email. If not get in touch cnsc-tech@ec-nantes.fr

Open a terminal and SSH as shown below

```
ssh username@liger-ec-nantes.fr
```

### 3. SLURM/CLAM

1. How to use SLURM to submit jobs on the cluster?
2. How to use CLAM to monitor usage and jobs?


- Understanding SLURM: SLURM (Simple Linux Utility for Resource Management) is a popular job scheduling and workload management system used in many high-performance computing environments. SLURM allows users to submit and manage jobs on a cluster of computers. It provides a framework for allocating resources (such as CPU cores, memory, and GPUs) and scheduling jobs efficiently.
- Logging in: To use SLURM, you need access to a cluster where SLURM is installed. Log in to the cluster using SSH or any other method provided by your system administrator.
- Logging in: To use SLURM, you need access to a cluster where SLURM is installed. Log in to the cluster using SSH or any other method provided by your system administrator.

### 4. Apptainer/Singularity Containers

Live Demonstration on the New Cluster(90 minutes session)

1. What are containers and why do we need them?
2. Downloading and using and already existing conatiner.
3. Creating a container from scratch.
4. How to use containers for reproducible research?
5. Record the video and share on Glicid platform/docs.

### 5. JupyterLab and Jupyter Notebook Tutorial

### 6. Python/Numba
Examples and code demos

HOW TO SUBMIT PYTHON SCRIPT ON THE CLUSTER.

Demonstrate the power of Numba/Python. Why use HPC?

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


## CONTENTS


# Connect by SSH



# 1. BASIC LINUX COMMANDS
# 2. SLURM
# 3. APTTAINERS/SINGULARITY CONTAINERS
# 4. Python

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

Python is slow but Numba makes it faster.
Example: Matrix Multiplication
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
