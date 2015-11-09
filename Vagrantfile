# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  
  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
    v.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.network :private_network, ip: "10.0.0.100"

  # Provisioning via shell
  config.vm.provision "shell", privileged: true, inline: <<-EOF
    echo "Installing docker"
    apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" > /etc/apt/sources.list.d/docker.list
    apt-get update
    apt-get purge lxc-docker*
    sudo apt-get install -y docker-engine

    echo "Installing docker-compose"
    curl -L https://github.com/docker/compose/releases/download/1.5.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose

    echo "Installation complete"
  EOF

  # Insert as needed - mounted folders
  # see https://docs.vagrantup.com/v2/synced-folders/basic_usage.html

  if Vagrant::Util::Platform.windows?
    config.vm.synced_folder "C:\\Users", "/c/Users"
  end
  #config.vm.synced_folder "/home", "/h"

end
