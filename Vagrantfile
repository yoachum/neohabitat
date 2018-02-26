# -*- mode: ruby -*-
# vi: set ft=ruby :

# If we're running on Windows, ensures that VBOX_INSTALL_PATH is appropriately set.
if Gem.win_platform?
  ENV["VBOX_INSTALL_PATH"] = "C:\\Program Files\\Oracle\\VirtualBox\\"
end

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.box_check_update = false

  config.vm.network "private_network", ip: "192.168.86.19"
  config.vm.network "forwarded_port", guest: 1337, host: 1337, host_ip: "0.0.0.0"
  config.vm.network "forwarded_port", guest: 1986, host: 1986, host_ip: "0.0.0.0"
  config.vm.network "forwarded_port", guest: 3307, host: 3307, host_ip: "0.0.0.0"
  config.vm.network "forwarded_port", guest: 5190, host: 5190, host_ip: "0.0.0.0"
  config.vm.network "forwarded_port", guest: 9001, host: 9001, host_ip: "0.0.0.0"
  config.vm.network "forwarded_port", guest: 27018, host: 27018, host_ip: "0.0.0.0"
  config.vm.network "forwarded_port", guest: 80, host: 8080, id: "nginx"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end

  # Explicitly enforces syncing of the local folder to /vagrant on the VM.
  config.vm.synced_folder ".", "/neohabitat"

  if Gem.win_platform?
    config.vm.provision :shell, binary: true, path: "./vagrant/build.sh"
  else
    config.vm.provision :shell, path: "./vagrant/build.sh"
  end
end
