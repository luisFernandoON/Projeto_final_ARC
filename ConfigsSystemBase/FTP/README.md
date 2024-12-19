# Instalar o Servidor FTP

Primeiro, atualize os pacotes do sistema:
    
    sudo apt-get update

Instale o servidor ProFTPD:

    sudo apt install proftpd -y

Verifique o status do serviço:

    sudo service proftpd status

- Configurar o ProFTPD:

Digite o seguinte código para editar o arquivo que contém a configuração:

    sudo nano /etc/proftpd/proftpd.conf

Ative e ajuste as opções a seguir (descomente as linhas necessárias):

ServerName "Servidor FTP"
DefaultRoot ~
RequireValidShell off
