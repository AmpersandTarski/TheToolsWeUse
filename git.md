# Git / Github

## What is Git?
Git is the version control system we use. Understanding the basics is essential for anyone working on Ampersand. Fortunately, there is good help available:

1. [The help at GitHub](https://help.github.com/articles/)
2. 

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
* Install [Tortoise Git](https://tortoisegit.org/ Windows Shell Interface to Git). 
    * Accept all defaults
* Install [SourceTree](http://www.sourcetreeapp.com).
    * No global ignore, further everything default
    * When at *Add an account*, select *GitHub* and supply your credentials.
* Install [KDiff3](http://sourceforge.net/projects/kdiff3/files/kdiff3/)
    * To select KDiff3 in SourceTree, go to SourceTree / Tools / Options / Diff and select KDiff3 for External Diff Tool and Merge Tool.

## Configuring Security
    * Generate a SSH Key
    *   Start / All programs / Git / Git GUI: 
        Help / Show SSH Key
        Press Generate Key
        You can supply a pass phrase, but that isn't mandatory, as long as you keep it for yourself. (it is in $home/.ssh/id_rsa). When you use a pass phrase, you'll have to supply it now and then.
    * Copy To Clipboard and mail to martijn@oblomov.com 
        Martijn will make sure that you can log in with your key on Sentinel and your own account at sentinel.tarski.nl
    * Op https://www.github.com (jouw persoonlijke pagina) naar Settings (tandwieltje rechtsboven) / SSH keys:
      Druk op "Add SSH Key"
       Title: beschrijving van de machine waarop je nu werkt (Bv. "Windows Laptop Stef")
       Key: Ctrl-V 
      Druk op "Add Key"
      
    Pin Git Bash to Start menu
    
    
