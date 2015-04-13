# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = false
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = false


  config.vm.define "salt" do |node|
    node.vm.box = "matyunin/centos7"
    node.vm.hostname = "salt"
    node.vm.network :private_network, ip:"10.1.1.10", :netmask => "255.255.255.0"

    node.vm.synced_folder "~/Vagrant/shared", "/home/shared"

    node.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end

    node.vm.provision :salt do |salt|
      salt.install_master = true
      salt.install_type = "stable"
    end

  end

  config.vm.define "server1" do |node|
    node.vm.box = "matyunin/centos7"
    node.vm.hostname = "server1"
    node.vm.network :private_network, ip:"10.1.1.11", :netmask => "255.255.255.0"

    node.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
    end

    node.vm.provision :salt do |salt|
      salt.install_master = false
      salt.install_type = "stable"
    end

  end

  config.vm.define "server2" do |node|
    node.vm.box = "matyunin/centos7"
    node.vm.hostname = "server2"
    node.vm.network :private_network, ip:"10.1.1.21", :netmask => "255.255.255.0"

    node.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
    end

    node.vm.provision :salt do |salt|
      salt.install_master = false
      salt.install_type = "stable"
    end

  end

end
