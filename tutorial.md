# Git Basics

## Creating a New Project

To get started using `git` you need to initial a repository. To do this you will
need to run the `git init` command. For the purpose of this tutorial run the
following commands in a bash shell or Git Bash on Windows.

```
mkdir git-tutorial
cd git-tutorial
git init
```

You can also initialize projects using `git init <directory>`. In response to
either of these commands you should see the following output from git

```
Initialized empty Git repository in .git/
```

## Copying Projects

There are many projects with already use git ([github](http://github.com)) to
work on any of these you need to clone the project. You can do this with the
`git clone <url>` command but for now we will move on and come back to this.

## Checking the Status

Now that the repository has been initialized we can check the status of the
working directory and the staging area. Lets check the status now by using
`git status`.

```
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```