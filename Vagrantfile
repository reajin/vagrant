# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"
  
  #forward ports
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 9090, host: 9090

  # name in `vagrant global-status`
  config.vm.define "ubuntu-test" do |t|
  end
  # name in VirtualBox
  config.vm.provider "virtualbox" do |v|
    v.name = "ubuntu-test"
  end

  config.vm.synced_folder "./docker/", "/opt/docker-compose/"

  #ansible  
  config.vm.provision "ansible" do |ansible|
   ansible.playbook = "./ansible/setup.yml"
   ansible.host_key_checking = "false"
   ansible.limit = "all"
  end

   config.vm.provision "shell", inline: <<-SHELL
     cd /opt/docker-compose/ && docker compose up -d
   SHELL

end
