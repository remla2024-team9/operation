Vagrant.configure("2") do |config|
  # Shared settings for all machines
  config.vm.box = "bento/ubuntu-24.04"
  config.vm.box_version = "202404.26.0"

  # Controller configuration
  config.vm.define "controller" do |controller|
    controller.vm.hostname = "controller"
    controller.vm.network "private_network", ip: "192.168.57.10"
    controller.vm.network "forwarded_port", guest: 3000, host: 3000
    controller.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = "2048"
    end
    controller.vm.synced_folder ".", "/vagrant", create: true
    controller.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook_controller.yml"
      ansible.verbose = "vvv"
    end
  end

  # Worker configurations
  N = 2
  (1..N).each do |i|
    config.vm.define "worker#{i}" do |worker|
      worker.vm.hostname = "worker#{i}"
      worker.vm.network "private_network", ip: "192.168.57.#{10+i}"
      worker.vm.network "forwarded_port", guest: 3000, host: 3000 + i
      worker.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = "4096"
      end
      worker.vm.synced_folder ".", "/vagrant", create: true
      worker.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "playbook_worker.yml"
        ansible.groups = { "workers" => ["worker#{i}"] }
        ansible.verbose = "vvv"
      end
    end
  end
end
