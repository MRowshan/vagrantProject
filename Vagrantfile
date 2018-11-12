# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
users = YAML.load_file("machines.yml")
Vagrant.configure("2") do |config|
	users.each do |user|
		config.vm.define user['name'] do |user_vm|
			user_vm.vm.box = user['box']
			user_vm.vm.box_check_update = false
  			#config.vm.network "forwarded_port", guest: 80, host: 8080
  			#config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
			user_vm.vm.network "private_network", ip: user['private_ip']
  			#config.vm.network "public_network"
  			#config.vm.synced_folder "../data", "/vagrant_data"
  			user_vm.vm.provider "virtualbox" do |vb|
     				vb.name = user['name']
     				vb.memory = user['memory']
     				vb.cpus = user['cpus']
  			end
			user['packages'].each do |package|
				user_vm.vm.provision "shell", inline: <<-SHELL
					sudo #{user['package_manager']} install #{package} -y
				SHELL
			end
			user['scripts'].each do |script|
  				user_vm.vm.provision "shell", path: "vagrant_scripts/#{script}"
			end
		end
	end
end

