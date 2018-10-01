# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX="centos/7"
NODES=1


# common initial script
$common_pg_init = <<SCRIPT
rpm -Uvh https://yum.postgresql.org/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm
yum install postgresql10-server postgresql10 postgresql10-contrib postgresql10-devel
yum install vim tmux
#chkconfig postgresql-9.6 on
yum install -y install avahi
sudo service avahi-daemon start
chkconfig avahi-daemon on
SCRIPT

Vagrant.configure("2") do |config|
	(1..NODES).each do |i|
		config.vm.define "node#{i}" do |subconfig|
			subconfig.vm.box = BOX
			subconfig.vm.hostname = "node#{i}"
			subconfig.vm.network "private_network", ip: "10.10.0.#{i+10}", virtualbox__intnet: true
			subconfig.vm.provision "shell", inline: $common_pg_init
		end
	end 	
end
