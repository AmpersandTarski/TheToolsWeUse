# Deploying to your own laptop

If you want to deploy RAP4 to your laptop, this chapter tells you how.

Each step in the installation process gets a separate section in this text.

This example has worked on my Macbook. If not, you may either change the commands below to the commands of your own computer, or set up a virtual linux machine on your laptop.



## Installing Docker

I installed docker following the instructions on `https://docs.docker.com/`

Then I checked that everything went successfully by means of the `which`-command:

```text
$ which docker
/usr/bin/docker
$ 
```

## Obtaining the files we need

We need only one file: `docker-compose.yml`  
To get it, I used the `wget` command, which gets stuff from the web:

```text
$ mkdir RAP4
$ cd RAP4
$ wget https://raw.githubusercontent.com/AmpersandTarski/RAP/master/docker-compose.yml
$ 
```

## Installing RAP4

To install RAP4 I have to type two commands:

```text
$  docker network create proxy
3f9552a7506ac5f2b5d9fcb158edae82f9f64e4e3d6b093916d624d118ba342a
$ docker compose up -d       
[+] Running 8/8
 ⠿ Network rap_db                           Created                        4.7s
 ⠿ Network rap_default                      Creat...                       4.0s
 ⠿ Container rap_dummy-student-prototype_1  Started                        4.5s
 ⠿ Container traefik                        Started                        6.9s
 ⠿ Container rap4-db                        Started                        5.1s
 ⠿ Container enroll                         Started                       12.4s
 ⠿ Container rap4                           Started                       12.6s
 ⠿ Container phpmyadmin                     Star...                       12.1s
$ 
```

To check whether this worked, I went to my browser and navigated to `http://localhost`.

I checked whether the containers are running by means of the `docker ps` command.

```text
$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS                                                                      NAMES
43edb0f3a4aa   2d806de52e67   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp                                                                     phpmyadmin
a6b937c3fe93   8edf637cc6bc   "docker-php-entrypoi…"   About a minute ago   Up About a minute   80/tcp                                                                     rap4
48f6477fdab8   ad69046676ea   "docker-php-entrypoi…"   About a minute ago   Up About a minute   80/tcp                                                                     enroll
d7ebdb394bfd   f965f5a1fff8   "/entrypoint.sh trae…"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, :::80->80/tcp, 0.0.0.0:443->443/tcp, :::443->443/tcp   traefik
982bacd58ba6   30a3b1fa460a   "docker-entrypoint.s…"   About a minute ago   Up About a minute   3306/tcp                                                                   rap4-db
$ 
```

Completion of this step allowed access to RAP4 from `localhost`:

![](../.gitbook/assets/schermafbeelding-2021-07-31-om-08.31.22.png)

Note that RAP runs on the insecure `http://` instead of `https://`.  This is not a problem if you keep your laptop safe from outsiders tresspassing. If you [depoy to a server](deploying-ounl-rap3.md), you need the setup for `https://`.

You will find that the database is accessible on `http://phpmyadmin/localhost`

![](../.gitbook/assets/schermafbeelding-2021-07-31-om-08.36.16.png)

The demonstration application, Enrollment, is accessible on `http://enroll.localhost`

![](../.gitbook/assets/schermafbeelding-2021-07-31-om-08.37.47.png)

