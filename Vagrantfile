# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "bento/fedora-25"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.network :private_network, ip: "192.168.56.10"
  config.vm.network "forwarded_port", guest: 9000, host: 9000
  config.vm.network "forwarded_port", guest: 9002, host: 9002


  config.vm.provider :virtualbox do |v|
      v.memory = 5000
      v.linked_clone = true
  end

  config.vm.define "app" do |app|
      app.vm.hostname = "pt.dev"
  end

  config.vm.provision "shell", inline: "nmcli connection reload; systemctl restart network.service"

  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.sudo = true
      ansible.ask_vault_pass = true
  end
end
