FROM ubuntu:bionic

#### Install dependences #####
RUN apt update && \
    apt-get install -y cmake build-essential g++-8 git wget libeigen3-dev doxygen curl swig ruby-dev cppcheck && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 800 --slave /usr/bin/g++ g++ /usr/bin/g++-8 --slave /usr/bin/gcov gcov /usr/bin/gcov-8

### Install lcov ####
WORKDIR /root
RUN git clone https://github.com/linux-test-project/lcov.git
WORKDIR /root/lcov
RUN git checkout 1e0df571
RUN make install
WORKDIR /root
RUN rm -r lcov

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
RUN cmake .. -DCMAKE_BUILD_TYPE=coverage && \
    make -j8 && \
    make doc && \
    curl -s https://github.com/ignitionrobotics/ign-cmake/raw/master/tools/doc_check.sh && \
    make test && \
    make coverage && \
    curl -s https://raw.githubusercontent.com/codecov/codecov-bash/4678d212cce2078bbaaf5027af0c0dafaad6a095/codecov -X gcovout -X gcov && \
    make codecheck && \
    make install

WORKDIR /root