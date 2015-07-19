## This HowTo shows the way to build firmware image using Linux Containers. ##

This method allows you to create build environment in 2-5 minutes.

The first thing you'll need is to install <a href='http://docs.docker.com/installation/'>Docker</a>**.**

Put the following to file called `Dockerfile':
```
FROM debian:latest

RUN apt-get clean all && \
    apt-get -y update && \
    apt-get -y upgrade && \
    apt-get -y install  build-essential \
                        gawk \
                        pkg-config \
                        gettext \
                        automake \
                        autogen \
                        texinfo \
                        autoconf \
                        libtool \
                        bison \
                        flex \
                        zlib1g-dev \
                        libgmp3-dev \
                        libmpfr-dev \
                        libmpc-dev \
                        git \
                        sudo \
                        vim && \
    apt-get -y purge manpages \
                     xauth \
                     debconf-i18n && \
    apt-get -y autoremove && \
    apt-get -y autoclean && \
    apt-get clean all

WORKDIR /opt/rt-n56u/trunk
```

Create the image:
```
docker build --no-cache --rm -f Dockerfile -t fwbuilder:latest .
```

Run it:
```
docker run -it fwbuilder /bin/bash

# Clone remote repository:
git init /opt/rt-n56u
git remote add origin https://code.google.com/p/rt-n56u/
git pull origin master
```

Follow instructions to build the firmware:
```
cat /opt/rt-n56u/readme.eng.txt
```

If you type "exit" or press CTRL+D container stop running. If you need to start it again you need to find out its ID:
```
docker ps -a
docker start CONTAINER_ID
docker attach CONTAINER_ID
```

After that you can commit changes to the image in order not to create image every time.
Press _**[CTRL](CTRL.md)+P+Q**_ and run:
```
docker ps
docker commit CONTAINER_ID COMMIT_IMG_NAME
docker attach CONTAINER_ID
```
_<sup>(COMMIT_IMG_NAME - is any name you like)</sup>_


As an example you cat put aliases in global zone to ~/.bashrc:
```
alias clear_tree='docker run -t COMMIT_IMG_NAME ./clear_tree'
alias update_tree='docker run -t COMMIT_IMG_NAME git pull origin master'
alias build_firmware='docker run -t COMMIT_IMG_NAME ./build_firmware'
```

**Next time** to build the firmware you can run:
```
clear_tree
update_tree
build_firmware
```