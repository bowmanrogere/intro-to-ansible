# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define 'controlNode' do |controlNode|
    controlNode.vm.box = "geerlingguy/centos7"
    controlNode.vm.hostname = "control-node"
    controlNode.vm.synced_folder ".", "/home/vagrant/ansible", type: "virtualbox"
    controlNode.vm.network "private_network", ip: "10.0.0.100"
    controlNode.vm.provision "shell", inline: <<-SHELL
      sudo yum install -y ansible
    SHELL
  end
  config.vm.define 'managedNode' do |managedNode|
    managedNode.vm.box = "geerlingguy/centos7"
    managedNode.vm.hostname = "managed-node"
    managedNode.vm.network "private_network", ip: "10.0.0.101"
    managedNode.vm.provision "shell", inline: <<-SHELL
      sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
      sudo service sshd restart
    SHELL
  end
end
