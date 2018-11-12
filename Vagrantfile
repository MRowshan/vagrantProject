# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
users = YAML.load_file("machines.yml")
Vagrant.configure("2") do |config|
	users.each do |user|
		config.vm.box = user['box']
		config.vm.box_check_update = false
  		#config.vm.network "forwarded_port", guest: 80, host: 8080
  		#config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
		config.vm.network "private_network", ip: user['private_ip']
  		#config.vm.network "public_network"
  		#config.vm.synced_folder "../data", "/vagrant_data"
  		config.vm.provider "virtualbox" do |vb|
     		# Display the VirtualBox GUI when booting the machine
     		vb.gui = true
     		vb.name = user['name']
  	
     		# Customize the amount of memory on the VM:
     		vb.memory = user['memory']
     		vb.cpus = user['cpu']
  		end
		user['scripts'].each do |script|
  			config.vm.provision "shell", path: "vagrant_scripts/#{script}"
		end
	end
end
