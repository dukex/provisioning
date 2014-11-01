# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network :public_network,  ip: "192.168.33.22"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 256]
  end

  {
    'app' => '192.168.77.21',
    'db'  => '192.168.77.22',
    'bot' => '192.168.77.23'
  }.each do |hostname, ip|
    config.vm.define hostname do |machine|
      machine.vm.hostname = 'app'
      machine.vm.network "private_network", ip: ip
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    ansible.limit = "all"
  end
end
