# Start with CUDA base image
FROM trackdr/cudadocker/cudadocker7.5
MAINTAINER me

# Install opencv prerequisites...
RUN sudo apt-get update -qq && sudo apt-get install -y --force-yes \
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
    unzip;

# RUN sudo apt-get clean

# RUN sudo pip3 install numpy

# RUN mkdir /usr/local/src

# Build CMake 3.3.2 to autodetect Python 3.4 and higher for OpenCV Build
# =================================
WORKDIR /usr/local/src
RUN wget https://cmake.org/files/v3.3/cmake-3.3.2.tar.gz
RUN tar zxvpf cmake-3.3.2.tar.gz
WORKDIR /usr/local/src/cmake-3.3.2
RUN ./configure
RUN make -j6
RUN make install
ENV CMAKE_ROOT=/usr/local/share/cmake-3.3

# Build OpenCV 3.x
# =================================
WORKDIR /usr/local/src
RUN git clone https://github.com/Itseez/opencv.git
RUN git clone https://github.com/Itseez/opencv_contrib.git
RUN git clone https://github.com/Itseez/opencv_extra.git
ENV OPENCV_TEST_DATA_PATH=/usr/local/src/opencv_extra/testdata/
RUN mkdir -p opencv/release
WORKDIR /usr/local/src/opencv/release
RUN cmake -D CMAKE_BUILD_TYPE=RELEASE \
          -D CMAKE_INSTALL_PREFIX=/usr/local \
          -D WITH_FFMPEG=ON \
          -D WITH_EIGEN=ON \
          -D WITH_TBB=ON \
          -D WITH_V4L=ON \
          -D WITH_CUDA=ON \
          -D INSTALL_C_EXAMPLES=ON \
          -D INSTALL_PYTHON_EXAMPLES=ON \
          -D BUILD_EXAMPLES=ON \
          -D INSTALL_TESTS=ON \
          -D WITH_NVCUVID=OlN \
          -D WITH_IPP=OFF \
          -D OPENCV_EXTRA_MODULES_PATH=/usr/local/src/opencv_contrib/modules \
          /usr/local/src/opencv
RUN make -j6
RUN sudo make install
RUN sudo sh -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'
RUN sudo ldconfig

# Additional python modules
RUN sudo pip2 install imutils
RUN sudo pip3 install imutils

# =================================

# Remove all tmpfile
# =================================
WORKDIR /usr/local/
#RUN rm -rf /usr/local/src
# =================================

WORKDIR /data
