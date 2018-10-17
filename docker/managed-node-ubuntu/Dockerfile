FROM ubuntu:18.04
MAINTAINER JeriChen<jeri.chen0110@gmail.com>

ENV TZ=Asia/Taipei

# ADD .bashrc
ADD ./././files/bashrc.conf .bashrc

# Update the index of available packages.
RUN apt-get update

# Install the requires package.
RUN apt-get install -y tzdata
RUN apt-get install -y vim
RUN apt-get install -y net-tools
RUN apt-get install -y openssh-server
RUN apt-get install -y openssh-client
RUN apt-get install -y python
RUN apt-get install -y sudo
RUN apt-get install -y curl
RUN apt-get install -y wget
RUN apt-get install -y bash-completion
RUN apt-get install -y openssl
RUN apt-get clean

# Setting timezone
RUN echo "Asia/Taipei" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# Setting the sshd.
RUN mkdir /var/run/sshd
RUN echo 'root:password' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

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
