# -*- mode: ruby -*-
# vi: set ft=ruby :

# Sample vagrantfile to create 2 hosts, Centos based and test keepalived is really intalled.
# VM's start with 2 interface. The usual NAT interface (eth0) for management and a "private network"
# so the two VM can "see" each other.

# You just have to change the "keepalived_shared_ip" depending on which IP network you have
# configured in your private network

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "rafacas/centos64-i386-plain"
  config.vm.network "private_network", type: "dhcp"



  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    config.vm.provision "ansible" do |ansible|
       ansible.playbook = "playbook.yml"
       ansible.extra_vars ={ keepalived_role: "master",
                             keepalived_shared_iface: "eth1",
                             keepalived_shared_ip: "172.28.128.100"  }
    end
    
  end

  config.vm.define "slave" do |slave|
    slave.vm.hostname = "slave"
    config.vm.provision "ansible" do |ansible|
       ansible.playbook = "playbook.yml"
       ansible.extra_vars ={keepalived_role: "slave",
                             keepalived_shared_iface: "eth1",
                             keepalived_shared_ip: "172.28.128.100"  }

    end
    
  end

  

end
