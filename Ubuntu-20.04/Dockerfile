FROM hossein20s/docker-workstation:ml-pytorch-nvidia
MAINTAINER HosseinAkhlaghpour@gmail.com

# docker build -t hossein20s/docker-workstation:ml-pytorch-mobile .
# use developer as the main user to install-> use sudo for any RUN command

ENV DEBIAN_FRONTEND=noninteractive
EXPOSE 22 4000
ENV DISPLAY :0
ARG USER=developer
ARG UID=1000

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

user root

ARG TIMEZONE="America/Los_Angeles"
RUN echo ${TIMEZONE} > /etc/timezone

COPY env_ml.yml .
RUN conda env update --name ml --file env_ml.yml
# RUN sudo chgrp -R users /opt/conda/envs/ml && sudo chmod -R g+w /opt/conda/envs/ml

# Create the environment:
COPY env_python3.8.yml .
RUN conda env update --name python3.8 --file env_python3.8.yml
# RUN conda env create --file env_python3.8.yml

COPY env_python3.6.yml .
# RUN conda env update --name ag --file env_python3.6.yml
RUN conda env create --file env_python3.6.yml

COPY env_python2.7.yml .
RUN conda env update --name python2.7 --file env_python2.7.yml
# RUN conda env create --file env_python2.7.yml

# install PyCharm professional
RUN cd /tmp && \
    sudo wget -q https://download.jetbrains.com/python/pycharm-professional-2020.3.3.tar.gz -O pycharm.tar.gz && \
    sudo mkdir -p /opt/apps && cd /opt/apps && sudo tar xvfz /tmp/pycharm.tar.gz && sudo rm /tmp/pycharm.tar.gz

RUN sudo apt-get update -y && sudo apt --fix-broken install -y \
  && sudo apt install coinor-libcbc-dev coinor-cbc -y

RUN sudo chgrp -R users /opt/conda/envs && sudo chmod -R g+w /opt/conda/envs

ENTRYPOINT ["/nxserver.sh"]

#USER $UID
#WORKDIR /home/${USER}
