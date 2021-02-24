FROM hossein20s/docker-workstation:pytorch-nvidia
MAINTAINER HosseinAkhlaghpour@gmail.com

# docker build -t hossein20s/docker-workstation:pytorch-nvidia-django .
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

RUN sudo chgrp -R users /opt/conda/envs && sudo chmod -R g+w /opt/conda/envs

ENTRYPOINT ["/nxserver.sh"]

#USER $UID
#WORKDIR /home/${USER}
