# -*- mode: ruby -*-
# vi: set ft=ruby :

$script_centos = <<SCRIPT
  sed -i 's/SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config
  setenforce 0
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.define "centos7_box" do |centos7_box|
    centos7_box.vm.box = "centos/7"
    centos7_box.vm.host_name = "centos7-vm"
    centos7_box.vm.network "public_network", ip: "192.168.1.111"
    centos7_box.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end
    centos7_box.vm.provision "shell", inline: $script_centos
  end
end