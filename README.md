# vagrant-cluster

Installs a cluster of master node and slave nodes for Debian. Configure as many servers as you want.

# Requirements
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](https://www.vagrantup.com/downloads.html)

# Dependencies
- [geerlingguy/ansible-role-docker](https://github.com/geerlingguy/ansible-role-docker)

# Usage
This command creates and configures guest machines according to your Vagrantfile.
```bash
vagrant up [name|id]
```

Force, or prevent, the provisioners to run.
```bash 
vagrant up --[no-]provision 
```

![demo.gif](https://github.com/rakauchuk/vagrant-cluster/blob/master/demo.gif)
