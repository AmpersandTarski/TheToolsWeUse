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

If have been able to access this machine through SSH, using the Admin user name and password. I have verified the PHP-version  by using the command `php --version`. In the sequel, I will refer to this machine as "the server".

## 2. Getting MySQL and phpMyAdmin to work

To run RAP3 requires Apache and MySQL. Both are already installed on the server. However, you need the database administrator password to set it up for Ampersand. This step requires a server, so you must have finished section 1 successfully.

To get into phpMyAdmin can only be done in localhost. This requires an SSH-tunnel into the server. The instruction is found on [https://docs.bitnami.com/azure/components/phpmyadmin](https://docs.bitnami.com/azure/components/phpmyadmin). I got it done using PuTTY as my SSH-client. Upon success, you can log in to phpMyAdmin in your browser using [http://127.0.0.1:8888/phpmyadmin](http://127.0.0.1:8888/phpmyadmin)  \(case sensitive!\)

Instructions on how to find the initial password for phpMyAdmin are found on [https://docs.bitnami.com/azure/faq/\#find\_credentials](https://docs.bitnami.com/azure/faq/#find_credentials). Since Bitnami-documentation on the web describes different ways to obtain the phpMyAdmin root password and only one of them works, I had a hard time getting the right password. I found it in the diagnostic data for startup, as described in the abovementioned link. When installing the virtual machine, DO NOT switch off the diagnostics for startup, because you will not get the log that contains the root-password.

After logging into phpMyAdmin as root, I created a user called 'ampersand' with password 'ampersand' and host 'localhost', in compliance with the defaults used in the Ampersand compiler. I have issued limited authorizations:

![](/assets/MySQL authorization.png)

As a consequence of these settings, users of RAP3 will not be able to reinstall RAP3, if we accidentally leave the "reinstall database" option alive.

## 3. Uploading and running RAP3

To run RAP3, the web-application must be installed on `/home/bitnami/htdocs`. This step requires sections 1 and 2 to be finished successfully. It also requires you to have a complete RAP3 web-application available for uploading to the server. If you don't have that web-application, you need to build it. Upon completion of step 9 you will have built that web-application by yourself.

To upload RAP3, I followed the instructions on [https://docs.bitnami.com/azure/faq/\#how-to-upload-files-to-the-server-with-sftp](https://docs.bitnami.com/azure/faq/#how-to-upload-files-to-the-server-with-sftp) to upload the RAP3 web-application from my laptop onto the server. I put it on /home/bitnami/htdocs, which is the location of web-applications on this particular configuration. \(On vanilla Linux this would be on /var/www, I guess\). You must change the authorization of the 'log' directory \(.../htdocs/RAP3/log/\) to 757 \(public write access\) or else the application won't work. This screenshot shows the situation after the transfer:![](/assets/Filezilla transfer confirmation.png)

You can test whether this is successful by browsing to `52.174.4.78/RAP3/`

It should show:

![](/assets/initial RAP3 screen.png)

If you need to restart the apache server for whatever reason, here is the command:

`sudo /opt/bitnami/ctlscript.sh restart apache`

## 3. Installing Haskell

In order to build an Ampersand-compiler, we need a Haskell installation. We only need a working machine, so this step merely requires section 1 to be finished successfully.

I have used Haskell stack for installing Haskell. First I installed `stack` by following the instructions on the internet for a generic Linux installation:

`bitnami@Wolfram:~$ sudo apt-get update`

`bitnami@Wolfram:~$ curl -sSL https://get.haskellstack.org/ | sh`

Stack works. It is installed to `/usr/local/bin/stack`.

Stack gives a warning about the PATH:

`WARNING: '/home/ampersandadmin/.local/bin' is not on your PATH.`

`For best results, please add it to the beginning of PATH in your profile.`

I ignored this warning for now.

Then I ran `stack setup` to get Haskell running. That works too. Especially the installing of GHC takes considerable time, which passes without generating any output. Knowing how much is involved in that, I decided not to give up and just wait for an hour or so.

## 4. Filling the Git repository with Ampersand files and Ampersand models

To build an Ampersand-compiler, we need the Ampersand source files, which reside in a GitHub repository. We can download these source files on a fresh server, so this step merely requires section 1 to be finished successfully. The RAP3 source files reside in a GitHub repository as well, so we'll just clone both repositories into the server.

Git comes preconfigured in Bitnami's LAMP configuration. I have used Git on the command line to get the Ampersand source code and the Ampersand model repository cloned onto the server.

I have created `/home/ampersandadmin/git` for storing the local clones. Here is what I did:

`mkdir ~/git`

`cd ~/git`

`git clone https://github.com/AmpersandTarski/Ampersand`

`git clone https://github.com/AmpersandTarski/Ampersand-models`

The directory `/home/ampersandadmin/git/Ampersand` contains the source code of the Ampersand compiler. The directory `/home/ampersandadmin/git/Ampersand-models` contains the source code of the Ampersand models.

To verify that the Ampersand clone has succeeded and that you are in the development branch, navigate to `~/git/Ampersand` and ask for the Git status:

`bitnami@Wolfram:~/git/Ampersand$ git status`

`On branch development`

`Your branch is up-to-date with 'origin/development'.`

`nothing to commit, working directory clean`

You can do the same in the `Ampersand-models` directory. There you must verify that you are in the master branch:

`bitnami@Wolfram:~/git/Ampersand$ cd ../Ampersand-models/`

`bitnami@Wolfram:~/git/Ampersand-models$ git status`

`On branch master`

`Your branch is up-to-date with 'origin/master'.`

`nothing to commit, working directory clean`

## 5. Creating an Ampersand-compiler

To generate RAP3 we need an Ampersand-compiler. The RAP3 user will also use that compiler. For both reasons, we need a working Ampersand compiler on the server. This step requires sections 3 and 4 to be finished successfully.

With the source code of the Ampersand-compiler on the system, I created an executable by running `stack install`. Here is what I did:

`cd ~/git/Ampersand`

`stack setup`

`stack install`

Something is still wrong, because this doesn't work.

## 6. Installing LaTeX and GraphViz

When the RAP3-user generates documentation, RAP3 will call on pdflatex, neato and dot. For this purpose we must install LaTeX and GraphViz. This can be done on a fresh server, so this step only requires section 1 to be finished successfully.

As RAP3 lets the user generate documentation, Ampersand needs the command `pdflatex` . For that purpose I installed:

`bitnami@Wolfram:~$ sudo apt-get install texlive-latex-base`

That worked.

For generating pictures, Ampersand needs the commands `dot` and `neato`. For that purpose I installed:

```
bitnami@Wolfram:~$ sudo apt-get install graphviz
```

That too worked.

## 7. Installing SmartGit \(a nice-to-have\)

For looking into the local Git repository, it is nice to have a Git-client installed. This step requires section 1 to be finished successfully.

When updates of Ampersand are being deployed, this is done via GitHub. For this reason it is convenient to have a Git-client on this machine. Sourcetree, however, does not work on Linux. So I installed Smartgit:

```
bitnami@Wolfram:~$  sudo add-apt-repository ppa:eugenesan/ppa

bitnami@Wolfram:~$  sudo apt-get update

bitnami@Wolfram:~$  sudo apt-get install smartgit
```

I have not yet figured out how to run Smartgit on this machine.

## 9. Generating the RAP3 application

This step requires sections 4 and 5 to be finished successfully.

## 10. Last minute changes before going to production

1. In the source code of RAP3, in the file SIAM\_importer.adl, the interface RAP3\_LoginForDevelopment.ifc must be disabled and the interface RAP3\_LoginForProduction.ifc must be enabled.
2. Is there anything we must alter in localsettings.php before going live?



