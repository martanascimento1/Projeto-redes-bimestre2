# Projeto-redes-bimestre2

Repositório para o trabalho das disciplinas de Serviços de Redes e Projeto e Infraestrutura de Redes, cujo objetivo é a configuração e execução de um ambiente de rede virtualizada.

# Grupo 1

**IFAL - Instituto Federal de Educação, Ciência e Tecnológia de Alagoas**
**Campus Arapiraca**

Débora Nycolli Jovino dos Santos

Júlia Victória Rodrigues de Melo

Maria Izabel Lemos da Silva

Marta Mirely Nascimento dos Santos

**4° ano - Curso Técnico em Informática (Turma 924)**

**Orientador: Alaelson Jatobá**

# Objetivo

O principal objetivo do trabalho desenvolvido é realizar uma rede de máquinas virtuais e físicas, entre 8 VMs e 4 computadores. Visando o aprendizado de uma topologia de rede lógica e física, abordando conceitos debatidos em sala de aula, tais como a montagem da prórpria rede física e como o entendimento sobre o funcionamento de uma rede LAN de computadores, em que esses computadores trocam informações.

# Visualização do ambiente de rede
* [Tabela de nomes e IP](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/TabeladenomeseIPs.md)
* [Configuração de hardware](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Configura%C3%A7%C3%A3odehardware.md)
* [Definições dos usuários](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Defini%C3%A7%C3%B5esdeusu%C3%A1rios.md)
* [Topologia física](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Topologiaf%C3%ADsica.md)

# Roteiro
Clique no link para navegar até o roteiro com os comandos utilizados para realizar as etapas da configuração de rede.

* [1. Configuração do ambiente](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Configura%C3%A7%C3%A3odoambiente.md)
* [2. Criando uma rede ponto a ponto com duas máquinas virtuais](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Criandoumaredepontoapontocomduasm%C3%A1quinasvirtuais.md)
* [3. Criando uma rede ponto a ponto física com dois PCs e uma LAN lógica com quatro VMs](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Cria%C3%A7%C3%A3odeumaredepontoapontof%C3%ADsicaentredoisPCseumaLANl%C3%B3gicacom4VMs.md)
* [4. Roteiro SSH Server (VMs Virtual Box e Ubuntu-Server) ](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/RoteiroSSH-Server(VMVirutalBoxeUbuntu-Server).md)
* [5. Acesso SSH com (Host Only) no Virtual Box ](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/AcessoRemotoSSHcom(HostOnly)noVirtualBox.md)
* [6. Configuração estática de nomes](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Configura%C3%A7%C3%A3oest%C3%A1ticadenomes.md)

# Como configurar o teclado da VM para pt-BR?
* [Reconfiguração de teclado para pt-BR ABNT2](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Reconfigura%C3%A7%C3%A3odoteclado.md)

# Testes

* PING

   - [IP](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/TestespingIP.md)
   - [HOSTNAME](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/TestespingFQDN.md)
   - [FQDN](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/TestespingFQDN.md)
   - [ALIASE](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Testespingalises.md)
   
* SSH

   - [IP](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/TestessshIP.md)
   - [HOSTNAME](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Testessshhostname.md)
   - [FQDN](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/TestessshFQDN%20.md)
   - [ALIASE](https://github.com/martanascimento1/Projeto-redes-bimestre2/blob/main/Testessshaliases.md)

# Considerações finais

Ao fim do desenvolvimento do projeto foi possível visualizar um topologia de rede formada por quatro computadores, quatro cabos de rede de par trançado (um quinto com acesso a rede de internet), um switch com 8 domínios de brodcast que trocavam informaçãoes através dos comandos ping e ssh, os quais permitiam uma conexão entre os computadores e as Máquinas Virtuais, podendo assim, acessar todas as máquinas que estavam ligadas a rede.
