### ansible 測試連線 inventory lab
ansible dev -m ping

### roles folder info
- defaults : 可被覆寫的變數
    - 一定要有main.yml
- files : 需複製到 Managed node 的檔案
- handlers
    - 一定要有main.yml
- meta : 特殊設定及其他依賴關係
    - 一定要有main.yml
- tasks : 主要的任務執行
    - 一定要有main.yml
- templates : 集中存放 Jinja2 模板的目錄
- tests
- vars : 不該被覆寫的變數
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