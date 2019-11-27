ARG CV_VER=4.1.2
FROM ubuntu:latest

#ENV PYTHON_VERSION 3.7
ENV OPENCV_VERSION ${CV_VER}

ENV NUM_CORES 4

# Turn off interactive dialogs of dpkg
# https://askubuntu.com/a/1013396/44054
# https://stackoverflow.com/a/44333806/424986
ENV DEBIAN_FRONTEND=noninteractive


# Install OpenCV
RUN apt-get -y update -qq && \
    apt-get -y install wget \
                       unzip \
                       \
                       # Required
                       build-essential \
                       cmake \
                       git \
                       pkg-config \
                       #libatlas-base-dev \
                       #libavcodec-dev \
                       #libavformat-dev \
                       #libgtk2.0-dev \
                       #libswscale-dev \
                       \
                       # Optional
                       #libdc1394-22-dev \
                       libjpeg-dev \
                       libpng-dev \
                       #libtbb2 \
                       #libtbb-dev \
                       libtiff-dev \
                       #libv4l-dev \
                       #libvtk6-dev \
                       &&\
    apt-get autoclean autoremove

    # Get OpenCV
RUN git clone https://github.com/opencv/opencv.git &&\
    cd opencv &&\
    git checkout $OPENCV_VERSION &&\
    cd / &&\
    # Get OpenCV contrib modules
    #git clone https://github.com/opencv/opencv_contrib &&\
    #cd opencv_contrib &&\
    #git checkout $OPENCV_VERSION &&\
    mkdir /opencv/build &&\
    cd /opencv/build &&\
    \
    # Lets build OpenCV
    cmake \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D BUILD_DOCS=OFF \
    -D BUILD_EXAMPLES=OFF \
    -D BUILD_JAVA=OFF \
    -D BUILD_JPEG=ON \
    -D BUILD_LIST=core,imgproc,imgcodecs \
    -D BUILD_PERF_TESTS=OFF \
    -D BUILD_PNG=ON \
    -D BUILD_PROTOBUF=OFF \
    -D BUILD_SHARED_LIBS=OFF \
    -D BUILD_TESTS=OFF \
    -D BUILD_TIFF=ON \
    -D BUILD_USE_SYMLINKS=OFF \
    -D BUILD_WEBP=OFF \
    -D BUILD_WITH_DEBUG_INFO=OFF \
    -D BUILD_WITH_DYNAMIC_IPP=OFF \
    -D BUILD_ZLIB=OFF \ 
    -D WITH_FFMPEG=OFF \
    -D WITH_OPENCL=OFF \ 
    -D WITH_QT=OFF \ 
    -D WITH_IPP=OFF \
    -D WITH_MATLAB=OFF \
    -D WITH_OPENGL=OFF \
    -D WITH_QT=OFF \ 
    -D WITH_TIFF=OFF \
    -D WITH_TBB=OFF \
    -D WITH_V4L=OFF \
    -D WITH_LAPACK=OFF \
    -D INSTALL_C_EXAMPLES=OFF \
    -D INSTALL_PYTHON_EXAMPLES=OFF \ 
    -D WITH_OPENEXR=OFF \
    .. &&\
    make -j$NUM_CORES &&\
    make install &&\
    ldconfig &&\
    \
    # Clean the install from sources
    cd / &&\
    rm -r /opencv 

# Change working dirs
WORKDIR /builds

# Define default command.
CMD ["bash"]