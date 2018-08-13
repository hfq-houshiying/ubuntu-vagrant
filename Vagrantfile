# -*- mode: ruby -*-
# vi: set ft=ruby :

N = 2

Vagrant.configure("2") do |config|
  config.env.enable
  config.vm.box = ENV['OS']
  config.vm.box_check_update = false
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true


  if  N == 1 
    config.vm.hostname = 'ubuntu'
    config.vm.network "private_network", ip: "10.0.8.100"
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = "1"
    end
  else
    (1..N).each do |i|
      config.vm.define "ubuntu-node-#{i}" do |node|
        node.vm.hostname = "ubuntu-node-#{i}"
        node.vm.network "private_network", ip: "10.0.8.10#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "2048"
          vb.cpus = "1"
        end
      end
    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    #insert ssh public key to vagrant user.
    if ! [ -f /opt/reg_ssh_pub ];then  
      echo "#{ENV['SSH_PUB']}" >>  /home/vagrant/.ssh/authorized_keys
      echo "done." >  /opt/reg_ssh_pub
    fi

    #replace apt sources to aliyun
    sed -i 's@archive.ubuntu.com@mirrors.aliyun.com@g' /etc/apt/sources.list

    #upgrade apt
    apt-get update
    
    #install required soft
    apt-get install -y pv git tmux htop iotop fabric gettext subversion expect realpath build-essential apache2-utils mysql-client-core-5.6 mysql-client-5.6 build-essential libpango1.0-0 libcairo2 libssl-dev libffi-dev libevent-dev libjpeg-dev libmemcached-dev libmysqlclient-dev libpng12-dev libpq-dev libxml2-dev libxslt1-dev libfreetype6-dev libssl-dev libffi-dev zlib1g-dev unixodbc-dev python-dev python-pip python-git python-imaging python-redis python-virtualenv
    
    #upgrade pip setuptools
    sudo pip install --upgrade pip setuptools

    #install ansible
    pip install ansible

    #install docker
    curl -sSL get.docker.com | bash
    sudo usermod -aG docker `whoami` 

    #install required soft for pip
    pip install uwsgi supervisor newrelic

    #update kernel to 4.4
    sudo apt-get install -y linux-generic-lts-xenial
    
    #reboot system
    reboot
  SHELL


  config.vm.provision "shell", inline: <<-SHELL
    echo "deploy done"
  SHELL
end
