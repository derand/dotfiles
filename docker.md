
### Start boot2docker

    boot2docker start
    $(boot2docker shellinit)

### Start temp container and attach

    docker run -i -t resin/rpi-raspbian:wheezy bash

### Remove all unused images

    docker images -a -q |xargs docker rmi
