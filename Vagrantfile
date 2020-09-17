# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|
  
  config.vm.define "dockerserver" do |dockerserver|
    dockerserver.vm.box = "centos/7"
    dockerserver.vm.hostname = "dockerserver.eduami.org"
    dockerserver.vm.network "private_network", ip: "192.168.50.24"
    dockerserver.vm.network "forwarded_port", guest: 8080, host: 8080
    dockerserver.vm.network "forwarded_port", guest: 8761, host: 8761
    dockerserver.vm.network "forwarded_port", guest: 5672, host: 5672
    dockerserver.vm.network "forwarded_port", guest: 15672, host: 15672
    dockerserver.vm.provision "shell", path: "startup-dockerserver.sh"
    dockerserver.vm.synced_folder ".", "/vagrant", type: "rsync",
        rsync__exclude: ".git/"
    dockerserver.vm.provider "virtualbox" do |vb|
      vb.name = "dockerserver"
      vb.memory = 4024
      vb.cpus = 4
    end
  end
end
