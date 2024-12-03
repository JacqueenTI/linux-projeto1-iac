# linux-projeto1-iac
Repositório para os arquivos de script


Projeto INFRAESTRUTURA COMO CÓDIGO

Infraestrutura como código (IaC) é o gerenciamento e provisionamento da infraestrutura por meio de códigos, em vez de processos manuais.

Com a IaC, são criados arquivos de configuração que incluem as especificações da sua infraestrutura, facilitando a edição e distribuição de configurações. Ela também assegura o provisionamento do mesmo ambiente todas as vezes.

O controle de versão é uma parte importante da IaC. Os arquivos de configuração deve pertencer à fonte como qualquer outro código-fonte de software. Ao implantar a infraestrutura cpm código, também é possível separá-la em módulos, que podem ser combinados de diferentes maneiras por meio de automação.

Ao automatizar o provisionamento da infraestrutura com IaC, os desenvolvedores não precisam provisionar e gerenciar manualmente servidores, SO, armazenamento e outros componentes de infraestrutura sempre que criam ou implantam uma aplicação.

DIRETÓRIOS
/publico 		/adm	 		/ven 			/sec

GRUPOS
GRP_ADM		GRP_VEN		GRP_SEC

USUÁRIOS
carlos			debora			josefina
maria			sebastiana		amanda
joao			roberto			rogerio

Definições
Excluir diretórios, arquivos, grupos e usuários criados anteriormente;
Todo provisionamento deve ser feito em um arquivo do tipo Bash Script;
O dono de todos os diretórios criados será o usuário root;
Todos os usuários terão permissão total dentro do diretório publico;
Os usuários de cada grupo terão permissão de leitura, escrita e execução em diretórios de departamentos que eles não pertencem;
Subir arquivo de script criado para a sua conta no GitHub

Excluir diretórios, arquivos, grupos e usuários criados anteriormente;

Consultar diretórios
root@LinuxServer:/# ls -l
Excluir diretórios
root@LinuxServer:/# rm -Rf /Textos/
root@LinuxServer:/# rm -Rf /ven/

Consultar  usuário
root@LinuxServer:/# cat /etc/passwd
Excluir usuários
root@LinuxServer:/# userdel -r joao
root@LinuxServer:/# userdel -r guest
root@LinuxServer:/# userdel -r mariana

Consultar grupos
root@LinuxServer:/# cat /etc/group
Excluir grupos
root@LinuxServer:/# groupdel GRP_ADM
root@LinuxServer:/# groupdel GRP_VEN

Todo provisionamento deve ser feito em um arquivo do tipo Bash Script;

Criar diretório Script
root@LinuxServer:/# mkdir script

Criar arquivo  tipo Bash Scrip
root@LinuxServer:/script# nano iac1.sh

SCRIPT

#!/bin/bash

echo "Criando diretórios..."

mkdir /publico
mkdir /adm
mkdir /ven
mkdir /sec

echo "Criando grupos de usuários..."

groupadd GRP_ADM
groupadd GRP_VEN
groupadd GRP_SEC

echo "Criando usuários..."

useradd carlos -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM
useradd maria -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM
useradd joao -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM

useradd debora -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN 
useradd sebastiana -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN
useradd roberto -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN

useradd josefina -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC
useradd amanda -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC
useradd rogerio -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC

echo "Especificando permissões dos diretórios"

chown root:GRP_ADM /adm
chown root:GRP_VEN /ven
chown root:GRP_SEC /sec

chmod 770 /adm
chmod 770 /ven
chmod 770 /sec
chmod 777 /publico

echo "FIM"
Executar o script criado
root@LinuxServer:/script# chmod +x iac1.sh
root@LinuxServer:/script# ./iac1.sh
