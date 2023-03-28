### Install Vagrant and VirtualBox on your local machine

`cd ../backend`

`npm install`

`npm start`
Sure, I can help you with that. Here are the steps you can follow:

Install Vagrant and VirtualBox on your local machine.
Create a new directory for your project and navigate to it in the terminal.
Create a new Vagrantfile with the following contents:

### Create a project directory and navigate into it and initializa vagrant

`vagrant init`

#### this will create a Vagrantfile

### Add the following to the Vagrantfile

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "geerlingguy/ubuntu2004"

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end

end

```

### Create a file on the root directory and name it `playbook.yml`

### run the provision playbook with vagrant

`vagrant up --provision`
