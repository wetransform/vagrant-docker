vagrant-docker
==============

When boot2docker or Docker Toolbox just don't want to work, you can use this simple Vagrant VM as an alternative to use docker.

Ubuntu 14.04 (trusty) box installing *docker* and *docker-compose*.

By default has a fixed IP address: `10.0.0.100` (can be adapted, see *Configuration*)


Booting up and logging in
-------------------------

```
vagrant up
vagrant ssh
```


Doing Docker stuff
------------------

```
docker ...
```


Upgrading
---------

When the installation script in the Vagrantfile has been updated or you want to install the lastest docker version, run the provisioning again:

```
vagrant provision
```


Configuration
-------------

The file `vagrant.yml` can be used to configure the VM. See `vagrant.sample.yml` for an example. Following the different options are described in short:

* **cpus** - Number of virtual CPUs
* **cpucap** - The CPU execution cap
* **ram** - The system memory in MB
* **ip** - The machine's IP address
* **defaultShares** - If default shares should be mounted; currently this only applies for Windows, where `C:\Users` is available on `/c/Users` in the VM
* **shares** - List of custom mounted folders, each with the path on the **host** and the **vm**
