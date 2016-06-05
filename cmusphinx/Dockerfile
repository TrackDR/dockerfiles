FROM ubuntu:14.04
MAINTAINER me

# Install wget and build-essential
RUN sudo apt-get update && apt-get install -y --force-yes \
    git \
    g++ \
    autoconf \
    automake \
    build-essential \
    checkinstall \
    cmake \
    pkg-config \
    yasm \
    libtiff4-dev \
    libpng-dev \
    libjpeg-dev \
    libjasper-dev \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev \
    libdc1394-22-dev \
    libxine-dev \
    libgstreamer0.10-dev \
    libgstreamer-plugins-base0.10-dev \
    libv4l-dev \
    libtbb-dev \
    libgtk2.0-dev \
    libmp3lame-dev \
    libopencore-amrnb-dev \
    libopencore-amrwb-dev \
    libtheora-dev \
    libvorbis-dev \
    libxvidcore-dev \
    libtool \
    v4l-utils \
    default-jdk \
    wget \
    python-dev \
    python3-dev \
    python-numpy \
    python3-numpy \
    python-pip \
    python3-pip \
    libmp3lame-dev \
    x264 \
    libeigen3-dev \
    unzip \
    default-jdk \
    maven \
    gradle \
    gradle-doc \
    libgradle-core-java \
    libgradle-plugins-java \
    sox \
    mlocate \
    emacs;

WORKDIR /usr/local/src
RUN git clone https://github.com/cmusphinx/sphinx4

WORKDIR /usr/local/src/sphinx4
RUN gradle build
