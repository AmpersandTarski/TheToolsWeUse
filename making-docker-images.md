# Docker image
Before anyone can deploy an ampersand-repository (RAP3) the following images must be present on docker-hub.
- `ampersandtarski/ampersand-rap`
- `ampersandtarski/ampersandtarski/ampersand-prototype-db`
- `ampersandtarski/ampersand-prototype`

This chapter is a recipe for creating those images. (If you are only installing, you do not need this chapter.)

## Installing Docker

I followed the instructions on `https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/` .

Then I checked that docker was installed by means of the `which`-command:

```
sjo@lnx-hrl-202v:~$ which docker
/usr/bin/docker
sjo@lnx-hrl-202v:~$ which docker-compose
/usr/bin/docker-compose
```

## 4. Making a Docker image

This step requires a server with docker, so you must have finished section 3 successfully. I cloned `https://github.com/docker-ampersand/docker-ampersand`into `/home/ampersandadmin/docker-ampersand by the following command`:

```
sudo -i
git clone https://github.com/AmpersandTarski/docker-ampersand/ /home/$(whoami)/docker-ampersand
cd docker-ampersand/
docker build -t ampersand:latest ampersand
```

and sat back to watch an image being created. This takes over an hour. I left the session up and running, because stopping the session means that the docker build process stops. After coming back a day later, I verified that the image is present by running the same command again. That produced the following output:

```
Wolfram docker-ampersand # docker build -t ampersand:latest ampersand
Sending build context to Docker daemon 4.096 kB
Step 1 : FROM php:7-apache
 ---> 2720c02fc079
Step 2 : ENV PATH /texlive/bin/x86_64-linux:$PATH
 ---> Using cache
 ---> 45d62477f5e2
Step 3 : RUN apt-get update  && apt-get install -y --no-install-recommends git graphviz wget xorriso  && curl -sSL https://get.haskellstack.org/ | /bin/sh  && rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> e37542ec9301
Step 4 : ENV TL_VERSION 2016-20160523
 ---> Using cache
 ---> f95346ded414
Step 5 : ADD texlive.profile /tmp
 ---> Using cache
 ---> add9fd911c38
Step 6 : RUN cd ~  && wget -q   http://mirrors.ctan.org/systems/texlive/Images/texlive$TL_VERSION.iso  && wget -qO- http://mirrors.ctan.org/systems/texlive/Images/texlive$TL_VERSION.iso.sha512 | sha512sum -c  && osirrox -report_about NOTE -indev texlive$TL_VERSION.iso -extract / /usr/src/texlive  && rm texlive$TL_VERSION.iso  && /usr/src/texlive/install-tl -profile /tmp/texlive.profile  && rm -rf /usr/src/texlive  && rm /tmp/texlive.profile
 ---> Using cache
 ---> f0ebcd4cf50c
Step 7 : RUN mkdir ~/git  && cd ~/git  && git clone --branch development https://github.com/AmpersandTarski/Ampersand
 ---> Using cache
 ---> 08643d5cce73
Step 8 : RUN cd ~/git/Ampersand  && stack setup  && stack install --local-bin-path /usr/local/bin
 ---> Using cache
 ---> 636036e98214
Step 9 : RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer  && php -r "unlink('composer-setup.php');"
 ---> Using cache
 ---> e8648c6657f6
Successfully built e8648c6657f6
```

When you build an image where nothing changes \(as shown above\), this takes virtually no time at all. However, if you run a fresh image from scratch, it takes a while. Should you want to close your SSH-session in which docker is running, that docker process will be killed. If you want to leave docker running in the background, `https://www.tecmint.com/keep-remote-ssh-sessions-running-after-disconnection/` will help. Best thing is to anticipate on it. However, if you didn't anticipate this, you can still send docker to the background by `^Z` and give the `disown -h` command. \(The latter is however the least elegant way.\)

## 5. Making containers

This step requires a server with docker and images to build containers with. So you must have finished section 4 successfully. We are making three containers: one for the database, one for the RAP3 application, and one for PhpMyAdmin. Containers are built from images by the command `docker-compose`:

```
cd /home/ampersandadmin/docker-ampersand
docker-compose up -d
```

This command brings all three containers up, for which it requires the file `docker-compose.yml`to be available in the current directory.

I checked whether the containers are running by means of the `docker ps` command.

Completion of this step allowed access to RAP3 from an arbitrary computer on the internet:

![](/assets/import.png)

The database is accessible on port 8080:

![](/assets/phpMyAdmin.png)

## 6. Maintenance

The `docker-compose up` command aggregates the output of each container. When the command exits, all containers are stopped. Running `docker-compose up -d` starts the containers in the background and leaves them running.

To interfere with RAP3 as it is running, you need to get into the Rap3 container. It is not enough just being on the server, because all the data is in the container \(rather than directly on the server\). To go into the Rap3 container, use the command

```
docker exec -ti dockerampersand_rap3_1 /bin/bash
```

## 10. Local Settings

To inspect and change the local settings, you need the file `localsettings.php` on directory `~/git/Ampersand-models/RAP3/include`. This step requires section 5 to be finished successfully. This file contains comments that guide you to use the correct settings in a development situation and in a production situation. Read the file and follow the instructions it contains, especially when making the transition from development to production.

## 11. Last minute changes before going to production

1. In the source code of RAP3, in the file SIAM\_importer.adl:
   1. disable "RAP3\_LoginForDevelopment.ifc", to prevent users from seeing 
   2. enable "RAP3\_LoginForProduction.ifc"
   3. disable "../SIAM/SIAM\_AutoLoginAccount.adl"
2. Is there anything we must alter in localsettings.php before going live?



