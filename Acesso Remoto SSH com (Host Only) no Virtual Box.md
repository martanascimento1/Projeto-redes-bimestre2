# Acesso Remoto SSH com (Host Only) no Virtual Box

## Objetivo:
    * Configurar o acesso remoto à uma VM pelo terminal do PC via ssh.
    * Porta 22

### Login da VM ubuntu server

* Usuário da VM: ``administrador``
* Senha da VM: ``adminifal``

## 1) Ative ou crie uma interface no computador para comunicação entre o Host (PC) e a VM. 

* Clique em ``Arquivo``->``Host Network Manager``


![WhatsApp Image 2022-08-10 at 13 58 43](https://user-images.githubusercontent.com/103062784/184415886-6056b095-4b09-4986-9e71-570c63b5fa35.jpeg)



## 2) Configure o servidor DHCP do no adaptador VBoxNet0. 

* Clique em na aba ``Servidor DHCP``

![WhatsApp Image 2022-08-10 at 13 58 43 (1)](https://user-images.githubusercontent.com/103062784/184416000-39201056-b574-4476-aff4-a963276143dd.jpeg)


* Verifique a configuração das interfaces usando o ``Terminal``

```shell
ifconfig -a       # verifique a existência da interface ``vboxnet0``
```

![WhatsApp Image 2022-08-10 at 13 58 45](https://user-images.githubusercontent.com/103062784/184416421-7dfab9c4-ebea-4867-8904-62c1922f0670.jpeg)

## 3) Adicionar um adaptador (HostOnly) em uma VM

* Para dar acesso a uma VM via rede pelo ``Terminal`` do PC devemos adicionar um novo adapatador de rede à VM.


![WhatsApp Image 2022-08-10 at 13 58 45 (1)](https://user-images.githubusercontent.com/103062784/184416787-4bc5662a-a151-4f58-94fe-331d3518e063.jpeg)



## 5) Ative as configurações da Interface na VM para o servidor DHCP

* Verifique as interfaces com ``ifconfig -a``

```shell
ifconfig -a       # verifique a existência da interface ``enp0s8``
```
![WhatsApp Image 2022-08-10 at 13 58 46](https://user-images.githubusercontent.com/103062784/184417043-0252d852-4c45-46a8-830f-a4101b6557cb.jpeg)


* Configure as interfaces no netplan e ative o DHCO para o Adaptador 2 (enp0s8)

```shell
sudo nano /etc/netplan/01-netcfg.yaml
```
![WhatsApp Image 2022-08-10 at 13 58 46 (1)](https://user-images.githubusercontent.com/103062784/184417293-53a77335-5492-420b-9edf-a0fa2e374044.jpeg)


* ative as configurações:

```shell
sudo netplan apply
```

* cheque se pegou IP na nova interface de rede:

```shell
ifconfig -a
```
![WhatsApp Image 2022-08-10 at 13 58 46 (2)](https://user-images.githubusercontent.com/103062784/184417752-fcdb1edc-10c9-4c46-a170-6b52aa28229b.jpeg)


### Acessando uma VM remotamente:

* Exemplo: $ ssh ``<user>``@``<ipServidorRemoto>``
* Fazendo o login 
   * de: terminal-pc
   * para: 192.168.56.101

```shell
ssh administrador@192.168.56.101
```

# Exercício:

1) Acessar uma VM a partir do terminal do PC.
2) A partir da VM acessada faça ssh para as outras VMs da rede interna utilizando os IPs da rede 172.17.1.0
