# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV["VAGRANT_DEFAULT_PROVIDER"] = "libvirt"

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "centos/7"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.hostname = "jenkins.master"
    jenkins.vm.network :private_network, ip: "192.168.60.4"
    jenkins.vm.provider :libvirt do |v|
      v.memory = "4096"
      v.cpus = "2"
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbooks/provision.yaml"
    ansible.inventory_path = "inventories/hosts"
  end
end
