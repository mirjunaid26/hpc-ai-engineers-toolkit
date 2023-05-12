# HPC & Linux Toolkit
Instead of just searching and fixing bugs, I have decided to keep a record errors and the respective solutions.

## Linux
### L1. To deactivate `auto_autoactivate_conda` which displays `(base)` infront of the username. 
```
conda config --set auto_activate_base False
source ~/.bashrc
```


### L2. Configuring ssh config file
An ssh config file is a text file that contains all of your ssh connection information. This includes the hostname of the server you’re connecting to, the username you’re using to connect, the port number, and the protocol you want to use. You can also specify a key file to use for authentication, as well as other options.
```
vi .ssh/config
```
## CONDA Cheatsheet

### Conda Basics
C1. Verif conda is installed, check version number
```
conda info
```
C2. Update conda to the current version
```
conda update conda
```

