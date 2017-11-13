# Installation of RAP

RAP is a **R**epository for **A**mpersand **P**rojects. This tool is being used by the Open University of the Netherlands in the course [Rule Based Design](http://portal.ou.nl/web/ontwerpen-met-bedrijfsregels). It lets students analyse Ampersand models, generate functional specifications and make prototypes of information systems. It is the primary tool for students in relation to Ampersand.

Deployment means to install RAP3 on a web server, to make it work for a group of students. This text explains how.

## Automated deployment

We use Docker for automating the deployment and making RAP portable over different platforms. The following two sections report what we have done:

* to [deploy RAP on an Ordina server](/deploying-rap3-on-docker.md) in the Azure cloud;

* to [deploy RAP at the Open University](/deploying-ounl-rap3.md) on a server in the OUNL-datacenter.

These two reports will most likely contain enough information to let you reproduce the installation on a server of your own.

The last section of this chapter discusses the [making of docker images](/making-docker-images.md). You need a docker image in order to deploy RAP3.

## What Docker needs to do...

Docker is sheer magic. You don't have to understand it to run it. However, if you insist on knowing how it is done...

Here are ten steps to install RAP3 manually on a freshly created server:

#### 1. Setting up a server

You need a server that is connected to the internet, because RAP takes updates from a GitHub repository. A 2-core/8GB server is sufficient. A memory size under 3GB has shown to be insufficient. Ports for HTTP, HTTPS, SSL, and SFTP must be open.

#### 2. Getting MariaDB \(MySQL\) and phpMyAdmin to work

You need a database and a web-server. This explains why a LAMP-server is an obvious choice if you use a preconfigured server.

#### 3. Uploading and running RAP3

A quick way to install is to copy existing RAP3 code on your server. This allows you to test whether you can get the application live and visible to your users.

#### 4. Filling the Git repository with Ampersand files and Ampersand models

The source code of Ampersand and the source code of RAP3 must be downloaded from GitHub. The following repositories are used:

* Ampersand: _**development**_ branch \([https://github.com/AmpersandTarski/Ampersand/tree/development](https://github.com/AmpersandTarski/Ampersand/tree/development)\). This contains the source code of Ampersand.
* ampersand-models: _**master**_ branch \([https://github.com/AmpersandTarski/ampersand-models.git](https://github.com/AmpersandTarski/ampersand-models.git)\). This contains the source code of RAP3.

The source code of Ampersand is needed to build an Ampersand compiler. The source code of RAP3 is needed to compile and generate the RAP3 webapplication. You need Git to create a local clone of these repositories. Git is preferred over copying the files, because it gives assurance over installing the right version\(s\).

#### 5. Avoiding to install Haskell

You need Haskell to build an Ampersand compiler. For deploying RAP, we use the latest executable Ampersand-compiler for Linux, which is published periodically on the internet. This way, Haskell need not be installed

#### 6. Creating an Ampersand compiler

If you want, create your own Ampersand compiler. This way, you can pick a version by which to generate RAP3.

#### 7. Installing LaTeX and GraphViz

LaTeX and GraphViz are called by RAP3 to generate documentation. Therefore, both must be installed on the server.

#### 8. Generating the RAP3 application

You need to generate RAP3 to facilitate regular updates to the system.

#### 9. Local Settings

Some local settings may apply, which are brought together in one file. Use this to administer things like database account\(s\) and PHP time limit, logging, etcetera.

#### 10. Last minute changes before going to production

Things that are necessary for testing and development, such as logging, can be changed in the production version. These things are usually adapted shortly before going to production.

## Questions? Need help?

Don't hesitate to contact Han Joosten. He'll be glad to help out.

