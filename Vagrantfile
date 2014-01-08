# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "squeeze64"
  config.vm.hostname = "squeeze64"
  config.vm.box_url = "~/projects/vagrant/boxes/squeeze64.box"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 2048]
    v.customize ["modifyvm", :id, "--cpus", 4]
  end

  config.vm.network :private_network, ip: "10.1.1.2"
  config.vm.network :forwarded_port, guest: 8085, host: 8085
  config.vm.network :forwarded_port, guest: 8086, host: 8086
  config.vm.network :forwarded_port, guest: 8888, host: 8888
  config.vm.network :forwarded_port, guest: 4021, host: 4021

  config.vm.synced_folder "~/projects", "/home/vagrant/projects"

  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "provisioning/development"
    ansible.playbook = "provisioning/site.yml"
    ansible.host_key_checking = false
    ansible.verbose = "vvvv"
  end

end
