# gpucaffeipythondockeralt

cd; openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Install docker:

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9; sudo sh -c "echo deb https://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list"; sudo apt-get update; sudo apt-get install lxc-docker

Download cuda samples:

wget http://developer.download.nvidia.com/compute/cuda/7_0/Prod/local_installers/cuda_7.0.28_linux.run

Pull from dockerhub and run docker instance:

sudo docker pull trackdr/caffegpucaffeipythondockeralt; cd /usr/local/cuda-7.0/samples/1_Utilities/deviceQuery; make; /home/ubuntu/NVIDIA_CUDA-7.0_Samples/bin/x86_64/linux/release/deviceQuery; DOCKER_NVIDIA_DEVICES="--device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidiactl:/dev/nvidiactl --device /dev/nvidia-uvm:/dev/nvidia-uvm"; 
sudo docker run -d $DOCKER_NVIDIA_DEVICES -v /home/ubuntu/mycert.pem:/mycert.pem -p 5910:8888 -e "PASSWORD=replacethispassword" trackdr/gpucaffeipythondockeralt; sudo docker ps

OR Clone this repo and build and run docker instance:
git clone https://github.com/TrackDR/gpucaffeipythondockeralt; sudo docker build gpucaffeipythondockeralt; cd /usr/local/cuda-7.0/samples/1_Utilities/deviceQuery; make; /home/ubuntu/NVIDIA_CUDA-7.0_Samples/bin/x86_64/linux/release/deviceQuery; DOCKER_NVIDIA_DEVICES="--device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidiactl:/dev/nvidiactl --device /dev/nvidia-uvm:/dev/nvidia-uvm"; 
sudo docker run -d $DOCKER_NVIDIA_DEVICES -v /home/ubuntu/mycert.pem:/mycert.pem -p 5910:8888 -e "PASSWORD=replacethispassword" gpucaffeipythondockeralt; sudo docker ps

Run downloaded samples for cuda:

chmod +x cuda_7.0.28_linux.run; ./cuda_7.0.28_linux.run -extract=\`pwd\`; ./cuda-samples-linux-*.run -noprompt; cd /usr/local/cuda-7.0/samples/1_Utilities/deviceQuery; make; ../../bin/x86_64/linux/release/deviceQuery

cd /opt/caffe; make runtest

List containers:

sudo docker ps

Attach to instance:

sudo docker exec -it containerid bash

