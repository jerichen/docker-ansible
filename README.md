## 未完成
### 用docker composer 練習 ansible

### Control-Node-Ubuntu 
- ubuntu 18.04
    - install : ssh.ansible.

### Managed-Node-Ubuntu
- ubuntu 18.04
### Managed-Node-Centos
- centos 7

### ssh
ssh root@127.0.0.1 -p 2222

### generate ssh key
ssh-keygen -f ansible_rsa -C "ansible-jerichen"

### docker
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)