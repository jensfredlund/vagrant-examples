# Vagrant example01

This is a minimal Vagrant example that will install and configure a Ubuntu VM.   
  
**jf@Tzunami:~/vagrant-examples/example01$** vagrant up  
```  
Bringing machine 'ubuntu01.vb.lab' up with 'virtualbox' provider...  
```

## Settings  
Tweak the settings below in the Vagrantfile to fit your needs
```  
API_VERSION = 2                 # Vagrant API version  
SSH_PUB_KEY = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip # Copy SSH public key ~/.ssh/id_rsa.pub  
```
