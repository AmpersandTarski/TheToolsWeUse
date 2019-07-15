---
description: >-
  If you need an Ampersand compiler in a Docker image, use the one on Docker
  hub. It sits there ready for you to use. However, if you want to know how it
  is baked, carry on reading.
---

# Baking a Docker image that contains the Ampersand Compiler

## What I did

I wrote a Docker file that contains a recipe for building an Ampersand compiler and put it in the Ampersand repository on [docker/Dockerfile](https://github.com/AmpersandTarski/Ampersand/blob/feature/dockerize/docker/Dockerfile). Here are your ingredients for running it:

1. A machine that runs docker, to build your docker image with. I ran it on my MacBook.
2. Docker, which you need [installed on your machine](https://docs.docker.com/install/).
3. I am using 5G of memory to run Docker in. This is more than the standard 2G , which was insufficient for Ampersand. I used [this instruction](https://stackoverflow.com/questions/44533319/how-to-assign-more-memory-to-docker-container/44533437#44533437) to increase Docker's memory on my Macbook.

To run it, I cloned the Ampersand repository, into `~\Ampersand\`, and built the image with:

```text
docker build -f docker/Dockerfile -t myampersand:latest ~\Ampersand\
```

## The steps in the Docker file

Let us discuss the steps one-by-one. \(Please check [docker/Dockerfile](https://github.com/AmpersandTarski/Ampersand/blob/feature/dockerize/docker/Dockerfile), just in case it is inconsistent with this documentation.\) All of these steps happen automatically, as they are in the docker file.

The first statement states that the compiler is built on an Ubuntu vs. 16.04, which is rather arbitrary but consistent throughout the automated building process. For the sake of maintainability, we want the compiler to be generated on the same platform as it is used.

```text
FROM ubuntu:16.04 AS haskellstage
```

This building stage is called haskellstage because we use the Haskell compiler to build an Ampersand compiler. We use a [2-stage build](https://docs.docker.com/develop/develop-images/multistage-build/) to get a small Ampersand image without excess-software.

We use curl to obtain resources from the internet and git-core to clone source code from the Ampersand repository. So we `apt-get` both of them:

```text
RUN apt-get update &&\
    apt-get --yes install curl && \
    apt-get --yes install git-core
```

We use `stack` as our Haskell build system, so we get that from the internet. Haskell comes with stack, so no need to get Haskell separately.

```text
RUN curl -sSL https://get.haskellstack.org/ | sh
```

I made a working directory for no other purpose than to have everything in an empty directory.

```text
WORKDIR /Ampersand/
```

I used `git clone` to get the ampersand source files. It requires the directory to be empty

```text
# RUN git clone https://github.com/AmpersandTarski/Ampersand/ .
```

Ensure that the correct branch has been checked out, avoiding unexpected results just in case the repository has been left in some branch unintendedly.

```text
RUN git checkout development
```

Setting up the Haskell stack downloads approximately 177MB from the internet. Don't worry about the correct version of Haskell. It is specified in `stack.yaml`.

```text
RUN stack setup
```

Now everything is in place to compile Ampersand, resulting in a full-fledged Ampersand compiler. The executables are left in `/root/.local/bin`.

```text
RUN stack install
```

Now we go on the the production stage. We want a clean machine, identical to the one the code was generated in. So we use `ubuntu:16.04` again.

```text
FROM ubuntu:16.04
```

Now all we have to do is copy the executable to `/usr/local/bin`, where it normally sits.

```text
COPY --from=haskellstage /root/.local/bin
```

The next step needs attention. For some reason the following needs to be copied or else ampersand does not work. It yields a 3MB larger image. I'd like to know why this is necessary, because not knowing does not help to prevent maintenance tasks.

```text
COPY --from=haskellstage /usr/lib/x86_64-linux-gnu/libgmp* /usr/lib/x86_64-linux-gnu/
```

Just to check the version, I am asking at compile-time for the Ampersand version. Its SHA should be the same as you intended when you checked in your software into the Ampersand repository.

```text
RUN ampersand --version
```

