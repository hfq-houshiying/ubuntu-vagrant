# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = 'ubuntu/xenial64'
  config.env.enable
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  config.vm.box_check_update = false
  config.vm.hostname = 'ubuntu'
  config.vm.network "private_network", ip: "10.0.8.100"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = "2"
    #bugfix https://github.com/joelhandwell/ubuntu_vagrant_boxes/issues/1
    vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
  end


  config.vm.provision "shell", inline: <<-SHELL
    
    if ! [ -f /opt/reg_ssh_pub ];then  
      echo "#{ENV['SSH_PUB']}" >>  /home/vagrant/.ssh/authorized_keys
      echo "done." >  /opt/reg_ssh_pub
    fi
    
    sed -i 's@archive.ubuntu.com@mirrors.aliyun.com@g' /etc/apt/sources.list
    
    apt-get update
    
  SHELL


  config.vm.provision "shell", inline: <<-SHELL
    echo "deploy done"
  SHELL
end
