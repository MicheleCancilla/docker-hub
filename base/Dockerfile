FROM ubuntu:20.04

ARG CMAKE_VER=3.13.5
ARG GCC_VER=7

ENV NUM_CORES 4

# Turn off interactive dialogs of dpkg
# https://askubuntu.com/a/1013396/44054
# https://stackoverflow.com/a/44333806/424986
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y gcc-$GCC_VER g++-$GCC_VER gcc-$GCC_VER-base \
    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-$GCC_VER 100 \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-$GCC_VER 100
    
    
RUN apt-get update \
&& apt-get install -y wget graphviz \
    && wget https://github.com/Kitware/CMake/releases/download/v$CMAKE_VER/cmake-$CMAKE_VER-Linux-x86_64.sh \
      -q -O /tmp/cmake-install.sh \
    && chmod u+x /tmp/cmake-install.sh \
    && mkdir /home/cmake-$CMAKE_VER \
    && /tmp/cmake-install.sh --skip-license --prefix=/home/cmake-$CMAKE_VER \
    && rm /tmp/cmake-install.sh \
    && update-alternatives --install /usr/bin/cmake cmake /home/cmake-$CMAKE_VER/bin/cmake 100 \
    && update-alternatives --install /usr/bin/ctest ctest /home/cmake-$CMAKE_VER/bin/ctest 100 \
    && update-alternatives --install /usr/bin/cpack cpack /home/cmake-$CMAKE_VER/bin/cpack 100


# Change working dirs
WORKDIR /builds

# Define default command
CMD ["bash"]
