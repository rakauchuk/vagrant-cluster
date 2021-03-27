# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

# Using yaml to load external configuration files
require 'yaml'
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  config.ssh.insert_key = false

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.  
  config.vm.synced_folder ".", "/vagrant", type: "rsync"
  # Loading in the VM configuration information
  servers = YAML.load_file('servers.yaml')
  servers.each do |servers|
    config.vm.define servers["hostname"] do |server|
      # Every Vagrant development environment requires a box. You can search for
      # boxes at https://vagrantcloud.com/search.
      server.vm.box = servers["box"]
      config.vm.box_version = servers["box_version"]
      server.vm.hostname = servers["hostname"]
      server.vm.network :private_network, ip: servers["ip"]
      # Provider-specific configuration so you can fine-tune various
      # backing providers for Vagrant. These expose provider-specific options.
      # Example for VirtualBox:
      server.vm.provider :virtualbox do |vb|
        vb.memory = servers["memory"]
        vb.cpus = servers["cpus"]
        vb.name = servers["hostname"]
        # Limit to VM to 33% of available CPU
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "33"]
      end
    end
  end
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    cat /etc/centos-release
  SHELL
end
