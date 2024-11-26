### ansible 설치
```
apt-get install ansible
```

### ansible hosts 설정
```
## 기본 경로
/etc/ansible/hosts

## 사용자 지정
ansible -i /path/to/your_hosts <target> -m ping
ansible all -i test -m ping

ansible all -m ping -k

## 기본 경로 - key 파일
/etc/ansible/hosts
[web]
192.168.1.101 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

ansible all -m ping

ansible --version
ansible servers --list-hosts -v

# 적용받는 호스트를 먼저 확인
ansible linuxwork2 -m ping --list-hosts
```

### ansible option
-i : (--inventory-file) 적용될 호스트들에 대한 파일
-m : (--module-name) 모듈을 선택할 수 있도록
-k : (--ask-pass) 패스워드를 물어보도록 설정
-K : (--ask-become-pass) 권리자로 권한 상승
--list-hosts : 적용되는 호스트들을 확인


### uptime 확인하기
ansible all -m shell -a "uptime" -k

### disk용량 확인하기
ansible all -m shell -a "df -h"

### 메모리 확인하기
ansible all -m shell -a "free -h"

### 새로운 유저 만들기
ansible all -m user -a "name=bloter password=1234" -k

### 서비스 설치
ansible linuxwork2 -m apt -a "name=apache2 state=present"

### 파일 전송
ansible all -m copy -a "src=./mgmt.file dest=/tmp/"



### ansible-playbook
멱등성
vi add_hosts.yml
```
---
- name: Ansible_vim
  hosts: localhost

  tasks:
    - name: Add ansible hosts
      blockinfile:
        path: /etc/ansible/hosts
        block: |
          [ralf]
          10.10.10.10
```
ansible-playbook add_hosts.yml

PLAY [Ansible_vim] ************************************************************************************************************************************************

TASK [Gathering Facts] ********************************************************************************************************************************************
ok: [localhost]

TASK [Add ansible hosts] ******************************************************************************************************************************************
changed: [localhost]

PLAY RECAP ********************************************************************************************************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0


YAML은 마크업 언어가 아니다.
- xml을 넘어 json과 유사 혹은 거의 동일


