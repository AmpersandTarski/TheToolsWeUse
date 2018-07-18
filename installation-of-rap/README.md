# Installation of RAP

RAP is a **R**epository for **A**mpersand **P**rojects. This tool is being used by the Open University of the Netherlands in the course [Rule Based Design](http://portal.ou.nl/web/ontwerpen-met-bedrijfsregels). It lets students analyse Ampersand models, generate functional specifications and make prototypes of information systems. It is the primary tool for students in relation to Ampersand.

Deployment means to install RAP3 on a web server, to make it work for a group of students. This text explains how.

## The short story
You will find the complete and most recent source code of RAP3 on https://github.com/AmpersandTarski/RAP. The two steps are:
1. Build a docker-image from that source code.
2. Run that image on a docker platform.

It works on any computer that runs Docker. To do it you need two commands, one for each step.

To build a docker-image of RAP3, open a command line interface, clone the RAP repository (if you haven't already), go to the root directory of RAP and give the following command:
```
   .../git/RAP> docker build --tag ampersandtarski/ampersand-rap:latest .
```

If you want to deploy it, use
```
   .../git/RAP> docker-compose up -d
```
This deploys the RAP3 service on your docker-platform using the file ``docker-compose.yml``.

Now browse (preferrably in Chrome or Firefox) to http://localhost/RAP3 to see it work. If you want to deploy on different servers, you must adapt the `docker-compose.yml`-file in the root directory of the RAP repository.

## Examples of RAP3 deployment

We have deployed RAP3 on two servers and documented what we have done. Taken as examples, it might help you reproduce the installation on a server of your own:

* [deploying RAP on an Ordina server](deploying-rap3-with-azure-on-ubuntu.md) in the Azure cloud;
* [deploying RAP at the Open University](deploying-ounl-rap3.md) on a server in the OUNL-datacenter.


## What Docker does for you...

Docker is sheer magic. So stop reading here if you enjoy the magic. After all, you don't have to understand the process to run it. However, if you insist... Read on and learn how the trick is done. Don't blame us for spoiling the trick, though!

Here are ten steps to install RAP3 manually, without Docker, on a freshly created server:

### 1. Setting up a server

You need a server that is connected to the internet, because RAP takes updates from a GitHub repository. A 2-core/8GB server is sufficient. A memory size under 3GB has shown to be insufficient. Ports for HTTP, HTTPS, SSL, and SFTP must be open.

### 2. Getting MariaDB \(MySQL\) and phpMyAdmin to work

You need a database and a web-server. This explains why a LAMP-server is an obvious choice if you use a preconfigured server.

### 3. Uploading and running RAP3

A quick way to install is to copy the source code of RAP3 on your server and compile it with Ampersand. That gives you the RAP3 webapplication. You will find the complete Ampersand source code of RAP3 on [https://github.com/AmpersandTarski/RAP](https://github.com/AmpersandTarski/RAP). The main file is `./RAP3/RAP3.adl`.

### 4. Filling the Git repository with Ampersand files and Ampersand models

If you don't have an Ampersand compiler, you can build one using the Haskell sources of that compiler. You will find the source code on the development branch of the Ampersand repository \([https://github.com/AmpersandTarski/Ampersand/tree/development](https://github.com/AmpersandTarski/Ampersand/tree/development)\).

Use Git to create a local clone of these repositories. Git is preferred over copying the files, because you can repeatedly use it to ensure you get the right version.

### 5. Avoiding to install Haskell

To build an Ampersand compiler, you need Haskell. However, you can also use the latest executable Ampersand-compiler, which is published periodically on [http://ampersandtarski.github.io/](http://ampersandtarski.github.io/). This way, you don't need to build Ampersand and you can avoid installing Haskell.

### 6. Creating an Ampersand compiler

If you want, create your own Ampersand compiler. This way, you can pick a version by which to generate RAP3.

### 7. Installing LaTeX and GraphViz

LaTeX and GraphViz are called by RAP3 to generate documentation. Therefore, both must be installed on the server.

### 8. Generating the RAP3 application

You need to generate RAP3 to facilitate regular updates to the system.

### 9. Local Settings

Some local settings may apply, which are brought together in one file. Use this to administer things like database account\(s\) and PHP time limit, logging, etcetera.

### 10. Last minute changes before going to production

Things that are necessary for testing and development, such as logging, can be changed in the production version. These things are usually adapted shortly before going to production.

## Questions? Need help?

Don't hesitate to contact Han Joosten. He'll be glad to help out.

