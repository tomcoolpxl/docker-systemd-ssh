FROM centos:7

ENV container docker

# delete the unit files which might cause issues
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
  rm -f /lib/systemd/system/multi-user.target.wants/*; \
  rm -f /etc/systemd/system/*.wants/*; \
  rm -f /lib/systemd/system/local-fs.target.wants/*; \
  rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
  rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
  rm -f /lib/systemd/system/basic.target.wants/*;\
  rm -f /lib/systemd/system/anaconda.target.wants/*;

# install openssh, basic tools and mapages
RUN sed -i '/tsflags=nodocs/d' /etc/yum.conf && \
  yum -y update && \
  yum install -y epel-release && \
  yum -y install openssh-server openssh-clients man-pages man-db man vim nano ne sudo passwd iproute iputils bind-utils traceroute curl git htop wget httpie && \
  yum clean all

# add user
RUN groupadd user && \
  adduser -g user user && \
  echo user:pxl | chpasswd && \
  echo 'user  ALL=(ALL) ALL' >>  /etc/sudoers

# prepare sshd environment
RUN mkdir /var/run/sshd && \
  ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''
EXPOSE 22

VOLUME [ "/sys/fs/cgroup" ]

# start systemd PID1
CMD ["/usr/sbin/init"]