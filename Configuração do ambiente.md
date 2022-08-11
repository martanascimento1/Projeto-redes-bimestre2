# Configuração do Ambiente


A ferramenta utilizada para a criação e confifuração das máquinas virtuais será o VirtualBox. Sendo assim, é necessário instalar o aplicativo em seu computador.

Caso ainda não tenha instalado o aplicativo essa ação pode ser realizada pelo link [Download Virtual Box](https://www.virtualbox.org/wiki/Downloads)

Após a instalação, é necessário criar as pastas no computador.

## Pelo terminal do computador

1 - Entrar no teminal do linux (você pode acessá-lo pelo menu de configurações e procurar por "terminal").

2 - Logar no usuário redes. Você pode entrar pelo comando:

```shell
su redes
```
![Figura 1: Logando no usuário redes com o comando "su".](https://user-images.githubusercontent.com/98924290/183898793-dc7d84a8-7a30-43d2-ba81-4942b2347bcf.jpeg)

 Após isso, é necessário digitar a senha do usuário.

***usuário: redes***    
***senha: admin@Lab92***

- Observe que o a estrutura básica de comando para mudar de usuário é:

```shell
su nomeDoUsuário
```
3 - Agora deve-se acessar a pasta raiz do computador e nela criar as pastas que vão ser utilizadas para armazenamento das VMs e para guardar a imagem.

- Entre na pasta raiz do computador pelo comando:

```shell
cd /
```
![figura 2: Entrando na pasta raiz do computador.](https://user-images.githubusercontent.com/98924290/183899295-8c50c53c-b3ba-4d87-8904-13fdd01b6715.png)

- Observe que o comando básico para entrar em um diretório é:

```shell
cd nomeDoDiretório
```
- Crie a pasta labredes na raiz pelo comando:

```shell
sudo mkdir labredes
```
![mkdir labredes](https://user-images.githubusercontent.com/98924290/183906175-9db52f98-cb48-46fc-8589-e495ee8fb345.jpeg)

- Para vereficar se a pasta labredes foi criada efetue o seguinte comando no terminal:

```shell
ls -la
```
- O comando ls -la lista os arquivos contidos dentro daquele diretório.

- Dentro da pasta labredes crie a pasta images e a pasta VM

```shell
sudo mkdir images
```
![WhatsApp Image 2022-08-09 at 13 22 03 (2)](https://user-images.githubusercontent.com/98924290/183906258-9a7dbb02-2200-47be-bfec-873c93c759e4.jpeg)

- Dentro da pasta images, crie outra pasta 'original':

```shell
sudo mkdir original
```
![WhatsApp Image 2022-08-09 at 13 22 03 (3)](https://user-images.githubusercontent.com/98924290/183906295-07ad6b53-be07-42ba-951c-930e34381571.jpeg)

- Dentro da pasta labredes crie a pasta VM

```shell
sudo mkdir VM
```
![WhatsApp Image 2022-08-09 at 13 22 03 (4)](https://user-images.githubusercontent.com/98924290/183906337-a542f203-030f-4eb6-ae5e-11faa4625e31.jpeg)

- Agora dentro da pasta VM, crie outras pastas com a sua turma. Depois entre na pasta da sua turma e crie uma pasta com o seu nome.
- Ex.: 924/MariaIzabel

```shell
sudo mkdir suaTurma
```
![WhatsApp Image 2022-08-09 at 13 22 04](https://user-images.githubusercontent.com/98924290/183906673-59a3e64c-f87c-43d5-a844-663ca84a1155.jpeg)

```shell
su mkdir seuNome
```
![WhatsApp Image 2022-08-09 at 13 22 04 (1)](https://user-images.githubusercontent.com/98924290/183906704-4fd1ed47-de97-40f3-baaa-faf46d413286.jpeg)

- Ao final teremos uma hierarquia de pastas da seguinte forma:
  
**labredes/images/original**

**labredes/VM/suaTurma/seuNome**
  
 4 - Agora temos que adicionar o usuário aluno ao grupo redes. Isso pode ser realizado pelo comando:
 
 ```shell
sudo usermod -aG redes aluno
```
 ![WhatsApp Image 2022-08-09 at 13 22 04 (2)](https://user-images.githubusercontent.com/98924290/183907963-35efb58d-d1e0-41c1-adda-df6969c5c9c0.jpeg)

 - Após dado o comando acima, realize os outros: 
 
 ```shell
sudo chwn -R nobody:nogroup /labredes
```
![WhatsApp Image 2022-08-09 at 13 22 04 (3)](https://user-images.githubusercontent.com/98924290/183908240-8fd39af9-b23f-43ac-9371-73136faa7d05.jpeg)

 - O comando **chwn** modifica o dono da pasta labredes para o usuario nobody e grupo nogroup
 
 ```shell
ls -la
```
![WhatsApp Image 2022-08-09 at 13 22 05 (2)](https://user-images.githubusercontent.com/98924290/183909198-71de72eb-5033-450e-864b-bdcac6b80d63.jpeg)

```shell
sudo chgrp -R redes /labredes
```
 
![WhatsApp Image 2022-08-09 at 13 22 05](https://user-images.githubusercontent.com/98924290/183908419-079ad288-75f5-41f4-b65e-38e20e7ea013.jpeg)

 - O comando **chgrp** altera o proprietário de grupo do diretório /labredes para o grupo redes
 
 ```shell
sudo chmod -R 771 /labredes
```
![WhatsApp Image 2022-08-09 at 13 22 05 (1)](https://user-images.githubusercontent.com/98924290/183908501-a16df337-3ced-4abc-a2e9-0dcb007f11d8.jpeg)

 - O comando **chmod** altera as permissões do diretório para escrita pelos membros do grupo

```shell
ls -la
```
```shell
getent group
```
  ![WhatsApp Image 2022-08-09 at 13 22 05 (3)](https://user-images.githubusercontent.com/98924290/183907018-55da3c9f-7d0a-461e-9a42-63e2707b5e61.jpeg)
 
 - O comando **getent group** lista grupos

 5 - Copiar arquivos de imagens
  
 ## Pelo terminal do computador
  
 - Para copiar os arquivos de imagens dê o sequinte comando:
  
 OBS: é necessário que a máquina de origem dos arquivos esteja ligada para isso.
 
 ```shell
su nomeDoUsuário
```
 
![WhatsApp Image 2022-08-09 at 13 22 06 (1)](https://user-images.githubusercontent.com/98924290/183908820-0f58cb22-2ed6-444d-89c9-4224141e7aee.jpeg)

 ```shell
scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-20.04.4-desktop-amd64.iso /labredes/images/original
```
 ```shell
scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-20.04.4-desktop-amd64.iso /labredes/images/original
```
 ```shell
scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-22.04-live-server-amd64.iso /labredes/images/original
```
 - O comando **scp** faz uma cópia de um arquivo em um computador remoto para um diretório em um computador local
  
 - Verifique se os arquivos existem nos diretórios:
 
 ```shell
ls -la
```
 ## Pelo  programa Nautilus
  
  smb://192.168.101.10/iso-images
- user: aluno, senha: aluno

* copiar os arquivos da pasta public para a pasta  /labredes/images/original
