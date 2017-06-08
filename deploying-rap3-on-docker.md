# Ampersand in Ordina's cloud

In early 2017 the need arose for an Ampersand implementation in Ordina's cloud, to let young professionals get acquainted with Ampersand. We chose to implement RAP3 in Azure, because Ordina has an Azure subscription. RAP3 is the same environment that our students use at the Open Universiteit, so the maintainance of RAP3 can be reused for both target audiences.

This chapter is an account of the installation process. It serves the following purposes:

1. It is an example for others who want to deploy Ampersand.  
   We get requests now and then by people who want to deploy Ampersand, so we figured it is nice to have a documented example for them.

2. It documents the installation we made for Ordina.  
   We want maintenance of RAP3 to be transferrable to other persons, so we need to document the choices made and the reasons for making them.

3. It contains all information needed to make a deployment script for automated deployment.  
   We want to automate deployment, so that RAP3 will always be up to date with the most recent stable release of Ampersand.

## 0. Deployment approach

To automate the deployment, docker is at the heart of the deployment process. Docker is used to simplify the deployment of RAP and make this installation portable to many different computers.

We took a simple Linux machine, installed docker, and built docker images for RAP3 and created three containers: db, rap3, and phptools. The first one, db, runs MariaDB and contains the administration of RAP3 and the Ampersand scripts of users. The rap3 container contains the RAP3 application proper. It is accessed on port 80. The container phptools is present for maintainers to inspect the database through phpMyAdmin. It is accessible through port 8080.

Each step in the installation process is described by a separate section in the sequel.

## 1. Setting up the virtual machine

I needed an Azure account to enter the Azure portal and install a server for Ampersand. I got my account from Ordina. Azure offers preconfigured installations to kick-start a virtual machine. In principle any server that runs docker will work. I picked CoreOS, which is a minimal Linux platform and suitable for container computing with docker.

