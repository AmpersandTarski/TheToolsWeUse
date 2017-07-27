# Ampersand at the Open University of the Netherlands \(OUNL\)

In early 2016 the need arose to replace the RAP2 implementation of Ampersand by a RAP3 implementation, because RAP2 was insufficiently maintainable. This environment is used by students for completing the course Rule Based Design \(OBR, code ...\).  This implementation is hosted by ICTS, the IT-department of the university. We chose to implement RAP3 as a maintainable environment.

This chapter is an account of the installation process. It serves the following purposes:

1. It is an example for others who want to deploy Ampersand.  
   We get requests now and then by people who want to deploy Ampersand, so we figured it is nice to have a documented example for them.

2. It documents the installation we made for the Open University.  
   We want maintenance of RAP3 to be transferrable to other persons, so we need to document the choices made and the reasons for making them.

3. It contains all information needed to make a deployment script for automated deployment.  
   We want to automate deployment, so that RAP3 will always be up to date with the most recent stable release of Ampersand.

Each step in the installation process gets a separate section in this text. It is not necessary to do them in the given order.

## 1. Setting up the virtual machine

I got a server from the Open University's IT-department.

The following settings apply:

|  |  |
| :--- | :--- |
| server name | lnx-hrl-202v |
| OS | Ubuntu 16.04.2 LTS \(GNU/Linux 4.4.0-83-generic x86\_64\) |
| Admin user name | sjo |
| verification type | password \(Stef Joosten knows the password\) |
| Size |  |
| Inbound port: HTTP | TCP/80 |
| Inbound port: HTTPS | TCP/443 |
| Inbound port: SSH | TCP/22 |
| Inbound port: SFTP | TCP/22 |
| Public IP-adres | 145.20.188.96 |
| PHP version \(RAP3 requires PHP version 5.6 or higher\) |  |
| `{APPDIR}`=  the directory into which the RAP3 files will be deployed | /srv/www/htdocs |
| `{APPACC}`=  the account under which the RAP3 application will run \(the apache account, i.e. ${APACHE\_RUN\_USER} c.q. ${APACHE\_RUN\_GROUP} as defined in apache2.conf\) | wwwrun |
| `{APPHOST}` =  the URI of the machine that hosts the RAP3 application \(e.g. 'mydomain.org', or 'rap3.mydomain.org'\) | rap.cs.ou.nl |
| `{APPPORT}` =  the port at which the Apache server will be listening | 80 |
| `{APPURI}` = the URI at which the RAP3 application will be accessible for browsers \(e.g. 'mydomain.org/spreg', or 'spreg.mydomain.org'\) |  |
| `{APPURL}` = the full name for calling the application \(e.g. [https://mydomain.org:8080/spreg](https://mydomain.org:8080/spreg)', or [https://spreg.mydomain.org\](https://spreg.mydomain.org%29\) |  |

## Conventions for OU servers

/unload gebruiken voor source code bestanden

tijdelijke bestanden op /tmp

standaardpakketten op /opt neerzetten

/var is bedoeld voor logbestanden

## Getting access to the server

At the OU, we need VPN to gain access with SSH to a server. This requires approval from the IT department. I got a raw Ubuntu machine, meaning that the port settings \(specified above\) and VPN have to be requested at the IT-servicedesk.

I can now access this machine through SSH \(using PUTTY, which I downloaded from the Internet\), but only after installing a VPN-tunnel to the server \(using Pulse Secure\).  In the sequel, I will refer to this machine as "the server". This gave me access through a command line interface \(CLI\). Ubuntu gave me bash as its CLI.


## Git

With Ubuntu 16.04, Git comes pre-installed. I checked this by means of the `which`-command:

```
sjo@lnx-hrl-202v:~$ which git
/usr/bin/git
```

## Installing Docker

Since this is a fresh machine, docker has to be installed. By just typing `docker`, the server advised to install Docker by means of the command `sudo apt install docker.io`. This turned out to be a bad advice, because it resulted in a too old version of docker. Instead, I followed the instructions on `https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/` .

Then I checked that everything went successfully by means of the `which`-command:

```
sjo@lnx-hrl-202v:~$ which docker
/usr/bin/docker
sjo@lnx-hrl-202v:~$ which docker-compose
/usr/bin/docker-compose
```

## Security
TODO: make sure that `{APPHOST}` can be found by DNS.

* if you want to use HTTPS, then ensure you install a valid server certificate \(e.g. through [https://letsencrypt.org/](https://letsencrypt.org/%29%29%29\)



## 10. Local Settings

To inspect and change the local settings, you need the file `localsettings.php` on directory `~/git/Ampersand-models/RAP3/include`. This step requires section 4 to be finished successfully. This file contains comments that guide you to use the correct settings in a development situation and in a production situation. Read the file and follow the instructions it contains, especially when making the transition from development to production.

## 11. Last minute changes before going to production

1. In the source code of RAP3, in the file SIAM\_importer.adl:
   1. disable "RAP3\_LoginForDevelopment.ifc", to prevent users from seeing 
   2. enable "RAP3\_LoginForProduction.ifc"
   3. disable "../SIAM/SIAM\_AutoLoginAccount.adl"
2. Read and follow the instructions in `localsettings.php` before going live.



