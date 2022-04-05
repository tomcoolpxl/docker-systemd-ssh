FROM ubuntu:22.04

ARG NEWUSER=user
ARG PASSWORD=pxl
ENV container=docker
ENV LC_ALL=C
ENV DEBIAN_FRONTEND=noninteractive

# install openssh, basic tools and manpages
RUN apt-get update && \
  yes | unminimize && \
  apt-get install -y openssh-client vim nano ne man-db sudo iproute2 iputils-ping passwd net-tools dnsutils traceroute curl git htop wget httpie && \
  apt-get install -y python3 && \
  apt-get install -y openssh-server && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install systemd
COPY files/systemctl3.py /usr/bin/systemctl
COPY files/journalctl3.py /usr/bin/journalctl

# prepare sshd environment
RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config && \
  systemctl start ssh.service && \
  systemctl enable ssh.service
EXPOSE 22

# add user
RUN useradd -ms /bin/bash $NEWUSER && \
  echo $NEWUSER:$PASSWORD | chpasswd && \
  echo "$NEWUSER  ALL=(ALL) ALL" >>  /etc/sudoers

# start systemd PID1
CMD ["/usr/bin/systemctl"]