FROM nvcr.io/nvidia/l4t-base:r32.4.3
MAINTAINER HosseinAkhlaghpour@gmail.com

# docker build -t hossein20s/docker-workstation:nano-pytorch .
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

RUN apt update && apt install -y sudo python3.7-dev
RUN rm /usr/bin/python /usr/bin/python3 && ln -s /usr/bin/python3.7 /usr/bin/python && ln -s /usr/bin/python3.7 /usr/bin/python3
RUN apt install -y python3-pip python3-setuptools  libopenblas-base libfreetype6-dev protobuf-compiler \
   libprotobuf-dev openssl libssl-dev libcurl4-openssl-dev cython3 libxml2-dev libxslt1-dev python3-numpy python3-scipy\
   python3-matplotlib python3-pandas python3-opencv cmake libjemalloc-dev libboost-dev  libboost-filesystem-dev \
   libboost-system-dev libboost-regex-dev python3-dev autoconf flex bison  libssl-dev curl libhdf5-dev \
   libc-ares-dev libeigen3-dev libatlas-base-dev libopenblas-dev libblas-dev liblapack-dev

RUN ln -s /usr/bin/pip3 /usr/bin/pip
RUN libjpeg-dev libfreetype6-dev pkg-config libpng-dev libhdf5-serial-dev hdf5-tools

RUN  pip3 install pytest psutil requests pyyaml
#RUN wget https://nvidia.box.com/shared/static/cs3xn3td6sfgtene6jdvsxlr366m2dhq.whl -O torch-1.7.0-cp36-cp36m-linux_aarch64.whl && \
#    pip3 install torch-1.7.0-cp36-cp36m-linux_aarch64.whl
# pip3 install Cython==0.29.21 && \
# pip3 install h5py==2.10.0 && \
# pip3 install git-all
# pip3 install fastparquet
# pip3 install pyarrow
# pip3 install matplotlib pillow==5.4.1

# Option1: Using unencrypted password/ specifying password
RUN useradd -m ${USER} --uid=${UID} && echo "${USER}:${PW}" | chpasswd \
&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
&& adduser ${USER} users && adduser ${USER} sudo \
&& usermod --shell /bin/bash ${USER}

ENTRYPOINT ["/bin/sh", "-c", "$0 \"$@\"", "tail -f /dev/null"]

USER ${USER}