Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.boot_timeout = 600
  config.vm.network "public_network", type: "dhcp"
  config.vm.synced_folder "./ConfigsSystemBase", "/vagrant_config" #liga a pasta do sistema base com a pasta na maquina virtual
  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"  #Define a quantidade de memoria que a VM usara
    vb.cpus = 2         #Define a quantidade de nucleos que a VM usara
  end

  config.vm.provision "shell", inline: <<-SHELL
    
    sudo apt-get update
    #Instala o apache, bind9, isc-dhcp-server, nfs-kernel-server e vsftpd
    sudo apt-get install -y apache2 bind9 isc-dhcp-server nfs-kernel-server vsftpd

    #Renomeia o arquivo .conf para .conf.bkp
    sudo mv /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.bkp
    #Renomeia o arquivo isc-dhcp-server, adicionando .bkp
    sudo mv /etc/default/isc-dhcp-server /etc/default/isc-dhcp-server.bkp

    #Para evitar a fadiga, esse comando pega a configuração(dhcp.conf) pre-feita e joga na pasta /etc/dhcp
    sudo cp /vagrant_config/dhcpd.conf /etc/dhcp/dhcpd.conf
    #Mesma coisa do comando acima, mas na pasta /etc/default
    sudo cp /vagrant_config/isc-dhcp-server /etc/default/isc-dhcp-server

    #Reinicia o servidor DHCP para aplicar as novas configurações
    sudo systemctl restart isc-dhcp-server

  SHELL
end
