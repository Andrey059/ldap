# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :server => {
        :box_name => "centos/7",
        :ip_addr => '192.168.11.150'
  },
  :client => {
        :box_name => "centos/7",
        :ip_addr => '192.168.11.151'
  },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      config.vm.define boxname do |box|

          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s

          box.vm.network "private_network", ip: boxconfig[:ip_addr]

          box.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "512"]
          end

          config.vm.provision "ansible" do |ansible|
	      ansible.verbose = "vvv"
	      ansible.playbook = "Playbook.yml"
	      ansible.become = "true"
	  end

      end
  end
end
