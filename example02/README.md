# Vagrant example02

This is a Vagrant example with synced folders using Virtualbox guest additions   
  
**jf@Tzunami:~/vagrant-examples/example02$** vagrant up  
```  
Bringing machine 'ubuntu02.vb.lab' up with 'virtualbox' provider...  
```

## Settings  
Tweak the settings below in the Vagrantfile to fit your needs
```  
API_VERSION = 2                 # Vagrant API version  
SSH_PUB_KEY = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip # Copy SSH public key ~/.ssh/id_rsa.pub  
```
