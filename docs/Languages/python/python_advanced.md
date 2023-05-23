# Python Advanced

[TOC]

# Regular Expressions

## Basic Patterns
### use of `.`
    - matches any character
### use of `*`
    - matches 0 or more repetition of a char/set
### use of `+`
    - matches 1 or more repetition of a char/set
### use of `?`
    - matches 0 or 1 repetition of a char/set
    - also works as a Non-greedy pattern (with repeaters)
        - means in string '<b>Hello</b>' pattern r'<.*>' will match the whole string instead of '<b>'
        - but if pattern is used as r'<.*?>' then will match '<b>' only
        - AKA pcre (Perl Compatible Regular Expression)
### use of `\`
    - sign of speciality
    - used before any special chars, to match that char
### use of `\t`, `\r`, `\n`
    - \t matches a tab
    - \r matches a carriage return (line break) in Mac, \n\r in Windows
    - \n matches a line break ( carriage return) in Linux & Windows
    - note: On "old" printers, \r sent the print head back to the start of the line, and \n advanced the paper by one line. Both were therefore necessary to start printing on the next line.
### use of `\b` (start and end of word anchors)
    - matches the boundary between word and non-word chars
    - matches the position called word boundaries
        - match has zero length
        - usually before (including start of the line) and after a word
        -e.g. <here>apple<here>
### use of `\B`
    - opposite of \b
    - matches every position where \b does not
### use of `\s`
### use of `\d`
### use of `\D`
### use of `\w`
### use of `\W`
### use of `[]`
    - dash - inside []
    - dot . inside []
### use of `()`
### use of `^` (Start of String Anchors)
    - with square bracket (set of chars)
### use of `$` <!--`$`-->  (End of String Anchors)
### use of `|`
### use of syntax (`? ...`)
    - Lookarounds
        - +ve Lookahead
        - -ve Lookahead
        - +ve Lookbehind
        - -ve Lookbehind
    - Non-Capturing Group

## Builtin Functions:
### re.search
### re.group
### re.findall
    - with files
    - with groups
### re.sub
### re.compile
### extra options to above functions


## Examples:
- Repetitions
- Leftmost and largest
- Square Brackets (Set of chars)
    - Email example
- Group Extraction
- Greedy vs Non-Greedy
- Substitution

```python
import re

str = "This#is#$% a&%name%$ #"
r = re.sub(r'(?<=[\w])([\W]+)(?=[\w])', ' ', str)
print(r)
r = re.sub(r'(?<=[A-Za-z0-9])([^A-Za-z0-9]+)(?=[A-Za-z0-9])', ' ', str)
print(r)
r = re.sub(r'q(?=u)', ' ', 'quit')
print(r)
```

- remove white spaces from starting of the line but line break

```python
regex = r'^[^\S\n]+'

#or if regex supports PCRE
regex = r'^[\h]+'
```

Credits:

- https://www.rexegg.com/regex-disambiguation.html#lookarounds
- www.regular-expressions.info




# Multithreading & Multiprocessing

## GIL - Global Interpreter Lock
- Is a mutex (mutual exclusion attribute) in python 
- protects python objects from multiple threads
- i.e. prevents multiple threads to execute python (byte)codes at once inorder to protect access to python objects
- i.e. provides lock to protect shared mutable state
- The lock is necessary because CPython's Interpreter or memory management is not thread safe
    - for example, when two threads simultaneously increment the reference count of the same object, the reference count could end up being incremented only once instead of twice.
