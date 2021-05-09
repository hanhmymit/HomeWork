# Pratice 1 - Install Ansible and Deploy WordPress(docker) using Ansible


##### Step 1: Install Ansible
Install on Ubuntu
```console
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible
```
Check install Ansible successful 
```console
$ ansible --version
```
It will has line ```config file = /etc/ansible/ansible.cfg ```

##### Step 2: Create your own ```ansible.cfg``` file on your folder
After create ```ansible.cfg``` file, you can run
```console
$ ansible --version
```
It will has line ```config file = {path_to_your_folder_create_file_config}/ansible.cfg ```  (compare to step 1)


##### Step 3: Create your own ```inventory.ini``` file on your folder
```inventory.ini``` define hosts, groups you want to manage

my ```inventory.ini``` file
```console
[db]
192.168.5.10
[web]
192.168.5.11
192.168.5.12
[web:vars]
ansible_user=thang2
ansible_ssh_pass=2
ansible_become_password=2
[db:vars]
ansible_user=thang
ansible_ssh_pass=1
ansible_become_password=1
```

Then, you change your own  ```ansible.cfg``` file 
```console
...
host_key_checking = False
inventory = {path_your_own_inventory_file}
...
```

#### Step 4: Test Ansible with your own ```ansible.cfg``` file
ping all machine you defined on your own ```inventory.ini``` file
```console 
 ansible all -m ping 
```
It will look like
![image](https://user-images.githubusercontent.com/43313369/117580672-45537080-b123-11eb-9336-f3acf9a29b59.png)

#### Step 5: Install Docker & Docker Compose on group ```web```
```console
---
- name: test playbook
  hosts: web
  gather_facts: false

  tasks:
  - name: install docker
    become: yes
    apt:
     name: docker.io
     state: present
  - name: Install docker-compose
    become: yes
    apt:
     name: docker-compose
     state: present
```


#### Step 6: Deploy WordPress with Docker-Compose
Download file docker-compose.yml then run
```console
---
- name: test playbook
  hosts: web
  gather_facts: false
  tasks:
  - name: download file compose (mariadb+wordpress)
    become: yes
    get_url:
     url: https://raw.githubusercontent.com/bitnami/bitnami-docker-wordpress/master/docker-compose.yml
     dest: /home/docker-compose.yml
     force_basic_auth: yes
  - name: deploy wordpress with docker-compose
    become: yes
    command: docker-compose up -d
    args:
     chdir: /home
```
# Result
Go to *http://localhost:80* or *https://localhost:443* to test
![image](https://user-images.githubusercontent.com/43313369/117582919-9b79e100-b12e-11eb-9846-bc3bfbd133eb.png)

