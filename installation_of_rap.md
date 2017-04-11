# Installation of RAP

RAP is a tool that is being used by the Open University of the Netherlands in the course [Rule Based Design](http://portal.ou.nl/web/ontwerpen-met-bedrijfsregels). It lets students analyse Ampersand models, generate functional specifications and make prototypes of information systems. It is the primary tool for students in relation to Ampersand.

We are currently working on a new version, RAP3. We hope to deploy RAP3 on November 1st, 2016. Deployment means to install RAP3 on a web server, to make it work for a group of students. This text explains how. Even though RAP3 is not ready for use, it can already be installed on a server. It just won't let you use all features.

**NOTE 2**: Be very cautious not to break RAP2! RAP2 is still needed as a safety precaution, in case we cannot deliver RAP3 in time.

## Requirements for deploying RAP

##### 1. Setting up a server

You need a server that is connected to the internet, because RAP takes updates from a GitHub repository. A 4-core/8GB server is sufficient. A memory size under 3GB has shown to be insufficient. Ports for HTTP, HTTPS, SSL, and SFTP must be open.

##### 2. Getting MariaDB \(MySQL\) and phpMyAdmin to work

You need a database and a web-server. This explains why a LAMP-server is an obvious choice if you use a preconfigured server.

##### 3. Uploading and running RAP3

A quick way to install is to copy existing RAP3 code on your server. This allows you to test whether you can get the application live and visible to your users.

##### 4. Filling the Git repository with Ampersand files and Ampersand models

The source code of Ampersand and the source code of RAP3 must be downloaded from GitHub. The following repositories are used:

* Ampersand: _**development**_ branch \([https://github.com/AmpersandTarski/Ampersand/tree/development](https://github.com/AmpersandTarski/Ampersand/tree/development)\). This contains the source code of Ampersand.
* ampersand-models: _**master**_ branch \([https://github.com/AmpersandTarski/ampersand-models.git](https://github.com/AmpersandTarski/ampersand-models.git)\). This contains the source code of RAP3.

The source code of Ampersand is needed to build an Ampersand compiler. The source code of RAP3 is needed to compile and generate the RAP3 webapplication. You need Git to create a local clone of these repositories. Git is preferred over copying the files, because it gives assurance over installing the right version\(s\).

##### 5. Installing Haskell

You need Haskell to build an Ampersand compiler.

##### 6. Creating an Ampersand compiler

You need an Ampersand compiler to generate RAP3 from its source code.

##### 7. Installing LaTeX and GraphViz

LaTeX and GraphViz are called when a RAP3 user generates documentation. Therefore, they must be installed on the server.

##### 8. Installing SmartGit \(a nice-to-have\)

If you want to inspect the Git-repository on you server, it is nice to have a Git client.

##### 9. Generating the RAP3 application

You need to generate RAP3 to facilitate regular updates to the system.

##### 10. Local Settings

Some local settings may apply, which are brought together in one file. Use this to administer things like database account\(s\) and PHP time limit, logging, etcetera.

##### 11. Last minute changes before going to production

Things that are necessary for testing and development, such as logging, can be changed in the production version. These things are usually adapted shortly before going to production.

# Work in progress!

The application of RAP still is heavily under development. Therefore, this recipe might change. Also, instructions about maintenance will follow. Watch the progress of RAP3 by checking [this issue](https://github.com/AmpersandTarski/Ampersand/issues/449)

## Experience

RAP3 has been installed in different situations. Some of these situations are documented in the sequel. You can use it as example for deployments of your own. A dear wish is to create an installation script that will automate deployment, but we have not yet found the time to do that.

## Security

The Apache server writes files and creates directories. Normally, this would be a security risk, but in this case it is designed behaviour.

## Questions? Need help?

Don't hesitate to contact Han Joosten. He'll be glad to help out.

