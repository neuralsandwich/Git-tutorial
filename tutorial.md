# Git Basics

* [Creating Projects](#creating-a-new-project)
* [Checking Repository Status](#checking-the-status)
* [Staging & Commiting](#adding-content--committing)
* [History Log](#viewing-history)
* [Removing Files & Mistakes](#removing-reverting-resetting--cleaning)
* [Branching](#branches)

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
`git clone <url>` command but for now we will move on.

## Checking the Status

Now that the repository has been initialized we can check the status of the
working directory and the staging area. Lets check the status now by using
`git status`.

```
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```

## Adding Content & Committing

Now that we can get `git` to tell us the status of the repository, lets create
some content for git to keep track of.

```
echo "foo" > foo.txt
echo "bar" > bar.txt
```

By adding files to the working directory of the repository we have changes its
status. Lets check how the change the status of the repository, run `git
status` again

```
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    bar.txt
    foo.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Adding these files changed the working directory of our repository, we can use
the `git add <file>` command to add these changes to the staging area. This
is an area which tracks which changes to the working directory will be in the
next commit. The staging area doesn't change the repository as these changes
won't actually be recorded until you commit them. This is one of Git's more
unique features, it allows you to craft your commits splitting changes into
relevant groups, instead of just saving all of your changes since the last
commit.

To add your changes run `git add .`, this command adds all changes to files in
the repository (but not deleted files). Now check the result by running
`git status` again. You should see the following output:

```
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   bar.txt
    new file:   foo.txt

```

`git add` can also be used to add directories in the same manner as files, it
is simple `git add <directory>`.

Now that you have some changes in the staging area, we can go ahead and create
your first commit: `git commit -m "Initial commit"`. The `-m` tells `git commit`
that you are giving it a message on the command line (without it this will open
the default text editor set in your `.gitconfig`, but we will ignore this
detail).

Now our changes that were in the staging area have been stored as a commit. If
you run `git status` again you will see the following message.

```
On branch master
nothing to commit, working directory clean
```

## Viewing History

All version control systems including Git show a projects commit history. The
`git log` command displays the commited snapshots, showing you your commit
history. If you run `git log` you should see similar output:

```
Author: Sean Jones <neuralsandwich@gmail.com>
Date:   Sat May 10 15:38:15 2014 +0100

    Initial commit
```

Lets create some more commits so we can see how git log really works.

```
echo "foobar" > foobar.txt
echo " is not bar" >> foo.txt
echo " is not foo" >> bar.txt
```

git add -p

git log, more history

This ID can be used in commands like git log <since>..<until> to refer to
specific commits. For instance, git log 3157e..5ab91 will display everything
between the commits with ID's 3157e and 5ab91. Aside from checksums, branch
names (discussed in the Branch Module) and the HEAD keyword are other common
methods for referring to individual commits. HEAD always refers to the current
commit, be it a branch or a specific commit.

The ~ character is useful for making relative references to the parent of a
commit. For example, 3157e~1 refers to the commit before 3157e, and HEAD~3 is
the great-grandparent of the current commit.

The idea behind all of these identification methods is to let you perform
actions based on specific commits. The git log command is typically the
starting point for these interactions, as it lets you find the commits you want
to work with.

Different git log formats

```
git log -n <limit>
git log --oneline
git log --stat
git log -p
git log --author"<pattern>"
git log --grep="<pattern>"
git log <since>..<until>
git log <file>
git log --graph --decorate --oneline
```

Even more changes

```
mkdir 
touch
```

## Removing, Reverting, Resetting & Cleaning

```
git rm --cached <file>
```

```
git commit -m "Lots of changes going on here"
```

git rm -r <dir>

git commit --amend

## Branches

## Remote Repositories

### Bare Repositories
