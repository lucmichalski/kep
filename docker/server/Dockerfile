FROM library/python:3.7.1-alpine
MAINTAINER Michalski Luc <michalski.luc@gmail.com>

# change to temp dir
WORKDIR /temp

# install git and build-base (GCC, etc.)
RUN apk update && apk upgrade && \
    apk add --no-cache --no-progress bash git openssh lapack-dev musl-dev g++ gcc gfortran && \
    apk add build-base && \
    python -m pip install -U pip

RUN pip install flasgger

# install requirements first to engage docker cache
RUN wget https://raw.githubusercontent.com/LIAAD/kep/master/requirements.txt -O requirements.txt
RUN pip install -r requirements.txt

# install kep and dependencies via pip
RUN pip install git+https://github.com/liaad/kep.git
RUN pip install git+https://github.com/boudinfl/pke
RUN pip install git+https://github.com/LIAAD/yake.git
RUN pip install langcodes

# install spacy language models
RUN python -m spacy download en && \
    python -m spacy download es && \
    python -m spacy download fr && \
    python -m spacy download pt && \
    python -m spacy download de && \
    python -m spacy download it && \
    python -m spacy download nl && \
    python -m spacy download el

# Copy server startup script
COPY ./kep-rest-api.py /temp

# Expose server port
ENV SERVER_PORT 5890
EXPOSE "$SERVER_PORT"

RUN apk add --no-cache --no-progress nano bash

# set default command
CMD [ "python", "kep-rest-api.py" ]
