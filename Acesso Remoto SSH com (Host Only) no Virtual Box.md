# Acesso Remoto SSH com (Host Only) no Virtual Box

## Objetivo:
    * Configurar o acesso remoto à uma VM pelo terminal do PC via ssh.

### Fazer login da VM ubuntu server

* Usuário da VM: ``administrador``
* Senha da VM: ``adminifal``

## 1) Ativar ou criar uma interface no computador para comunicação entre o Host (PC) e a VM. 

* Clicar em ``Arquivo``->``Host Network Manager``


![WhatsApp Image 2022-08-10 at 13 58 43](https://user-images.githubusercontent.com/103062784/184415886-6056b095-4b09-4986-9e71-570c63b5fa35.jpeg)



## 2) Configurar o servidor DHCP do no adaptador VBoxNet0. 

* Clicar na aba ``Servidor DHCP``

![WhatsApp Image 2022-08-10 at 13 58 43 (1)](https://user-images.githubusercontent.com/103062784/184416000-39201056-b574-4476-aff4-a963276143dd.jpeg)


* Verificar a configuração das interfaces usando o ``Terminal``

```shell
ifconfig -a       # verifique a existência da interface ``vboxnet0``
```

![WhatsApp Image 2022-08-10 at 13 58 45](https://user-images.githubusercontent.com/103062784/184416421-7dfab9c4-ebea-4867-8904-62c1922f0670.jpeg)

## 3) Adicionar um adaptador (HostOnly) em uma VM

* Para dar acesso a uma VM via rede pelo ``Terminal`` do PC deve-se adicionar um novo adapatador de rede à VM.


![WhatsApp Image 2022-08-10 at 13 58 45 (1)](https://user-images.githubusercontent.com/103062784/184416787-4bc5662a-a151-4f58-94fe-331d3518e063.jpeg)



## 5) Ativar as configurações da Interface na VM para o servidor DHCP

* Verificar as interfaces com ``ifconfig -a``

```shell
ifconfig -a       # verifique a existência da interface ``enp0s8``
```
![WhatsApp Image 2022-08-10 at 13 58 46](https://user-images.githubusercontent.com/103062784/184417043-0252d852-4c45-46a8-830f-a4101b6557cb.jpeg)


* Configurar as interfaces no netplan e ative o DHCP para o Adaptador 2 (enp0s8)

```shell
sudo nano /etc/netplan/01-netcfg.yaml
```
![WhatsApp Image 2022-08-10 at 13 58 46 (1)](https://user-images.githubusercontent.com/103062784/184417293-53a77335-5492-420b-9edf-a0fa2e374044.jpeg)


* Ativar as configurações:

```shell
sudo netplan apply
```

* Checar se pegou o IP na nova interface de rede:

```shell
ifconfig -a
```
![WhatsApp Image 2022-08-10 at 13 58 46 (2)](https://user-images.githubusercontent.com/103062784/184417752-fcdb1edc-10c9-4c46-a170-6b52aa28229b.jpeg)


### Acessar uma VM remotamente:

* Exemplo: $ ssh ``<administrador>``@``<192.168.56.101>``
* Fazendo o login 
   * de: terminal-pc
   * para: 192.168.56.101

```shell
ssh administrador@192.168.56.101
```

![WhatsApp Image 2022-08-10 at 14 26 41](https://user-images.githubusercontent.com/103062784/184418573-38cb8395-e932-4edd-b42b-00762e38e3be.jpeg)
![WhatsApp Image 2022-08-10 at 14 26 41 (1)](https://user-images.githubusercontent.com/103062784/184418681-86c1b704-68b8-4ede-9598-41c7a6772aa8.jpeg)
![WhatsApp Image 2022-08-10 at 14 26 41 (2)](https://user-images.githubusercontent.com/103062784/184418761-a3edc9e4-50b5-47e7-91d6-fd678102e1cf.jpeg)


### Tarefa final:

![WhatsApp Image 2022-08-10 at 14 26 42](https://user-images.githubusercontent.com/103062784/184418904-08299d47-421f-48f8-92ae-cf5010075eef.jpeg)
