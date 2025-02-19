## Prompts with Ansible Playbooks

Create and edit promptlab.yml in the same labs directory
```
cd ~/ansible-labs
```
```
vi promptlab.yml
```
```
---
- hosts: all
  become: yes
  user: ec2-user
  connection: ssh
  vars_prompt:
    - name: pkginstall
      prompt: Which package do you want to install?
      default: vim
      private: no
  tasks:
    - name: Install the package specified
      yum: pkg={{ pkginstall }} state=latest
```
save the file using ESCAPE + :wq!

Execute the playbook & you will be prompt for enter the package name which you want to install If no package is mentioned, vim is installed by default
```
ansible-playbook promptlab.yml
```
Verify if the specified package is installed. 
```
ansible all -m command -a "yum list installed 'vim*'"
```

