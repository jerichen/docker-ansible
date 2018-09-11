### ansible 測試連線 inventory lab
ansible dev -m ping

### roles folder info
- defaults : 默認變量存放目錄
    - 一定要有main.yml
- files : 需複製到 Managed node 的檔案
- handlers : 處理程式(當發生改變時需要執行的操作)
    - 一定要有main.yml
- meta : 角色依賴關係處理
    - 一定要有main.yml
- tasks : 具體執行的任務操作定義
    - 一定要有main.yml
- templates : 模板文件存放目錄
- tests
- vars : 變量文件目錄
    - 一定要有main.yml

### 全局變量
mkdir ~/dev/ansible/{group_vars,all}/ -p
touch ~/dev/ansible/group_vars/all/vars.yml

### 目錄建置
mkdir ~/dev//ansible/roles/example/{files,templates,tasks,handlers,vars,defaults,meta} -p

### main.yml建置
touch ~/dev/ansible/roles/example/{defaults,vars,tasks,meta,handlers}/main.yml

### run ansible
ansible-playbook ~/dev/ansible/playbook/example/playbook.yml

### run ansible add var 
ansible-playbook --extra-vars "hosts_name=dev" playbook/example/playbook.yml
ansible-playbook --extra-vars "hosts_name=dev web_site=blog" playbook/example/playbook.yml
ansible-playbook --e hosts_name=dev playbook/example/playbook.yml