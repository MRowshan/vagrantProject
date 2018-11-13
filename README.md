# vagrantProject

Creating virtual machines on VirtualBox using Vagrant
Requires id_rsa and id_rsa.pub in the directory for ssh connectivity between vm's

## Running Vagrant

Creating VM's  `vagrant up`
 - add the name of the vm to create specific vm's 
 
Deleting VM's `vagrant destroy`  
 - add `-f` to skip confirmation  
 - add the name of the vm to destroy specific vm's  

## YAML file

Machines are defined in the `machines.yml` file 
```yaml
- name: machine-1
  box: centos/7
  cpus: 1
  memory: 2048
  private_ip: 10.0.10.10
  package_manager: yum
  packages:
  - git
  scripts:
  - ssh_script
```
