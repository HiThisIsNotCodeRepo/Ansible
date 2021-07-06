# Ansible note
## Pre-requisite
On all node need to install python.
```shell=
python
```
![](https://i.imgur.com/SaWIIWx.png)
## Install
On control node
```shell=
yum install ansible -y
```
To view conf file directory
```shell=
ansible --version
```
Send public key to node to allow control
```shell=
ssh-keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.0.29
ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.0.196
```
Edit host list
```shell=
vim /etc/ansible/hosts

[node]
192.168.0.29
192.168.0.196
```
save and execute
```shell=
ansible node -m ping
```
![](https://i.imgur.com/QPcPSsU.png)
