# Learning Git by O'Reilly

- Git: a technology for tracking changes to a project and helping multiple people to collaborate on a project, **version control system**

created by Linus Torvalds to version control the Linux kernel

- commit: a version of your project

Graphical User Interface (GUI) and Command Line Interface (CLI, aka shell, terminal) -> 2 ways to interact with a computer

[](../../assets/git/command_prompt.png)

CLI in linux and macos: Terminal
CLI in windows: Git Bash

[](../../assets/git/option_and_argument.png)

word processor: edit rich text like Microsoft Word and Google Docs

Rich text is text with styles attached to or embedded within it.

list of CLI commands:

```bash
pwd # print working directory
clear
ls # list visible files and dirs
ls -a # list hidden and visible file and dirs
cd <path_to_dir> # change dir
mkdir <dir_name> # create a dir

git config --global --list # List the variables in the global Git configuration file and their values

git config --global user.name "<name>" # Set your name in the global Git configuration file

git config --global user.email "<email>" # Set your email address in the global Git configuration file
```

- Repository (repo): a project version controlled by git

- Local repo: stored on a computer
- Remote repo: hosted on a hosting service

## Initializing a Local Repo

- By initializing (creating) a repo, a hidden dir **.git** will be created that contains all the data on file changes

```bash
git init # Initialize a Git repo with default 'master' branch

git init -b <branch_name> # Initialize a Git repo and set the name for the initial branch to be <branch_name>

git config --global init.defaultBranch “<branch_name> # Set default branch name in Git config
```

## The Areas of Git

- Working directory: contains the files and directories in the project directory that represent one version of a project, where you make all the modifications to the content of a project

- Staging area: a rough draft space, represented by a file called **index** in .git (a binary file, created only if you have added at least one file to the staging area)

- Commit history: where your commits are saved, represented by the **objects** directory inside .git

\*\* commit: one version of your project (snapshot),
every commit has a commit hash (commit ID): unique 40-character hash, you only need first seven characters of a commit hash to refer to a commit

- Local repository

\*\* untracked file is a file in the working directory that Git is not version controlling, once you add this file to staging area and include it in a commit, it became a tracked file

**commit early, commit often**

- Commit steps:

1. add files to the staging area
2. make a commit with a commit message

```bash
git status
# Show the state of the working directory and the staging area (list all modified files)

git add <filename>
# Copy one file from working dir to the staging area

git add <filename> <filename> ...
# Add multiple files to the staging area

git add -A
# Add all the files in the working directory that have been edited or changed to the staging area

git commit -m “<message>”
# Create a new commit with a csommit message, changes became tracked

git log
# Show a list of commits which are reachable by following the parent links from the commit you are on when you execute the command in reverse chronological order, exit with pressing 'q'

git log --all
# Show a list of commits in reverse chronological order for all branches in a local repository
```

- git log shows below info about each commit:

1. commit hash
2. author name and email address
3. data and time commit was made
4. commit message

- Why to use Branches?

1. to work on the same project in different ways

2. to help multiple people work on the same project at the same time

official primary branch: main
secondary branch: topic/feature branches

- Branch: movable pointers to commits

- in .git/refs/heads s file is stored for each local branch.

- Tracked files in the working directory can be in one of two states:

1. Unmodified files that have not been edited since the last commit.

2. Modified files has been edited (and saved in the text editor)

Every commit, other than the very first one in a repository, has a parent commit.

```bash
git cat-file -p <commit_hash> # check the parent of the given commit

git branch
# List local branches

git branch <new_branch_name>
# Create a branch, branch name can't contain spaces

git switch <branch_name>
# Switch branches, not available in git older than version 2.23

git checkout <branch_name>
# Switch branches
```

- HEAD: a pointer that tells you which branch you are on (the version you are looking at)

- heads directory (.git/refs/heads) stores a file for every local branch in your local repo, while HEAD shows which branch you are on by referencing one of the files inside the heads directory

- git switch (checkout):

1. It changes the HEAD pointer to point to the branch you are switching onto.

2. It populates the staging area with a snapshot of the commit you are switching onto.

3. It copies the contents of the staging area into the working directory.

- Merging: integrate the changes made in one branch into another branch

- source branch: contain changes
- target branch: receives changes

\*\* A branch’s development history can be traced by following the parent links
of commits.

- Fast-forward merge: a type of merge that occurs when the development histories of the branches involved in the merge have not diverged—in other words, when it is possible to reach the target branch by following the parent links that make up the commit history of the source branch.

During a fast-forward merge,
Git takes the pointer of the target branch and moves it to the commit of the source branch.

If we can reach one branch through the commit history of another branch, we say that the development histories of the branches have not diverged.

- Three-way merge: a type of merge that occurs when the development histories of the branches involved in the merge have diverged.
  Development histories have diverged when it is not possible to reach the target branch by following the commit history of the source branch. In this case when you merge the source branch into the target branch, Git performs a three-way merge, creating a merge commit to tie the two development histories together; it then moves the pointer of the target branch to the merge commit.

\*\* A merge commit is a commit that
has more than one parent.

- Merge Conflict: occurs in three-way merges, 2 branches have different changes to the same files

- Merging steps:

1. Switch onto the target branch

2. Use the git merge command and pass in the name of the source branch

```bash
git merge <branch_name>
# Integrate changes from one branch into another branch

git checkout <commit_hash>
# Check out a commit

git switch -c <new_branch_name>
# Create a new branch and switch onto it

git checkout -b <new_branch_name>
# Create a new branch and switch onto it
```

\*\* switching branches changes the contents of your working directory

Git will not prevent you from switching branches if you make changes to files without saving them in the text editor, because those files will be considered unmodified files.

- Detached HEAD state: when you checkout a commit and HEAD points to a commit not a branch, in this way you can lookout at any version of your project,
  It is not recommended to make any changes to a repository while in detached HEAD state

- Git hosting services: gitHub, GitLab, Bitbucket

To transfer data between a local repository and a remote repository on a hosting service, you must connect and authenticate using either SSH or HTTPS.

The HTTPS protocol uses a username and some sort of password (or authentication credential) to allow you to securely connect to remote repositories.

The SSH protocol uses a public and private SSH key pair to allow you to securely connect to remote repositories. The three main steps to setting up SSH access are:

1. Create an SSH key pair on your computer.
2. Add the private SSH key to the SSH agent.
3. Add the public SSH key to the hosting service account.
