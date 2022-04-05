# docker-systemd-ssh
Docker containers with systemd and ssh that can be used for generic, educational purposes.

Apart from having limited systemd functionality, the containers come with a pre-configured ssh service and a pre-configured user. Extra tools are installed, so the containers can be used for general-purpose courses or examples.

The containers use a systemd or systemd-like process as their main process (PID 1), which means they will be continuously running unless explicitly stopped. This goes against the ephemeral nature of containers, but these containers with vm-like qualities are only meant for experimentation or computing labs.

## Usage
### Centos

docker hub tag: tomcoolpxl/centos7-systemd-ssh

see https://hub.docker.com/repository/docker/tomcoolpxl/centos-systemd-ssh

Start the container in the following manner.
```
docker run -d --name systemd-centos --tmpfs /tmp --tmpfs /run --tmpfs /run/lock -v /sys/fs/cgroup:/sys/fs/cgroup:ro -it -P tomcoolpxl/centos7-systemd-ssh:latest
```
Find out to which host port container port 22 is connected.
```
docker inspect systemd-centos| grep HostPort
```
You can now ssh into the container using the host port printed above, as the user 'user', password 'pxl'.
```
ssh user@localhost -p xxxx
```

### Ubuntu

docker hub tag: tomcoolpxl/ubuntu-20.04-systemd-ssh

see https://hub.docker.com/repository/docker/tomcoolpxl/ubuntu-systemd-ssh

Start the container, as you would do with any container.
```
docker run -d --name systemd-ubuntu -it -P tomcoolpxl/ubuntu-20.04-systemd-ssh:latest
```
Find out to which host port container port 22 is connected.
```
docker inspect systemd-ubuntu | grep HostPort
```
You can now ssh into the container using the host port printed above, as the user 'user', password 'pxl'.
```
ssh user@localhost -p xxxx
```

## Installed Software
- limited functionality systemd
- openssh service with enabled password authentication
- pre-configured and configurable user 'user', as part of the sudoers group
- network tools
  - openssh client
  - sudo
  - iproute tools
  - ping
  - net-tools
  - dns tools
  - traceroute
  - curl
  - wget
  - httpie
- generic tools
  - man pages
  - sudo
  - passwd
  - git
  - htop
  - vim
  - nano
  - ne
- python3 (ubuntu only)
## Sources
- using systemd in centos containers
  - https://github.com/CentOS/CentOS-Dockerfiles
- systemctl python script
  - https://github.com/gdraheim/docker-systemctl-replacement
  - https://github.com/gdraheim/docker-systemctl-images
