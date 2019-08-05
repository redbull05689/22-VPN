# -*- mode: ruby -*-
# vim: set ft=ruby :
home = ENV['HOME']

MACHINES = {
  :ovs => {
        :box_name => "centos/7",
        
        
  },
  :ovc => {
        :box_name => "centos/7",
        
        
  },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      config.vm.define boxname do |box|

          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s
          # box.vm.network "forwarded_port", guest: 8080, host: 8080
          # box.vm.network "forwarded_port", guest: 8443, host: 8443
          # box.vm.network "forwarded_port", guest: 8022, host: 8022

          #box.vm.network "forwarded_port", guest: 3260, host: 3260+offset

          box.vm.network "public_network", use_dhcp_assigned_default_route: true

          box.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", "1024"]
        #   vb.customize ["storagectl", :id, "--name", "SATA", "--add", "sata" ]
          vb.name = boxname.to_s

        #   boxconfig[:disks].each do |dname, dconf|
        #       unless File.exist?(dconf[:dfile])
        #         vb.customize ['createhd', '--filename', dconf[:dfile], '--variant', 'Fixed', '--size', dconf[:size]]
        #       end
        #       vb.customize ['storageattach', :id,  '--storagectl', 'SATA', '--port', dconf[:port], '--device', 0, '--type', 'hdd', '--medium', dconf[:dfile]]
        # end
          end
     

      case boxname.to_s
      when "ovs"
        box.vm.provision "shell", run: "always", inline: <<-SHELL
         
          mkdir ~/ovslab
          SHELL
          config.vm.provision "shell", path: "./provision.sh"
        when "ovc"
          box.vm.provision "shell", run: "always", inline: <<-SHELL
           
            mkdir ~/ovclab
            SHELL
      end

      end
   end
end

