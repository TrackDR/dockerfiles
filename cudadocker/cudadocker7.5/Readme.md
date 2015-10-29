#cudadocker75

Install docker:

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9; sudo sh -c "echo deb https://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list"; sudo apt-get update; sudo apt-get install lxc-docker

Run docker instance:

sudo docker pull trackdr/cudadocker; cd /usr/local/cuda/samples/1_Utilities/deviceQuery; make; /home/ubuntu/NVIDIA_CUDA-7.5_Samples/bin/x86_64/linux/release/deviceQuery; DOCKER_NVIDIA_DEVICES="--device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidiactl:/dev/nvidiactl --device /dev/nvidia-uvm:/dev/nvidia-uvm"; sudo docker run -ti $DOCKER_NVIDIA_DEVICES trackdr/cudadocker /bin/bash

Download samples for cuda:

chmod +x cuda_linux.run; ./cuda_linux.run -extract=pwd; ./cuda-samples-linux-*.run -noprompt; cd /usr/local/cuda-7.5/samples/1_Utilities/deviceQuery; make; ../../bin/x86_64/linux/release/deviceQuery

