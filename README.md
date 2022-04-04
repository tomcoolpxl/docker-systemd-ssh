# docker-systemd-ssh
Docker containers with systemd and ssh that can be used for generic, educational purposes.

Apart from having limited systemd functionality, the containers come with a pre-configured ssh service and a pre-configured user. Extra tools are installed, so the containers can be used for general-purpose courses or examples.

## Usage
### Centos
### Ubuntu
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
