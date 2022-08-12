# Configuração estática de Nomes

## Objetivo:
    * Configurar um serviço de nomes
    * configurar /etc/hosts

### Login da VM ubuntu server

* Usuário da VM: ``administrador``
* Senha da VM: ``adminifal``

## Serviço de nomes estático do Ubuntu:
>**_NOTA:_**
> Nomes de host estáticos são mapeamentos de nome de host para IP definidos localmente localizados no arquivo /etc/hosts. 
> Os nomes configurados no /etc/hosts têm precedência sobre o DNS por padrão. Assim, tentar resolver um nome de host e ele corresponder a uma entrada em /etc/hosts, ele não tentará procurar o registro no DNS. 
>O seguinte é um exemplo de um arquivo de hosts em que vários servidores locais foram identificados por nomes de host simples, aliases e seus nomes de >**_** domínio totalmente qualificados (FQDNs) equivalentes.

```
127.0.0.1 localhost
127.0.1.1 VM2-PC4-julia
192.168.24.1 grupo1-vm1-pc1 maria.grupo1-924.net    bel
192.168.24.2 grupo1-vm2-pc1 izabel.grupo1-924.net   iza
192.168.24.3 grupo1-vm1-pc2 marta.grupo1-924.net    crf
192.168.24.4 grupo1-vm2-pc2 mirely.grupo1-924.net   srn
192.168.24.5 grupo1-vm1-pc3 debora.grupo1-924.net   debs
192.168.24.6 grupo1-vm2-pc3 nycolli.grupo1-924.net  nick
192.168.24.7 grupo1-vm1-pc4 julia.grupo1-924.net    juju
192.168.24.8 grupo1-vm2-pc4 victoria.grupo1-924.net vic
```

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
| VM1-PC1-izabel    | 192.168.24.1   |  grupo1-vm1-pc1 |  maria.grupo1-924.net     |     mabel      |
| VM2-PC1-izabel    | 192.168.24.2   |  grupo1-vm2-pc1 |  izabel.grupo1-924.net    |     iza        |
| VM1-PC2-marta     | 192.168.24.3   |  grupo1-vm1-pc2 |  marta.grupo1-924.net     |     crf        |
| VM2-PC2-marta     | 192.168.24.4   |  grupo1-vm2-pc2 |  mirely.grupo1-924.net    |     srn        |
| VM1-PC3-debora    | 192.168.24.5   |  grupo1-vm1-pc3 |  debora.grupo1-924.net    |     debs       |
| VM2-PC3-debora    | 192.168.24.6   |  grupo1-vm2-pc3 |  nycolli.grupo1-924.net   |     niky       |
| VM1-PC4-julia     | 192.168.24.7   |  grupo1-vm1-pc4 |  julia.grupo1-924.net     |     juju       |
| VM2-PC4-julia     | 192.168.24.8   |  grupo1-vm2-pc4 |  victoria.grupo1-924.net  |     vic        |
----------------------------------------------------------------------------------------------------
```
* Em seguida, é preciso editar os arquivo /etc/hosts conforme as definições da Tabela de Endereços e Nomes (Tabela 1) e digitar o próximo comando. 

```shell
sudo nano /etc/hosts
```

* Exemplo do arquivo /etc/hosts na VM1:

```
127.0.0.1 localhost
127.0.1.1 VM1-PC4-julia
192.168.24.1 grupo1-vm1-pc1 maria.grupo1-924.net    bel
192.168.24.2 grupo1-vm2-pc1 izabel.grupo1-924.net   iza
192.168.24.3 grupo1-vm1-pc2 marta.grupo1-924.net    crf
192.168.24.4 grupo1-vm2-pc2 mirely.grupo1-924.net   srn
192.168.24.5 grupo1-vm1-pc3 debora.grupo1-924.net   debs
192.168.24.6 grupo1-vm2-pc3 nycolli.grupo1-924.net  nick
192.168.24.7 grupo1-vm1-pc4 julia.grupo1-924.net    juju
192.168.24.8 grupo1-vm2-pc4 victoria.grupo1-924.net vic

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

# Exercício:
Acessar uma VM a partir do terminal do PC e:

1) Ping para os hostnames, FQDNs e para os aliases que foram configurados nos 
2) Acessar uma VM a partir do terminal do PC e acesse as outras VMs utilizando os nomes.

