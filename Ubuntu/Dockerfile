FROM python:3.2


RUN mkdir -p /usr/src/app 
WORKDIR /usr/src/app 

# Various Python and C/build deps
RUN  apt-get update && apt-get install -y \ 
    wget \
    build-essential \
    git \
    pkg-config \
    libgtk-3-dev \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev libv4l-dev \
    libxvidcore-dev \
    libx264-dev \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    gfortran \
    openexr \
    libatlas-base-dev \
    python3-dev \
    python3-numpy \
    libtbb2 \
    libtbb-dev \
    libdc1394-22-dev

RUN wget https://github.com/Kitware/CMake/releases/download/v3.23.1/cmake-3.23.1.tar.gz
RUN tar xzvf cmake-3.23.1.tar.gz
RUN cd cmake-3.23.1 && ./configure && make && make install
    
RUN mkdir ~/opencv_build && cd ~/opencv_build && \
    git clone https://github.com/opencv/opencv.git &&\
    git clone https://github.com/opencv/opencv_contrib.git && \
    cd opencv && mkdir -p build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \ 
    -D INSTALL_C_EXAMPLES=ON \ 
    -D INSTALL_PYTHON_EXAMPLES=ON \ 
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \ 
    -D BUILD_EXAMPLES=OFF .. 

RUN make -j8
RUN make install \ 
    pkg-config --modversion opencv4 \ 
    python3 -c "import cv2; print(cv2.__version__)"

# COPY requirements.txt /usr/src/app/
# RUN pip install --no-cache-dir -r requirements.txt

COPY . /usr/src/app 