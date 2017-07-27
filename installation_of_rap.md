# Installation of RAP

RAP is a **R**epository for **A**mpersand **P**rojects. This tool is being used by the Open University of the Netherlands in the course [Rule Based Design](http://portal.ou.nl/web/ontwerpen-met-bedrijfsregels). It lets students analyse Ampersand models, generate functional specifications and make prototypes of information systems. It is the primary tool for students in relation to Ampersand.

We are currently working on a new version, RAP3. We hope to deploy RAP3 on November 1st, 2017. Deployment means to install RAP3 on a web server, to make it work for a group of students. This text explains how. Even though RAP3 is lacking some features, it can already be installed on a server.

## Automated deployment
RAP is meant to run on a server, so that multiple users can use it 24/7. We use Docker for automating the deployment and making RAP portable over different platforms.

Two docker installations are reported in the following sections. It will most likely contain enough information to let you reproduce the installation on a server of your own.

The last section of this chapter discusses the [making of docker images](/making-docker-images.md), mainly for maintenance purposes.

## Questions? Need help?
Don't hesitate to contact Han Joosten. He'll be glad to help out.

