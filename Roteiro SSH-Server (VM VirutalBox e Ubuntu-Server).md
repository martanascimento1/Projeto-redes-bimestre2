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

* formato: ``sudo hostnamectl set-hostname <hostname>``

* NA VM1-PC1 executar:

```shell
sudo hostnamectl set-hostname srv-vm1-pc2
```

![WhatsApp Image 2022-08-24 at 08 58 52](https://user-images.githubusercontent.com/103062784/186412988-fe47f99d-a590-490c-b368-ce7a81eb1b91.jpeg)


## Instalar o servidor SSH

### Inicialmente:
   1. acessar as configurações de cada VM e alterar novamente o Adaptador1 para **NAT**
   
![WhatsApp Image 2022-08-09 at 16 27 05 (2)](https://user-images.githubusercontent.com/103062784/184227599-655311a3-af26-4c62-87e5-15f68e266531.jpeg)

   3. Comentar as linhas de endereço IP estático e ativar o DHCP nas configurações do Netplan
   4. 
  ```shell
  sudo nano /etc/netplan/01-netcfg.yaml
  ```
  
  ![WhatsApp Image 2022-08-09 at 16 27 06](https://user-images.githubusercontent.com/103062784/184228132-af7598c3-6cb5-4912-b5f4-beb61af9e791.jpeg)

   
### Ceritificar-se que a VM está acessando a internet:

```shell
sudo apt update       # atualiza as definições e versões de pacotes/bibliotecas dos repositórios do ubuntu
```

![WhatsApp Image 2022-08-09 at 16 27 08](https://user-images.githubusercontent.com/103062784/184228903-ba58cd57-6ce8-4181-9413-5636a9904f43.jpeg)

```shell
sudo apt upgrade -y   # atualiza os pacotes com as novas definições e versões 
```

![WhatsApp Image 2022-08-09 at 16 37 18](https://user-images.githubusercontent.com/103062784/184229438-99c8d006-a4ac-4109-a725-153e2724a63a.jpeg)


![WhatsApp Image 2022-08-09 at 16 40 03](https://user-images.githubusercontent.com/103062784/184230024-ba20e666-0571-40ae-89a7-4659e5db0465.jpeg)

### Instalar o SSH Server

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
![WhatsApp Image 2022-08-09 at 17 59 25 (1)](https://user-images.githubusercontent.com/103062784/184234321-5a2f81d0-4a82-4749-bc08-c97b6de1befd.jpeg)


### Verificar o status das portas do sistema
```
netstat -an | grep LISTEN.  #verifique as conexões TCP na porta 22 se está como LINSTENING
```

![WhatsApp Image 2022-08-09 at 17 59 26](https://user-images.githubusercontent.com/103062784/184234379-f14be003-1f5f-4035-a94a-62d762fd1046.jpeg)

![WhatsApp Image 2022-08-09 at 17 59 27 (2)](https://user-images.githubusercontent.com/103062784/184234550-f1c3a047-c69b-4f71-b692-da15e9fca324.jpeg)


### Firewall 
* Para garantir o funcionamento correto do controle de acesso é necessário configurar o firewall para permitir conexões remota via protocolo SSH, na porta 22.
 
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

* Ativar o firewall:
```shell 
sudo ufw enable
```
![WhatsApp Image 2022-08-11 at 14 58 37](https://user-images.githubusercontent.com/103062784/184233768-f678988c-80f6-4e18-ba64-8418206d535b.jpeg)


### Refazendo a topologia de rede da Prática
* Coloque as configurações de interface de rede para o modo bridge em cada VM no VirtualBox:
![WhatsApp Image 2022-08-11 at 17 22 37](https://user-images.githubusercontent.com/103062784/184235445-1e172bac-74d3-4f1e-97d6-c45393859610.jpeg)


* Ative o endereçamento IP estático .
```shell
  sudo nano /etc/netplan/01-netcfg.yaml
  ```
  
![WhatsApp Image 2022-08-11 at 17 31 34](https://user-images.githubusercontent.com/103062784/184238748-52c18fd1-3991-4ad2-be89-71995015bd81.jpeg)

### Acessar uma VM remotamente:

* Exemplo: $ ssh ``<administrador>``@``<192.168.24.4>``
* Fazendo o login 
   * de: srv-vm1-pc1    
   * para: srv-vm2-pc1
   
   ![WhatsApp Image 2022-08-09 at 17 59 29](https://user-images.githubusercontent.com/103062784/184239317-eab51b35-c558-4a92-a8de-4a6109e033af.jpeg)


```shell
ssh administrador@192.168.24.4
```


# Tarefa final:

1) Acessar a partir da VM1-PC1 todas as outras via ssh:
2) Criar um usuário (use o comando ``sudo adduser``) .

![WhatsApp Image 2022-08-09 at 17 59 31 (1)](https://user-images.githubusercontent.com/103062784/184239940-20056125-d319-4f04-a0e9-137eecaa4ad0.jpeg)



4) Façalogin via ssh nos servidores usando cada usuário criado.


![WhatsApp Image 2022-08-09 at 17 59 31](https://user-images.githubusercontent.com/103062784/184239878-50283f8d-3469-41bd-bd31-33ad5533aadc.jpeg)
![WhatsApp Image 2022-08-12 at 15 28 46](https://user-images.githubusercontent.com/103062784/184421432-324a5a5d-8fd6-4abc-9034-157b4da635f3.jpeg)

