# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "geerlingguy/ubuntu2004"

  config.vm.network "private_network", ip: "192.168.56.11"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  # config.vm.provision "docker" do |d|
  #   d.pull_images "mongo:latest", "rkepha/yolo-backend:1.0.1-buster", "rkepha/yolo-client:1.0.1-buster"
  # end
  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end

end

