# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  # Definindo as configurações para a máquina master
  config.vm.define "master" do |master|
    master.vm.box = "ubuntu/bionic64"
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.50.10"
    master.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end
    master.vm.provision "shell", inline: <<-SHELL
      # Atualizando o sistema
      sudo apt-get update
      sudo apt-get install -y docker.io
      sudo usermod -aG docker vagrant
    SHELL
  end

  # Definindo as configurações para as máquinas nodes
  ["node01", "node02", "node03"].each_with_index do |node, index|
    config.vm.define node do |node_config|
      node_config.vm.box = "ubuntu/bionic64"
      node_config.vm.hostname = node
      node_config.vm.network "private_network", ip: "192.168.50.#{index + 11}"
      node_config.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
      end
      node_config.vm.provision "shell", inline: <<-SHELL
        # Atualizando o sistema
        sudo apt-get update
        sudo apt-get install -y docker.io
        sudo usermod -aG docker vagrant
      SHELL
    end
  end
  
end
