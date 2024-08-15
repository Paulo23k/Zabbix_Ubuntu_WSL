# Zabbix_Ubuntu_WSL
Este repositório contém um guia passo a passo para instalar e configurar o Zabbix no Ubuntu usando o Windows Subsystem for Linux WSL.
1. [Atualizar e Preparar o Sistema](
Abra o Ubuntu no WSL.
Atualize os pacotes e instale as dependências necessárias:
sudo apt update && sudo apt upgrade -y
sudo apt install -y wget gnupg2 software-properties-common
)
2. [Adicionar o Repositório Zabbix](
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-2+ubuntu22.04_all.deb
sudo dpkg -i zabbix-release_6.0-2+ubuntu22.04_all.deb
Em seguida, atualize a lista de pacotes:
sudo apt update
)

4. [Instalar o Servidor Zabbix, Frontend e Agente](sudo apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
)
5. [Configurar o Banco de Dados](sudo apt install -y mariadb-server
)
6. [Importar o Esquema do Banco de Dados](#importar-o-esquema-do-banco-de-dados)
7. [Configurar o Servidor Zabbix](#configurar-o-servidor-zabbix)
8. [Iniciar os Serviços](#iniciar-os-serviços)
9. [Acessar o Frontend do Zabbix](#acessar-o-frontend-do-zabbix)
10. [Configurar o Zabbix](#configurar-o-zabbix)
11. [Comandos Extras](#comandos-extras)
