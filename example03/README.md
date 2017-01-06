# Vagrant example03

This is a Vagrant multi machine example that will install and configure 3 identical Ubuntu nodes in Virtualbox   
  
**username@laptop:/home/username/vagrant-examples/example03$** vagrant up  
```  
Bringing machine 'node1' up with 'virtualbox' provider...  
Bringing machine 'node2' up with 'virtualbox' provider...  
Bringing machine 'node3' up with 'virtualbox' provider...  
```

## Settings  
Tweak the settings below in the Vagrantfile to fit your needs
```  
API_VERSION = 2                 # Vagrant API version  
BOX_IMAGE = "ubuntu/xenial64"   # Install VMs with Vagrant BOX ubuntu/xenial64  
VM_NAME = "node"                # Virtualbox name & hostname will start with node(integer)  
VM_COUNT = 3                    # Number of VMs to create  
SSH_PUB_KEY = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip # Copy SSH public key ~/.ssh/id_rsa.pub  
```
