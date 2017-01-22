# Vagrant example05
*This is a Vagrant multi machine example for Virtualbox that is using a YAML file to define VMs*

```
jf@Tzunami:~/vagrant-examples/example05$ vagrant up
Bringing machine 'ubuntu-01' up with 'virtualbox' provider...
Bringing machine 'ubuntu-02' up with 'virtualbox' provider...
Bringing machine 'ubuntu-03' up with 'virtualbox' provider...
==> ubuntu-01: Importing base box 'ubuntu/xenial64'...
```

## Vagrant multi-machine YAML configuration file
```
jf@Tzunami:~/vagrant-examples/example05$ cat servers.yaml
---
- name: ubuntu-01
  group: Ubuntu servers
  box: ubuntu/xenial64
  ip: 192.168.56.211
  cpu: 2
  ram: 2048
  shell: |
    apt-get update
    apt-get install irssi -y
    useradd jf -d /home/jf -s /bin/bash
    mkdir -vp /home/jf/.ssh
    echo "ssh-rsa AAAABMCo7MjGI3bi7l4BOy9jj9bH38xsbZk1j/krMxG/9zdG25uQLglL8w5Mywct/+G681yLQCDEHgU1peesDuPdypS9uWbuT06NnBhxNb9hC5zhva9vV+afkRJLWru20dOaExeaTVrA4uuzYEdllHvUNcYNznhK3lFw== jf@Tzunami" >> /home/jf/.ssh/authorized_keys
    echo 'jf ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/lusers
    chown -vR jf:jf /home/jf
- name: ubuntu-02
  group: Ubuntu servers
  box: ubuntu/xenial64
  ip: 192.168.56.212
  cpu: 2
  ram: 2048
  shell: |
    apt-get update
- name: ubuntu-03
  group: Ubuntu servers
  box: ubuntu/xenial64
  ip: 192.168.56.213
  cpu: 1
  ram: 1024
  shell: |
    apt-get update
```
