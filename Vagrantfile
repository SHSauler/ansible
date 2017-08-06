# -*- mode: ruby -*-
# vi: set ft=ruby :

# locale settings for machine
ENV["LC_ALL"] = "en_US.UTF-8"

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "misp-dev" do |m|
    m.vm.box = "ubuntu/xenial64"
    m.vm.hostname = "misp-dev.local"
    m.vm.network "forwarded_port", guest: 80, host: 8080
    m.vm.network "forwarded_port", guest: 443, host: 4443
    m.vm.provider "virtualbox" do |vb|
     vb.name = "misp-dev"
     vb.customize ["modifyvm", :id, "--memory", "2048"]
     
     # Troubleshooting issues via VB GUI. You can disable this if it's not needed!
     vb.gui = true
   end

  #m.ssh.username = "user"
  #m.ssh.password = "asdes123"
  #m.ssh.host = "work"
  #m.ssh.keys_only = true
  #m.ssh.forward_agent = false
  m.ssh.insert_key = true

  m.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "misp-vagrant.yml"
        ansible.verbose = "v"
        ansible.sudo = true
    #ansible.host_key_checking = false
        #ansible.raw_arguments = ["--connection=paramiko"]
    end
  end
end
