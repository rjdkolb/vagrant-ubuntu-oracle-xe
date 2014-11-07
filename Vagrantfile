# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/precise64"
  config.vm.box_check_update = false

  config.vm.host_name = "oracle"

  config.vm.network :hostonly, "192.168.33.10"

  # Port forward Oracle TNSlistener
  config.vm.network "forwarded_port", guest: 1521, host: 1521

  config.vm.provider "virtualbox" do |vb|
    # Enable DNS behind NAT
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # VM name and available memory
    vb.customize ["modifyvm", :id, "--name", "oracle", "--memory", "3048"]
  end

  config.vm.provision "puppet" do |puppet|
    puppet.module_path = "modules"
    puppet.manifests_path = "manifests"
    puppet.manifest_file  = "base.pp"
    #puppet.options = "--verbose --trace"
  end

end

# EOF
