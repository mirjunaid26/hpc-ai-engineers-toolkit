# HPC Toolkit - ECN Supercomputing Center



## CONTENTS


# Connect by SSH



# 1. BASIC LINUX COMMANDS
# 2. SLURM
# 3. APTTAINERS/SINGULARITY CONTAINERS
# 4. Python


--------------------------------------------------------------------------------------------------------------------------------------------
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
