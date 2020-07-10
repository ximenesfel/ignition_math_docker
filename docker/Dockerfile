FROM gcc:8.4

###### Install cmake #########
RUN wget https://github.com/Kitware/CMake/releases/download/v3.17.3/cmake-3.17.3-Linux-x86_64.sh \
      -q -O /tmp/cmake-install.sh \
      && chmod u+x /tmp/cmake-install.sh \
      && mkdir /usr/bin/cmake \
      && /tmp/cmake-install.sh --skip-license --prefix=/usr/bin/cmake \
      && rm /tmp/cmake-install.sh

ENV PATH="/usr/bin/cmake/bin:${PATH}"

#### Install dependences #####
RUN apt update && \
    apt-get install -y libeigen3-dev doxygen swig


### Install ignition cmake #####

WORKDIR /root
RUN git clone -b ign-cmake2 https://github.com/ignitionrobotics/ign-cmake
WORKDIR /root/ign-cmake
RUN mkdir build
WORKDIR /root/ign-cmake/build
RUN cmake .. -DCMAKE_INSTALL_PREFIX=/usr/local/
RUN make -j8
RUN make install
WORKDIR /root
RUN rm -r ign-cmake

####### Install gtest/gmock #######
WORKDIR /root
RUN wget -O googletest.zip https://github.com/google/googletest/archive/release-1.10.0.zip
RUN unzip googletest.zip
RUN mv googletest-release-1.10.0 googletest

WORKDIR /root/googletest
RUN mkdir build

WORKDIR /root/googletest/build
RUN cmake .. && \
    make -j4 && \
    make install && \
    ldconfig

WORKDIR /root
RUN rm -r googletest googletest.zip

### Install ignition math #####

WORKDIR /root
RUN git clone -b ign-math6 https://github.com/ignitionrobotics/ign-math
WORKDIR /root/ign-math
RUN mkdir build
WORKDIR /root/ign-math/build
RUN cmake ..
RUN make -j8
RUN make install

WORKDIR /root