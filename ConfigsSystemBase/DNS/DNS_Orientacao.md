# Instalar o Servidor DNS

Primeiro, atualize os pacotes do sistema:

    sudo apt-get update

Em seguida, instale o serviço DNS:

    sudo apt-get install bind9

Após a instalação, edite o arquivo de configuração padrão para criar uma zona

    comando para acessar o arquivo:

    sudo nano /etc/dhcp/dhcpd.conf

    Contieudo exemplo para editar dentro do arquivo:

    zone "ItaloLuis.com" {
    type master;
    file "/etc/bind/db.ItaloLuis.com";
    };


Agora vamos criar o arquivo com os registros DNS:

    Acesse o arquivo usando:

    sudo nano /etc/bind/db.ItaloLuis.com 

    logo em seguida preencha com uma estrutura como essa abaixo:

    $TTL 86400
    @    IN    SOA   ns1.ItaloLuis.com. admin.ItaloLuis.com. (
                2025010901 ; Serial
                3600       ; Refresh
                1800       ; Retry
                1209600    ; Expire
                86400 )    ; Minimum TTL
    @    IN    NS    ns1.ItaloLuis.com.
    @    IN    NS    ns2.ItaloLuis.com.
    @    IN    A     192.168.1.1
    ns1  IN    A     192.168.1.2
    ns2  IN    A     192.168.1.3


Após finalizar essa configuração, vamos reiniciar o serviço para aplicar as novas alterações.

    vamos usar os seguintes comandos:

    caso não tinha iniciado o seu serviço DNS utilize esse comando:
    sudo systemctl start bind9
    sudo systemctl enable bind9

    Caso já estiver sendo execultando, utulize esse comando:

    sudo systemctl restart bind9

    E para testar utilize o seguinte comando:

    dig @localhost exemplo.com
 