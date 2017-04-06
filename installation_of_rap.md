# Installation of RAP

RAP is a tool that is being used by the Open University of the Netherlands in the course [Rule Based Design](http://portal.ou.nl/web/ontwerpen-met-bedrijfsregels). It lets students analyse Ampersand models, generate functional specifications and make prototypes of information systems. It is the primary tool for students in relation to Ampersand.

We are currently working on a new version, RAP3. We hope to deploy RAP3 on November 1st, 2016. Deployment means to install RAP3 on a web server, to make it work for a group of students. This text explains how. Even though RAP3 is not ready for use, it can already be installed on a server. It just won't let you use all features.

**NOTE 1**: Because RAP is still in development, the branches to use in this stage are:

* Ampersand: _**development**_ branch \([https://github.com/AmpersandTarski/Ampersand/tree/development](https://github.com/AmpersandTarski/Ampersand/tree/development)\)
* ampersand-models: _**master**_ branch \([https://github.com/AmpersandTarski/ampersand-models.git](https://github.com/AmpersandTarski/ampersand-models.git)\)

**NOTE 2**: Be very cautious not to break RAP2! RAP2 is still needed as a safety precaution, in case we cannot deliver RAP3 in time.

## Recipe to install RAP:

Ampersand at the Open University of the Netherlands \(OUNL\)

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

## 2. Getting MySQL and phpMyAdmin to work

## 3. Uploading and running RAP3

## 4. Filling the Git repository with Ampersand files and Ampersand models

## 5. Installing Haskell

## 6. Creating an Ampersand-compiler

## 7. Installing LaTeX and GraphViz

## 8. Installing SmartGit \(a nice-to-have\)

## 9. Generating the RAP3 application

## 10. Local Settings

## 11. Last minute changes before going to production

# Work in progress!

The application of RAP still is heavily under development. Therefore, this recipe might change. Also, instructions about maintenance will follow. Watch the progress of RAP3 by checking [this issue](https://github.com/AmpersandTarski/Ampersand/issues/449)

## Questions? Need help?

Don't hesitate to contact Han Joosten. He'll be glad to help out.

