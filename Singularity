# Spack container (https://github.com/spack/spack)
#    Set the user argument 'package' to specify the Spack package to
#    install.  Otherwise, it will just build a base Spack container
#    image.
# 
#    Sample workflow:
# $ hpccm.py --recipe recipes/spack.py --userarg package="gromacs@2018.2 +cuda" > Dockerfile.gromacs.spack
# $ docker build -t gromacs.spack -f Dockerfile.gromacs.spack .
# $ nvidia-docker run --rm -ti gromacs.spack bash -l
# container:/> spack load gromacs
# 

BootStrap: docker
From: nvidia/cuda:10.2-devel-centos7
%post
    . /.singularity.d/env/10-docker*.sh

# Python
%post
    yum install -y \
        python2 \
        python3
    rm -rf /var/cache/yum/*

# GNU compiler
%post
    yum install -y \
        gcc \
        gcc-c++ \
        gcc-gfortran
    rm -rf /var/cache/yum/*

%post
    cd /
    mkdir -p /opt && cd /opt && git clone --depth=1 --branch v0.16.1 https://github.com/spack/spack spack && cd -
    ln -s /opt/spack/share/spack/setup-env.sh /etc/profile.d/spack.sh
    ln -s /opt/spack/share/spack/spack-completion.bash /etc/profile.d

%environment
    export FORCE_UNSAFE_CONFIGURE=1
    export PATH=/opt/spack/bin:$PATH
%post
    export FORCE_UNSAFE_CONFIGURE=1
    export PATH=/opt/spack/bin:$PATH

%post
    cd /
    spack install [u'gcc@10.1', u'openmpi%gcc10.1']
    spack clean --all


