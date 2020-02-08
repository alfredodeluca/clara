# -*- mode: ruby -*-
# vi: set ft=ruby :

LB_IP="192.168.100.10"
DB_IP="192.168.100.20"
NODES_SUBNET="192.168.100"

Vagrant.configure(2) do |config|

#
### Joomla nodes
#

(1..2).each do |i|
  config.vm.define "joomla#{i}" do |node|
    node.vm.box = "ubuntu/bionic64"
    node.vm.box_version = "20190918.0.0"
    node.vm.network "private_network", ip: "#{NODES_SUBNET}.1#{i}"
    node.vm.hostname = "joomla#{i}"
    node.vm.provider :virtualbox do |v|
      v.cpus = 2
      v.memory = 2048
    end
  end
end

#
### Load Balancer
#
  config.vm.define "joomla-lb" do |compass|
    compass.vm.box = "ubuntu/bionic64"
    compass.vm.box_version = "20190918.0.0"
    compass.vm.network "private_network", ip: "#{LB_IP}"
    compass.vm.hostname = "joomla-lb"
    compass.vm.provider :virtualbox do |v|
      v.cpus = 2
      v.memory = 2048
    end
  end
#
### MySQL server
#
  config.vm.define "joomla-db" do |compass|
    compass.vm.box = "ubuntu/bionic64"
    compass.vm.box_version = "20190918.0.0"
    compass.vm.network "private_network", ip: "#{DB_IP}"
    compass.vm.hostname = "joomla-db"
    compass.vm.provider :virtualbox do |v|
      v.cpus = 3
      v.memory = 3072
    end
  end
#
### Provisioning  
#
config.vm.provision "ansible" do |ansible|      
  ansible.playbook = "ansible/playbook.yml"
end
end

