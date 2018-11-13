# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
users = YAML.load_file("machines.yml")
Vagrant.configure("2") do |config|
	users.each do |user|
		config.vm.define user['name'] do |user_vm|
			set_hostname(user_vm, user['name'])
			set_box(user_vm, user['box'])
			set_cpus(user_vm, user['cpus'])
			set_memory(user_vm, user['memory'])
			set_private_ip(user_vm, user['private_ip'])
			install_packages(user_vm, user['package_manager'], user['packages'])
			run_scripts(user_vm, user['scripts'])
			add_users(user_vm, user['users'])
		end
	end
end


def set_hostname(user_vm, hostname)
	user_vm.vm.provider "virtualbox" do |vb|
		vb.name = hostname
	end
end

def set_box(user_vm, box)
	user_vm.vm.box = box
end

def set_cpus(user_vm, cpus)
	user_vm.vm.provider "virtualbox" do |vb|
     		vb.cpus = cpus
	end
end

def set_memory(user_vm, memory)
	user_vm.vm.provider "virtualbox" do |vb|
		vb.memory = memory
	end
end

def set_private_ip(user_vm, private_ip)
	user_vm.vm.network "private_network", ip: private_ip
end

def install_packages(user_vm, package_manager, packages)
	packages.each do |package|
		user_vm.vm.provision "shell", inline: <<-SHELL
			sudo #{package_manager} install #{package} -y
		SHELL
	end
end

def run_scripts(user_vm, scripts)
	scripts.each do |script|
  		user_vm.vm.provision "shell", path: "vagrant_scripts/#{script}"
	end
end

def add_users(user_vm, users)
	users.each do |user|
		user_vm.vm.provision "shell", inline: <<-SHELL
			sudo useradd #{user}
	SHELL
	end
end
