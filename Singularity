BootStrap: docker
From: nvidia/cuda:10.2-devel-centos7

%labels
AUTHOR p.arcuri@cineca.it
VERSION v1.0


%post
yum install -y  git
mkdir -p /opt
cd /opt
git clone https://github.com/wilicc/gpu-burn.git
cd gpu-burn

# build gpu-burn
make COMPUTE=37

# create a run script
cat << EOF > gpu_burn.sh
#!/bin/bash
cd /opt/gpu-burn
./gpu_burn 120
EOF

chmod 755 gpu_burn.sh

%environment
export PATH=/opt/gpu-burn:${PATH}

%runscript
gpu_burn.sh

