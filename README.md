vagrant-docker
==============

When boot2docker or Docker Toolbox just don't want to work, you can use this simple Vagrant VM as an alternative to use docker.

Ubuntu 14.04 (trusty) box installing *docker* and *docker-compose*.

By default has a fixed IP address: `10.0.0.100`


Booting up and logging in
-------------------------

```
vagrant up
vagrant ssh
```


Doing Docker stuff
------------------

```
sudo docker ...
```


Configuration
-------------

Adapt the configuration in the Vagrantfile as you see fit.

### Access to host file system
At the end of the Vagrantfile you can find examples on including synced folders in the VM.
Adapt them as needed to use resources from your host in the VM.
By default on Windows `C:\Users` is mounted to `/c/Users` inside the VM.
