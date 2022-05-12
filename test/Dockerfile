FROM alpine:latest

# Download of dependecies
RUN apk update && apk upgrade && apk --no-cache add \
        git \
        unzip

# Download opencv + opencv_contrib rename and unpack
RUN mkdir /opencv_build && cd /opencv_build && \
  wget -c https://github.com/opencv/opencv/archive/3.2.0.zip  -O opencv.zip && \
  unzip opencv.zip && rm opencv.zip && \
  wget -c https://github.com/opencv/opencv_contrib/archive/3.2.0.zip -O opencv_contrib.zip && \
  unzip opencv_contrib.zip && rm opencv_contrib.zip \
  && \
  cd /opencv-3.2.0 && mkdir build && cd build
