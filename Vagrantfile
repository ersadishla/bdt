# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|

  # MySQL Cluster dengan 3 node
  (1..3).each do |i|
    config.vm.define "db#{i}" do |node|
      node.vm.hostname = "db#{i}"
      node.vm.box = "bento/ubuntu-16.04"
      node.vm.network "private_network", ip: "192.168.17.#{i+16}"

      node.vm.provider "virtualbox" do |vb|
        vb.name = "db#{i}"
        vb.gui = false
        vb.memory = "1024"
      end

      node.vm.provision "shell", path: "deployMySQL1#{i}.sh", privileged: false
    end
  end

  config.vm.define "proxy" do |proxy|
    proxy.vm.hostname = "proxy"
    proxy.vm.box = "bento/ubuntu-16.04"
    proxy.vm.network "private_network", ip: "192.168.17.16"

    proxy.vm.provider "virtualbox" do |vb|
      vb.name = "proxy"
      vb.gui = false
      vb.memory = "512"
    end

    proxy.vm.provision "shell", path: "deployProxySQL.sh", privileged: false
  end

end
