[TOC]

# Intro

- [Book](https://git-scm.com/book/en/v2)
- [Ref](https://git-scm.com/docs)
- [Cheatsheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)

## What?

## Why?
1. As a collaboration tool
2. As a version control tool

# Terminologies
## master
## origin
## remote
## url


# Setup & Config

## `config`

### CRLF, LF, CR

#### Windows Only 
- Then turn off automatical convertions, and stick to CRLF only

```
git config --global core.autocrlf false
```

#### Linux/Mac Only
- If on `LF` system, then do this to convert any CRLF to LF
- but not LF to CRLF

```
git config --global core.autocrlf input
```

#### If Both
- Then set this in Windows system only
    - auto-converting CRLF line endings into LF when you add a file to the index
    - and vice versa when it checks out code onto your filesystem
    - hence Git will be having LF but windows filesystem will always have CRLF
    
```
git config --global core.autocrlf true
```

# Inspection & Comparision

## `diff`

### Compare local with remote branch

```
git diff <masterbranch_path> <remotebranch_path>

#or 

git diff master origin/master
```

## `diff-tree`

### List all the files in a commit

```
git diff-tree --no-commit-id --name-only -r bd61ad98
```

## `show`
### List all the files in a commit

```
git show --pretty="" --name-only bd61ad98  
```


# Commands
## init

### `--bare`
- Source: http://www.saintsjd.com/2011/01/what-is-a-bare-git-repository/

## clone
- Normal Way  `git clone url:repo`

- Clone a specific release  `git clone url:repo --branch <tag#>  `

## pull
- `git pull origin master`
- `git pull origin master -f`
- `git pull --rebase origin master`

## add
## rm
## commit
- commit -m "message"
- commit --amend
    - to re-phrase the commit message; iff commit has not been pushed
    
## push
## checkout
## status
## log
To see in descriptive format

```bash
git log --graph --decorate --oneline
```

where:  
    --graph: shows flow  
    --decorate: shows branch names  
    --oneline: compact description in single line  

## reflog
To see in short

## reset


# Uses

## Branching
- Lets say you have 2 branches:
    - master
    - dev
- Options:
    - create a new branch dev
    ```bash
    git checkout -b dev
    ```
    - dev is active
    ```bash 
    git checkout dev
    ```
    - master is active
    ```bash 
    git checkout master
    ```
    - dev is active & incorporate master in it
    ```bash 
    git checkout dev
    git merge master
    ```
    - master is active & incorporate dev in it
    ```bash 
    git checkout master
    git merge dev
    ```
    
    - delete a local branch if completely merged 
    ```bash
    git branch -d dev
    ```
    - delete a local branch if not merged 
    ```bash
    git branch -D dev
    ```
    
    - delete a remote branch
    ```bash
    git push origin :dev
    ```
    
    - Rename your local branch.
        - If you are on the branch you want to rename:
        ```bash
        git branch -m new-name
        ```
        - If you are on a different branch:
        ```bash
        git branch -m old-name new-name
        ```
    
    - Delete the old-name remote branch and push the new-name local branch.
    ```bash
    git push origin :old-name new-name
    ```
    
    - Reset the upstream branch for the new-name local branch.
        - Switch to the branch and then:
        ```bash
        git push origin -u new-name
        ```

- Golden rules   
    - first incorporate master into dev
    - check compatibility/bugs/conflicts & resolve them
    - now incorporate/merge dev in master
    
## Merging    

### merge Vs rebase
1. Both are used for same purpose but with different approach
2. Integrates changes from one branch to another  

### merge
* Lets say, if you're woring on a feature in a dedicated branch. And someone makes a commit in master branch and you want to pull those changes to your feature branch, i.e.

```
      A---B---C feature
     /
D---E---F---G master

here A,B,C are commits in feature. F,G are new commits in master
```

then:

```bash
git checkout feature
git merge master
```
Or in one line 
```bash
git merge master feature
```
** This will create a new commit in feature branch called as "merge commit" and feature branch will have same history as master (but not vice-versa)**
i.e.
```
      A---B---C---(*) feature
     /           /
D---E---F---G---H master

here (*) is merge commit
```

* Very active master branch can pollute the feature branch.  

### rebase:

* Alternative to merging
* rebases feature branch onto master branch

```bash
git checkout feature
git rebase master
```

** shifts the entire feature branch to tip/(latest node) of the master branch.**
i.e.

```
               A'--B'--C' feature
             /
D---E---F---G master

here A',B',C' are brand new commits
```

* instead of creating "merge commit", it creates **brand new commits** in feature branch for all the commits created earlier on the feature branch (the changes will same, but with new commit infos)
* i.e. re-writes branch history
* Benifits over merge
    * gives cleaner history log by avoiding un-necessary "merge commits"
    * results in perfectly linear project history  

**Golden rules to use rebase**:
* never use rebase on any public branch: Means, don't rebase the master branch onto feature branch (it is opposite of rebasing feature branch onto master branch). It will create a brand new commit/history in master branch which will affect other developers.

### rebase one branch on the top of another

```
         Branch-1   Branch-2
         X--Y     A--B--C 
        /        /
D---E---F---G---H   master


After rebaseing Branch-1 on the top of Branch-2

         A--B--C--X--Y   Branch-1
        /    
         A--B--C         Branch-2
        /       
D---E---F---G---H        master

```

```bash
git checkout branch1
git rebase branch2
```
        
## Reverting back to old commits
https://stackoverflow.com/questions/4114095/how-to-revert-a-git-repository-to-a-previous-commit
        
## Reseting
```bash
git checkout <branch>

git reflog

pick the commit_sha one prior to the the incident

git reset --hard <commit_sha>

--hard    Matches the working tree and index to that of the tree being
               switched  to. Any changes to tracked files in the working tree since
               <commit> are lost.




git reset --merge <commit_sha>
or 
git reset --merge <head_count>

--merge       Resets the index to match the tree recorded by the named commit, and
              updates the files that are different between the named commit and
              the current commit in the working tree.
```

## Modify last commit Message

```bash
git commit -a -m
```

## Modify a particular commit

If you want to modify files at commit <SHA>

```bash
git rebase -i <SHA>
```

You will get a editor opened up with list of all the commits prior to that.

Change the `pick` to `edit` for that particular commit <SHA>. Save & close the editor.
    
Make changes to your files.

After that add or rm files.

If you want to change the commit msg also then

```bash
git commit -a
```

Then continue rebasing

```bash
git rebase --continue
```


## Squashing last x commits into one

If you want to squash last X commits into single commit then

```bash
git rebase -i HEAD~X
```

You will get a editor opened up with list of all the X commits.

Change the `pick` to `s` for all the commits except the oldest one into which you want to merge all the lastest. 

Save & close the editor.

Again you'll get an editor with list & order of all the squashed commits. (if you want you can change the commit msgs at this moment)

Then continue rebasing

```bash
git rebase --continue
```

Done.


# Misc
## Travis CI (Continue Integration)
Continuous Integration is the practice of merging in small code changes frequently - rather than merging in a large change at the end of a development cycle. The goal is to build healthier software by developing and testing in smaller increments.

- [Source](https://docs.travis-ci.com/user/getting-started/)

### Prerequisites
To start using Travis CI, make sure you have all of the following:

- GitHub login
- Project hosted as a repository on GitHub
- Working code in your project
- Working build or test script

### Steps to Integrate CI
- Using github login to  
    - [TravisCI.org](TravisCI.org) for public repositories
    - [TravisCI.com](TravisCI.com) for private repositories
- Enable the repo in CI portal   
- Add `.travis.yml` file to the repo to tell Travis CI what to do
    - e.g.
    ```yaml
    
    language: python
    python:
      - "3.6.4"
    # command to install dependencies
    install:
      # - pip install -r requirements.pip
      - pip install pipenv
      - "pipenv install --dev"
    # command to run tests
    script:
      # - pytest src/test.py # or py.test for Python versions 3.5 and below
      - pipenv run pytest src/test.py # or py.test for Python versions 3.5 and below
  ```
  
  - Infrastructure options  
  ```yaml

    os: linux

    dist: trusty

    sudo: enabled

    ```
    
- Add the `.travis.yml` file to git, commit and push, to trigger a Travis CI build
    - Travis only runs builds on the commits you push after you’ve enabled the repository in Travis CI.
- check the build page
- embbed build status on github page

## Setup SSH key
### Generate or Get ssh key
#### Generate
```bash
ssh-keygen
```

#### Set paraphrase

#### Get
```bash
ls ~/.ssh
```

### Add the key to the ssh-agent
#### Start
```bash
eval `ssh-agent` 
```

#### Add
```bash
ssh-add ~/.ssh/<private_key_file>
```
where <private_key_file> is generally id_rsa

#### Provide paraphrase

### Add the public key to your VCS portal settings
#### Copy hash of public key
```bash
cat ~/.ssh/id_rsa.pub

or

xclip -sel clip ~/.ssh/id_rsa.pub
```

#### Paste in settings

#### Update remotes with ssh url
```bash
git remote rm origin

git remote add origin git@bitbucket.org:toransahu/ethereal-machines-backend.git
```
