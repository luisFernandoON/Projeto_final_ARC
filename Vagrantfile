Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.network "public_network", type: "dhcp"
  config.vm.synced_folder "./ConfigsSystemBase", "/vagrant_config"
  

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y apache2 bind9 isc-dhcp-server nfs-kernel-server vsftpd
  SHELL
end