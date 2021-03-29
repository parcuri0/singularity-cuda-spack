# Python
%post
    apt-get update -y
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python \
        python3
    rm -rf /var/lib/apt/lists/*

# GNU compiler
%post
    apt-get update -y
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        g++ \
        gcc \
        gfortran
    rm -rf /var/lib/apt/lists/*

%post
    apt-get update -y
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        autoconf \
        build-essential \
        bzip2 \
        ca-certificates \
        coreutils \
        curl \
        environment-modules \
        git \
        gzip \
        libssl-dev \
        make \
        openssh-client \
        patch \
        pkg-config \
        tar \
        tcl \
        unzip \
        zlib1g
    rm -rf /var/lib/apt/lists/*

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
    spack install [u'gcc@8.3', u'cuda@10.2', u'openmpi%gcc8.3^cuda@10.2']
    spack clean --all


