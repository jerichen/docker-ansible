## 未完成

### 用docker composer 練習 ansible

### Control-Node-Ubuntu 
- ubuntu 18.04
    - install : ssh.ansible.

### Managed-Node-Ubuntu
- ubuntu 18.04
    - ssh username: master
    - ssh password: password
### Managed-Node-Centos
- centos 7
    - ssh username: master
    - ssh password: password

### ssh
ssh root@127.0.0.1 -p 2222

### generate ssh key
ssh-keygen -f ansible_rsa -C "ansible-jerichen"

### docker info
- stop all container : docker stop $(docker ps -a -q)
- remove all container : docker rm $(docker ps -a -q)
- remove all image : docker rmi $(docker images -q)

### ansible info
- macOS取得本機ip指令 : ifconfig en0
- lab : [dev] 需設定本機端ip
- 測試連線成功指令 : ansible dev -m ping