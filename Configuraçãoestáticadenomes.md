# Configuração estática de Nomes

## Objetivo:
    * Configurar um serviço de nomes
    * configurar /etc/hosts

### Login da VM ubuntu server

* Usuário da VM: ``administrador``

![WhatsApp Image 2022-08-12 at 15 00 11](https://user-images.githubusercontent.com/103062866/184416796-2bd177b6-6b34-4f15-8a0f-f4e5c34a8c8b.jpeg)


## Serviço de nomes estático do Ubuntu:
>**_NOTA:_**
> Nomes de host estáticos são mapeamentos de nome de host para IP definidos localmente localizados no arquivo /etc/hosts. 
> Os nomes configurados no /etc/hosts têm precedência sobre o DNS por padrão. Assim, tentar resolver um nome de host e ele corresponder a uma entrada em /etc/hosts, ele não tentará procurar o registro no DNS. 
>O seguinte é um exemplo de um arquivo de hosts em que vários servidores locais foram identificados por nomes de host simples, aliases e seus nomes de >**_** domínio totalmente qualificados (FQDNs) equivalentes.

![WhatsApp Image 2022-08-11 at 17 05 49](https://user-images.githubusercontent.com/103062866/184416639-898d36b0-ad14-4cdd-b4c5-6109c64bce52.jpeg)

```
127.0.0.1 localhost
127.0.1.1 VM2-PC4-julia
192.168.24.1 grupo1-vm1-pc1 maria.grupo1-924.ifalara.net    bel
192.168.24.2 grupo1-vm2-pc1 izabel.grupo1-924.ifalara.net   iza
192.168.24.3 grupo1-vm1-pc2 marta.grupo1-924.ifalara.net    crf
192.168.24.4 grupo1-vm2-pc2 mirely.grupo1-924.ifalara.net   srn
192.168.24.5 grupo1-vm1-pc3 debora.grupo1-924.ifalara.net   debs
192.168.24.6 grupo1-vm2-pc3 nycolli.grupo1-924.ifalara.net  nick
192.168.24.7 grupo1-vm1-pc4 julia.grupo1-924.ifalara.net    juju
192.168.24.8 grupo1-vm2-pc4 victoria.grupo1-924.ifalara.net vic
```
![WhatsApp Image 2022-08-26 at 14 50 39](https://user-images.githubusercontent.com/103062784/186963264-5a97cb8f-eedc-4d96-8c6f-f2db15121c91.jpeg)


>**Observação**: observa-se que cada um dos servidores recebeu aliases além de seus nomes próprios e FQDNs. 
>* ``grupo1-vm1-pc1`` foi mapeado para o nome ``bel``
>* ``grupo1-vm2-pc1`` foi mapeado para o nome ``iza``
>* ``grupo1-vm1-pc2`` foi mapeado para o nome ``crf``
>* ``grupo1-vm2-pc2`` é referido como ``srn`` 
>* ``grupo1-vm1-pc3`` é referido como ``debs`` 
>* ``grupo1-vm2-pc3`` como ``nick`` 
>* ``grupo1-vm1-pc4`` como ``juju`` e 
>* ``grupo1-vm2-pc4`` como ``vic``.

## Configurar o serviço de nomes estático.

```
Tabela 1: Definições de endereços IPs da Rede e Nomes de Hosts
----------------------------------------------------------------------------------------------------
|     DESCRICAO     |       IP        |    hostname    |           FQDN            |     aliase     |             
----------------------------------------------------------------------------------------------------
| VM1-PC1-izabel    | 192.168.24.1   |  grupo1-vm1-pc1 |  maria.grupo1-924.ifalara.net     |  mabel |
| VM2-PC1-izabel    | 192.168.24.2   |  grupo1-vm2-pc1 |  izabel.grupo1-924.ifalara.net    |  iza   |
| VM1-PC2-marta     | 192.168.24.3   |  grupo1-vm1-pc2 |  marta.grupo1-924.ifalara.net     |  rf    |
| VM2-PC2-marta     | 192.168.24.4   |  grupo1-vm2-pc2 |  mirely.grupo1-924.ifalara.net    |  srn   |
| VM1-PC3-debora    | 192.168.24.5   |  grupo1-vm1-pc3 |  debora.grupo1-924.ifalara.net    |  debs  |
| VM2-PC3-debora    | 192.168.24.6   |  grupo1-vm2-pc3 |  nycolli.grupo1-924.ifalara.net   |  niky  |
| VM1-PC4-julia     | 192.168.24.7   |  grupo1-vm1-pc4 |  julia.grupo1-924.ifalara.net     |  juju  |
| VM2-PC4-julia     | 192.168.24.8   |  grupo1-vm2-pc4 |  victoria.grupo1-924.ifalara.net  |  vic   |
----------------------------------------------------------------------------------------------------
```
* Em seguida, é preciso editar os arquivo /etc/hosts conforme as definições da Tabela de Endereços e Nomes (Tabela 1) e digitar o próximo comando. 

```shell
sudo nano /etc/hosts
```
![WhatsApp Image 2022-08-26 at 14 50 39](https://user-images.githubusercontent.com/103062784/186963294-87ff5fe9-cb07-49de-9b26-8bc84f3bb73b.jpeg)


* Exemplo do arquivo /etc/hosts na VM1:

```
127.0.0.1 localhost
127.0.1.1 VM1-PC4-julia
192.168.24.1 grupo1-vm1-pc1 maria.grupo1-924.ifalara.net    bel
192.168.24.2 grupo1-vm2-pc1 izabel.grupo1-924.ifalara.net   iza
192.168.24.3 grupo1-vm1-pc2 marta.grupo1-924.ifalara.net    crf
192.168.24.4 grupo1-vm2-pc2 mirely.grupo1-924.ifalara.net   srn
192.168.24.5 grupo1-vm1-pc3 debora.grupo1-924.ifalara.net   debs
192.168.24.6 grupo1-vm2-pc3 nycolli.grupo1-924.ifalara.net  nick
192.168.24.7 grupo1-vm1-pc4 julia.grupo1-924.ifalara.net    juju
192.168.24.8 grupo1-vm2-pc4 victoria.grupo1-924.ifalara.net vic

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

> **É necessário fazer isso em todas as VMS!!!**

### Agora, acesse uma VM remotamente:

* Exemplo: $ ssh ``<user>``@``<ipServidorRemoto>``
* Fazendo o login 
   * de: terminal-pc
   * para: 192.168.56.101

```shell
ssh administrador@192.168.56.101
```
![WhatsApp Image 2022-08-11 at 17 41 14](https://user-images.githubusercontent.com/103062866/184417046-d0ef0c68-a289-4581-98cb-813442ab2897.jpeg)

# Exercício:
Acessar uma VM a partir do terminal do PC e:

1) Ping para os hostnames, FQDNs e para os aliases que foram configurados nos 
2) Acessar uma VM a partir do terminal do PC e acesse as outras VMs utilizando os nomes.
![WhatsApp Image 2022-08-11 at 16 13 42](https://user-images.githubusercontent.com/103062866/184417085-6881700b-2354-4b9f-b68e-ee352be69399.jpeg)
![WhatsApp Image 2022-08-11 at 16 13 47](https://user-images.githubusercontent.com/103062866/184417104-28ece24a-76b9-4f26-8757-b7ef463f407b.jpeg)


[Navegar de volta para roteiro](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/README.md)
