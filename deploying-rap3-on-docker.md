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

This step requires a server, so you must have finished section 1 successfully.  Docker is used to simplify the deployment of RAP and make this installation portable to many different computers. To install docker I followed the following steps in the given order:

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

## 3. Making a Docker image

I cloned `https://github.com/wentinkj/docker-ampersand` into `/home/ampersandadmin/docker-ampersand`

Then I ran the command `docker build -t ampersand:latest ampersand` and sat back \(for over an hour\) to watch an image being created.

## 10. Local Settings

To inspect and change the local settings, you need the file `localsettings.php` on directory `~/git/Ampersand-models/RAP3/include`. This step requires section 5 to be finished successfully. This file contains comments that guide you to use the correct settings in a development situation and in a production situation. Read the file and follow the instructions it contains, especially when making the transition from development to production.

## 11. Last minute changes before going to production

1. In the source code of RAP3, in the file SIAM\_importer.adl:
   1. disable "RAP3\_LoginForDevelopment.ifc", to prevent users from seeing 
   2. enable "RAP3\_LoginForProduction.ifc"
   3. disable "../SIAM/SIAM\_AutoLoginAccount.adl"
2. Is there anything we must alter in localsettings.php before going live?



