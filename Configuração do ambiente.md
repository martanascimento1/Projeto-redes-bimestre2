# Configuração do Ambiente


A ferramenta utilizada para a criação e confifuração das máquinas virtuais será o VirtualBox. Sendo assim, é necessário instalar o aplicativo em seu computador.

Caso ainda não tenha instalado o aplicativo essa ação pode ser realizada pelo link [Download Virtual Box](https://www.virtualbox.org/wiki/Downloads)

Após a instalação, é necessário criar as pastas no computador.

## Pelo terminal do computador

1 - Entrar no teminal do linux (você pode acessá-lo pelo menu de configurações e procurar por "terminal").

2 - Logar no usuário redes. Você pode entrar pelo comando:

##### su redes 

 Após isso, é necessário digitar a senha do usuário.

***usuário: redes***    
***senha: admin@Lab92***

- Observe que o a estrutura básica de comando para mudar de usuário é:

##### su nomeDoUsuário

3 - Agora deve-se acessar a pasta raiz do computador e nela criar as pastas que vão ser utilizadas para armazenamento das VMs e para guardar a imagem.

- Entre na pasta raiz do computador pelo comando:

##### cd /

- Observe que o comando básico para entrar em um diretório é:

##### cd nomeDoDiretório

- Crie a pasta labredes na raiz pelo comando:

##### sudo mkdir labredes

- Para vereficar se a pasta labredes foi criada efetue o seguinte comando no terminal:

##### ls -la

- O comando ls -la lista os arquivos contidos dentro daquele diretório.
- Dentro da pasta labredes crie a pasta images e a pasta VM

##### sudo mkdir images
##### sudo mkdir VM

- Dentro da pasta images, crie outra pasta 'original':

##### sudo mkdir original

- Agora dentro da pasta VM, crie outras pastas com a sua turma. Depois entre na pasta da sua turma e crie uma pasta com o seu nome.
- Ex.: 924/MariaIzabel

##### sudo mkdir suaTurma
##### sudo mkdir seuNome
  
- Ao final teremos uma hierarquia de pastas da seginte forma:
  
**labredes/images/original**
**labredes/VM/<suaTurma>/<seuNome>**
  
 4 - Agora temos que adicionar o usuário aluno ao grupo redes. Isso pode ser realizado pelo comando:
  
 #####  sudo usermod -aG redes aluno
  
 - Após dado o comando acima, realize os outros: 
  
 ##### sudo chown -R nobody:nogroup /labredes
  
 - O comando **chwn** modifica o dono da pasta labredes para o usuario nobody e grupo nogroup
  
 ##### ls -la
  
 ##### sudo chgrp -R redes /labredes
  
 - O comando **chgrp** altera o proprietário de grupo do diretório /labredes para o grupo redes
  
 ##### sudo chmod -R 771 /labredes 
  
 - O comando **chmod** altera as permissões do diretório para escrita pelos membros do grupo
  
 ##### ls -la
  
 ##### getent group
  
 - O comando **getent group** lista grupos
  
 5 - Copiar arquivos de imagens
  
 ## Pelo terminal do computador
  
 - Para copiar os arquivos de imagens dê o sequinte comando:
  
 OBS: é necessário que a máquina de origem dos arquivos esteja ligada para isso.
  
 ##### scp aluno@192.168.101.10:~/Public/iso-images/mini.iso /labredes/images/original
 ##### scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-20.04.4-desktop-amd64.iso /labredes/images/original
 ##### scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-22.04-live-server-amd64.iso /labredes/images/original
  
 - O comando **scp** faz uma cópia de um arquivo em um computador remoto para um diretório em um computador local
  
 - Verifique se os arquivos existem nos diretórios:
  
 ##### ls -la
  
 ## Pelo  programa Nautilus
  
  smb://192.168.101.10/iso-images
- user: aluno, senha: aluno

* copiar os arquivos da pasta public para a pasta  ``/labredes/images/original``