The following settings were made:

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
| Public IP-adres | 52.232.97.91 \(static\) |
| PHP version \(RAP3 requires PHP version 5.6 or higher\) |  |
| `{APPDIR}`=  the directory into which the RAP3 files will be deployed |  |
| `{APPACC}`=  the account under which the RAP3 application will run \(the apache account, i.e. ${APACHE\_RUN\_USER} c.q. ${APACHE\_RUN\_GROUP} as defined in apache2.conf\) |  |
| `{APPHOST}` =  the URI of the machine that hosts the SPReg application \(e.g. 'mydomain.org', or 'rap3.mydomain.org'\) |  |
| `{APPPORT}` =  the port at which the Apache server will be listening | 80 |
| `{APPURI}` = the URI at which the RAP3 application will be accessible for browsers \(e.g. 'mydomain.org/spreg', or 'spreg.mydomain.org'\) |  |
| `{APPURL}` = the full name for calling the application \(e.g. [https://mydomain.org:8080/spreg](https://mydomain.org:8080/spreg)', or [https://spreg.mydomain.org\](https://spreg.mydomain.org%29\) |  |

I have been able to access this machine through SSH, using the Admin user name and password. In the sequel, I will refer to this machine as "the server". I have verified the machine was live by logging in via Putty \(a popular SSH-client\).

TODO: make sure that `{APPHOST}` can be found by DNS.

* if you want to use HTTPS, then ensure you install a valid server certificate \(e.g. through [https://letsencrypt.org/\](https://letsencrypt.org/%29\) 

## 2. Port settings

In order to access the database, we told the virtual machine to open port 80 for http and port 8080 to phpmyadmin. These settings were made in the Azure portal via `netwerkinterfaces > beveiligingsgroep > inkomende beveiligingsregels`. Two rules were added:

1. A rule called http, which makes the server listen to port 80/TCP.
2. A rule called phpmyadmin, which makes the server listen to port 8080/TCP.

No rule was added for the database, so the database is only open to phpMyAdmin and RAP3, or from within its container.

## 3. Installing Docker

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

To check whether ampersandadmin is member of the docker group, use command id`. Then logout and login again.`

## 4. Making a Docker image

This step requires a server with docker, so you must have finished section 3 successfully. I cloned `https://github.com/wentinkj/docker-ampersand` \(commit 04c4023\) into `/home/ampersandadmin/docker-ampersand`

Then I ran the command `docker build -t ampersand:latest ampersand` and sat back to watch an image being created. This takes over an hour. After coming back a day later, I verified that the image is present by running the same command again. That produced the following output:

```
Wolfram docker-ampersand # docker build -t ampersand:latest ampersand
Sending build context to Docker daemon 4.096 kB
Step 1 : FROM php:7-apache
 ---> 2720c02fc079
Step 2 : ENV PATH /texlive/bin/x86_64-linux:$PATH
 ---> Using cache
 ---> 45d62477f5e2
Step 3 : RUN apt-get update  && apt-get install -y --no-install-recommends git graphviz wget xorriso  && curl -sSL https://get.haskellstack.org/ | /bin/sh  && rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> e37542ec9301
Step 4 : ENV TL_VERSION 2016-20160523
 ---> Using cache
 ---> f95346ded414
Step 5 : ADD texlive.profile /tmp
 ---> Using cache
 ---> add9fd911c38
Step 6 : RUN cd ~  && wget -q   http://mirrors.ctan.org/systems/texlive/Images/texlive$TL_VERSION.iso  && wget -qO- http://mirrors.ctan.org/systems/texlive/Images/texlive$TL_VERSION.iso.sha512 | sha512sum -c  && osirrox -report_about NOTE -indev texlive$TL_VERSION.iso -extract / /usr/src/texlive  && rm texlive$TL_VERSION.iso  && /usr/src/texlive/install-tl -profile /tmp/texlive.profile  && rm -rf /usr/src/texlive  && rm /tmp/texlive.profile
 ---> Using cache
 ---> f0ebcd4cf50c
Step 7 : RUN mkdir ~/git  && cd ~/git  && git clone --branch development https://github.com/AmpersandTarski/Ampersand
 ---> Using cache
 ---> 08643d5cce73
Step 8 : RUN cd ~/git/Ampersand  && stack setup  && stack install --local-bin-path /usr/local/bin
 ---> Using cache
 ---> 636036e98214
Step 9 : RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer  && php -r "unlink('composer-setup.php');"
 ---> Using cache
 ---> e8648c6657f6
Successfully built e8648c6657f6
```

## 5. Making containers

This step requires a server with docker and images to build containers with. So you must have finished section 4 successfully. We are making three containers: one for the database, one for the RAP3 application, and one for PhpMyAdmin. Containers are built from images by the command `docker-compose`:

```
cd /home/ampersandadmin/docker-ampersand call
docker-compose up -d
```

This command brings all three containers up, for which it requires the file `docker-compose.ymlt`to be available in the current directory.

I checked whether the containers are running by means of the `docker ps` command.

Completion of this step allowed access to RAP3 from an arbitrary computer on the internet:

![](/assets/import.png)

The database is accessible on port 8080:

![](/assets/phpMyAdmin.png)

## 6. Maintenance

The `docker-compose up` command aggregates the output of each container. When the command exits, all containers are stopped. Running `docker-compose up -d` starts the containers in the background and leaves them running.

To interfere with RAP3 as it is running, you need to get into the Rap3 container. It is not enough just being on the server, because all the data is in the container \(rather than directly on the server\). To go into the Rap3 container, use the command

```
docker exec -ti dockerampersand_rap3_1 /bin/bash
```

## 10. Local Settings

To inspect and change the local settings, you need the file `localsettings.php` on directory `~/git/Ampersand-models/RAP3/include`. This step requires section 5 to be finished successfully. This file contains comments that guide you to use the correct settings in a development situation and in a production situation. Read the file and follow the instructions it contains, especially when making the transition from development to production.

## 11. Last minute changes before going to production

1. In the source code of RAP3, in the file SIAM\_importer.adl:
   1. disable "RAP3\_LoginForDevelopment.ifc", to prevent users from seeing 
   2. enable "RAP3\_LoginForProduction.ifc"
   3. disable "../SIAM/SIAM\_AutoLoginAccount.adl"
2. Is there anything we must alter in localsettings.php before going live?



