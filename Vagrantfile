# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # On macOS:
  #config.vm.network "private_network", type: "dhcp"
  # On Windows:
  config.vm.network "private_network", ip: "192.168.57.2", netmask: "255.255.255.0"

  N = 2 # Number of worker nodes
  (1..N).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = "bento/ubuntu-24.04"
      node.vm.hostname = "node-#{i}"
      node.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = "4096"
      end
      # Setup private network, if required
      node.vm.network "private_network", ip: "192.168.57.#{10+i}"
    end
  end

  config.vm.define "controller" do |controller|
    controller.vm.box = "bento/ubuntu-24.04"
    controller.vm.hostname = "controller"
    controller.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = "2048"
    end
    
    controller.vm.network "private_network", ip: "192.168.57.10"

    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.verbose = "vvv"
    end
  end
end