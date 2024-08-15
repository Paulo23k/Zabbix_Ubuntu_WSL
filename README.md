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

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y wget gnupg2 software-properties-common
