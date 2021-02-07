FROM hossein20s/docker-workstation:nvidia
MAINTAINER HosseinAkhlaghpour@gmail.com

# docker build -t hossein20s/docker-workstation:webots-pytorch .
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
# Disable dpkg/gdebi interactive dialogs

# Determine Webots version to be used and set default argument
ARG WEBOTS_VERSION=R2021a
ARG WEBOTS_PACKAGE_PREFIX=

# Install Webots runtime dependencies
RUN apt update && apt install --yes wget && rm -rf /var/lib/apt/lists/
RUN wget https://raw.githubusercontent.com/cyberbotics/webots/master/scripts/install/linux_runtime_dependencies.sh
RUN chmod +x linux_runtime_dependencies.sh && ./linux_runtime_dependencies.sh && rm ./linux_runtime_dependencies.sh && rm -rf /var/lib/apt/lists/

# Install X virtual framebuffer to be able to use Webots without GPU and GUI (e.g. CI)
RUN apt update && apt install --yes xvfb && rm -rf /var/lib/apt/lists/

# Install Webots
WORKDIR /usr/local
RUN wget https://github.com/cyberbotics/webots/releases/download/$WEBOTS_VERSION/webots-$WEBOTS_VERSION-x86-64$WEBOTS_PACKAGE_PREFIX.tar.bz2
RUN tar xjf webots-*.tar.bz2 && rm webots-*.tar.bz2
ENV QTWEBENGINE_DISABLE_SANDBOX=1
ENV WEBOTS_HOME /usr/local/webots
ENV PATH /usr/local/webots:${PATH}


COPY env_ml.yml .

RUN conda env update --name ml --file env_ml.yml
RUN sudo chgrp -R users /opt/conda/envs/ml && sudo chmod -R g+w /opt/conda/envs/ml

ENTRYPOINT ["/nxserver.sh"]

#USER $UID
#WORKDIR /home/${USER}
