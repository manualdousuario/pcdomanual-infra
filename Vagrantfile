# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-SCRIPT
adduser --disabled-password --gecos "" pcdomanual
adduser pcdomanual sudo
echo 'pcdomanual ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/pcdomanual
mkdir /home/pcdomanual/.ssh
cp /home/vagrant/.ssh/authorized_keys /home/pcdomanual/.ssh/authorized_keys
chown -R pcdomanual:pcdomanual /home/pcdomanual/.ssh
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.network "private_network", ip: "192.168.56.10"
  config.vm.provision "shell", inline: $script
end
