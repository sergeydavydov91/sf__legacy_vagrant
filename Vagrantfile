ENV['VAGRANT_SERVER_URL'] = 'http://vagrant.elab.pro'
# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
echo I am provisioning...
date > /etc/vagrant_provisioned_at
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: $script
    config.vm.network "forwarded_port", guest: 5432, host: 15432
end

Vagrant::Config.run do |config|
  config.vm.box = "debian/bullseye64"
  config.vm.host_name = "postgresql" 

  config.vm.share_folder "bootstrap", "/mnt/bootstrap", ".", :create => true
  config.vm.provision :shell, :path => "Vagrant-setup/bootstrap.sh"
  
  # PostgreSQL Server port forwarding

  #config.vm.forward_port 5432, 15432
end