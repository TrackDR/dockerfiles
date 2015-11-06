# Start with CUDA base image
FROM trackdr/cudadocker/cuda7.5docker
MAINTAINER me

# Install git, bc and dependencies
RUN apt-get update && apt-get install -y \
  git \
  bc \
  libatlas-base-dev \
  libatlas-dev \
  libboost-all-dev \
  libprotobuf-dev \
  libgoogle-glog-dev \
  libgflags-dev \
  protobuf-compiler \
  libhdf5-dev \
  libleveldb-dev \
  liblmdb-dev \
  libsnappy-dev \
  python-pip \
  python-dev \
  python3-pip \
  python3-dev \
  python-numpy \
  python-scipy \
  python-skimage \
  python-protobuf \
  python-yaml \
  libopencv-dev

# Copy cudnn libraries into docker file
COPY cuda/lib64/libcudnn.so /usr/local/cuda/lib64/libcudnn.so
COPY cuda/lib64/libcudnn.so.7.0 /usr/local/cuda/lib64/libcudnn.so.7.0
COPY cuda/lib64/libcudnn.so.7.0.64 /usr/local/cuda/lib64/libcudnn.so.7.0.64
COPY cuda/include/cudnn.h /usr/local/cuda/include/cudnn.h
COPY cuda_7.5.18_linux.run /cuda_7.5.18_linux.run

WORKDIR /
RUN ./cuda_7.5.18_linux.run -extract=`pwd`
RUN ./cuda-samples-linux-*.run -noprompt
RUN cd /usr/local/cuda/samples/1_Utilities/deviceQuery && make

# Clone Caffe repo and move into it
RUN cd /opt && git clone -b future https://github.com/longjon/caffe && cd caffe
RUN cd /opt/caffe/python && for req in $(cat requirements.txt); do pip install $req; done
RUN cd /opt/caffe && cp Makefile.config.example Makefile.config
RUN cd /opt/caffe && sed -i '/^# WITH_PYTHON_LAYER := 1/s/^# //' Makefile.config
RUN cd /opt/caffe && sed -i '/^# USE_CUDNN := 1/s/^# //' Makefile.config
RUN cd /opt/caffe && make -j12 all
RUN cd /opt/caffe && make pycaffe
RUN cd /opt/caffe && make test

ENV PYTHONPATH /opt/caffe/python:$PYTHONPATH

