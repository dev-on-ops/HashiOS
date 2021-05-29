#######################################################################
#Example vm creation with static description blocks
Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
    config.vm.define "hashiserver01" do |bootserver01|
      bootserver01.vm.box = "hashicorp/bionic64"
      bootserver01.vm.hostname = "hashiserver01"
      bootserver01.vm.network "private_network", ip: "192.168.255.101"
      bootserver01.vm.network :forwarded_port, guest: 5240, host: 5240
      bootserver01.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--cpus", 2]
        v.customize ["modifyvm", :id, "--memory", "4096"]
        v.customize ["modifyvm", :id, "--name", "hahsiserver01"]
      end
    end
    config.vm.define "hashiclient01" do |bootclient01|
      bootclient01.vm.box = "hashicorp/bionic64"
      bootclient01.vm.hostname = "bootclient01"
      bootclient01.vm.network "private_network", ip: "192.168.255.102"
      bootclient01.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--cpus", 2]
        v.customize ["modifyvm", :id, "--memory", "4096"]
        v.customize ["modifyvm", :id, "--name", "hashiclient01"]
      end
    end
  end
  ##############################################################################
  