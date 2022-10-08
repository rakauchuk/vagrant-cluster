# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant", type: "rsync"
  servers = YAML.load_file('servers.yaml')
  servers.each do |servers|
    config.vm.define servers["hostname"] do |server|
      server.vm.box = servers["box"]
      config.vm.box_version = servers["box_version"]
      server.vm.hostname = servers["hostname"]
      server.vm.network :private_network, ip: servers["ip"]
      server.vm.provider :virtualbox do |vb|
        vb.memory = servers["memory"]
        vb.cpus = servers["cpus"]
        vb.name = servers["hostname"]
      end
    end
  end
  config.vm.provision "ansible", type: :ansible_local do |ansible|
    ansible.galaxy_role_file = "requirements.yml"
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3" }
  end
end
