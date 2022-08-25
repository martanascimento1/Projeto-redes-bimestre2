# Configuração de teclado na VM

* **Locale** define as variáveis de ambiente que especificam a região, o idioma e as variantes de teclado do sistema que o usuário deseja ver na interface ou no terminal virtual.
As bibliotecas e as aplicações também verificam essas variável para carregar o idioma adequado de acordo com as preferências do usuário.

* A configurações de **Locale** basicamente consistem em um código de idioma (language code), um país/região (country/region code), data e formato de hora (time/date format), formatação numérica (numbers format setting), formatação monetária (currency format setting), cores (Color setting), etc. 


* Identifique os idiomas carregados no sistema com ``locale``
* Pelo terminal da VM:

```shell
locale
```  
  Figura 1: Saída de tela do comando **locale** antes da configuração.  

*  O **localectl** é uma interface que facilita as configurações de locale no linux.
* ``localectl status`` exibe as configurações atuais de idioma e layout de teclado atuais.

```shell
localectl status
```
  Figura 2: Saída de tela do comando **locale status** antes da configuração.  

* Instale o pacote de idiomas para português:

```shell
sudo apt install language-pack-pt -y
```

* Verifique se o pacote de idioma foi instalado

```shell
locale -a
```

## Configuração do idioma e teclado para ``pt_BR`` 
* Escolha o pacote pt_BR.utf8
```shell
sudo localectl set-locale LANG=pt_BR.utf8
sudo localectl set-x11-keymap br abnt2 
localect status # verifique a saída de tela 
```
	
 Figura 3: Configuração do idioma e do layout de teclado para pt-br.

* Reinicie a VM com ``sudo reboot``

[Navegar de volta para roteiro](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/564319c685f6ec504080630dc9989612b4fc7b61/README.md)

