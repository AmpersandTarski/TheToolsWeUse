---
description: >-
  When you deploy RAP you may run into situations where RAP does not work. This
  section is meant to help you to ensure that all deployment conditions are
  satisfied in your configuration.
---

# Deployment Configuration

## Permissions for log files

Write permission is needed for log files. The pod in which RAP runs defines a volume called `log` in which the log files are written. This means that the files are stored outside the container on the machine that hosts the docker platform. 

## Docker group

You have a host computer in which the docker platform runs. \(In deploying RAP3 for the OUNL that would be the machine with domain name `rap.cs.ou.nl`\). To avoid permission errors \(and the use of `sudo`\), add your user to the `docker` group. [Read more](https://docs.docker.com/engine/installation/linux/linux-postinstall/).

