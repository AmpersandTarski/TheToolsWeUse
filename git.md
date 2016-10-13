# Git / Github

Git is the version control system we use. Understanding the basics is essential for anyone working on Ampersand. Fortunately, there is good help available:

1. [The help at GitHub](https://help.github.com/articles/)

## Getting started with Git
* Create yourself an account at [GitHub](https://www.github.com), if you don't have one already. 
* Ask one of the administrators of Ampersand to add you as member to the team.
* Make sure to install the appropriate related Git tools, for ease of working.

### Tools for Git
To work with Git in an easy way, it is recommended to install some extra tooling.
*  Install [Git for Windows](http://msysgit.github.io/).
    *  Accept all defaults, except:
        * 4th screen check "Windows Explorer integration" / "Simple context menu" / "Git Bash here"
        * 6th screen "Use Git from the Windows Command Prompt"
* Install [TortoiseGit](https://tortoisegit.org/). 
    * Accept all defaults
* Install [SourceTree](http://www.sourcetreeapp.com).
    * No global ignore, further everything default
    * When at *Add an account*, select *GitHub* and supply your credentials.
* Install [KDiff3](http://sourceforge.net/projects/kdiff3/files/kdiff3/)
    * To select KDiff3 in SourceTree, go to SourceTree / Tools / Options / Diff and select KDiff3 for External Diff Tool and Merge Tool.
* Pin Git Bash to Start menu

## Configuring Security
* **Generate a SSH Key**
    * Start / All programs / Git / Git GUI: Help / Show SSH Key
    * Press Generate Key. You can supply a pass phrase, but that's optional. You should of course keep it for yourself. (it is in *$home/.ssh/id_rsa*). When you use a pass phrase, you will have to supply it now and then.
* **Access to Sentinel**. If you need access to the Sentinel, copy your public key to Clipboard and mail to [Martijn](mailto:martijn@oblomov.com).
He will make sure that you can log in with your key on Sentinel and your own account at sentinel.tarski.nl
* **Access to repositories of AmpersandTarski** (GitHub). 
    * Go to your [personal settings](https://github.com/settings/profile)
    * press *Add SSH Key*
    * Title: add a description of the machine you currently work on (eg. "Windows Laptop Stef")
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
        * At "SSH Client" just fill in:   C:\Program Files (x86)\Git\bin\ssh.exe
    
## Using Sentinel
As soon as your key is registered at sentinel.tarski.nl, you can log in with
    * ssh sentinel@sentinel.tarski.nl
    * ssh USERNAME@sentinel.tarski.nl
        
