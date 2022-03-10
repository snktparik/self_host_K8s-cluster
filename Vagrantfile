# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # Kubernetes Master Server
  config.vm.define "kmaster" do |kmaster|
    kmaster.vm.box = "generic/centos8"
    kmaster.vm.hostname = "kmaster.home.lab"
    kmaster.vm.network "private_network", ip: "172.168.1.10"
    kmaster.vm.provider "vmware_desktop" do |v|
      v.vmx["displayName"] = "kmaster"
      v.vmx["memsize"] = 2048
      v.vmx["numvcpus"] = 2
    end
  end

  NodeCount = 3

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "kworker#{i}" do |workernode|
      workernode.vm.box = "generic/centos8"
      workernode.vm.hostname = "kworker#{i}.home.lab"
      workernode.vm.network "private_network", ip: "172.168.1.1#{i}"
      workernode.vm.provider "vmware_desktop" do |v|
        v.vmx["displayName"] = "kworker#{i}"
        v.vmx["memsize"] = 1024
        v.vmx["numvcpus"] = 2
      end
    end
  end

end