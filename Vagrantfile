# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true

  config.vm.box_check_update = true
  config.vm.network :private_network, type: "dhcp"
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define :proxy do |proxy|
    proxy.vm.hostname = "proxy.haproxy.test"

    proxy.vm.provider :libvirt do |libvirt|
      libvirt.nested = true
      libvirt.cpu_mode = "host-model"
      libvirt.cpus = 1
      libvirt.memory = 4096
    end

    proxy.vm.synced_folder "certs", "/certs", type: "rsync"
    proxy.vm.synced_folder "proxy", "/vagrant", type: "rsync"
  end

  config.vm.define :server do |server|
    server.vm.hostname = "server.haproxy.test"

    server.vm.provider :libvirt do |libvirt|
      libvirt.nested = true
      libvirt.cpu_mode = "host-model"
      libvirt.cpus = 1
      libvirt.memory = 4096
    end

    server.vm.synced_folder "server", "/vagrant", type: "rsync"
  end

end
