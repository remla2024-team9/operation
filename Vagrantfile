# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # On macOS:
  #config.vm.network "private_network", type: "dhcp"
  # On Windows:
  config.vm.network "private_network", ip: "192.168.57.2", netmask: "255.255.255.0"

  config.vm.define "controller" do |controller|
    controller.vm.box = "bento/ubuntu-24.04"
    config.vm.box_version = "202404.26.0"
    controller.vm.hostname = "controller"
    controller.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = "2048"
    end
    controller.vm.network "private_network", ip: "192.168.57.10"
    controller.vm.synced_folder ".", "/vagrant", create: true
    controller.vm.provision "ansible_local" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbook_controller.yml"
      ansible.verbose = "vvv"
    end
  end

  N = 2
  (1..N).each do |i|
    config.vm.define "worker#{i}" do |worker|
      worker.vm.box = "bento/ubuntu-24.04"
      config.vm.box_version = "202404.26.0"
      worker.vm.hostname = "worker#{i}"
      worker.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = "4096"
      end
      worker.vm.network "private_network", ip: "192.168.57.#{10+i}"
      worker.vm.synced_folder ".", "/vagrant", create: true
      worker.vm.provision "ansible_local" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "playbook_worker.yml"
        ansible.groups = { "workers" => ["worker#{i}"] }
        ansible.verbose = "vvv"
      end
    end
  end
end
