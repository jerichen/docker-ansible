### ansible client
- ubuntu 18.04
    - install : ssh.ansible

### server 
- ubuntu 18.04
- centos 7

### ssh
ssh root@127.0.0.1 -p 2222
ssh-keygen -f ansible_rsa -C "ansible-jerichen"


### docker
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)