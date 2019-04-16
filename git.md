---
description: >-
  We use Git for version control, with the shared Ampersand repository located
  at Github. This chapter provides the information to get to the repository and
  clone it for having your own local copy.
---

# Version control with Git

We use Git for the following purposes:

## Getting started with Git

1. to have a shared source code repository;
2. to work on different features in parallel without having to coordinate that with each other;
3. to prevent loss of code because multiple copies exist on multiple sites;
4. to have an accurate registration of changes, their authors, and the time each change has occured.

Understanding the basics of Git is essential for anyone working on Ampersand. Fortunately, there is good help available:

1. [The help at GitHub](https://help.github.com/articles/)

* If you want  write access to the Ampersand repo, create yourself an account at [GitHub](https://www.github.com), if you don't have one already. You don't need that if you just want to read.
* Ask one of the administrators of Ampersand to add you as member to the team if you want/need write access to the Ampersand repo or any other repo in the project.
* If you need a local copy on your own computer, install [Git for Windows](http://msysgit.github.io/) or [Git for MacOS](https://nl.atlassian.com/git/tutorials/install-git#mac-os-x) to stay abreast with the latest version.
* When installing for Windows:
  * Accept all defaults, except:
  * 4th screen check "Windows Explorer integration" / "Simple context menu" / "Git Bash here"
  * 6th screen "Use Git from the Windows Command Prompt"

## Tools for Git

Git works from the command prompt. There are however some tools that make life easier when you work with Git. Not necessary, but very much appreciated.

* Install [TortoiseGit](https://tortoisegit.org/) to use Git in your Windows Explorer. 
  * Accept all defaults
* Install [SourceTree](http://www.sourcetreeapp.com) to visualize the history in the most popular Git client.
  * No global ignore, further everything default
  * When at _Add an account_, select _GitHub_ and supply your credentials.
* Install [KDiff3](http://sourceforge.net/projects/kdiff3/files/kdiff3/) to get help in merging conflicts. To avoid KDiff3, you can merge conflicts from your editor or IDE as well.
  * To select KDiff3 in SourceTree, go to SourceTree / Tools / Options / Diff and select KDiff3 for External Diff Tool and Merge Tool.
* Pin Git Bash to Start menu to use Git from a command line interface.

## Configuring Security

To avoid typing a GitHub password for every commit you make, [install an SSH-key](https://help.github.com/articles/connecting-to-github-with-ssh/). Here is the short version:

* **Generate a SSH Key**
  * Start / All programs / Git / Git GUI: Help / Show SSH Key
  * Press Generate Key. You can supply a pass phrase, but that's optional. You should of course keep it for yourself. \(it is in _$home/.ssh/id\_rsa_\). When you use a pass phrase, you will have to supply it now and then.
* **Access to repositories of AmpersandTarski** \(GitHub\). 
  * Go to your [personal settings](https://github.com/settings/profile)
  * press _Add SSH Key_
  * Title: add a description of the machine you currently work on \(eg. "Windows Laptop Stef"\)
  * Key: past your generated key 
  * Press "Add Key"

## Checking out Ampersand source code

By default, the Git directory in your home directory will be used for all local repositories. The easies way is to use SourceTree for manipulating repo's.

* It is also pretty easy using Git Bash:
  * cd git
  * git clone git@github.com:AmpersandTarski/Ampersand.git
* TortoiseGit
  * First time, you have to configure ssh: 
    * Start / All Programs / TortoiseGit / Network:
    * At "SSH Client"  fill in:   C:\Program Files \(x86\)\Git\bin\ssh.exe

## Working Practices

1. The [Ampersand repository at Github](https://github.com/AmpersandTarski/Ampersand/) contains the authoritative source code of Ampersand.
2. The master branch is used for releases only. @hanjoosten is currently the primary guardian of the release process.
3. The development branch is used only to commit developments that are ready to be tested by the Ampersand inner-circle.
4. Every developer develops on his or her own branch\(es\). Typically these are spawned from the development branch.



