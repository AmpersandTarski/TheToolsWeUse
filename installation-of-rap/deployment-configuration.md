---
description: >-
  When you deploy RAP you may run into situations where RAP does not work. This
  section is meant to help you to ensure that all deployment conditions are
  satisfied in your configuration.
---

# Deployment Configuration

## Permissions for log files

Write permission is needed for log files. The pod in which RAP runs defines a volume called `log` in which the log files are written. This means that the files are stored outside the container on the machine that hosts the docker platform. 

