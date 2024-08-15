# Zabbix no Ubuntu (WSL) - Passo a Passo

Este repositório contém um guia passo a passo para instalar e configurar o Zabbix no Ubuntu usando o Windows Subsystem for Linux (WSL).

## Índice

1. [Atualizar e Preparar o Sistema](#atualizar-e-preparar-o-sistema)
2. [Adicionar o Repositório Zabbix](#adicionar-o-repositório-zabbix)
3. [Instalar o Servidor Zabbix, Frontend e Agente](#instalar-o-servidor-zabbix-frontend-e-agente)
4. [Configurar o Banco de Dados](#configurar-o-banco-de-dados)
5. [Importar o Esquema do Banco de Dados](#importar-o-esquema-do-banco-de-dados)
6. [Configurar o Servidor Zabbix](#configurar-o-servidor-zabbix)
7. [Iniciar os Serviços](#iniciar-os-serviços)
8. [Acessar o Frontend do Zabbix](#acessar-o-frontend-do-zabbix)
9. [Configurar o Zabbix](#configurar-o-zabbix)
10. [Comandos Extras](#comandos-extras)

## Atualizar e Preparar o Sistema

Abra o Ubuntu no WSL.

Atualize os pacotes e instale as dependências necessárias:
````
sudo apt update && sudo apt upgrade -y
sudo apt install -y wget gnupg2 software-properties-common
````
## Adicionar o Repositório Zabbix

Importe a chave GPG do Zabbix:
```
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-2+ubuntu22.04_all.deb
sudo dpkg -i zabbix-release_6.0-2+ubuntu22.04_all.deb
```
Em seguida, atualize a lista de pacotes:
```
sudo apt update
```
## Instalar o Servidor Zabbix, Frontend e Agente
```
sudo apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```
## Configurar o Banco de Dados

Instale o MariaDB:
```
sudo apt install -y mariadb-server
```
Inicie o serviço MariaDB:
```
sudo systemctl start mariadb
```
Crie o banco de dados e o usuário para o Zabbix:
```
sudo mysql -u root -p
```
Dentro do MySQL:
```
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER 'zabbix'@'localhost' IDENTIFIED BY 'sua_senha';
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
## Importar o Esquema do Banco de Dados
```
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```
## Configurar o Servidor Zabbix

Edite o arquivo de configuração do Zabbix:
```
sudo nano /etc/zabbix/zabbix_server.conf
```
Encontre a linha DBPassword e adicione a senha do banco de dados que você criou:
```
DBPassword=sua.senha
(Não esqueça de descomentar a linha.)
```
## Iniciar os Serviços

Inicie os serviços do Zabbix:
```
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
```
## Acessar o Frontend do Zabbix
```
No navegador, acesse http://seuip/zabbix ou seuip/zabbix
```
OBS: Se der um erro de linguagem no WSL, que é comum, basta rodar esses comandos:
```
locale-gen pt_BR.UTF-8
update-locale
sudo systemctl restart apache2
```
## Comandos Extras
Para visualizar os usuários no MariaDB:
```
SELECT user, host FROM mysql.user;
```
Login: Admin
Senha: zabbix

SEJA FELIZ 🫡
