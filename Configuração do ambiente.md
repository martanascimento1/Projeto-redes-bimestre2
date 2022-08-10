# Configuração do Ambiente


A ferramenta utilizada para a criação e confifuração das máquinas virtuais será o VirtualBox. Sendo assim, é necessário instalar o aplicativo em seu computador.

Caso ainda não tenha instalado o aplicativo essa ação pode ser realizada pelo link [Download Virtual Box](https://www.virtualbox.org/wiki/Downloads)

Após a instalação, é necessário criar as pastas no computador.

## Pelo terminal do computador

1 - Entrar no teminal do linux (você pode acessá-lo pelo menu de configurações e procurar por "terminal").

2 - Logar no usuário redes. Você pode entrar pelo comando:

##### su redes

![Figura 1: Logando no usuário redes com o comando "su".](https://user-images.githubusercontent.com/98924290/183898793-dc7d84a8-7a30-43d2-ba81-4942b2347bcf.jpeg)

 Após isso, é necessário digitar a senha do usuário.

***usuário: redes***    
***senha: admin@Lab92***

- Observe que o a estrutura básica de comando para mudar de usuário é:

##### su nomeDoUsuário

3 - Agora deve-se acessar a pasta raiz do computador e nela criar as pastas que vão ser utilizadas para armazenamento das VMs e para guardar a imagem.

- Entre na pasta raiz do computador pelo comando:

##### cd /

![figura 2: Entrando na pasta raiz do computador.](https://user-images.githubusercontent.com/98924290/183899295-8c50c53c-b3ba-4d87-8904-13fdd01b6715.png)

- Observe que o comando básico para entrar em um diretório é:

##### cd nomeDoDiretório

- Crie a pasta labredes na raiz pelo comando:

##### sudo mkdir labredes

![mkdir labredes](https://user-images.githubusercontent.com/98924290/183906175-9db52f98-cb48-46fc-8589-e495ee8fb345.jpeg)

- Para vereficar se a pasta labredes foi criada efetue o seguinte comando no terminal:

##### ls -la

![ls -la labredes](https://user-images.githubusercontent.com/98924290/183906211-b94fbe38-4a92-41b9-8925-268a4921fdf2.jpeg)

- O comando ls -la lista os arquivos contidos dentro daquele diretório.

- Dentro da pasta labredes crie a pasta images e a pasta VM

##### sudo mkdir images

![WhatsApp Image 2022-08-09 at 13 22 03 (1)](https://user-images.githubusercontent.com/98924290/183906253-797dcd18-e695-4a18-add7-f3ad779bce49.jpeg)

![WhatsApp Image 2022-08-09 at 13 22 03 (2)](https://user-images.githubusercontent.com/98924290/183906258-9a7dbb02-2200-47be-bfec-873c93c759e4.jpeg)

- Dentro da pasta images, crie outra pasta 'original':

##### sudo mkdir original

![WhatsApp Image 2022-08-09 at 13 22 03 (3)](https://user-images.githubusercontent.com/98924290/183906295-07ad6b53-be07-42ba-951c-930e34381571.jpeg)

- Dentro da pasta labredes crie a pasta VM

##### sudo mkdir VM

![WhatsApp Image 2022-08-09 at 13 22 03 (4)](https://user-images.githubusercontent.com/98924290/183906337-a542f203-030f-4eb6-ae5e-11faa4625e31.jpeg)

- Agora dentro da pasta VM, crie outras pastas com a sua turma. Depois entre na pasta da sua turma e crie uma pasta com o seu nome.
- Ex.: 924/MariaIzabel

##### sudo mkdir suaTurma

![WhatsApp Image 2022-08-09 at 13 22 04 (1)](https://user-images.githubusercontent.com/98924290/183906440-1d6c9c3c-cadd-4d26-b645-40fdb5a19119.jpeg)

##### sudo mkdir seuNome

![figura 10: Criando a pasta com o nome do estudante na pasta da turma.](https://user-images.githubusercontent.com/98924290/183901449-114be008-9a47-4d65-b7fa-aebad27a3463.jpeg)

- Ao final teremos uma hierarquia de pastas da seguinte forma:
  
**labredes/images/original**

**labredes/VM/suaTurma/seuNome**
  
 4 - Agora temos que adicionar o usuário aluno ao grupo redes. Isso pode ser realizado pelo comando:
  
 #####  sudo usermod -aG redes aluno
 
  ![figura 11: Adicionando o usuário alunos ao grupo redes.](https://user-images.githubusercontent.com/98924290/183901741-3a13493d-1284-495d-b90e-0ed459e87e04.jpeg)
  
 - Após dado o comando acima, realize os outros: 
  
 ##### sudo chown -R nobody:nogroup /labredes
 
 ![figura 12: Modificando o proprietário da pasta labredes.](https://user-images.githubusercontent.com/98924290/183902549-36e546ae-c2de-41af-952d-ebe527ad176d.jpeg)

 - O comando **chwn** modifica o dono da pasta labredes para o usuario nobody e grupo nogroup
  
 ##### ls -la
 
 ![figura 13](https://user-images.githubusercontent.com/98924290/183904132-d0631169-07a5-4d2a-b902-482376c12705.jpeg)

 ##### sudo chgrp -R redes /labredes
 
  ![figura 14: Modificando o proprietário do grupo /labredes para o grupo redes.](https://user-images.githubusercontent.com/98924290/183902905-c9548514-5005-4f09-83b6-409a8b236661.jpeg)

 - O comando **chgrp** altera o proprietário de grupo do diretório /labredes para o grupo redes
  
 ##### sudo chmod -R 771 /labredes 
 
 ![figura 15: Alterando as permissões do diretório. ](https://user-images.githubusercontent.com/98924290/183903160-8b4715ae-9050-4087-8a6c-aa684f7f996b.jpeg)

 - O comando **chmod** altera as permissões do diretório para escrita pelos membros do grupo
  
 ##### ls -la
  
 ##### getent group
 
![figura 16](https://user-images.githubusercontent.com/98924290/183904448-54744eaa-332e-4156-a230-1990a20e107d.jpeg)
 
 - O comando **getent group** lista grupos
  
 5 - Copiar arquivos de imagens
  
 ## Pelo terminal do computador
  
 - Para copiar os arquivos de imagens dê o sequinte comando:
  
 OBS: é necessário que a máquina de origem dos arquivos esteja ligada para isso.
  
 ##### scp aluno@192.168.101.10:~/Public/iso-images/mini.iso /labredes/images/original
 
 ![figura 17: Copiando os arquivos de images](https://user-images.githubusercontent.com/98924290/183905159-1a0d27dc-55a5-4af2-9e69-745ec79ff3a3.jpeg)

 ##### scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-20.04.4-desktop-amd64.iso /labredes/images/original
 ##### scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-22.04-live-server-amd64.iso /labredes/images/original
 
 - O comando **scp** faz uma cópia de um arquivo em um computador remoto para um diretório em um computador local
  
 - Verifique se os arquivos existem nos diretórios:
  
 ##### ls -la
  
 ## Pelo  programa Nautilus
  
  smb://192.168.101.10/iso-images
- user: aluno, senha: aluno

* copiar os arquivos da pasta public para a pasta  /labredes/images/original
