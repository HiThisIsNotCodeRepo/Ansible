# Role manual
Create role
```shell=
ansible-galaxy init demoRole
```
Add file to `demoRole/tasks/main.yml`,`demoRole/templates`
```shell=
cat > demoRole/templates/demo.j2 << EOF
Server="{{demo_server}}"
Host="{{ansible_hostname}}"
Cache="{{ansible_memtotal_mb//2}}"
EOF

cat > demoRole/vars/main.yml << EOF
demo_server: 255.255.255.255
EOF

cat > demoRole/tasks/main.yml << EOF
- name: Copy Conf file
  template: src=./demo.j2 dest=~/demo
EOF

cat > demo_role_playbook.yml << EOF
- hosts: node
  roles:
    - demoRole
EOF
```
