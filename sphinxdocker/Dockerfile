FROM ubuntu:14.04
MAINTAINER me

RUN sudo apt-get update -qq && sudo apt-get install -y --force-yes \
    git \
    default-jdk \
    maven \
    gradle \
    
WORKDIR /usr/local/src
RUN git clone https://github.com/cmusphinx/sphinx4
WORKDIR /usr/local/src/sphinx4/sphinx4-core
RUN gradle build

