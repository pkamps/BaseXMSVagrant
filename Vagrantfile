# -*- mode: ruby -*-
# vi: set ft=ruby :
#

# Requirements
# ------------

Vagrant.require_version ">= 1.3.0"

unless Vagrant.has_plugin?("vagrant-hostsupdater")
  raise "!*! Plugin required !*!\n\n\tvagrant plugin install vagrant-hostsupdater\n"
end

Vagrant.configure("2") do |config|
  config.vm.box     = "vivid-server-cloudimg-i386-vagrant-disk1"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/vivid/current/vivid-server-cloudimg-i386-vagrant-disk1.box"
  #config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-i386-vagrant-disk1.box"
  #PEK: doesn't work in my version of vagrant
  config.vm.network :private_network, ip: "192.168.37.66"

  config.vm.hostname = "basexms"
  config.vm.synced_folder "share", "/var/www", type: "nfs"

  config.ssh.username = "vagrant"

  config.vm.provider :virtualbox do |vb|
    #vb.customize ["modifyvm", :id, "--memory", 2048]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.provision :ansible do |ansible|
	ansible.host_key_checking = false
    ansible.playbook = "ansible/main.yml"
    ansible.inventory_path = "ansible/inventories/vagrant"
    ansible.limit = 'all'
    #enable to see verbose output like json return values
	#ansible.verbose = 'v'
	ansible.extra_vars = {env: "dev"}
  end
end
