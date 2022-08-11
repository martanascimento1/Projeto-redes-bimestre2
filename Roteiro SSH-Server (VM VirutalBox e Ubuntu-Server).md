# Roteiro SSH-Server (VM VirutalBox e Ubuntu-Server)

## Objetivo:
    * Configurar o acesso remoto via ssh nos servidores VM-LAB01 e VM-LAB02 dos PCs 1 e dois utilizados nas práticas anteriores.
    * Protocolo SSH, SCP, SFTP 
    * Porta 22
### Login nas VMs

* Usuário da VM: ``administrador``
* Senha da VM: ``adminifal``


```
Tabela 1: Definições de endereços IPs da Rede e Nomes de Hosts
Tabela 1: Definições de endereços IPs das redes:
--------------------------------------
|     DESCRICAO     |       IP       |   hostname
--------------------------------------
| rede              | 192.168.24.0   |  
| máscara           | 255.255.255.0  | 
| Gateway           | 192.168.24.14  |  
| VM1-PC1-izabel    | 192.168.24.1   |  grupo1-vm1-pc1
| VM2-PC1-izabel    | 192.168.24.2   |  grupo1-vm2-pc1
| VM1-PC2-marta     | 192.168.24.3   |  grupo1-vm1-pc2
| VM2-PC2-marta     | 192.168.24.4   |  grupo1-vm2-pc2
| VM1-PC3-debora    | 192.168.24.5   |  grupo1-vm1-pc3
| VM2-PC3-debora    | 192.168.24.6   |  grupo1-vm2-pc3
| VM1-PC4-julia     | 192.168.24.7   |  grupo1-vm1-pc4
| VM2-PC4-julia     | 192.168.24.8   |  grupo1-vm2-pc4
--------------------------------------

### Atribuir nomes aos servidores ``hostname``

* formato: ``sudo hostnamectl set-hostname <hostname>``

* NA VM1-PC1 executar:
```shell
sudo hostnamectl set-hostname srv-vm1-pc1
```
![WhatsApp Image 2022-08-09 at 16 27 05](https://user-images.githubusercontent.com/103062784/184226890-e578f926-69a9-452c-88dc-7ba97191a5b3.jpeg)

* Fazer o mesmo nas outras VMs, seguindo as definições de nomes da tabela.


## Instalando o servidor SSH

### Antes de Começar:
   1. acessar as configurações de cada VM e altere novamente o Adaptador1 para **NAT**
   ![Uploading WhatsApp Image 2022-08-09 at 16.27.05 (1).jpeg…]()

   3. Comente as linhas de endereço IP estático e ative o DHCP nas configurações do Netplan
   
### Ceritifique-se que a VM está acessando a internet:

```shell
sudo apt update       # atualiza as definições e versões de pacotes/bibliotecas dos repositórios do ubuntu
sudo apt upgrade -y   # atualiza os pacotes com as novas definições e versões 
```

### Instale o SSH Server

```shell
systemctl status ssh
sudo apt-get install openssh-server
systemctl status ssh
```

### Verifique o status das portas do sistema
```
netstat -an | grep LISTEN.  #verifique as conexões TCP na porta 22 se está como LINSTENING
```

### Firewall 
* Para garantir o funcioamento correto do controle de acesso devemos configurar o firewall para permitir conexões remota via protocolo SSH, na porta 22.
 
```shell
sudo ufw status
sudo ufw allow ssh.    # ativa o ssh no firewall UFW do ubuntu.
sudo ufw status
```
    
* Para ativar o firewall:
```shell 
sudo ufw enable
```

### Refazendo a topologia de rede da Prática
* Retorne as configurações de interface de rede para o modo bridge em cada VM no VirtualBox e ative o endereçamento IP estático conforme a Tabela 1.

### Acessando uma VM remotamente:

* Exemplo: $ ssh ``<user>``@``<ipServidorRemoto>``
* Fazendo o login 
   * de: srv-vm1-pc1  
   * para: srv-vm2-pc1

```shell
ssh administrador@172.17.1.2
```



# Exercício:

1) Acessar a partir da VM1-PC1 todas as outras via ssh:
2) Crie dois usuários (use o comando ``sudo adduser``) em cada servidor com o nome dos alunos da dupla.
3) Faça o login via ssh nos servidores usando cada usuário criado.

