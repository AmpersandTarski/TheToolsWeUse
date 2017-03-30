* [ ] # Ampersand in Ordina's cloud

In early 2017 the need arose for an Ampersand implementation in Ordina's cloud, to let young professionals get acquainted with Ampersand. We chose to implement RAP3 in Azure, because Ordina has an Azure subscription. RAP3 is the same environment that our students use at the Open Universiteit, so the maintainance of RAP3 can be reused for both target audiences.

This chapter is an account of the installation process. It serves the following purposes:

1. It is an example for others who want to deploy Ampersand.  
   We get requests now and then by people who want to deploy Ampersand, so we figured it is nice to have a documented example for them.

2. It documents the installation we made for Ordina.  
   We want maintenance of RAP3 to be transferrable to other persons, so we need to document the choices made and the reasons for making them.

3. It contains all information needed to make a deployment script for automated deployment.  
   We want to automate deployment, so that RAP3 will always be up to date with the most recent stable release of Ampersand.

Each step in the installation process gets a separate section in this text. It is not necessary to do them in the given order.dir

## 1. Setting up the virtual machine

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
| PHP version \(RAP3 requires PHP version 5.6 or higher\) | 5.6.27 |

If have been able to access this machine through SSH, using the Admin user name and password. I have verified the PHP-version  by using the command `php --version`.

## 2. Uploading RAP3

This step requires section 1 to be finished successfully. It also requires you to have the complet RAP3 web-application available.

I followed the instructions on [https://docs.bitnami.com/azure/faq/\#how-to-upload-files-to-the-server-with-sftp](https://docs.bitnami.com/azure/faq/#how-to-upload-files-to-the-server-with-sftp) to upload the RAP3 web-application from my laptop onto the server. I put it on /home/bitnami/htdocs, which is the location of web-applications on this particular configuration. \(On vanilla Linux this would be on /var/www, I guess\).

You can test whether this is successful by browsing to `52.174.4.78/RAP3/`

It should show:![](/assets/initial RAP3 screen.png)

![](/assets/initial RAP3 screen.png)

## 3. Installing Haskell

This step requires section 1 to be finished successfully.

I have used Haskell stack for installing Haskell. First I installed `stack` by following the instructions on the internet for a generic Linux installation:

`bitnami@Wolfram:~$ sudo apt-get update`

`bitnami@Wolfram:~$ curl -sSL https://get.haskellstack.org/ | sh`

Stack works. It is installed to `/usr/local/bin/stack`.

Stack gives a warning about the PATH:

`WARNING: '/home/ampersandadmin/.local/bin' is not on your PATH.`

`For best results, please add it to the beginning of PATH in your profile.`

I ignored this warning for now.

Then I ran `stack setup` to get Haskell running. That works too. Especially the installing of GHC takes considerable time, which passes without generating any output. Knowing how much is involved in that, I decided not to give up and just wait for an hour or so.

## 4. Filling the Git repository with Ampersand files

This step requires section 1 to be finished successfully.

Git comes preconfigured in Bitnami's LAMP configuration. I have used Git on the command line to get the Ampersand source code and the Ampersand model repository cloned onto the server.

I have created `/home/ampersandadmin/git` for storing the local clones. Here is what I did:

`mkdir ~/git`

`cd ~/git`

`git clone https://github.com/AmpersandTarski/Ampersand`

`git clone https://github.com/AmpersandTarski/Ampersand-models`

The directory `/home/ampersandadmin/git/Ampersand` contains the source code of the Ampersand compiler. The directory `/home/ampersandadmin/git/Ampersand-models` contains the source code of the Ampersand models.

## 5. Creating an Ampersand-compiler

This step requires sections 3 and 4 to be finished successfully.

With the source code of the Ampersand-compiler on the system, I created an executable by running `stack install`. Here is what I did:

`cd ~/git/Ampersand`

`stack install`

`stack setup`

`stack install`

For some reason, stack install gives an error message the first time, because it cannot find the  ghc-8.0.1 compiler. Running stack setup for the second time helps, even though it made me wait long for a second time. I don't know what is going on, but it gave me time to document it \(in this very text\). Anyway, the second time stack install was run, it generated an Ampersand compiler. That too takes a long time, but at least it produces output to show progress.

## 6. Installing LaTeX and GraphViz

This step requires section 1 to be finished successfully.

As RAP3 lets the user generate documentation, Ampersand needs the command `pdflatex` . For that purpose I installed:

`bitnami@Wolfram:~$ sudo apt-get install texlive-latex-base`

That worked.

For generating pictures, Ampersand needs the commands `dot` and `neato`. For that purpose I installed:

```
bitnami@Wolfram:~$ sudo apt-get install graphviz
```

That too worked.

## 7. Installing SmartGit \(a nice-to-have\)

This step requires section 1 to be finished successfully.

When updates of Ampersand are being deployed, this is done via GitHub. For this reason it is convenient to have a Git-client on this machine. Sourcetree, however, does not work on Linux. So I installed Smartgit:

```
bitnami@Wolfram:~$  sudo add-apt-repository ppa:eugenesan/ppa

bitnami@Wolfram:~$  sudo apt-get update

bitnami@Wolfram:~$  sudo apt-get install smartgit
```

I have not yet figured out how to run Smartgit on this machine.

## 8. Getting MySQL and phpMyAdmin to work

This step requires section 1 to be finished successfully.

To get into phpMyAdmin can only be done in localhost. This requires an SSH-tunnel into the server. The instruction is found on [https://docs.bitnami.com/azure/components/phpmyadmin](https://docs.bitnami.com/azure/components/phpmyadmin). I got it done using PuTTY as my SSH-client. Upon success, you can log in to phpMyAdmin in your browser using [http://127.0.0.1:8888/phpmyadmin](http://127.0.0.1:8888/phpmyadmin)  \(case sensitive!\)

Instructions on how to find the initial password for phpMyAdmin are found on [https://docs.bitnami.com/azure/faq/\#find\_credentials](https://docs.bitnami.com/azure/faq/#find_credentials). Since Bitnami-documentation on the web describes different ways to obtain the phpMyAdmin root password and only one of them works, I had a hard time getting the right password. I found it in the diagnostic data for startup, as described in the abovementioned link. When installing the virtual machine, DO NOT switch off the diagnostics for startup, because you will not get the log that contains the root-password.

After logging into phpMyAdmin as root, I created a user called 'ampersand' with password 'ampersand' and host 'localhost', in compliance with the defaults used in the Ampersand compiler. I have issued limited authorizations: ![](/assets/MySQL authorizations.png)

## 9. Generating the RAP3 application

This step requires sections 4 and 5 to be finished successfully.

