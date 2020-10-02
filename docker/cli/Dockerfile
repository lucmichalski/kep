FROM library/python:3.7.1-alpine
MAINTAINER Michalski Luc <michalski.luc@gmail.com>

# change to temp dir
WORKDIR /temp

# install git and build-base (GCC, etc.)
RUN apk update && apk upgrade && \
    apk add --no-cache --no-progress bash git openssh && \
    apk add build-base

# install yake via pip
RUN pip install git+https://github.com/liaad/pke.git

# set default command
ENTRYPOINT ["pke"]
