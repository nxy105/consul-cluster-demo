# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.box = "trusty64"

  # configure consul1
  config.vm.define "consul1" do |consul1|
      $script = <<SCRIPT
apt-get install daemon
echo "Installing Consul"
cp /vagrant/bin/consul /usr/local/bin/
daemon -X "consul agent -server -bootstrap -data-dir /tmp/consul -node=consul1 -bind 172.0.0.10"
SCRIPT

      consul1.vm.provision "shell", inline: $script
      consul1.vm.hostname = "consul1"
      consul1.vm.network "private_network", ip: "172.0.0.10"
  end

  # configure consul2
  config.vm.define "consul2" do |consul2|
      $script = <<SCRIPT
apt-get install daemon
echo "Installing Consul"
cp /vagrant/bin/consul /usr/local/bin/
daemon -X "consul agent -server -data-dir /tmp/consul -node=consul2 -bind 172.0.0.11 -join 172.0.0.10"
SCRIPT

      consul2.vm.provision "shell", inline: $script
      consul2.vm.hostname = "consul2"
      consul2.vm.network "private_network", ip: "172.0.0.11"
  end

  # configure status
  config.vm.define "status" do |status|
      $script = <<SCRIPT
apt-get install daemon
echo "Installing and Configuring Consul Status UI"
cp /vagrant/bin/consul /usr/local/bin/
daemon -X "consul agent -client=172.0.0.12 -ui-dir /vagrant/web/ -data-dir /tmp/consul -node=status -bind 172.0.0.12 -join 172.0.0.10"
SCRIPT

      status.vm.provision "shell", inline: $script
      status.vm.hostname = "status"
      status.vm.network "private_network", ip: "172.0.0.12"
  end

  # configure service1
  config.vm.define "service1" do |service1|
      $script = <<SCRIPT
apt-get install daemon

echo "Installing and Configuring Consul"
cp /vagrant/bin/consul /usr/local/bin/
mkdir /etc/consul.d/
cp /vagrant/config/service1.json /etc/consul.d/mysvc.json
daemon -X "consul agent -data-dir /tmp/consul -node=service1 -config-dir /etc/consul.d -bind 172.0.0.13 -join 172.0.0.10"

echo "Installing and Configuring Demo Service"
cp /vagrant/bin/demo /usr/local/bin/
daemon -X "demo -addr=:8045"

SCRIPT
      service1.vm.provision "shell", inline: $script
      service1.vm.hostname = "service1"
      service1.vm.network "private_network", ip: "172.0.0.13"
  end

  # configure service2
  config.vm.define "service2" do |service2|
      $script = <<SCRIPT
apt-get install daemon

echo "Installing and Configuring Consul"
cp /vagrant/bin/consul /usr/local/bin/
mkdir /etc/consul.d/
cp /vagrant/config/service2.json /etc/consul.d/mysvc.json
daemon -X "consul agent -data-dir /tmp/consul -node=service2 -config-dir /etc/consul.d -bind 172.0.0.14 -join 172.0.0.10"

echo "Installing and Configuring Demo Service"
cp /vagrant/bin/demo /usr/local/bin/
daemon -X "demo -addr=:8076"

SCRIPT
      service2.vm.provision "shell", inline: $script
      service2.vm.hostname = "service2"
      service2.vm.network "private_network", ip: "172.0.0.14"
  end

  # configure demo
  config.vm.define "demo" do |demo|
      $script = <<SCRIPT
apt-get install daemon

echo "Installing and Configuring Consul"
cp /vagrant/bin/consul /usr/local/bin/
mkdir /etc/consul.d/
cp /vagrant/config/demo.demo.json /etc/consul.d/demo.json
daemon -X "consul agent -data-dir /tmp/consul -node=demo -config-dir /etc/consul.d -bind 172.0.0.15 -join 172.0.0.10"

echo "Installing and Configuring Demo App"
cp /vagrant/bin/demo /usr/local/bin/
daemon -X "demo -addr=:80"

SCRIPT
      demo.vm.provision "shell", inline: $script
      demo.vm.hostname = "demo"
      demo.vm.network "private_network", ip: "172.0.0.15"
  end

  # limit memory
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "256"]
  end

end
