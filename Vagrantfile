# -*- mode: ruby -*-
# vi: set ft=ruby :

require "yaml"

ENV["VAGRANT_DEFAULT_PROVIDER"] = "libvirt"

VAGRANTFILE_API_VERSION = "2"

current_dir = File.dirname(File.expand_path(__FILE__))
if File.file?("#{current_dir}/vagrant.yaml")
  config_file = YAML.load_file("#{current_dir}/vagrant.yaml")
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "centos/7"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.hostname = config_file["jenkins_master"]["hostname"]
    jenkins.vm.network :private_network, ip: config_file["jenkins_master"]["ip"]
    jenkins.vm.provider :libvirt do |v|
      v.memory = config_file["jenkins_master"]["resources"]["memory"]
      v.cpus = config_file["jenkins_master"]["resources"]["cpus"]
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = config_file["ansible"]["playbook_path"]
    ansible.inventory_path = config_file["ansible"]["inventory_path"]
  end
end
