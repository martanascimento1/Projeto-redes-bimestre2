
# Configuração de uma rede ponto a ponto com duas máquinas virtuais

* Abrir terminal
* logar com o usuário ``redes`` senha: admin@Lab92
```bash
 su redes
```

* Verifique se os diretórios abaixo existem e se os arquivos de imagens também. Se não, acesse o tutorial [Configuração do ambiente]([https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/95c398380f36e4ffdb142c7c6a5f60bf2d08fe10/Configura%C3%A7%C3%A3o%20do%20ambiente.md]).

```
/labredes/images/original
/labredes/VM/924/<NomeDoAluno>
```

* Instale o Virtualbox Extension Pack

```
   su redes
   sudo apt install virtualbox-ext-pack
```

## Criando uma Rede Ponto a Ponto com Duas Máquinas Virtuais

* Faremos a criação de uma rede ponto a ponto com duas VMs dentro do VirtualBox.
* Para que isso ocorra tanto as VMs devem ser configuradas como as interfaces de rede dessas VMs.
* A Figura 1 ilustra a topologia de Rede dentro do VitualBox

<p><center> Figura 1: Topologia de Rede Ponto a Ponto usando o VitualBox, com duas VMs com suas NICs em modo Rede Interna</center></p>   
   
![WhatsApp Image 2022-08-11 at 21 48 15](https://user-images.githubusercontent.com/103062733/184265422-9f463f31-e8a4-4bfb-bdac-46bc2065d7a6.jpeg)

### Importar VMs no VirtualBox

* O arquivo .OVA é um formato de exportação de VM utilizado pelo VirtualBox
* Este arquivo deve ser importado para criar as duas VMs que precisamos para fazer esta tarefa de rede ponto a ponto.

* A Figura 2 Ilustra as configurações para a importação das VMs: VM1-PC3-debora e VM2-PC3-nycolli
<p><center>Figura 2: Criando uma VM a partir de um arquivo OVA
 
![184224800-9b10b210-cf25-4103-972b-63c53931d3b6](https://user-images.githubusercontent.com/103062733/184265457-9db87a39-4c37-44e4-8360-29a05729490c.jpeg)


![WhatsApp Image 2022-08-11 at 21 40 18](https://user-images.githubusercontent.com/103062733/184265464-4c5b0239-9dff-4e53-bd7e-d7f945308fc7.jpeg)

### Configurando as NICs das VMs

* Para que a VMs utilizem a mesma rede interna é necessário acessar as configurações de Rede de cada VM e selecionar o modo ``rede interna`` e definir o nome da rede. ``labredes`` será o nome escolhido da nossa rede virtual. Utilize o mesmo nome nas duas VMs.


### Fazendo login nas VMs

* Usuário da VM: ``administrador``
* Senha da VM: ``adminifal``

<p><center> Figura 3: Telas das duas VMs em execução</center></p>   
 
![WhatsApp Image 2022-08-12 at 15 05 46](https://user-images.githubusercontent.com/103062733/184417765-6ff59e16-19c1-496b-91e3-1a5a600e74f1.jpeg)


## Configuração estática de endereço IP na interface de rede 

* O Ubuntu utiliza um arquivo YAML para configurar as interfaces de rede
* este arquivo se contra na pasta ``/etc/netplan/``
* digite: 

```shell
ifconfig -a
ls -la /etc/netplan
cat /etc/netplan/01-netcfg.yaml
```
* Verifique o nome correto do arquivo no seu servidor. No exemplo a seguir, o nome do arquivo é ***01-netcfg.yaml***


### Na VM1-PC3

* instale as ferramentas de rede

```bash
$ sudo apt install net-tools -y
```
*  Edite o arquivo  ***01-netcfg.yaml*** 

```bash
$ sudo nano /etc/netplan/01-netcfg.yaml
```
*  Adicione as linhas para a configuração estática do IP para configurar o IP para ``172.17.0.2/24``. 
```
network:
    ethernets:
        enp0s3:                           # nome da interface que está sendo configurada. Verifique com o comando 'ifconfig -a'
            addresses: [192.168.24.5/28]    # IP e Máscara do Host.
            gateway4: 192.168.24.14          # IP do Gateway
            dhcp4: false                  # dhcp4 false -> cliente DHCP está desabilitado, logo o utilizará o IP do campo 'addresses'
    version: 2
```
*  Após salvar o arquivo é necessário aplicar as configurações, com o **netplan apply**. Depois veja a configuração das interfaces com ****ifconfig -a***

```bash
$ sudo netplan apply
$ ifconfig -a
```

### Na VM2-PC3

* instale as ferramentas de rede

```bash
$ sudo apt install net-tools -y
```
*  Edite o arquivo  ***01-netcfg.yaml*** 

```bash
$ sudo nano /etc/netplan/01-netcfg.yaml
```
*  Adicione as linhas para a configuração estática do IP para configurar o IP para ``172.17.0.2/24``.

```
network:
    ethernets:
        enp0s3:                           # nome da interface que está sendo configurada. Verifique com o comando 'ifconfig -a'
            addresses: [192.168.24.6]    # IP e Máscara do Host.
            gateway4: 192.168.24.14         # IP do Gateway
            dhcp4: false                  # dhcp4 false -> cliente DHCP está desabilitado, logo o utilizará o IP do campo 'addresses'
    version: 2
```
*  Após salvar o arquivo é necessário aplicar as configurações, com o **netplan apply**. Depois veja a configuração das interfaces com ****ifconfig -a***

```bash
$ sudo netplan apply
$ ifconfig -a
```
### Configuração da rede interna do VirtualBox

* A Figura 4 Ilustra as configurações para a importação das VMs: VM-LAB01 e VM-LAB02

<p><center> Figura 4: Configuração das NICs como modo ``rede interna``</center></p>   
   
![WhatsApp Image 2022-08-11 at 16 44 30](https://user-images.githubusercontent.com/103062733/184226195-b11c91fe-b720-408c-ade4-cfdfb8891d36.jpeg)

### Teste a conectividade entre as VMs com o comando ``ping``

   * Ping da VM1 para VM2

```shell
ping 192.168.24.6       # ctrl + c para finalizar o comando
```
   * Ping da VM2 para VM1

```shell
ping 192.168.24.5       # ctrl + c para finalizar o comando
```
