# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # set to false, if you do NOT want to check the correct VirtualBox Guest Additions version when booting this box
  if defined?(VagrantVbguest::Middleware)
    config.vbguest.auto_update = true
  end

  config.vm.box = "puppetlabs/ubuntu-14.04-64-puppet"
  config.vm.box_version = "1.0.1"
  
  # Port Forwarding
  # --------------------
  
  # ELK
  config.vm.network :forwarded_port, guest: 5601, host: 5601
  config.vm.network :forwarded_port, guest: 9200, host: 9200
  config.vm.network :forwarded_port, guest: 9300, host: 9300
  
  #config.vm.network :forwarded_port, guest: 8000, host: 8000
  #config.vm.network :forwarded_port, guest: 8080, host: 8080
  #config.vm.network :forwarded_port, guest: 8011, host: 8011

  #Mongod
  #config.vm.network "forwarded_port", guest: 27017, host: 27017


  # Local folder sync
  config.vm.synced_folder "/Users/rbrennan/beachbody/codebase/OrderExplorer", "/var/www/orderexplorer",
    create: true,
    group: "vagrant",
    owner: "www-data",
    mount_options: ["dmode=775,fmode=664"]

  config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--cpus", "2", "--memory", "2048"]
  end

  config.vm.provider "vmware_fusion" do |v, override|
     ## the puppetlabs ubuntu 14-04 image might work on vmware, not tested? 
    v.provision "shell", path: 'ubuntu.sh'
    v.box = "phusion/ubuntu-14.04-amd64"
    v.vmx["numvcpus"] = "2"
    v.vmx["memsize"] = "2048"
  end
  config.vm.provision "shell", path: 'setup.sh'
  config.vm.provision "puppet",  manifest_file: "default.pp"
end