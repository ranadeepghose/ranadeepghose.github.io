---
title: Git for Dummies - Part 02
author: ranadeep
date: 2022-08-14 07:51:00 +0530
categories: [Git, How To]
tags: [intro, installation process]
---

## How to Use Git

In the [first part of this series](https://3point0.blog/posts/git-for-dummies-part-01/), we have discussed about the history, use and concepts of Git. To actually use Git, we need to have the program installed in our system. Let's see how to install Git in various platforms like MacOS, Windows and Linux.

## Installation

### How to Install Git on MacOS

There are several ways of installing Git in MacOS. In fact, if XCode or its CLI (Command Line Interface) is installed, their is a fair chance that Git has already been installed along with it. To find out if your MacOS has Git installed, open the Terminal and enter the following code:

```console
git --version
```
If it is installed in your Mac, it will return the Git version; if not, it will show the following message:

![Mac message if Git not installed](/assets/img/post-images/mac-git-version-check.png){: .shadow width="1000" height="453" style="max-width: 90%"}


Click on the install button to install developer tools required to use Git on your Mac. The developer tools include XCode and XCode App Development utilities. 

#### Install Git with Homebrew

[Homebrew](https://brew.sh/){:target="_blank"} is a popular package manager for MacOS and Linux. If you do not have Homebrew in your Mac, you can install the same with the following command:

```console
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Once installed, make sure you update to the latest version with the following command:

```console
brew update
```

Finally, once Homebrew is installed and updated, enter the following command to install Git:

```console
brew install git
```

#### Install Git with MacPorts

If you already have [MacPorts](https://www.macports.org/install.php){:target="_blank"} installed to manage packages on MacOS, use the following instructions to install Git:

- Update MacPorts from the Terminal

```console
sudo port selfupdate
```

- Search for the latest Git ports and variations:

```console
port search git
```

```console
port variants git
```

- Install Git with bash completion, the OS X keychain helper, and the docs:

```console
sudo port install git +bash_completion+credential_osxkeychain+doc
```

### How to Install Git on Windows

If you are a Windows user, it is easy to install Git with the standalone installer. Download the latest [Git Installer for Windows](https://git-scm.com/download/win){:target="_blank"}. Double click on the installer to start the installation process. When you see the install prompt, click on Yes button, agree to the terms and follow the **Next** and **Finish** prompts to complete the installation. The default options are suitable for most users.

You can now use the Windows Command Prompt or Git Bash to start using Git.

### How to Install Git on Linux with Package Managers

Check first to see if Git is already installed in your system with 

```console
git --version
```

If already installed, it will return the Git version, if not, it will give the following error:

```console
-bash: git: command not found
```

#### Installing Git on Ubuntu or Debian

For Ubuntu or Debian, Git packages are available through [APT (Advanced Package Tool)](https://wiki.debian.org/Apt){:target="_blank"}.

To install Git using apt-get, first run the update command.

```console
sudo apt-get update
```

Then run the install command.

```console
sudo apt-get install git
```

And finally verify the installation was successful by running the version command.

```console
git --version
```

If successfully installed, it will return the Git version.

#### Installing Git on Fedora

For Fedora, Git packages are available through [dnf](https://docs.fedoraproject.org/en-US/quick-docs/dnf/){:target="_blank"} and [yum](https://fedoraproject.org/wiki/Yum){:target="_blank"}.

For dnf, use the following command from the shell

```console
sudo dnf install git
```

or the following for yum

```console
sudo yum install git
```

Verify the installation was successful by running the version command.

```console
git --version
```

If successfully installed, it will return the Git version.

#### Installing Git on CentOS

For CentOS, Git can be installed using yum, similar to Fedora.

#### Installing Git on Arch Linux

Arch Linux uses [pacman](https://wiki.archlinux.org/title/pacman){:target="_blank"} to install Git with the following command:

```console
sudo pacman -Sy git
```

#### Installing Git on Gentoo

For Gentoo, use [emerge](https://wiki.gentoo.org/wiki/Emerge){:target="_blank"} to install Git.

```console
sudo emerge --ask --verbose dev-vcs/git
```

### How to Install Git on Linux from Source

#### For Ubuntu / Debian

- Install necessary dependencies using apt-get.

```console
sudo apt-get update
```

```console
sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev asciidoc xmlto docbook2x
```

- Clone the Git source.

```console
git clone https://git.kernel.org/pub/scm/git/git.git
```

- To build Git and install it under /usr, run make:

```console
make all doc info prefix=/usr
```

```console
sudo make install install-doc install-html install-info install-man prefix=/usr
```

#### For Fedora

- You can install the necessary build dependencies with dnf from your shell:

```console
sudo dnf install curl-devel expat-devel gettext-devel openssl-devel perl-devel zlib-devel asciidoc xmlto docbook2X
```

Or if you are using yum, you may need to install the Extra Packages for Enterprise Linux (EPEL) repository first:

```console
sudo yum install epel-release
```

```console
sudo yum install curl-devel expat-devel gettext-devel openssl-devel perl-devel zlib-devel asciidoc xmlto docbook2X
```

- Symlink docbook2X to the filename that the Git build expects:

```console
sudo ln -s /usr/bin/db2x_docbook2texi /usr/bin/docbook2x-texi
```

- Clone the Git source.

```console
git clone https://git.kernel.org/pub/scm/git/git.git
```

- To build Git and install it under /usr, run make:

```console
make all doc prefix=/usr
```

```console
sudo make install install-doc install-html install-man prefix=/usr
```

#### For CentOS

- Install dependencies first:

```console
sudo yum group install "Development tools"
```

```console
sudo yum install gettext-devel openssl-devel perl-CPAN perl-devel zlib-devel
```

- Next, from [Git's release page](https://github.com/git/git/tags){:target="_blank"} select a stable Git version (one without an -rc suffix) you prefer to install.

- Once you have selected the preferred Git version, right click and copy the link of the file with the `tar.gz` extension.

- Download the selected url with `wget`:

```console
wget https://github.com/git/git/archive/refs/tags/v2.37.2.tar.gz -O gitdownloadversion.tar.gz
```
This command downloads `v2.37.2.tar.gz` as `gitdownloadversion.tar.gz`.

- Use the following command to unpack the file using `tar`, then decompress and extract the file using `-zxf` option:

```console
tar -zxf gitdownloadversion.tar.gz
```

- Change directory to the new unpacked folder:

```console
cd gitdownloadversion-*
```

- To compile the downloaded Git files, create a Makefile:

```console
make configure
./configure --prefix=/usr/local
```

- When Makefile is ready, compile and install:

```console
sudo make install
```

- Verify the installation was successful by running the version command.

```console
git --version
```

If successfully installed, it will return the Git version.

So that is how you can install Git on your system. In the next part, we will discuss how to configure Git and use it.