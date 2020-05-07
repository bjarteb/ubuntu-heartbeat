# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/bionic64"

  config.hostmanager.enabled = true
  config.hostmanager.manage_guest = true

  # create k8s control plane(s)
  (1..2).each do |i|
    config.vm.define "lb#{i}" do |node|
      node.vm.hostname = "lb#{i}"
      node.vm.network :private_network, ip: "10.0.10.1#{i}"
      node.vm.network "forwarded_port", guest: 80, host: "808#{i}"
      node.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", 1024]
      end
      node.vm.provision "ansible" do |ansible|
        ansible.inventory_path = "inventory"
        ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3" }
        ansible.become = true
        ansible.playbook = "provisioning/install_node.yml"
        #ansible.tags = "test"
      end
    end
  end

end
