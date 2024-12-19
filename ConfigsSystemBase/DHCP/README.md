-Instalar o Servidor DHCP

Primeiro, atualize os pacotes do sistema:

    sudo apt-get update

Em seguida, instale o serviço DHCP:

    sudo apt-get install isc-dhcp-server

Após a instalação, edite o arquivo de configuração padrão do servidor DHCP:]

    sudo nano /etc/dhcp/dhcpd.conf

-Reiniciar o Serviço DHCP

Para aplicar as novas configurações, reinicie o serviço DHCP:

    sudo service isc-dhcp-server restart

Verifique se o serviço foi reiniciado corretamente, checando o status:

    sudo service isc-dhcp-server status
  
Configuração do dhcpd.conf:

    ddns-update-style none;

    subnet 192.168.100.0 netmask 255.255.255.0 {
    range 192.168.100.10 192.168.100.110;
    option subnet-mask 255.255.255.0;
    option domain-name "ItaloLuis.com";
    option domain-name-servers 8.8.8.8, 8.8.4.4;
    option routers 192.168.100.1;
    default-lease-time 600;
    max-lease-time 7200;
}


