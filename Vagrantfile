# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "cliente" do |s1|
    s1.vm.box = "ubuntu/focal64"
    s1.vm.network "private_network", type: "static", ip: "192.168.56.9"
    s1.vm.hostname = "gabrielegabriel-cliente"
    s1.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"
    end
    s1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get upgrade -y
      apt-get install -y curl vim htop
    SHELL
  end

  config.vm.define "servidor" do |s2|
    s2.vm.box = "centos/7"
    s2.vm.network "forwarded_port", guest: 9080, host: 9080
    s2.vm.network "forwarded_port", guest: 27017, host: 27017
    s2.vm.network "private_network", type: "static", ip: "192.168.56.10"
    s2.vm.hostname = "gabrielegabriel-servidor"
    s2.vm.synced_folder "./", "/vagrant"
    s2.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"
    end
    s2.vm.provision "shell", inline: <<-SHELL
      sudo yum -y update
      sudo yum install -y yum-utils git wget
      sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
      sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      sudo systemctl start docker
      sudo chmod 666 /var/run/docker.sock
      sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      sudo chmod +x /usr/local/bin/docker-compose
      docker-compose -f /vagrant/docker-compose.yml up -d
    SHELL
  end
end
