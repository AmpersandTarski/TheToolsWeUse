* [ ] # Ampersand in Ordina's cloud

In early 2017 the need arose for an Ampersand implementation in Ordina's cloud, to let young professionals get acquainted with Ampersand. We chose to implement RAP3 in Azure, because Ordina has an Azure subscription. RAP3 is the same environment that our students use at the Open Universiteit, so the maintainance of RAP3 can be reused for both target audiences.

This chapter is an account of the installation process. It serves the following purposes:

1. It is an example for others who want to deploy Ampersand.  
   We get requests now and then by people who want to deploy Ampersand, so we figured it is nice to have a documented example for them.

2. It documents the installation we made for Ordina.  
   We want maintenance of RAP3 to be transferrable to other persons, so we need to document the choices made and the reasons for making them.

3. It contains all information needed to make a deployment script for automated deployment.  
   We want to automate deployment, so that RAP3 will always be up to date with the most recent stable release of Ampersand.

## Setting up the virtual machine

I needed an Azure account to enter the Azure portal and install a server for Ampersand. I got my account from Ordina, using the Azure subscription named 'Ordina TC - RT O Pega - Learning'. Azure offers preconfigured installations to kick-start a virtual machine. I picked LAMP by Bitnami.

The following settings were made:

|  |  |
| :--- | :--- |
| server name | Wolfram |
| type VM-disk | HDD |
| OS | Ubuntu 14.04.5 |
| configuration | Bitnami LAMP 5.6.27-0 |
| documentation | [https://docs.bitnami.com/azure/infrastructure/lamp](https://docs.bitnami.com/azure/infrastructure/lamp) |
| Admin user name | ampersandadmin |
| verification type | password \(Stef Joosten knows the password\) |
| Resource group | Ampersand |
| location | Western Europe |
| Size | 1 core, 1.75 GB, 2 disks, Max. IOP's 2x500 |
| Inbound ports: | HTTP \(TCP/80\) |
|  | HTTPS \(TCP/443\) |
|  | SSH \(TCP/22\) |
| Public IP-adres | 52.174.4.78 |

I have been able to access this machine through SSH, using the Admin user name and password.

## Installing Haskell

I have used Haskell stack for installing Haskell. First I installed `stack` by following the instructions on the internet for a generic Linux installation:

`bitnami@Kahl:~$ curl -sSL https://get.haskellstack.org/ | sh`

At first it broke, because the machine did not get access to certain files, but some fiddling \(which I cannot reproduce\) got the job done. Stack works. It is installed to `/usr/local/bin/stack`.

Then I ran `stack setup` to get Haskell running. That works too. Especially the installing of GHC takes considerable time, which passes without generating any output. Knowing how much is involved in that, I decided not to give up and just wait for an hour or so.

## Installing LaTeX and GraphViz

As RAP3 lets the user generate documentation, Ampersand needs the command `pdflatex` . For that purpose I installed:

`bitnami@Kahl:~$ sudo apt-get install texlive-latex-base`

That worked.

For generating pictures, Ampersand needs the commands `dot` and `neato`. For that purpose I installed:

```
bitnami@Kahl:~$ sudo apt-get install graphviz
```

That too worked.

## Installing SmartGit \(a nice-to-have\)

When updates of Ampersand are being deployed, this is done via GitHub. For this reason it is convenient to have a Git-client on this machine. Sourcetree, however, does not work on Linux. So I installed Smartgit:

```
bitnami@Kahl:~$  sudo add-apt-repository ppa:eugenesan/ppa

bitnami@Kahl:~$  sudo apt-get update

bitnami@Kahl:~$  sudo apt-get install smartgit
```

I have not yet figured out how to run Smartgit on this machine.

## Filling the Git repository with Ampersand files

Git comes preconfigured in Bitnami's LAMP configuration. I have used Git on the command line to get the Ampersand source code and the Ampersand model repository cloned onto the server.

I have created `/home/ampersandadmin/git` for storing the local clones. Here is what I did:

`cd /home/ampersandadmin/git`

`git init`

`git clone https://github.com/AmpersandTarski/Ampersand`

`git clone https://github.com/AmpersandTarski/Ampersand-models`

The directory `/home/ampersandadmin/git/Ampersand` contains the source code of the Ampersand compiler. The directory `/home/ampersandadmin/git/Ampersand-models` contains the source code of the Ampersand models.

## Getting MySQL and phpMyAdmin to work

Instructions on how to find the initial password for MySQL and phpMyAdmin are found on [https://docs.bitnami.com/azure/faq/\#find\_credentials](https://docs.bitnami.com/azure/faq/#find_credentials).

