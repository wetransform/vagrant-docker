# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu-14.04-amd64"
  config.vm.box_url = "https://github.com/jose-lpa/packer-ubuntu_14.04/releases/download/v2.0/ubuntu-14.04.box"

  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
    v.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.network :private_network, ip: "10.0.0.100"

  # Insert as needed - mounted folders
  # see https://docs.vagrantup.com/v2/synced-folders/basic_usage.html

  #config.vm.synced_folder "C:\\Users", "/c/Users"
  #config.vm.synced_folder "/home", "/h"
end