- hence, GIL is here to make python thread-safe, wherever needed
- GIL is controversial because due to it python's multithreading lack few features like 
- python's multithreaded codes cannot utilize multiprocessor system
- the longer operations like I/O, image processing happens outside the GIL
- it is only bottleneck for codes which enter GIL for longer time
- GIL can causes scheduling IO-bound threads ahead of a CPU-bound threads
- inshort, GIL is only bad for multi-core CPU - bound thread operations
- each forked process have separate GIL
- Jython, IronPython does not have GIL
- writing a C extension needs GIL
- in Cython the GIL exists, but can be released temporarily using a "with" statement - [read more](https://notes-toransahu.notebooks.azure.com/nb//notebooks/python/Python-Basics.ipynb#with)
- extra: https://stackoverflow.com/questions/1294382/what-is-a-global-interpreter-lock-gil

                                                                                                   
- Note : cython & CPython are different
                                                                                                   
### Some terminologies

#### Concurrency
* When two or more task can start, run & complete in overlapping time periods.
* It doesn't necessarily mean they'll ever be running at the same instant.
* e.g. Multi-tasking on a single core

#### Parallelism
* When two are more tasks are executed simultaneously.

#### process
* is an instance of a program running in a computer 
* can contain one or more threads
* has its independent memory space
* are spawned by creating a Process() object and then calling its start() method

#### thread
* is a sequence of instructions within a process
* as a light-weight process
* all threads shares the same memory space of the process 

<img src="https://www.javamex.com/tutorials/threads/ThreadDiagram.png" alt="process block">


### Multi-threading

* can be implemented to speedup the program using module : **threading**
* thread-based <s>parallelism</s> concurrency
* CPython implementation uses a python construct GIL (global interpreter lock). GIL makes sure that at a time only single thread can execute.
* a thread acquires GIL --> executes just for a while --> passes GIL to next thread
* happens very quickly that human cannot detect, and creates illusion of multiple thread running simultaneously.
* in reality all threads works turn by turn into the same core of CPU
* **parallel CPU computation not possible due to GIL**
* **but parallel IO operations are possible (it releases GIL on IO)**
* GIL passing is an overhead here.

#### Note:
* can turn off GIL - dirty practice
* this will result in messed memory management
* need to be very careful while writting semaphores & mutex properly

#### Use of thread
* in GUI apps to keep UI threads responsive
* IO tasks (network IO or filesystem IO)

#### Facts
* using multiple-threads for CPU bound tasks will result in worse performance than a single thread


### Multi-processing

* used to speedup CPU bound tasks using module: **multiprocessing**
* process-based parallelism
* module results in full CPU utilization
* Inter-process communication can be achieved using **queues and pipes**
*


#### pipe
* is a duplex(two way) communication channel

```python
from multiprocessing import Process

def f(name):
    print('hello', name)

if __name__ == '__main__':
    p = Process(target=f, args=('bob',))
    p.start()
    p.join()
```

Out: hello bob

```python

from multiprocessing import Process
import os

def info(title):
    print(title)
    print('module name:', __name__)
    print('parent process:', os.getppid())
    print('process id:', os.getpid())

def f(name):
    info('function f')
    print('hello', name)

if __name__ == '__main__':
    info('main line')
    p = Process(target=f, args=('bob',))
    p.start()
    p.join()  
```

Out: 

```
main line
module name: __main__
parent process: 65
process id: 66
function f
module name: __main__
parent process: 66
process id: 80
hello bob
```

### What is .join()?
* The join() method, when used with threading or multiprocessing, is not related to str.join()
* it's not actually concatenating anything together
* It just means "wait for this [thread/process] to complete"
* The name join is used because the multiprocessing module's API is meant to look as similar to the threading module's API
* The reason why is called join is that is joining the processes into a single one.

<img src="https://i.stack.imgur.com/IRpP1.jpg">

Note: 
* By default, when the main process is ready to exit, it will implicitly call join() on all running multiprocessing Process instances
* This isn't as clearly stated in the multiprocessing docs as it should be, but it is mentioned in the Programming Guidelines section.
* non-daemonic processes will be automatically be joined.
* can override this behavior by setting the daemon flag on the Process to True prior to starting the process:

```python
from multiprocessing import Process
import os

def say_hello():
    print("Hello")

p = Process(target=say_hello)
p.daemon = True
p.start()

# Both parent and child will exit here, since the main process has completed.
# the child process will be terminated as soon as the main process completes:
```

Out:
Hello

### daemon

**In Linux: A daemon is a long-running background process that answers requests for services.
There are also some other processes like orphan & zombie**

* The process has daemon flag
* a Boolean value
* This must be set before start() is called
* The initial value is inherited from the creating process
* When a process exits, it attempts to terminate all of its daemonic child processes

# Files

## File Handling
- How
    - Using `try`, `except`, `finally` 
    - Using `with` (pythonic way)
- Why
    - to manage resources effeciently
    - file descriptors (fd) are limited at OS level, so we can save fd by closing after use
    
## Using `try`, `except`, `finally`
- the step `finally` is important here for us
    - to use `finally` we need to write whole `try`, `except`, `finally` block in each languages
- `finally` is important because we need `f.close()` here to close the file descriptor with 100% guarantee
- file descriptors (fd) are limited at OS level, so we can save fd by closing after use
- code:
    ```python
    try:
        f = open('csv.txt', 'r', encoding='utf-8')
        f.write('abc')
    except:
        pass
    finally:
        f.close()
    ```    

## Using `with`
- Read [here](https://notes-toransahu.notebooks.azure.com/nb//notebooks/python/Python-Basics.ipynb#with)
- code:
    ```python
    with open('csv.txt', 'r', encoding='utf-8') as f:
        f.readline()
    ```

# JSON Operations
## `import json`
## flask: `jsonify()`


# Shipping Python Solution
- never ship .py files
    - `find /path/to/your/files -type f -name "*.py" -delete`
- can ship .pyc or .pyo files

## .pyc
- compiled
- size(.py) < size(.pyc)

## .pyo
- compiled + optimized
    - removed doc strings
    - does not contain "set the current line to ..." bytecode instructions
    - for faster performance
    - renaming .pyo to .pyc works fine
        - `find "ETHEREAL_DIR"/Ray/src/ -type f -name "*.pyo" -exec bash -c 'mv $0 ${0/.pyo/.pyc}' {} \;`
- size(.pyo) < size(.pyc)
- `python -O -m compileall /path/to/your/files`
- **Note - After this, you may get some import issues**

## .exe
- Source
    - http://docs.python-guide.org/en/latest/shipping/freezing/
    - https://pyinstaller.readthedocs.io/en/v3.3.1/
    
- Note:
    - Freezing Python code on Linux into a Windows executable was only once supported in PyInstaller and later dropped
    - All solutions need MS Visual C++ dll to be installed on target machine, except py2app. Only Pyinstaller makes self-executable exe that bundles the dll when passing --onefile to Configure.py.


### PyInstaller
- Uses the OS support to load the dynamic libraries, thus ensures full compatibility
- available for windows, linux, macOS etc.

```bash
pyinstaller -i <icon.ico> --windowed --onefile <python_file.py>

```

### py2exe

    
# Python Version Management

## Setting default Python Version

### By creating softlink to /usr/bin/python file
- not recommanded
- will affect other applications using another version of python
- can be done like:

```bash
ln -l /usr/bin/python /usr/bin/python3.6

ln -l /usr/bin/python /home/toran/anaconda/bin/python3.6
```

### By aliasing python
- not recommanded
- will conflict when python will encounter in other commands like 
    - which python
    - python manage.py runserver
- can be done like:

```bash
alias python='/home/toran/anaconda/bin/python3.6`
```

### By setting PATH env variable
- recommanded with anaconda
- works on particular shell only
- for persistency; include the command in .bashrc or .zshrc file
- can be done like:

```bash
export PATH="/home/toran/anaconda3/bin:<dollar>PATH"
```


## Anaconda
- install it from official site
- you can also choose miniconda over regular anaconda
    - can be used in production env/ deployments etc.
### Linux    
- set anaconda python as default

    ```bash
    export PATH="/home/toran/anaconda3/bin:<dollar>PATH"
    ```
    
### Windows
- set anaconda python as default

```bash
C:\ProgramData\Miniconda3\Scripts\activate

#if using git bash
. /c/ProgramData/Miniconda3/Scripts/activate
``` 

## virtualenv

## pipenv
- officially recommended dependency management system
- automagically 
    - installs dependencies in venv
    - keep record in Pipfile
        - packages section
        - dev-packages section
    - keeps record of dependencies with specific version in Pipfile.lock file
    - if `requirements.txt` already exists, installs dep from there
    - installs & uninstalls deps

### Installation
```bash
pip install pipenv
```

### Usage

####  create venv
```bash
pipenv install 
```
####  create venv with specific python version
```bash
pipenv --two install 

pipenv --three install 
```

- will initialize the venv with that python version

####  install/uninstall dependencies
```bash
pipenv install nose2

pipenv uninstall nose2
```

####  lock dependencies for production
```bash
pipenv lock
```
- will keep record of all the deps in Pipfile.lock file with their specific versions

####  install dependencies only for development

```bash
pipenv install --dev  nose2
```

- will keep this record in [dev-packages] section
- and will do not install it by default
- to install dev packages; need to do:

```bash
pipenv install --dev
```

####  install dependencies with other options

- `--dev`: Install both develop and default packages from Pipfile.lock.
- `--system`: Use the system pip command rather than the one from your virtualenv.
- `--ignore-pipfile`: Ignore the Pipfile and install from the Pipfile.lock.
- `--skip-lock`: Ignore the Pipfile.lock and install from the Pipfile. In addition, do not write out a Pipfile.lock reflecting changes to the Pipfile. 


#### run command within venv
```bash
pipenv run which python
```

#### remove venv
```bash
pipenv --rm
```

#### see venv details/path
```bash
pipenv --venv
```

#### enter venv shell
```bash
pipenv shell
```

#### clean venv
- uninstall all the packages not recorded in Pipfile

```bash
pipenv clean
```

#### update venv
- locks & then update all the packages

```bash
pipenv update
```

#### security check
- checks for compliance with PEP 508 [Dependency specification for Python Software Packages](https://www.python.org/dev/peps/pep-0508/) as well as package safety

```bash
pipenv check
```

# Python Package Distribution (PyPi)

## Project Structure

There are various guidelines:

- https://packaging.python.org/en/latest/tutorials/packaging-projects/
- https://py-pkgs.org/03-how-to-package-a-python#how-to-package-a-python (A very good read)
- https://docs.python.org/3/reference/import.html#namespace-packages
- https://peps.python.org/pep-0420/

```
/example_pkg
  /pkg1
    __init__.py
  /pkg2
    /pkg2_1
  setup.py
  LICENSE
  README.md

```

where 
- <s>`__init__.py` should contain a variable `name='example_pkg'`</s>
- `setup.py` should look like [this gist](https://gist.github.com/toransahu/669efbb90a5019bb4a766d3c385de90c)
    - where classifiers can be like [this](https://pypi.org/classifiers/) or  [gist](https://gist.github.com/toransahu/bd3bc184bae068c72d6dad7f7c1b0138)
- `README.md` should be present, which will define the `long_description` about  the package
- `LICENSE` should be accurate with the [list](https://choosealicense.com/)
- packages
    - if want to includes all the packages/subpackages
        - use defaultone `packages=setuptools.find_packages(),`
    - else define manually like
        - `packages=['pkg1', 'pkg2', 'pkg2.pkg2_1']`

Note: After installing the package, you able to import packages with names listed in `packages` var.

## Pre-requisites
```bash
#setuptools & wheel - to create build in .whl as well as .tar.gz. format
python3 -m pip install --user --upgrade setuptools wheel


#twine - to upload build in pypi server
python3 -m pip install --user --upgrade twine
```

## Build
- change directory where `setup.py` is  & run

```bash
python3 setup.py sdist bdist_wheel
```

output will be like

```
dist/
  example_pkg-0.0.1-py3-none-any.whl
  example_pkg-0.0.1.tar.gz
```  

## Test Distribution

```bash
twine upload --repository-url https://test.pypi.org/legacy/ dist/*
```


## Final Distribution

```bash
twine upload --repository-url https://upload.test.pypi.org/legacy/ dist/*

#OR

twine upload dist/*
```

## Rebuild
- delete `build`, `dist`, & `*.egg-info` files then build again


## Test 

### (Test) Package
```bash
python3 -m pip install --index-url https://test.pypi.org/simple/ example_pkg
```


### (Final)  Package
```bash
python3 -m pip install example_pkg
```

## Advanced - Run Package in Command Line

Source: http://python-packaging.readthedocs.io/en/latest/command-line-scripts.html


## FAQ
- You're not allowed

- File already exists

- File already exists, change version

- `particular line` is not know/right

# Python Linter & PEP-8
- I found flake8, autopep8 & yapf similar
- but I found black best among them
    - quotes: double
    - no extra line change
    - only draw back is bad list slice formating
        - create issue: https://github.com/python/black/issues

## Python Templates

### PyCharm Live & File Templates
https://gist.github.com/toransahu/6080cbf2cc1a8808f19bd0eccafc5ef0

### Vim Template
https://github.com/toransahu/vim-template/blob/master/templates/%3Dtemplate%3D.py
