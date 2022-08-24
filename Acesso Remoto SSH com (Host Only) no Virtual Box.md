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

![WhatsApp Image 2022-08-23 at 16 56 33](https://user-images.githubusercontent.com/103062784/186419341-e45ce1db-5d48-4eff-a72a-a51f95bb3704.jpeg)


* Verifique a configuração das interfaces usando o ``Terminal``

```shell
ifconfig -a       # verifique a existência da interface ``vboxnet0``
```

![WhatsApp Image 2022-08-10 at 13 58 45](https://user-images.githubusercontent.com/103062784/184416421-7dfab9c4-ebea-4867-8904-62c1922f0670.jpeg)

## 3) Adicionar um adaptador (HostOnly) em uma VM

* Para dar acesso a uma VM via rede pelo ``Terminal`` do PC devemos adicionar um novo adapatador de rede à VM.


![WhatsApp Image 2022-08-23 at 17 00 23](https://user-images.githubusercontent.com/103062784/186419548-2bdd195e-446d-4331-879e-aaa883eaf6cc.jpeg)



## 5) Ative as configurações da Interface na VM para o servidor DHCP

* Verifique as interfaces com ``ifconfig -a``

```shell
ifconfig -a       # verifique a existência da interface ``enp0s8``
```

![WhatsApp Image 2022-08-24 at 09 38 34](https://user-images.githubusercontent.com/103062784/186420423-6a0fc045-05e3-4c70-ac19-2b504603caaa.jpeg)

* Configure as interfaces no netplan e ative o DHCP para o Adaptador 2 (enp0s8)

```shell
sudo nano /etc/netplan/01-netcfg.yaml
```

![WhatsApp Image 2022-08-24 at 13 34 43](https://user-images.githubusercontent.com/103062784/186473822-64fab47f-8797-401a-9c02-8b565ab63680.jpeg)


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
![WhatsApp Image 2022-08-23 at 17 09 40](https://user-images.githubusercontent.com/103062784/186421408-571f0b5e-cb87-466a-bfa7-2c1200f03dfd.jpeg)




# Exercício:

1) Acessar uma VM a partir do terminal do PC.


![WhatsApp Image 2022-08-23 at 17 10 56](https://user-images.githubusercontent.com/103062784/186421483-446d70c9-33c1-40f5-b462-465b459b107a.jpeg)
