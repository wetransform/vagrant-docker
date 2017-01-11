# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'

VAGRANTFILE_API_VERSION = "2"

options = File.exist?('vagrant.yml') ? YAML.load_file('vagrant.yml') : Hash.new

# default values
if !options['cpus']
  options['cpus'] = 2
end
if !options['cpucap']
  options['cpucap'] = "70"
end
if (!options['ram'])
  options['ram'] = "4096"
end
if (!options['ip'])
  options['ip'] = "10.0.0.100"
end
if (options['defaultShares'].nil?)
  options['defaultShares'] = true
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  
  config.vm.provider "virtualbox" do |v|
    v.cpus = options['cpus']
    v.customize ["modifyvm", :id, "--cpuexecutioncap", options['cpucap']]
    v.customize ["modifyvm", :id, "--memory", options['ram']]
  end

  config.vm.network :private_network, ip: options['ip']

  # Provisioning via shell
  config.vm.provision "shell", privileged: true, inline: <<-EOF
    echo "Installing docker"
    apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" > /etc/apt/sources.list.d/docker.list
    apt-get update
    apt-get purge lxc-docker*
    sudo apt-get install -y docker-engine

    echo "Installing docker-compose"
    curl -L https://github.com/docker/compose/releases/download/1.9.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose

    echo "Installing docker-compose bash completion"
    curl -L https://raw.githubusercontent.com/docker/compose/$(docker-compose --version | awk 'NR==1{print $NF}')/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose

    echo "Setting up docker access w/o sudo"
    chown -R vagrant: /home/vagrant/.docker/
    usermod -aG docker vagrant

    echo "Installation complete"
  EOF

  # Mounted folders
  # see https://docs.vagrantup.com/v2/synced-folders/basic_usage.html

  if options['defaultShares']
    if Vagrant::Util::Platform.windows?
      config.vm.synced_folder "C:\\Users", "/c/Users"
    end
  end

  # configured shares
  shares = options['shares']
  if !shares.nil?
    shares.each do |share|
      config.vm.synced_folder share['host'], share['vm']
    end
  end

end
