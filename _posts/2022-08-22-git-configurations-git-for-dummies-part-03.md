---
title: Git Configurations - Git for Dummies, Part 03
author: ranadeep
date: 2022-08-22 06:45:00 +0530
categories: [Git, How To]
tags: [intro]
---

## Configure Git

Previously, we have discussed about how to install Git on various platforms. After you [install Git](https://3point0.blog/posts/git-for-dummies-part-02/), the next step is to configure it before it us used for the first time.

To configure Git, we use the command `git config`. This command can accept parameters and arguements and can set and obtain the configuration variables.

There are 3 different configuration levels in Git. They are:

1. **System** (`--system`) - This configuration level covers an entire user, machine and all the repos in it. Changes made in this level affects the entire system and all repos in the system is affected. Editing the system level configuration is often discouraged because of this.

2. **Global** (`--global`) - This configuration level affects the User level. This means that configuration changes will apply to all the files of the user who is currently operating the system. 

3. **Repository** (`--local`) - This configuration level only affects a specific repo (repository). 

The configuration variables can be located at various places depending on your platform. 

In GNU/Linux systems they are generally located in 3 different places:

-   `/etc/gitconfig` -  stores System Level configurations.
-   `~/.gitconfig` - stores Global configurations.
-   `~/<RepoFolder>/.git/config` - stores Repository Level configurations.

In Windows system, they are located in:

-   `C:\Documents\Git\etc\gitconfig` - stores System Level configurations.
-   `C:\Document and Settings\<UserName>\.gitconfig` or `C:\Users\<UserName>\.gitconfig` - stores Global configurations.
-   `C:\<RepoFolder>\.git\config` - stores Repository Level configurations.

In Mac, config files are located similar to Linux:

-   `/usr/local/git/etc/gitconfig` - stores System Level configurations.
-   `~/.gitconfig` - stores Global configurations.
-   `~/<RepoFolder>/.git/config` - stores Repository Level configurations.

### Configure Username and Email

After installing, the first step should be to set your username and email correctly.

To set up Git username and email use the following commands:

```console
git config --global user.name <your name>
git config --global user.email <user@email.com> 
```
> Please replace `<your name>` and `<user@email.com>` with your own name and email.
{: .prompt-warning }

### Configure Default Text Editor

By default, Git uses your default text editor through one of the shell environment variables `VISUAL` or `EDITOR`. Otherwise it falls back to the `vi` editor. However, if you wish to set one of your favorite editors as default, you need to use the `core.editor` setting, e.g.

```console
git config --global core.editor editor-name
```

1. To setup **Sublime Text** as default editor in Windows:

```console
git config --global core.editor "'C:/Program Files/Sublime Text 2/sublime_text.exe' -n -w"
```

or in Mac/Linux:

```console
git config --global core.editor "'/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl' -n -w"
```

2. To setup **VSCode** as default editor:

```console
git config --global core.editor "code --wait"
```

3. To setup **Atom** as default editor:

```console
git config --global core.editor "atom --wait"
```

### List Configurations

Once the basic configuration is in place, use the following command to check if the configurations have updated:

```console
git config --list
```

The output of the above command should echo the following information:

```console
user.name=exampleuser
user.email=user@email.com
core.editor=editor-name
```

These were the basic configurations you will need to start working with Git. However, there are several other configuration parameters that you can modify as per your requirements. You can find a full and detailed [list of Git Configuration here](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration){:target="_blank"}.

That's all for now, in the next part we will discuss how to use [Git with a Local Repository](https://3point0.blog/posts/working-with-local-repositories-git-for-dummies-part-04/).




