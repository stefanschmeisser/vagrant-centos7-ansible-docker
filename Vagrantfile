# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    config.vm.box = "centos/7"
    config.ssh.insert_key = false

    config.vm.provider :virtualbox do |v|
        v.name = "gitlab"
        v.memory = 512
        v.cpus = 2
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    config.vm.hostname = "gitlab"
    #config.vm.network :private_network, ip: "192.168.178.42"
    config.vm.network "public_network", ip: "192.168.178.38"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.network :forwarded_port, guest: 443, host: 8443

    # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
    config.vm.define :gitlab do |gitlab|
    end

    # Ansible provisioner.
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/ansible/playbook.yaml"
        ansible.become = true
    end

end
