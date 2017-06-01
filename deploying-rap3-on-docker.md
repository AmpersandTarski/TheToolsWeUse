# Ampersand in Ordina's cloud

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

The following settings were \(or will be\) made:

|  |  |
| :--- | :--- |
| subscription in Azure | Ordina TC - RT O Pega - Learning |
| server name | Wolfram |
| type VM-disk | SDD |
| Virtueel netwerk | AmpersandRAP3-vnet |
| subnet | default \(10.0.0.0/24\) |
| OS | Linux |
| configuration | CoreOS |
| documentation | [https://coreos.com/os/docs/latest/booting-on-azure.html](https://coreos.com/os/docs/latest/booting-on-azure.html) |
| Admin user name | ampersandadmin |
| verification type | password \(Stef Joosten knows the password\) |
| Resource group \(in Azure\) | AmpersandRAP3 |
| location \(in Azure\) | Western Europe |
| Size | Standard DS11 v2 \(2 kernen, 14 GB geheugen\) |
| Inbound port: HTTP | TCP/80 |
| Inbound port: HTTPS | TCP/443 |
| Inbound port: SSH | TCP/22 |
| Inbound port: FTP | TCP/21 |
| Public IP-adres | 52.232.97.91 |
| PHP version \(RAP3 requires PHP version 5.6 or higher\) |  |
| `{APPDIR}`=  the directory into which the RAP3 files will be deployed |  |
| `{APPACC}`=  the account under which the RAP3 application will run \(the apache account, i.e. ${APACHE\_RUN\_USER} c.q. ${APACHE\_RUN\_GROUP} as defined in apache2.conf\) |  |
| `{APPHOST}` =  the URI of the machine that hosts the SPReg application \(e.g. 'mydomain.org', or 'rap3.mydomain.org'\) |  |
| `{APPPORT}` =  the port at which the Apache server will be listening | 80 |
| `{APPURI}` = the URI at which the RAP3 application will be accessible for browsers \(e.g. 'mydomain.org/spreg', or 'spreg.mydomain.org'\) |  |
| `{APPURL}` = the full name for calling the application \(e.g. [https://mydomain.org:8080/spreg](https://mydomain.org:8080/spreg)', or [https://spreg.mydomain.org\](https://spreg.mydomain.org%29\) |  |

The reason to pick CoreOS as flavour for Linux is that this is a minimal installation especially directed towards container computing.

I have been able to access this machine through SSH, using the Admin user name and password. In the sequel, I will refer to this machine as "the server". I have verified the machine was live by logging in via Putty \(a popular SSH-client\).

TODO: make sure that `{APPHOST}` can be found by DNS.

* if you want to use HTTPS, then ensure you install a valid server certificate \(e.g. through [https://letsencrypt.org/\](https://letsencrypt.org/%29\) 

## 2. Installing Docker

This step requires a server, so you must have finished section 1 successfully. To install docker I followed the following steps in the given order:

| step | Linux command |
| :--- | :--- |
| To work as root | sudo -i |
| To obtain docker-compose | /usr/bin/mkdir -p /opt/bin/ |
|  | /usr/bin/curl -o /opt/bin/docker-compose -sL [https://github.com/docker/compose/releases/download/1.11.1/run.sh](https://github.com/docker/compose/releases/download/1.11.1/run.sh) |
|  | /usr/bin/chmod +x /opt/bin/docker-compose |
| To add the current user \(ampersandadmin\) to the docker group | usermod -aG docker $\(whoami\) |
| To start the docker daemon | systemctl enable docker |
| now reboot the machine | reboot |

I checked that docker is running by:

docker ps

I checked that docker-compose is available  
 by:

which docker-compose

## 3. Getting MySQL and phpMyAdmin to work

To run RAP3 requires Apache and MySQL. Both are already installed on the server. However, you need the database administrator password to set it up for Ampersand. This step requires docker, so you must have finished section 2 successfully.

To get into phpMyAdmin can only be done in localhost. This requires an SSH-tunnel into the server. The instruction is found on [https://docs.bitnami.com/azure/components/phpmyadmin](https://docs.bitnami.com/azure/components/phpmyadmin). I got it done using PuTTY as my SSH-client. Upon success, you can log in to phpMyAdmin in your browser using [http://127.0.0.1:8080/phpmyadmin](http://127.0.0.1:8888/phpmyadmin)  \(case sensitive!\)

The initial password for phpMyAdmin is specified in the .yml file.

After logging into phpMyAdmin as root, I created a user called 'ampersand' with password 'ampersand' and host 'localhost', in compliance with the defaults used in the Ampersand compiler. I have issued limited authorizations:

![](/assets/MySQL authorization.png)

## 4. Uploading and running RAP3

If you have a complete installation of RAP3, you can upload it on the system.

You can test whether this is successful by browsing to `52.174.4.78/RAP3/`

It should show:

![](/assets/initial RAP3 screen.png)

## 5. Filling the Git repository with Ampersand files and Ampersand models

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

## 6. Installing Haskell

In order to build an Ampersand-compiler, we need a Haskell installation. This can be done on a clean machine, so this step requires section 2 to be finished successfully.

## 7. Creating an Ampersand-compiler

To generate RAP3 we need an Ampersand-compiler. The RAP3 user will also use that compiler. For both reasons, we need a working Ampersand compiler on the server. This step requires sections 5 and 6 to be finished successfully.

Having the source code of the Ampersand-compiler on the system, I created an executable by running `stack install`. Here is what I did:

`cd ~/git/Ampersand`

`stack setup`

`stack install`

A 1-core machine with 1.75GB memory has been shown too small to build the Ampersand-compiler. In that case, stack install does not show any progress. It got stuck without any hints about what is wrong. It did succeed on a 4-core 8GB configuration \(A4\).

## 8. Installing LaTeX and GraphViz

When the RAP3-user generates documentation, RAP3 will call on pdflatex, neato and dot. For this purpose we must install LaTeX and GraphViz. This can be done on a fresh server, so this step only requires section 1 to be finished successfully.

As RAP3 lets the user generate documentation, Ampersand needs the command `pdflatex` . For that purpose I installed:

`bitnami@Wolfram:~$ sudo apt-get install texlive`

That worked.

For generating pictures, Ampersand needs the commands `dot` and `neato`. For that purpose I installed:

```
bitnami@Wolfram:~$ sudo apt-get install graphviz
```

That too worked.

## 

## 9. Generating the RAP3 application

To generate the code of the RAP3 web-application, you need to run the Ampersand compiler on the RAP3 source code. So, this step requires sections 5 and 7 to be finished successfully.

It requires to execute the following commands:

```
cd ~/git/Ampersand-models/RAP3/
ampersand --meta-tables --add-semantic-metamodel -p/home/bitnami/htdocs/RAP3 RAP3.adl
chmod 757 /home/bitnami/htdocs/RAP3/log
```

Generating RAP3 might take a while. If everything works out, the compiler will terminate with the message: "Finished processing your model." If you want to monitor progress, append `--verbose` to the `ampersand` command. It will inform you of intermediate results. The chmod command is needed to ensure that your log directory is writable, in case RAP3 does logging. Logging can be switched on and off in your `localsettings.php` file.  Before compiling RAP3, you may want to check the version and the current branch of the RAP3 source code:

```
cd ~/git/Ampersand-models/
git status
```

If, for whatever reason, you want to delete earlier versions of the deployed RAP3-code, use this command:

`rm -r -f -d /home/bitnami/htdocs/RAP3`

## 10. Local Settings

To inspect and change the local settings, you need the file `localsettings.php` on directory `~/git/Ampersand-models/RAP3/include`. This step requires section 5 to be finished successfully. This file contains comments that guide you to use the correct settings in a development situation and in a production situation. Read the file and follow the instructions it contains, especially when making the transition from development to production.

## 11. Last minute changes before going to production

1. In the source code of RAP3, in the file SIAM\_importer.adl:
   1. disable "RAP3\_LoginForDevelopment.ifc", to prevent users from seeing 
   2. enable "RAP3\_LoginForProduction.ifc"
   3. disable "../SIAM/SIAM\_AutoLoginAccount.adl"
2. Is there anything we must alter in localsettings.php before going live?



