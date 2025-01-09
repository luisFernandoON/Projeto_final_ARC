# Instalar o Servidor NFS(Need for spee... Network File System)


Vamos realizar a Instalação do NFS, utilize o seguinte comando:

    sudo apt update
    sudo apt install nfs-kernel-server

Crie um diretorio para compartilhar:
    
    sudo mkdir -p /nfs/share

Ajuste as Permições dessa pasta com os proximos comandos:

    sudo chown nobody:nogroup /nfs/share
    sudo chmod 777 /nfs/share

Agora é a hora de configurar o arquivo de exportação, segue os passos.

    utulize esse comando para abrir o arquivo de configuração:

    sudo nano /etc/exports

    e adicione o seguinte comando: 
    
    /nfs/share 192.168.1.0/24(rw,sync,no_subtree_check)

Agora você atualiza as configurações do NFS com o proximo comando:

    sudo exportfs -a

Reinicie o serviço com o comando: 

    sudo systemctl start nfs-kernel-server


Agora vamos configurar o cliente.

    instalação:

    sudo apt update
    sudo apt install nfs-common -y

    cria a pasta de compartilhamento:

    sudo mkdir -p /mnt/nfs_share

    monte o diretorio:

    sudo mount 192.168.1.100:/nfs/share /mnt/nfs_share

    verifique se o compartilhamento esta montado com o comando: 

    df -h

    agora é a hora do teste. No servidor, crie arquivos na pasta criada lá no inicio "/nfs/share", e verifica no cliente, acessando "/mnt/nfs_share" para confirmar se os arquivos estarão lá.