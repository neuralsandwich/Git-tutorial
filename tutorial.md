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
`git log` command displays the commited snapshots, showing your commit history.
If you run `git log` you should see similar output:

```
Author: Sean Jones <neuralsandwich@gmail.com>
Date:   Sat May 10 15:38:15 2014 +0100

    Initial commit
```

Let's create some more commits so we can see what `git log` looks like when
populated with more than one commit.

```
echo "foobar" > foobar.txt
echo "foo is not bar" > foo.txt
echo "bar is not foo" > bar.txt
```

Instead of using `git add .`, use `git add -p` You should be prompted with output
similar to this:

```
diff --git a/bar.txt b/bar.txt
index 5716ca5..02626e7 100644
--- a/bar.txt
+++ b/bar.txt
@@ -1 +1,2 @@
 bar
+ is not foo
Stage this hunk [y,n,q,a,d,/,e,?]? 
```

Enter `y` and then `git commit -m "Add changes to foo & bar"`, finally do the
following:

```
git add foobar.txt
git commit -m "Add foobar.txt"
git log
```

Hopefully, you should see similar output:

```
commit bff897c9d3d27cfee74516935500388b417f1c11
Author: Sean Jones <neuralsandwich@gmail.com>
Date:   Sat May 10 22:50:14 2014 +0100

    Add foobar.txt

commit 0c5275028bd818395de035aa1733a3f2889532e5
Author: Sean Jones <neuralsandwich@gmail.com>
Date:   Sat May 10 22:45:13 2014 +0100

    Add changes to foo & bar

commit 36a24afa1548fb767439f36e3e8bee8458f571ee
Author: Sean Jones <neuralsandwich@gmail.com>
Date:   Sat May 10 22:23:27 2014 +0100

    Initial commit
```

This output is fairly simple to understand, every commit has a 40 character SHA1
hash, which is a checksum for the commit and a unique ID. Running `git log
--decorate` will show some extra output.

```
commit bff897c9d3d27cfee74516935500388b417f1c11 (HEAD, master)
Author: Sean Jones <neuralsandwich@gmail.com>
Date:   Sat May 10 22:50:14 2014 +0100

    Add foobar.txt
```

This extra output `(HEAD, master)` indicates that the latest commit `bff897c`
is the current commit and that it is the tip of the master branch. You can use
the `HEAD` reference and branch names with Git commands that require a commit
id.

Try some of the following commands, see the different output they produce:

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
git log --graph --stat -p --decorate
```
Using `git log <since>..<until>` command allows you to seen between the
specified range. For example `git log HEAD~2..HEAD`:

```
commit bff897c9d3d27cfee74516935500388b417f1c11
Author: Sean Jones <neuralsandwich@gmail.com>
Date:   Sat May 10 22:50:14 2014 +0100

    Add foobar.txt

commit 0c5275028bd818395de035aa1733a3f2889532e5
Author: Sean Jones <neuralsandwich@gmail.com>
Date:   Sat May 10 22:45:13 2014 +0100

    Add changes to foo & bar

```
The `~` character is used for referencing the relative parent of the specified
commit. HEAD~1 being the commit previous to HEAD and bff897c~1 being 0c52750,
the commit before bff897c. For more information about `git log` visit [here]
(http://git-scm.com/docs/git-log)

## Removing, Reverting, Resetting & Cleaning

Now that we have some history in the repository, let's use it for what it is
mean to do, store file versions safely. Run the following command `cat foo.txt`
you should see 

```
foo is not bar
```

Even more changes

```
mkdir 
touch
git add
```

`git rm --cached <file>`

```
git commit -m "Lots of changes going on here"
```

git rm -r <dir>

git commit --amend

## Branches

## Remote Repositories

### Bare Repositories
