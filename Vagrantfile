Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.boot_timeout = 600
  config.vm.network "public_network", type: "dhcp"
  config.vm.synced_folder "./ConfigsSystemBase", "/vagrant_config" #liga a pasta do sistema base com a pasta na maquina virtual

  config.vm.provision "shell", inline: <<-SHELL
    
    sudo apt-get update
    #Instala o apache, bind9, isc-dhcp-server, nfs-kernel-server, vsftpd e samba
    sudo apt-get install -y apache2 bind9 isc-dhcp-server nfs-kernel-server proftpd samba smbclient

  #Configurando ================DHCP================

    #Renomeia o arquivo .conf para .conf.bkp
    sudo mv /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.bkp
    #Renomeia o arquivo isc-dhcp-server, adicionando .bkp
    sudo mv /etc/default/isc-dhcp-server /etc/default/isc-dhcp-server.bkp

    #Para evitar a fadiga, esse comando pega a configuração(dhcp.conf) pre-feita e joga na pasta /etc/dhcp
    sudo cp /vagrant_config/DHCP/dhcpd.conf /etc/dhcp/dhcpd.conf
    #Mesma coisa do comando acima, mas na pasta /etc/default
    sudo cp /vagrant_config/DHCP/isc-dhcp-server /etc/default/isc-dhcp-server

    
    sudo systemctl restart isc-dhcp-server

  #Configurando ================DNS================

    sudo mv /etc/bind/named.conf.options /etc/bind/named.conf.options.bkp 
    sudo cp /vagrant_config/DNS/named.conf.options /etc/bind/named.conf.options

    sudo mv /etc/bind/named.conf.local /etc/bind/named.conf.local.bkp
    sudo cp /vagrant_config/DNS/named.conf.local /etc/bind/named.conf.local

  
    sudo systemctl restart bind9


  #Configurando ================FTP================

    sudo mv /etc/proftpd/proftpd.conf /etc/proftpd/proftpd.conf.bkp 
    sudo cp /vagrant_config/FTP/proftpd.conf /etc/proftpd/proftpd.conf

    # Cria o diretório de transferências para o FTP
    sudo mkdir -p /transferencias
    sudo useradd webmaster -d /transferencias -s /bin/false # Cria usuário sem shell de login
    sudo chown webmaster -R /transferencias # Define permissões do diretório
    sudo chmod -R 755 /transferencias

    sudo systemctl restart proftpd

  #Configurando ================NFS================

    sudo mv /etc/exports /etc/exports.bkp
    sudo mv /etc/default/nfs-common /etc/default/nfs-common.bkp

    sudo cp /vagrant_config/NFS/exports /etc/exports
    sudo cp /vagrant_config/NFS/nfs-common /etc/default/nfs-common
    sudo mkdir -p /nfs_shared 
    echo "/nfs_shared *(rw,sync,no_root_squash)" | sudo tee -a /etc/exports 
    sudo chmod 777 /nfs_shared
    sudo systemctl restart nfs-kernel-server

  #Configurando ================APACHE================

    sudo mkdir -p /var/www/html/site 
    echo "<h1>Servidor Apache funcionando!</h1>" | sudo tee /var/www/html/site/index.html

    
    sudo cp /vagrant_config/apache_site.conf /etc/apache2/sites-available/site.conf
    sudo a2ensite site.conf
    sudo systemctl reload apache2 

  #Configurando ================SAMBA================

    sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.bkp 
    sudo cp /vagrant_config/SAMBA/smb.conf /etc/samba/smb.conf

    # Cria o diretório compartilhado e define permissões
    sudo mkdir -p /samba_shared
    sudo chown nobody:nogroup /samba_shared
    sudo chmod 777 /samba_shared

    # Reinicia o serviço Samba para aplicar as configurações
    sudo systemctl restart smbd

    sudo systemctl enable isc-dhcp-server
    sudo systemctl enable bind9
    sudo systemctl enable apache2
    sudo systemctl enable smbd
    sudo systemctl enable proftpd
    sudo systemctl enable nfs-kernel-server


  SHELL
end
