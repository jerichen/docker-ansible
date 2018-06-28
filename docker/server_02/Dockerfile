FROM centos:7
MAINTAINER JeriChen<jeri.chen0110@gmail.com>

ENV TZ=Asia/Taipei

RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y openssh-server
RUN apt-get install -y net-tools
RUN mkdir -p /var/run/sshd
RUN mkdir -p mkdir/root/.ssh/

# 修改root密碼
RUN echo root:password | chpasswd

# 產生key
RUN ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -P "N"

# 配置ssh
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# 開放port 22
EXPOSE 22

CMD /usr/sbin/sshd -D &
