
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.network "private_network", ip: "192.168.56.101"
  config.vm.hostname = "projeto-final-ARC"  # Define o nome da máquina virtual

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"    # Define 4 GB de RAM
    vb.cpus = 2           # Define 2 CPUs
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y apache2 bind9 isc-dhcp-server nfs-kernel-server vsftpd
  SHELL
end