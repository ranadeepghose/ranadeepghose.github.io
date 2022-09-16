---
title: Working with Local Repositories - Git for Dummies, Part 04
description: This tutorial covers the step by step process to push data from git local repository to remote repository.
author: ranadeep
date: 2022-08-22 10:35:00 +0530
categories: [Git, How To]
tags: [intro]
---

## Use Git with Local Repository

We have learnt how to install and [configure Git](https://3point0.blog/posts/git-for-dummies-part-03/) already. Now we will see how we can use Git with a local repository.

A *repository*, often called a *repo* in short, is noting more than a collection of files and folders along with the history of the changes made to them. The changes are tracked with the help of *commits* which are snapshots of a particular file at various points of time in the file's history. The commits help us to refer or revert back to a place in the file's timeline if there are bugs / errors in the code. It must be remembered that commits are not automatic. We have to manually stage a commit after making a series of changes in a file.

If you have a project directory that is in your local machine and does not have version control, you can easily add Git to it. The first step here is to go into the project's directory:

```console
// in Linux
cd /home/user/<Project Directory>

// in MacOS
cd /Users/user/<Project Directory>

// in Windows
cd C:/Users/user/<Project Directory>
```

and then use the `init` command:

```console
git init
```

## Git Init

The `init` command creates a new subdirectory named `.git` inside your project folder. This is the skeleton repository of Git - everything that Git stores and manipulates, is located in this subdirectory. 

A newly-initialized `.git` directory contains the following structure:

```
config
description
HEAD
hooks/
info/
objects/
refs/
```
- `config` - This file contains the project-specific configuration options.
- `description` - This file is only used by the [GitWeb Program](https://git-scm.com/book/en/v2/Git-on-the-Server-GitWeb){:target="_blank"}.
- `info/` - This directory keeps a global exclude file for all ignored patterns that are not supposed to be tracked in a `.gitignore` file.
- `hooks/` - This directory contains client-side or server-side hook scripts. Learn more about [Git Hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks#_git_hooks){:target="_blank"}.

The remaining four entries of the structure, the `HEAD`, the `objects/` directory, the `refs/` directory and the not-yet created `index` files are the core parts of Git.

- `objects/` - This directory stores all the content for your database.
- `refs/` - This directory stores pointers into commit objects in that data (branches, tags, remotes etc.).
- `HEAD` - This file points to the branch you currently have checked out.
- `index` - This file is where Git stores your staging area information.

## Staging Area - Git Add

So now if you make changes to a certain file within your project and want Git to track the changes, you need to add the file to the staging area. (Remember the diagram from [How Git Works](https://3point0.blog/posts/git-for-dummies-part-01/#how-git-works) in Part 01?)

Git recognizes when a file is modified, but it does not track it automatically unless you stage it. The staging area provides a security layer where you can review the changes before finally committing them.

So check which files Git is tracking with the `git status` command and then to add a file to the staging are, use the following command:

```console
git add [filename]
```

You must replace the **[filename]** with the actual name of the file you have made changes to e.g. if you have modified a `style.css` file, your command would be 

```console
git add style.css
```

You can also stage all the files in the working directory by running

```console
git add .
```
So what happens if you have made a mistake and want to remove a file from the staging area. To *unstage* a file, use the following command

```console
git rm --cached [filename]
```

So to remove `style.css` from the staging area, you will need to write

```console
git rm --cached style.css
```

## Making Commits with Git Commit

Once file(s) are staged, they are ready for the final commit. A commit is a save point, more like a snapshot of your file at a particular point of time. You can refer or revert back to these points whenever you want.

To check if you have any files ready to be committed you can again use the `git status` command. And when there are files ready to be committed, we use

```console
git commit -m "Remarks about Commit"
```

The above command with commit the staged file(s) with a short note which describes the changes. The `-m` flag is a must, followed by a short description / note / remark about the commit that will help to identify later what the commit was about.

> It is good practice to provide clear, short, simple and descriptive commit messages for every commit, as it helps to understand what a commit is all about.
{: .prompt-info}

To check the history of commits, you can run the `git log` command. The output shows a log of all the commits made, who made the commit, the date of the commit and the commit notes.

## Revert a Commit

If for any reason you want revert a commit you can use the `git revert` command - undoes the commit you made to remove the changes from the master branch. The command does not remove the commit from commit history. It only adds a new commit specifying that it has reverted the specified commit.

To revert to a specific commit, you must first find the commit ID. It is a 7 character code you can see at the beginning of each commits when you run the `git log` command. Once you have the commit ID, run

```console
git revert [commit ID]
```

## Git Reset

If you are sure that wish to undo or delete parts of your code and you will not need it anymore, you can do a `git reset`. This command **permanently** takes you back to a certain point in your development process and all changes after that point are unstaged. 

To reset, use

```console
git reset [commit ID]
```

> Please note that `git reset` is **permanent** and **irreversible**.
{: .prompt-danger }

> You can also specify a `--hard` flag. This will remove all unstaged files **permanently**.
{: .prompt-info} 

## Branches

Branches are used by developers for modifying files, to fix bugs or develop new features without disturbing the working portions of the project. 

The main branch is generally named `master` and is reserved for clean, working version of the code. It is the stable version which is already released or published. 

Branching creates an isolated environment where code is modified for various purposes and if finalized, the branch can be merged with the `master`. Generally new branches are named after the issue it is fixing or the feature it is implementing. Git keeps track of all branches and so you can jump to any branch or from branches to branches without overwriting or disturbing other branches in the repo.

![Git Branching](/assets/img/post-images/git-branch.webp){: .shadow width="1000" height="453" style="max-width: 90%"}

To create a Git branch, use the following command:

```console
git branch [branch-name]
```

> Please replace `[branch-name]` with the name of your branch.
{: .prompt-warning}

Some basic commands for `git branch` are:


|Option     |Description                        |
|:----------|----------------------------------:| 
| -r        | List the remote branches          |
| -a        | Show both local & remote branches |
| -m        | Rename old branch                 |
| -d        | Delete a branch                   |
| -r -d     | Delete a remote branch            |


## Merging

When a branch is ready, it needs to be *merged* with the `master`. For this we use the `git merge` command. Merging changes means implementing the changes into the `master` branch.

To see the existing branches, use the following command:

```console
git branch -a
```

This will give you a list of all the branches you have. If you are working on a branch, before you merge you need to switch to the branch you want to merge into, e.g. if you are working on a branch named `new-features`, and you want to merge this branch into the `master` branch, then you need to switch to the `master` branch first. To do this, use the following command:

```console
git checkout master
```

After you have switched on to the `master` branch use the following command to merge the changes:

```console
git merge [branch-name]
```

> Please replace `[branch-name]` with the name of your branch.
{: .prompt-warning}

And with that Git automatically inputs your changes to the master branch.

In the next part, we will learn how to work with Git remote repositories.




