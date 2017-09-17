# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "server" do |server|
    memory_var_name = "PHPSERV_MEMORY"
    ip_var_name = "PHPSERV_IP"

    server.vm.box = "bento/debian-9.1"
    server.vm.hostname = "server"
    server.vm.network "private_network", ip: ENV[ip_var_name] || "192.168.1.10"

    server.vm.provider "virtualbox" do |vb|
      vb.memory = ENV.has_key?(memory_var_name) ? Integer(ENV[memory_var_name]) : 1024
      vb.cpus = 1
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end

    server.vm.provision :shell, :path => "provisioning/scripts/ansible-stretch"
    server.vm.provision :shell, :inline => "cd /vagrant/provisioning/ansible/ && sudo ansible-playbook dockerbox.yml"
  end
end
