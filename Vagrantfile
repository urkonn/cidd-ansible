# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
    
  config.vm.define :master do |master_config|
    master_config.vm.box = "ubuntu/trusty64"
    master_config.vm.box_url = "https://atlas.hashicorp.com/ubuntu/boxes/trusty64"
  
    master_config.vm.network :forwarded_port, guest: 8080, host: 8888
    master_config.vm.network :forwarded_port, guest: 8081, host: 8881
    master_config.vm.network :forwarded_port, guest: 5000, host: 5555
    master_config.vm.network :private_network, ip: "192.168.33.10"
  
    master_config.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/masterservers.yml"
      #ansible.raw_arguments = "--check"
      ansible.inventory_path = "vagrant_ansible_inventory_master"
      ansible.verbose = "v"
    end
  end
  
  
  config.vm.define :slave do |slave_config|
    slave_config.vm.box = "ubuntu/trusty64"
    slave_config.vm.box_url = "https://atlas.hashicorp.com/ubuntu/boxes/trusty64"
  
    slave_config.vm.network :forwarded_port, guest: 13001, host: 1301
    slave_config.vm.network :forwarded_port, guest: 13002, host: 1302
    slave_config.vm.network :private_network, ip: "192.168.33.30"
  
    slave_config.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/slaveservers.yml"
      #ansible.raw_arguments = "--check"
      ansible.inventory_path = "vagrant_ansible_inventory_slave"
      ansible.verbose = "v"
      ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    end
  end

end
