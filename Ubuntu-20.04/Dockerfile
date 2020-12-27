FROM nvcr.io/nvidia/l4t-ml:r32.4.4-py3
MAINTAINER HosseinAkhlaghpour@gmail.com

# docker build -t hossein20s/jetson-nano:ml .
# use developer as the main user to install-> use sudo for any RUN command

ARG TIMEZONE="America/Los_Angeles"
ARG USER=developer
ARG UID=1000
ARG GID=1000
# default password for user
ARG PW=developer

ENV DEBIAN_FRONTEND=noninteractive
EXPOSE 22 4000
ENV DISPLAY :0

RUN apt update
RUN apt install -y sudo # python3.7-dev
RUN apt install -y python3-pip python3-setuptools python3-matplotlib cython3 openssl protobuf-compiler hdf5-tools
# libopenblas-base libfreetype6-dev  \
#   libprotobuf-dev libssl-dev libcurl4-openssl-dev libxml2-dev libxslt1-dev python3-numpy python3-scipy\
#    python3-pandas python3-opencv cmake libjemalloc-dev libboost-dev  libboost-filesystem-dev \
#   libboost-system-dev libboost-regex-dev python3-dev autoconf flex bison  libssl-dev curl libhdf5-dev \
#   libc-ares-dev libeigen3-dev libatlas-base-dev libopenblas-dev libblas-dev liblapack-dev

RUN rm /usr/bin/python /usr/bin/python3 && ln -s /usr/bin/python3.6 /usr/bin/python && ln -s /usr/bin/python3.6 /usr/bin/python3 && ln -s /usr/bin/pip3 /usr/bin/pip
#RUN apt install -y libjpeg-dev libfreetype6-dev pkg-config libpng-dev libhdf5-serial-dev


# RUN pip3 install matplotlib pillow==5.4.1 python-llvmlite
#RUN wget https://nvidia.box.com/shared/static/cs3xn3td6sfgtene6jdvsxlr366m2dhq.whl -O torch-1.7.0-cp36-cp36m-linux_aarch64.whl && \
#    pip3 install torch-1.7.0-cp36-cp36m-linux_aarch64.whl
# pip3 install h5py==2.10.0 && \
# pip3 install git-all
RUN pip3 install fastparquet
RUN pip3 install Cython==0.29.21
RUN pytest psutil requests pyyaml
# RUN pip3 install pyarrow
RUN PYARROW_CMAKE_OPTIONS="-DARROW_ARMV8_ARCH=armv8-a" pip3 install pyarrow

# Option1: Using unencrypted password/ specifying password
RUN useradd -m ${USER} --uid=${UID} && echo "${USER}:${PW}" | chpasswd \
&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
&& adduser ${USER} users && adduser ${USER} sudo \
&& usermod --shell /bin/bash ${USER}

ENTRYPOINT ["/bin/sh", "-c", "$0 \"$@\"", "tail -f /dev/null"]

USER ${USER}