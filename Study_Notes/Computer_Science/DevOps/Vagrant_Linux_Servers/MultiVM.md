Doc: https://developer.hashicorp.com/vagrant/docs/multi-machine

# Create Multivm
> [!important]
> Multiple machines are defined within the same project [Vagrantfile](https://developer.hashicorp.com/vagrant/docs/vagrantfile) using the `config.vm.define` method call. This configuration directive is a little funny, because it creates a Vagrant configuration within a configuration.
> 
> Make sure all the other vms are powered off or deleted before running this one. Since this will create lots of vms and occupy lots of disk storage.
```bash
Vagrant.configure("2") do |config|
    config.vm.define "web01" do |web01|
      web01.vm.box = "spox/ubuntu-arm" 
      web01.vm.box_version = "1.0.0"
      web01.vm.hostname = "web01"
      web01.vm.network "private_network", ip: "192.168.56.41"
      web01.vm.provider "vmware_desktop" do |vmware|
        vmware.ssh_info_public = true
        vmware.gui = true
       end
    end
  
    config.vm.define "web02" do |web02|
      web02.vm.box = "spox/ubuntu-arm" 
      web02.vm.box_version = "1.0.0"
      web02.vm.hostname = "web02"
      web02.vm.network "private_network", ip: "192.168.56.42"
      web02.vm.provider "vmware_desktop" do |vmware|
        vmware.ssh_info_public = true
        vmware.gui = true
       end
    end
  

    config.vm.define "db01" do |db01|
      db01.vm.box = "bandit145/centos_stream9_arm"
      db01.vm.hostname = "db01"
      db01.vm.network "private_network", ip: "192.168.56.43"
      db01.vm.provider "vmware_desktop" do |vmware|
        vmware.ssh_info_public = true
        vmware.gui = true
       end
      db01.vm.provision "shell", inline: <<-SHELL
        yum install -y wget unzip mariadb-server -y
        systemctl start mariadb
        systemctl enable mariadb
        # Additional provisioning steps for db01
      SHELL
    end
  end
```


# Get Into The Console/Deletion
> [!important]
> If we want to visit the console of one of the vms, we would have to specify the name of the vm, like `vagrant ssh web01`
> Same way, if we want to stop particular vm, `vagrant halt web02`. And `vagrant destroy web03` to destroy particular vm.
> 





