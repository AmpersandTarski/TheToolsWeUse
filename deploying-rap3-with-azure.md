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

Azure offers preconfigured installations to kick-start a virtual machine. I picked LAMP by Bitnami.

The following settings were made:

|  |  |
| :--- | :--- |
| server name | Kahl |
| type VM-disk | HDD |
| Admin user name | ampersandadmin |
| verification type | password \(Stef Joosten knows the password\) |
| Resource group | Ampersand |
| location | Western Europe |
| Size | 1 core, 1.75 GB, 2 disks, Max. IOP's 2x500 |
| Inbound ports | HTTP \(TCP/80\) |
|  | HTTPS \(TCP/443\) |
|  | SSH \(TCP/22\) |
|  |  |

 



