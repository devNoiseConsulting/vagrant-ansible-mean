# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "ubuntu/trusty64"

  config.ssh.forward_agent = true

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.111.222"
  config.vm.network "forwarded_port", guest: 9000, host: 9000


  #syncs entire project directory to ~/application on target machine
  config.vm.synced_folder ".", "/home/vagrant/application"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end

  #provisions the environment
  config.vm.provision "ansible" do |ansible|
    ansible.limit = 'all'
    ansible.extra_vars = { user: "vagrant" }
    ansible.inventory_path = "provisioning/hosts"
    ansible.playbook = "provisioning/mean.yml"
  end
end
