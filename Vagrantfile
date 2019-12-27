#-*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.network "private_network", ip: "192.168.50.25"

  config.vm.provider "virtualbox" do |vb|
    config.vm.box = "ubuntu/xenial64"
    vb.memory = 4096
    vb.cpus = 2
  end

  config.vm.provider "vmware_fusion" do |vmw|
    config.vm.box = "bento/ubuntu-16.04"
    vmw.gui = false
    vmw.vmx["ethernet0.virtualDev"] = "vmxnet3"
    vmw.vmx["memsize"] = 4096
    vmw.vmx["numvcpus"] = 2
    vmw.whitelist_verified = true
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y install python python-setuptools
  SHELL

  config.vm.provision "ansible_local" do |ansible|
    ansible.config_file = "/vagrant/ansible/ansible.cfg"
    ansible.playbook = "/vagrant/ansible/main.yml"
  end

  config.vm.synced_folder "../st2", "/home/vagrant/local/st2", type: "rsync", rsync__exclude: ["virtualenv/"]
  config.vm.synced_folder "/Users/zach/Repos/packs_dev/", "/opt/stackstorm/packs_dev"
end

