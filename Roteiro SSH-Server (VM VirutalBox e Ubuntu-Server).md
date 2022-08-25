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

* NA VM executar:

sudo hostnamectl set-hostname grupo1-vm1-pc2
```

![WhatsApp Image 2022-08-24 at 08 58 52](https://user-images.githubusercontent.com/103062784/186412988-fe47f99d-a590-490c-b368-ce7a81eb1b91.jpeg)


## Instalar o servidor SSH

### Inicialmente:
   1. acessar as configurações de cada VM e alterar novamente o Adaptador1 para **NAT**
   
![WhatsApp Image 2022-08-23 at 16 04 30](https://user-images.githubusercontent.com/103062784/186413199-fe692b27-6095-42e7-938d-cf3d97474570.jpeg)


   2. Comentar as linhas de endereço IP estático e ativar o DHCP nas configurações do Netplan usando o comando :
  
  ```shell
  sudo nano /etc/netplan/01-netcfg.yaml
  ```
  
  ![WhatsApp Image 2022-08-23 at 16 06 47](https://user-images.githubusercontent.com/103062784/186413326-74b90cbe-6e71-4859-8b21-57623dc1ddc6.jpeg)

   
### Ceritificar-se que a VM está acessando a internet:

* Para atualizar as definições e versões de pacotes/bibliotecas dos repositórios do ubuntu:

```shell
sudo apt update        
```

![WhatsApp Image 2022-08-23 at 16 14 59](https://user-images.githubusercontent.com/103062784/186413396-45f409e1-5d36-452d-9df2-1d38fe4733dc.jpeg)

* Para atualizar os pacotes com as novas definições e versões:

```shell
sudo apt upgrade -y  
```

![WhatsApp Image 2022-08-23 at 16 16 48](https://user-images.githubusercontent.com/103062784/186413582-e1edf441-d3a2-4407-9918-b1bd55a03c0e.jpeg)


![WhatsApp Image 2022-08-09 at 16 40 03](https://user-images.githubusercontent.com/103062784/184230024-ba20e666-0571-40ae-89a7-4659e5db0465.jpeg)

### Instalar o SSH Server

* Para ver o status:

```shell
systemctl status ssh
```

![WhatsApp Image 2022-08-23 at 16 18 40](https://user-images.githubusercontent.com/103062784/186413701-561f02f7-3a54-467d-aa6a-72092ab9c166.jpeg)

* Para instalar:


``` shell
sudo apt-get install openssh-server
```
![WhatsApp Image 2022-08-23 at 16 19 47](https://user-images.githubusercontent.com/103062784/186413785-2a42e60d-605d-4246-8634-3451437cf427.jpeg)



```shell
systemctl status ssh
```

![WhatsApp Image 2022-08-23 at 16 21 21](https://user-images.githubusercontent.com/103062784/186413858-91c239b5-15c9-46bc-97ea-0ad6ffa8c33f.jpeg)




### Verificar o status das portas do sistema

* Verificando se as conexões TCP na porta 22 está como LINSTENING:

``` shell
netstat -an | grep LISTEN.  
```
![WhatsApp Image 2022-08-23 at 16 22 12](https://user-images.githubusercontent.com/103062784/186413961-1c6ddafc-3cdd-48c6-af04-e73131dc63cb.jpeg)



![WhatsApp Image 2022-08-09 at 17 59 27 (2)](https://user-images.githubusercontent.com/103062784/184234550-f1c3a047-c69b-4f71-b692-da15e9fca324.jpeg)


### Firewall 
* Para garantir o funcionamento correto do controle de acesso é necessário configurar o firewall para permitir conexões remota via protocolo SSH, na porta 22.
 
```shell
sudo ufw status
```

![WhatsApp Image 2022-08-23 at 16 23 49](https://user-images.githubusercontent.com/103062784/186414205-82eeb75b-5aff-4ec1-ba27-2ceb5806c88a.jpeg)

* Para ativar o ssh no firewall UFW do ubuntu.

```shell
sudo ufw allow ssh.    
```
![WhatsApp Image 2022-08-23 at 16 24 44](https://user-images.githubusercontent.com/103062784/186414270-6a978c7e-67b0-4d62-8db7-fdbbcf2b7670.jpeg)


```shell
sudo ufw status
```

![WhatsApp Image 2022-08-24 at 09 26 35](https://user-images.githubusercontent.com/103062784/186418100-9604f84f-7114-4b2c-8a68-45461dad2b8a.jpeg)

* Ativar o firewall:
```shell 
sudo ufw enable
```

![WhatsApp Image 2022-08-24 at 09 24 57](https://user-images.githubusercontent.com/103062784/186417839-90f1e71f-f69f-4001-a570-73e3171d0fe9.jpeg)

### Refazendo a topologia de rede da Prática
* Coloque as configurações de interface de rede para o modo bridge em cada VM no VirtualBox:

![WhatsApp Image 2022-08-23 at 16 28 59](https://user-images.githubusercontent.com/103062784/186414445-dd10b3ac-59ec-4df9-a0f4-00e0ed347740.jpeg)


* Ative o endereçamento IP estático .

```shell
  sudo nano /etc/netplan/01-netcfg.yaml
  ```
  
![WhatsApp Image 2022-08-23 at 16 31 49](https://user-images.githubusercontent.com/103062784/186414529-9b8544c3-a7de-4096-8f9a-e281101d3b56.jpeg)


### Acessar uma VM remotamente:

* Exemplo: $ ssh ``<administrador>``@``<192.168.24.4>``
* Fazendo o login 
   * de: srv-vm1-pc1    
   * para: srv-vm2-pc1

```shell
ssh administrador@192.168.24.4
```

![WhatsApp Image 2022-08-23 at 16 41 49 (1)](https://user-images.githubusercontent.com/103062784/186414779-64a7fe71-b0b9-44be-a538-96e6cebb7a47.jpeg)

# Tarefa final:

1) Acessar a partir da VM1-PC1 todas as outras via ssh:
2) Criar um usuário (use o comando ``sudo adduser``) .



![WhatsApp Image 2022-08-24 at 09 14 23](https://user-images.githubusercontent.com/103062784/186415648-54bd9143-9ec7-40bc-a607-62595ebd4204.jpeg)


4) Faça login via ssh nos servidores usando cada usuário criado.

* Use:
 ```shell
  ssh marta@192.168.24.3
  ```
![WhatsApp Image 2022-08-23 at 16 47 44](https://user-images.githubusercontent.com/103062784/186415777-2f181263-37f5-4bd5-a3c9-7c1187207b67.jpeg)
![WhatsApp Image 2022-08-23 at 16 49 03](https://user-images.githubusercontent.com/103062784/186415856-4afec1b1-f0d7-4414-b90f-b0cf8ab5ac1d.jpeg)

[Navegar de volta para roteiro](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/564319c685f6ec504080630dc9989612b4fc7b61/README.md)
