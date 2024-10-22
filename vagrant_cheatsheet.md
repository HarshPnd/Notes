# Install Vagrant
### Download and Install from - https://developer.hashicorp.com/vagrant/downloads

    vagrant -v     
get the vagrant version 

    vagrant global-status   
outputs status of all vagrant machines

    vagrant global-status --prune 
same as above, but prunes invalid entries

    --help    
use with any vagrant command to see help options e.g vagrant box --help



# Install or Setup a Provider (Virtualbox)

### Download and Install from - https://www.virtualbox.org/wiki/Downloads 

    vboxmanage -v    
get the version of virtualbox



## Creating Vagrantfile (vagrant env)

Create a new folder and go to the folder location from Command Prompt/Terminal

    vagrant init    
Initializes a new Vagrant project with a Vagrantfile

    vagrant init ＜boxpath＞ 
Initialize Vagrant with a specific box vagrant init hashicorp/bionic64

    vagrant validate  
validates vagrantfile

    vagrant status   
outputs status of the vagrant machine

----

### Vagrantfile Box Search https://portal.cloud.hashicorp.com/vagrant/discover

### Vagrantfile Generator  https://vagrantfile-generator.vercel.app/

---


## Starting and Stopping VM

    vagrant up    
starts vagrant environment (also provisions only on the FIRST vagrant up)

    vagrant halt    
stops the vagrant machine

    vagrant suspend   
suspends a virtual machine (remembers state)

    vagrant resume   
resume a suspended machine (vagrant up works just fine for this as well)

    vagrant provision   
forces reprovisioning of the vagrant machine

    vagrant reload    
restarts vagrant machine, loads new Vagrantfile configuration

    vagrant reload --provision 
restart the virtual machine and force provisioning

    vagrant status    
outputs status of the vagrant machine




## Getting into a VM

    vagrant ssh     
connects to machine via SSH

    vagrant ssh ＜boxname＞ 
If you give your box a name in your Vagrantfile, you can ssh into it with boxname




## Cleaning up a VM

    vagrant destroy   
stops and deletes all traces of the vagrant machine

    vagrant destroy -f    
same as above, without confirmation




## Boxes

    vagrant box list    
see a list of all installed boxes on your computer

    vagrant box add ＜name＞ ＜url＞ 
download a box image to your computer

    vagrant box outdated   
check for updates vagrant box update

    vagrant box remove ＜name＞ 
deletes a box from the machine
    vagrant package    
packages a running virtualbox env in a reusable box **vagrant package --output mybox.box**




## Provisioning Commands

### Vagrantfile ＞ add block ＞ config.vm.provision

    config.vm.provision "shell",
        inline: "echo Hello, World"

---

    config.vm.provision "shell", inline: ＜＜-SHELL
        sudo apt-get update
        sudo apt-get install apache2 -y
    SHELL

### OR

Create a separate file having Provision Scripts and provide the location in Vagrantfile

    config.vm.provision :shell, path: "provision.sh"
---
    vagrant provision   
if VM is already running, runs the provisioners defined in your Vagrantfile

    vagrant reload --provision 
reloads the Vagrantfile and runs the provisioners




## Networking

Add in Vagrantfile

### Port Forwarding
    config.vm.network "forwarded_port", guest: 80, host: 8080
**maps port 80 of the VM to port 8080** on the host machine

    config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
    config.vm.usable_port_range = (8000..9000)

### Creating Public Network

    config.vm.network "public_network", ip: "192.168.1.100"
if IP address is not given, a default IP will be assigned

### Creating Private Network

    config.vm.network "private_network", ip: "192.168.50.4"
This will create a private network with the IP address of **192.168.50.4**




## Sharing Folder

By default **./** on your computer is shared as **/vagrant** on the VM

**Edit Vagrantfile** 

    config.vm.synced_folder "./data", "/vagrant_data"

shares the folder **data** present on the vagrantfile folder to a folder called **vagrant_data** on the VM


## Snapshot Commands

**What is a Snapshot** 
- Full copy of the VM in its Current state
- Can be used to revert back to a previous state of the VM
- All configurations - disk contents, apps, packages, folders, memory
- Creates backup of the Virtual Machine 
- Restoring the VM from an earlier state

**Snapshot Commands**
---
    vagrant snapshot save ＜name＞  
creates a snapshot from the current state of the machine

    vagrant snapshot list    
lists all snapshots of the current machine

    vagrant snapshot restore ＜name＞ 
restores machine from the specific snapshot

    vagrant snapshot delete ＜name＞ 
deletes the specific snapshot

<u> ***Note:*** </u> 
- Snapshots do not include the Vagrantfile or any other configuration files in your project directory
- These files are separate from the snapshot and can be shared or  version controlled separately 


## Plugin Commands

Plugins are add-ons to enhance functionality of a tool

### Available Plugins : https://github.com/hashicorp/vagrant/wiki/Available-Vagrant-Plugins

    vagrant plugin install ＜plugin-name＞ 
installs the specified Vagrant plugin

    vagrant plugin list     
lists all installed Vagrant plugins

    vagrant plugin update ＜plugin-name＞ 
to update a plugin

    vagrant plugin repair    
to repair installed plugins in case of error

    vagrant plugin uninstall ＜plugin-name＞ 
uninstalls the specified Vagrant plugin

    vagrant plugin expunge    
to delete all plugins

    vagrant plugin expunge --reinstall  
to reinstall all expunged plugins 


# Sample VagrantFile

for the following file you need to create **provision.sh** file with the desired script or you can comment out the **config.vm.provision** line

    Vagrant.configure("2") do |config|
      config.vm.box = "centos/7"
      config.vm.provision :shell, path: "provision.sh"
      # config.vm.network "public_network", ip: "192.168.10.102"
      config.vm.network "public_network"
      # config.vm.network "private_network", type: "dhcp" 
      config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
      config.vm.usable_port_range = (8000..9000)
    end


---
## Sample **provision.sh** for the above file

    #!/bin/bash

    # Set up yum for CentOS
    cd /etc/yum.repos.d/
    sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*  
    sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*


    # Install httpd server
    sudo yum install httpd -y
    sudo systemctl start httpd

    # Write the first webpage
    cd /var/www/html
    cat >> index.html << EOF
    Hello World!!!!
    from node1
    EOF