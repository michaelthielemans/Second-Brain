## What is a virtual environment VENV

this is a location where you can run a python interpreter , all the needed packages and libraries needed for that python application are available in that location(environment).
When creating a new virtual environment, a extra folder will be created where alle the packages will reside .

## pre-requisites for creating a virtual environment

it is possible that you need to install the virtualenv module
```bash
pip3 install virtualenv
```
## Create a python3 virtual environment

```
python3 -m venv /path/to/new/virtual/environment`

-m -> make
venv -> this is the module that will do the creating
path -> the path and name of the directory where all the libraries will be placed
```

## Activating the VENV
```bash
source <venv_dir>/bin/activate
```

The `source` command in Linux is a shell built-in command that executes the commands from a script in the **current shell environment** rather than starting a new subshell. This allows the script to modify the environment variables or other settings of the current shell session.

### **Difference Between `source` and Running a Script Directly**

|**Feature**|**`source` Command**|**Direct Execution (e.g., `./script.sh`)**|
|---|---|---|
|**Environment Variables**|Affects current shell|Does not affect current shell|
|**Subshell**|No|Yes|
|**Script Permissions**|Not required to be executable|Must be executable (`chmod +x`)|
## Check the packages that are available in the venv

```
pip3 list
```

push the packages to the requirements file
```
pip3 freeze > requirements.txt
```

```
pip3 install -r requirments.txt
```

## deactivate the venv
```
deactivate
```