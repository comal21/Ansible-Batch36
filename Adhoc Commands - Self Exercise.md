Here are some useful **ad-hoc** Ansible command examples for practice. These commands are run from the Ansible **control node** and execute tasks on managed nodes without needing a playbook.

---

## 🔹 **Basic Connection & Ping**
Check connectivity to all hosts in the inventory:  
```bash
ansible all -m ping
```
Check connectivity to a specific host/group:  
```bash
ansible webservers -m ping
```

---

## 🔹 **Gather System Information**
Get system uptime:  
```bash
ansible all -m command -a "uptime"
```
Check memory usage:  
```bash
ansible all -m shell -a "free -m"
```
Check disk usage:  
```bash
ansible all -m shell -a "df -h"
```

---

## 🔹 **User & Group Management**
Create a new user:  
```bash
ansible all -m user -a "name=devops password={{ 'MySecurePass' | password_hash('sha512') }} state=present"
```
Delete a user:  
```bash
ansible all -m user -a "name=devops state=absent"
```
Add a user to a group:  
```bash
ansible all -m user -a "name=devops groups=sudo append=yes"
```

---

## 🔹 **File & Directory Operations**
Create a directory:  
```bash
ansible all -m file -a "path=/opt/testdir state=directory mode=0755"
```
Create an empty file:  
```bash
ansible all -m file -a "path=/opt/testfile.txt state=touch"
```
Remove a file:  
```bash
ansible all -m file -a "path=/opt/testfile.txt state=absent"
```

---

## 🔹 **Package Management**
Install a package (e.g., `nginx`):  
```bash
ansible all -m apt -a "name=nginx state=present" -b   # For Debian/Ubuntu
ansible all -m yum -a "name=nginx state=present" -b    # For RHEL/CentOS
```
Remove a package:  
```bash
ansible all -m apt -a "name=nginx state=absent" -b
```
Update all packages:  
```bash
ansible all -m apt -a "update_cache=yes upgrade=dist" -b
```

---

## 🔹 **Service Management**
Start a service:  
```bash
ansible all -m service -a "name=nginx state=started" -b
```
Stop a service:  
```bash
ansible all -m service -a "name=nginx state=stopped" -b
```
Restart a service:  
```bash
ansible all -m service -a "name=nginx state=restarted" -b
```
Check service status:  
```bash
ansible all -m systemd -a "name=nginx state=started" -b
```

---

## 🔹 **Managing Files & Permissions**
Copy a file to remote hosts:  
```bash
ansible all -m copy -a "src=/home/user/myfile.txt dest=/tmp/myfile.txt mode=0644"
```
Download a file from a remote host:  
```bash
ansible all -m fetch -a "src=/var/log/syslog dest=/home/user/logs/" -b
```
Change file permissions:  
```bash
ansible all -m file -a "path=/tmp/myfile.txt mode=0644 owner=root group=root"
```

---

## 🔹 **Execute Commands & Scripts**
Run a simple command:  
```bash
ansible all -m command -a "hostname"
```
Run a shell script on remote hosts:  
```bash
ansible all -m script -a "/home/user/myscript.sh"
```
Run a command as a different user:  
```bash
ansible all -m command -a "whoami" -b -U someuser
```

---

## 🔹 **Reboot & Shutdown**
Reboot all servers:  
```bash
ansible all -m reboot -b
```
Shutdown a server:  
```bash
ansible all -m command -a "shutdown -h now" -b
```

---

## 🔹 **Networking & Firewall**
Check open ports:  
```bash
ansible all -m command -a "netstat -tulnp"
```
Enable a firewall rule:  
```bash
ansible all -m ufw -a "rule=allow port=80 proto=tcp" -b
```
Disable a firewall rule:  
```bash
ansible all -m ufw -a "rule=deny port=22 proto=tcp" -b
```

---

These commands will help you get hands-on experience with **Ansible ad-hoc tasks**. Let me know if you need more! 🚀
