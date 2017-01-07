# Vagrant example04

*This is a Vagrant multi machine example that will create up to six clusters with (x) number of virtual machines in each cluster using Virtualbox as VM provider.*

**jf@Tzunami:~/vagrant-examples/example04$** vagrant up  
```  
Bringing machine 'Cluster1-server1' up with 'virtualbox' provider...  
Bringing machine 'Cluster1-server2' up with 'virtualbox' provider...  
Bringing machine 'Cluster2-server1' up with 'virtualbox' provider...  
Bringing machine 'Cluster2-server2' up with 'virtualbox' provider...  
Bringing machine 'Cluster3-server1' up with 'virtualbox' provider...  
Bringing machine 'Cluster3-server2' up with 'virtualbox' provider...  
Bringing machine 'Cluster4-server1' up with 'virtualbox' provider...  
Bringing machine 'Cluster4-server2' up with 'virtualbox' provider...  
Bringing machine 'Cluster5-server1' up with 'virtualbox' provider...  
Bringing machine 'Cluster5-server2' up with 'virtualbox' provider...  
Bringing machine 'Cluster6-server1' up with 'virtualbox' provider...  
Bringing machine 'Cluster6-server2' up with 'virtualbox' provider...  
```

## Cluster settings  
*Tweak the settings below in the Vagrantfile to customize a specific cluster*
```  
# Cluster(x) settings
CLUSTER(x)_VM_COUNT = 2                    # Create x number of VMs in cluster(x). Set to 0 for disabling this cluster
CLUSTER(x)_BOX_IMAGE = "ubuntu/xenial64"   # Vagrant BOX  
CLUSTER(x)_VM_NAME = "Cluster1-server"     # Virtualbox name & hostname for the cluster1 VMs: (Cluster(x)-server1, Cluster(x)-server2, ...)  
CLUSTER(x)_VM_GROUP = "Cluster1"           # Tag all VMs belonging to cluster(x) in Virtualbox with this group  
CLUSTER(x)_VM_RAM = 1024                   # How much RAM memory should each VM have?  
CLUSTER(x)_VM_CPU = 1                      # How many vCPU's should each VM have?  
CLUSTER(x)_VM_SUBNET = "192.168.56.1"      # Assign private network IP to 192.168.56.1#{i}. Example: 192.168.56.11, 192.168.56.12, ...  
CLUSTER(x)_VM_SHARED_FOLDER = "~/vshare"   # Mount directory ~/vshare from laptop to VM on path /vagrant  
```

## Shell provisioning for all clusters
*The shell commands below will be executed on all VMs on all activated clusters*
```
$ALL_CLUSTERS_SHELL_PROVISION = <<SCRIPT

    echo "#### Running shell provisioning for all clusters ####"

    # Create SSH user on all clusters
    useradd jf -d /home/jf -s /bin/bash
    mkdir -vp /home/jf/.ssh
    echo #{SSH_PUB_KEY} >> /home/jf/.ssh/authorized_keys
    echo 'jf ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/lusers
    chown -vR jf:jf /home/jf

    # APT on all clusters
    apt-get update
    apt-get upgrade -y


SCRIPT
```

## Custom shell provisioning for a specific cluster
*The example shell commands below will be executed on all VMs in each activated cluster*
```
$CLUSTER1_SHELL_PROVISION = <<SCRIPT

    echo "#### Running shell provisioning for cluster1 ####"
    apt-get install nginx -y

SCRIPT

$CLUSTER2_SHELL_PROVISION = <<SCRIPT

    echo "#### Running shell provisioning for cluster2 ####"
    apt-get install mariadb-server -y  

SCRIPT

$CLUSTER3_SHELL_PROVISION = <<SCRIPT

    echo "#### Running shell provisioning for cluster3 ####"
    apt-get install screen irssi -y

SCRIPT

$CLUSTER4_SHELL_PROVISION = <<SCRIPT

    echo "#### Running shell provisioning for cluster4 ####"

SCRIPT

$CLUSTER5_SHELL_PROVISION = <<SCRIPT

    echo "#### Running shell provisioning for cluster5 ####"

SCRIPT

$CLUSTER6_SHELL_PROVISION = <<SCRIPT

    echo "#### Running shell provisioning for cluster6 ####"

SCRIPT
```

## Global settings
*The global settings will be used in every activated cluster and on every server in that cluster*  

```
API_VERSION = 2                                                          # Install VMs using Vagrant API version 2
SSH_PUB_KEY = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip  # Read in this SSH public key so we can insert it into any VM if we want
```
