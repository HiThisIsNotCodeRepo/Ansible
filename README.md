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

[nodes]
node1 ansible_ssh_host=192.168.0.17
node2 ansible_ssh_host=192.168.0.34
```
save and execute
```shell=
ansible node -m ping
```
![](https://i.imgur.com/QPcPSsU.png)
## Install Go

### get_url
```shell=
ansible nodes -m get_url -a "url=https://golang.org/dl/go1.16.5.linux-amd64.tar.gz dest=~"
```
### unarchive
```shell=
ansible nodes -m unarchive -a "src=~/go1.16.5.linux-amd64.tar.gz dest=/usr/local remote_src=yes"
```
### lineinfile
```shell=
ansible nodes -m lineinfile -a "line='export GOROOT=/usr/local/go' dest=/etc/profile"
ansible nodes -m lineinfile -a "line='export GOROOT=/usr/local/go' dest=/root/.bashrc"
ansible nodes -m lineinfile -a "line='export GOPATH=~/gocode' dest=/etc/profile"
ansible nodes -m lineinfile -a "line='export GOPATH=~/gocode' dest=/root/.bashrc"
ansible nodes -m lineinfile -a "line='export PATH=\$GOPATH/bin:\$GOROOT/bin:\$PATH' dest=/etc/profile"
ansible nodes -m lineinfile -a "line='export PATH=\$GOPATH/bin:\$GOROOT/bin:\$PATH' dest=/root/.bashrc"
```
### verify
```shell=
ansible nodes -a "go version"
```

## Install Docker
```shell=
ansible nodes -m yum -a 'name=yum-utils state=installed'
ansible nodes -m shell -a 'sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo'
ansible nodes -m yum -a 'name=docker-ce state=installed'
ansible nodes -m yum -a 'name=docker-ce-cli state=installed'
ansible nodes -m yum -a 'name=containerd.io state=installed'
ansible nodes -m systemd -a 'name=docker enabled=yes'
ansible nodes -m systemd -a 'name=docker state=started'
```
## Build in variable
```shell=
# ipv4 info
ansible_all_ipv4_addresses
# disk info
ansible_devices
# distribution info
ansible_distribution
# distribution version
ansible_distribution_version
# system type 32 bit or 64 bit
ansible_machine
# eth0 info
ansible_eth0
# hostname
ansible_hostname
# kernel info
ansible_kernel
# lvm info
ansible_lvm
# total mem
ansible_memtotal_mb
# free mem
ansible_memfree_mb
# mem info
ansible_memory_mb
# swap mem
ansible_swaptotal_mb
# swap free mem
ansible_swapfree_mb
# mount info
ansible_mounts
# cpu info
ansible_processor
# vcpu info
ansible_processor_vcpus
# python info
ansible_python_version
```
