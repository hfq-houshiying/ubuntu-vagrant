# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = 'ubuntu/trusty64'
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
  end


  config.vm.provision "shell", inline: <<-SHELL
    if ! [ -f /opt/reg_ssh_pub ];then  
      echo "#{ENV['SSH_PUB']}" >>  /home/vagrant/.ssh/authorized_keys
      echo "done." >  /opt/reg_ssh_pub
    fi

    sed -i 's@archive.ubuntu.com@mirrors.aliyun.com@g' /etc/apt/sources.list

    apt-get update
  
    apt-get install pv git tmux htop iotop fabric gettext subversion expect realpath build-essential apache2-utils mysql-client-core-5.6 mysql-client-5.6 build-essential libpango1.0-0 libcairo2 libssl-dev libffi-dev libevent-dev libjpeg-dev libmemcached-dev libmysqlclient-dev libpng12-dev libpq-dev libxml2-dev libxslt1-dev libfreetype6-dev libssl-dev libffi-dev zlib1g-dev unixodbc-dev python-dev python-pip python-git python-imaging python-redis python-virtualenv

    pip install uwsgi supervisor newrelic
  SHELL


  config.vm.provision "shell", inline: <<-SHELL
    echo "deploy done"
  SHELL
end
