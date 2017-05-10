$script = <<SCRIPT
	echo "yum install wget"
	echo "y
	" | yum install wget
	echo "chkconfig ntpd on"
	chkconfig ntpd on
	echo "service ntpd start"
	service ntpd start
	echo "ssh-keygen"
	ssh-keygen
	echo "cd /root/.ssh"
	cd /root/.ssh
	echo "cp id_rsa /vagrant/"
	cp id_rsa /vagrant/
	echo "cat id_rsa.pub >> authorized_keys"
	cat id_rsa.pub >> authorized_keys
	echo "cd /home/vagrant"
	cd /home/vagrant
	echo "wget http://public-repo-1.hortonworks.com/ambari/centos6/1.x/updates/1.4.3.38/ambari.repo"
	wget http://public-repo-1.hortonworks.com/ambari/centos6/1.x/updates/1.4.3.38/ambari.repo
	echo "cp ambari.repo /etc/yum.repos.d"
	cp ambari.repo /etc/yum.repos.d
	echo "yum repolist"
	yum repolist
	echo "yum install ambari-server"
	echo "y
	" | yum --nogpg install -y ambari-server
	echo "ambari-server setup"
	echo "y\nn\ny\n" | ambari-server setup
	echo "ambari-server start"
	ambari-server start
	echo "FINISHED"
SCRIPT
  
Vagrant.configure("2") do |config|

  config.vm.synced_folder ".", "/vagrant", type: "nfs"
  config.vm.box = "centos/6"
  config.vm.box_check_update = false
  
  #config.vm.hostname = "dataforward" --> Bug in Centos/7 prevents hostname configuration...
  
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provider "virtualbox" do |vb|
     vb.gui = false
     vb.memory = "8196"
   end
  
  config.vm.provision "shell", inline: $script

end
