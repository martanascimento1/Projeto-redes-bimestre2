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
   
![WhatsApp Image 2022-08-09 at 16 27 05 (2)](https://user-images.githubusercontent.com/103062784/184227599-655311a3-af26-4c62-87e5-15f68e266531.jpeg)

   3. Comente as linhas de endereço IP estático e ative o DHCP nas configurações do Netplan
  ```shell
  sudo nano /etc/netplan/01-netcfg.yaml
  ```
  
  ![WhatsApp Image 2022-08-09 at 16 27 06](https://user-images.githubusercontent.com/103062784/184228132-af7598c3-6cb5-4912-b5f4-beb61af9e791.jpeg)

   
### Ceritifique-se que a VM está acessando a internet:

```shell
sudo apt update       # atualiza as definições e versões de pacotes/bibliotecas dos repositórios do ubuntu
```

![WhatsApp Image 2022-08-09 at 16 27 08](https://user-images.githubusercontent.com/103062784/184228903-ba58cd57-6ce8-4181-9413-5636a9904f43.jpeg)

```shell
sudo apt upgrade -y   # atualiza os pacotes com as novas definições e versões 
```

![WhatsApp Image 2022-08-09 at 16 37 18](https://user-images.githubusercontent.com/103062784/184229438-99c8d006-a4ac-4109-a725-153e2724a63a.jpeg)


![WhatsApp Image 2022-08-09 at 16 40 03](https://user-images.githubusercontent.com/103062784/184230024-ba20e666-0571-40ae-89a7-4659e5db0465.jpeg)

### Instale o SSH Server

```shell
systemctl status ssh
```
![WhatsApp Image 2022-08-09 at 17 59 18](https://user-images.githubusercontent.com/103062784/184231049-750b3141-a30b-499c-bfbf-6b5fa95bf317.jpeg)


``` shell
sudo apt-get install openssh-server
```

![WhatsApp Image 2022-08-09 at 17 59 19](https://user-images.githubusercontent.com/103062784/184231225-f585a94b-4ccd-4596-87d9-67a9e1b7a202.jpeg)

```shell
systemctl status ssh
```
![WhatsApp Image 2022-08-09 at 17 59 25](https://user-images.githubusercontent.com/103062784/184231778-568d2a30-e830-45df-9ef5-d79111544708.jpeg)


### Verifique o status das portas do sistema
```
netstat -an | grep LISTEN.  #verifique as conexões TCP na porta 22 se está como LINSTENING
```

![WhatsApp Image 2022-08-09 at 17 59 25](https://user-images.githubusercontent.com/103062784/184232536-fa80802d-f5f3-4bdc-ad1e-0109084e6638.jpeg)


### Firewall 
* Para garantir o funcioamento correto do controle de acesso devemos configurar o firewall para permitir conexões remota via protocolo SSH, na porta 22.
 
```shell
sudo ufw status
```
![WhatsApp Image 2022-08-09 at 17 59 27](https://user-images.githubusercontent.com/103062784/184233376-baf13abf-44ae-400e-976c-eea5182f49b4.jpeg)


```shell
sudo ufw allow ssh.    # ativa o ssh no firewall UFW do ubuntu.
```
![WhatsApp Image 2022-08-09 at 17 59 27 (1)](https://user-images.githubusercontent.com/103062784/184233489-461048d0-50a7-439f-91ff-05fb881d7da1.jpeg)

```shell
sudo ufw status
```
![WhatsApp Image 2022-08-09 at 17 59 28](https://user-images.githubusercontent.com/103062784/184233663-219d022e-1499-4f97-ae3b-49e3223a220f.jpeg)

* Para ativar o firewall:
```shell 
sudo ufw enable
```
![WhatsApp Image 2022-08-11 at 14 58 37](https://user-images.githubusercontent.com/103062784/184233768-f678988c-80f6-4e18-ba64-8418206d535b.jpeg)


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

