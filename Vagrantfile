# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  $num_instances = 3
  $os = "ubuntu"
  $osver = "jammy64"
  config.dns.tld = "vagrant.test"

  (1..$num_instances).each do |i|
    config.vm.define vm_name = "#{$os}-#{$osver}-#{i}" do |config|
      config.vm.hostname = vm_name
      config.vm.box = "#{$os}/#{$osver}"
      config.vm.provision "shell" do |s|
        ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
        s.inline = <<-SHELL
        echo #{ssh_pub_key} >> /home/ubuntu/.ssh/authorized_keys;
        apt update -y;
        apt upgrade -y;
        apt install -y python3 ca-certificates;
        SHELL
      end
    end
  end
end
