FROM centos:6
MAINTAINER JeriChen<jeri.chen0110@gmail.com>

ENV TZ=Asia/Taipei

# Update the index of available packages.
RUN yum update -y

# Install the requires package.
RUN yum install -y vim
RUN yum install -y net-tools
RUN yum install -y openssh-server
RUN yum install -y openssh-clients
RUN yum install -y python
RUN yum install -y sudo
RUN yum install -y curl
RUN yum install -y wget
RUN yum install -y epel-release
RUN yum install -y bash-completion
RUN yum install -y openssl
RUN yum clean all

# Setting the sshd.
RUN mkdir /var/run/sshd
RUN echo 'root:password' | chpasswd

# Generate the ssh host keys.
RUN ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -N ''
RUN ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N ''

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# Create a new user.
# - username: master
# - password: password
RUN useradd --create-home --shell /bin/bash \
      --password $(openssl passwd -1 password) master

# Add sudo permission.
RUN echo 'master ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

# Setting ssh public key.
RUN wget https://raw.githubusercontent.com/jerichen/docker-ansible/master/docker/files/ssh/id_rsa.pub \
      -O /tmp/authorized_keys && \
      mkdir /home/master/.ssh && \
      mv /tmp/authorized_keys /home/master/.ssh/ && \
      chown -R master:master /home/master/.ssh/ && \
      chmod 644 /home/master/.ssh/authorized_keys && \
      chmod 700 /home/master/.ssh

EXPOSE 22

# Run ssh server daemon.
CMD ["/usr/sbin/sshd", "-D"]


