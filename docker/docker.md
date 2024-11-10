# Guia de Instalação do Docker no Windows e Linux (WSL2)

## Introdução

Este guia detalha como instalar e configurar o Docker no Windows, utilizando duas abordagens: instalando diretamente no Windows ou utilizando o Docker através do **WSL2** (Windows Subsystem for Linux 2). O Docker é uma ferramenta essencial para a criação e execução de ambientes de desenvolvimento isolados, que permite trabalhar com contêineres de forma eficiente. Vamos explorar as melhores práticas, principais comandos e como configurar o Docker para um desenvolvimento ágil e seguro.

## Menu

- [Guia de Instalação do Docker no Windows e Linux (WSL2)](#guia-de-instalação-do-docker-no-windows-e-linux-wsl2)
  - [Introdução](#introdução)
  - [Menu](#menu)
  - [O Que é Docker?](#o-que-é-docker)
  - [Requisitos](#requisitos)
  - [Instalação do Docker no Windows](#instalação-do-docker-no-windows)
  - [Instalação do Docker no Linux via WSL2](#instalação-do-docker-no-linux-via-wsl2)
  - [Configuração do Docker no WSL2](#configuração-do-docker-no-wsl2)
  - [Melhores Práticas para Uso do Docker](#melhores-práticas-para-uso-do-docker)
  - [Principais Comandos Docker](#principais-comandos-docker)
  - [Conclusão](#conclusão)

## O Que é Docker?

O **Docker** é uma plataforma de código aberto que permite a criação, execução e gestão de contêineres. Um contêiner é uma unidade leve e independente que contém tudo o que uma aplicação precisa para rodar, incluindo código, bibliotecas, e dependências. Isso facilita o desenvolvimento, já que o ambiente da aplicação se mantém consistente, seja em sua máquina local ou em servidores de produção.

## Requisitos

- **Windows 10** (versão 2004 ou superior) ou **Windows 11**
- Conta de administrador no sistema
- Conexão com a internet
- **WSL2** habilitado (para instalação no Linux via WSL2)

## Instalação do Docker no Windows

O Docker Desktop é a maneira mais fácil de instalar o Docker diretamente no Windows, possibilitando também a integração com o WSL2. Vamos seguir os passos abaixo:

1. **Baixar o Docker Desktop**
   - Acesse o site oficial do Docker: [Docker Desktop Download](https://www.docker.com/products/docker-desktop)
   - Baixe o instalador e execute-o.

2. **Instalar o Docker Desktop**
   - Siga o assistente de instalação. Durante a instalação, certifique-se de marcar a opção para habilitar o WSL2.

3. **Configurar o Docker Desktop**
   - Após a instalação, abra o Docker Desktop.
   - Vá até as configurações e ative a integração com o WSL2. Isso permitirá que você utilize o Docker no Ubuntu ou em outras distribuições Linux que você tenha instalado no WSL2.

4. **Verificar a Instalação**
   - Para garantir que o Docker foi instalado corretamente, abra o **PowerShell** ou o **Prompt de Comando** e execute:
     ```powershell
     docker --version
     ```

## Instalação do Docker no Linux via WSL2

Se você estiver utilizando o **WSL2** com uma distribuição Linux (por exemplo, Ubuntu), pode instalar o Docker diretamente no ambiente Linux, sem precisar do Docker Desktop.

1. **Atualizar Pacotes**
   - Primeiro, abra o terminal do Ubuntu e atualize os pacotes:
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```

2. **Instalar Dependências do Docker**
   - Instale algumas dependências necessárias:
     ```bash
     sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
     ```

3. **Adicionar o Repositório do Docker**
   - Adicione a chave GPG do Docker:
     ```bash
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
     ```
   - Adicione o repositório oficial do Docker ao APT:
     ```bash
     sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
     ```

4. **Instalar o Docker**
   - Atualize os pacotes e instale o Docker:
     ```bash
     sudo apt update
     sudo apt install docker-ce -y
     ```

5. **Verificar a Instalação**
   - Verifique se o Docker foi instalado corretamente:
     ```bash
     docker --version
     ```

6. **Permitir que seu Usuário Use o Docker sem `sudo`**
   - Adicione seu usuário ao grupo `docker` para não precisar usar `sudo` em cada comando:
     ```bash
     sudo usermod -aG docker $USER
     ```
   - Feche o terminal e abra-o novamente para que as alterações tenham efeito.

## Configuração do Docker no WSL2

Após a instalação, é importante configurar o Docker para funcionar bem com o **WSL2**:

- **Integração com o Docker Desktop**: No Docker Desktop, vá até as configurações e certifique-se de que a integração com o WSL2 está ativada para a distribuição que você deseja usar (ex.: Ubuntu).
- **Configurar o Daemon do Docker**: Caso esteja utilizando diretamente no WSL2, você pode precisar configurar o daemon do Docker para iniciar automaticamente:
  ```bash
  sudo service docker start
  ```

## Melhores Práticas para Uso do Docker

1. **Manter as Imagens Atualizadas**: Sempre verifique se suas imagens estão atualizadas, principalmente para correções de segurança.
   ```bash
   docker pull nome_da_imagem
   ```

2. **Remover Contêineres e Imagens Inúteis**: Para evitar o acúmulo de imagens e contêineres antigos que ocupam espaço desnecessário, utilize:
   ```bash
   docker system prune
   ```

3. **Utilizar `docker-compose` para Orquestração**: Para projetos mais complexos, use o Docker Compose para gerenciar vários contêineres de forma simplificada.

## Principais Comandos Docker

- **Verificar Versão**:
  ```bash
  docker --version
  ```

- **Baixar uma Imagem**:
  ```bash
  docker pull nome_da_imagem
  ```

- **Executar um Contêiner**:
  ```bash
  docker run -d -p 8080:80 nome_da_imagem
  ```
  - **-d**: Executa o contêiner em segundo plano.
  - **-p**: Mapeia a porta do contêiner para uma porta no host.

- **Listar Contêineres Ativos**:
  ```bash
  docker ps
  ```

- **Parar um Contêiner**:
  ```bash
  docker stop ID_do_container
  ```

- **Remover um Contêiner**:
  ```bash
  docker rm ID_do_container
  ```

- **Remover Imagens**:
  ```bash
  docker rmi nome_da_imagem
  ```

## Conclusão

Com este guia, você aprendeu como instalar o Docker tanto diretamente no Windows quanto no Linux via **WSL2**, além de configurar o Docker e seguir melhores práticas para garantir um desenvolvimento mais eficiente e organizado. O Docker é uma ferramenta poderosa que pode facilitar muito a criação de ambientes de desenvolvimento consistentes e seguros.

Para mais informações e documentação oficial, consulte:
- [Documentação oficial do Docker](https://docs.docker.com/)
- [Docker no WSL2](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers)
