# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  def send_key(s)
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      mkdir -p /root/.ssh/
      touch /root/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "db" do |db|
    db.vm.hostname = "db.test"
    db.vm.network :private_network, ip: "192.168.1.2"
    db.vm.provision "shell" do |s|
      send_key(s)
    end
  end
  config.vm.define "redis" do |redis|
    redis.vm.hostname = "redis.test"
    redis.vm.network :private_network, ip: "192.168.1.3"
    redis.vm.provision "shell" do |s|
      send_key(s)
    end
  end
  config.vm.define "app" do |app|
    app.vm.hostname = "app.test"
    app.vm.network :private_network, ip: "192.168.1.4"
    app.vm.provision "shell" do |s|
      send_key(s)
    end
  end
end
