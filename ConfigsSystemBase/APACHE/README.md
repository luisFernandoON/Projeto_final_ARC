# Instalar o Servidor Apache

Primeiramente instale o Apache:

    sudo apt install apache2 -y
    
Verifique se o serviço do Apache está em funcionamento:

    sudo service apache2 status

- Configurar o Firewall:

Permita conexões HTTP e HTTPS no firewall:

    sudo ufw allow 80
    sudo ufw allow 443

Após ajustar as permissões, recarregue o firewall:

    sudo ufw reload

