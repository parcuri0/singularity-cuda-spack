BootStrap: docker
From: nvidia/cuda:10.2-devel-centos7

%post
yum install -y  git
mkdir -p /opt
cd /opt
git clone https://github.com/wilicc/gpu-burn.git
cd gpu-burn

# build gpu-burn
make COMPUTE=37

