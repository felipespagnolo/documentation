# Guia de Instalação do WSL2 no Windows

## Introdução

O **Windows Subsystem for Linux 2 (WSL2)** é uma tecnologia que permite aos usuários do Windows executar um ambiente Linux nativo, incluindo distribuições como Ubuntu, diretamente no Windows, sem a necessidade de uma máquina virtual completa. Isso facilita o uso de ferramentas de desenvolvimento Linux em um ambiente Windows, integrando ambos os sistemas de maneira eficiente. Este guia descreve como instalar o **WSL2** no Windows, passo a passo.

## Menu

- [Guia de Instalação do WSL2 no Windows](#guia-de-instalação-do-wsl2-no-windows)
  - [Introdução](#introdução)
  - [Menu](#menu)
  - [Requisitos](#requisitos)
  - [Passo 1: Verificar a Compatibilidade](#passo-1-verificar-a-compatibilidade)
  - [Passo 2: Habilitar o WSL](#passo-2-habilitar-o-wsl)
  - [Passo 3: Habilitar a Plataforma de Máquina Virtual](#passo-3-habilitar-a-plataforma-de-máquina-virtual)
  - [Passo 4: Definir o WSL2 como Versão Padrão](#passo-4-definir-o-wsl2-como-versão-padrão)
  - [Passo 5: Instalar uma Distribuição Linux](#passo-5-instalar-uma-distribuição-linux)
  - [Passo 6: Verificar a Versão do WSL](#passo-6-verificar-a-versão-do-wsl)
  - [Passo 7: Iniciar a Distribuição Linux](#passo-7-iniciar-a-distribuição-linux)
  - [Passo 8: Atualizar Pacotes do Sistema](#passo-8-atualizar-pacotes-do-sistema)
  - [Passo 9: Acessar o Sistema de Arquivos do Windows e Linux](#passo-9-acessar-o-sistema-de-arquivos-do-windows-e-linux)
  - [Passo 10: Atualizar o Kernel do WSL2 (Opcional)](#passo-10-atualizar-o-kernel-do-wsl2-opcional)
  - [Passo 11: Instalar Ferramentas Básicas de Desenvolvimento (Opcional)](#passo-11-instalar-ferramentas-básicas-de-desenvolvimento-opcional)
  - [Conclusão](#conclusão)

## Requisitos

- **Windows 10** (versão 2004 ou superior) ou **Windows 11**
- Conta de administrador no sistema
- Conexão com a internet para baixar as atualizações necessárias

## Passo 1: Verificar a Compatibilidade

Antes de habilitar o WSL, é importante verificar se sua versão do Windows é compatível. Para isso, abra o **Prompt de Comando** ou **PowerShell** e execute:

```powershell
systeminfo | find "Versão do SO"
```

Verifique se sua versão é igual ou superior à versão 2004 do Windows 10.

## Passo 2: Habilitar o WSL

Abra o **PowerShell** como **administrador** e execute o seguinte comando para habilitar o WSL:

```powershell
wsl --install
```

Este comando instala o WSL e define o **WSL2** como a versão padrão. Ele também instala a distribuição Linux Ubuntu por padrão.

- **wsl**: Refere-se ao Windows Subsystem for Linux.
- **--install**: Instrução para instalar o WSL com a versão mais recente (WSL2) e uma distribuição Linux padrão (Ubuntu).

Caso deseje apenas habilitar o recurso, sem instalar automaticamente uma distribuição, execute:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

Após habilitar o WSL, é recomendável **reiniciar o sistema** para garantir que todas as alterações sejam aplicadas corretamente.

## Passo 3: Habilitar a Plataforma de Máquina Virtual

Habilite a **Plataforma de Máquina Virtual**, necessária para o WSL2. No **PowerShell** como administrador, execute:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Após a execução, reinicie o computador para aplicar as alterações.

## Passo 4: Definir o WSL2 como Versão Padrão

Abra o **PowerShell** como administrador e defina o **WSL2** como a versão padrão para novas distribuições:

```powershell
wsl --set-default-version 2
```

- **--set-default-version 2**: Define que todas as novas distribuições Linux instaladas utilizarão a versão 2 do WSL.

## Passo 5: Instalar uma Distribuição Linux

Para instalar uma distribuição Linux, abra a **Microsoft Store** e procure por uma distribuição de sua escolha, como **Ubuntu**, **Debian** ou **Fedora**.

1. Abra a **Microsoft Store**.
2. Pesquise por "Ubuntu" (ou qualquer outra distribuição desejada).
3. Clique em **Obter** para instalar a distribuição.

Após a instalação, abra a distribuição para concluir a configuração inicial, criando um usuário e senha.

Para definir uma distribuição específica como padrão, você pode usar:

```powershell
wsl --set-default <nome_da_distribuicao>
```

Substitua `<nome_da_distribuicao>` pelo nome da distribuição desejada.

## Passo 6: Verificar a Versão do WSL

Para verificar qual versão do WSL sua distribuição está utilizando, execute no **PowerShell**:

```powershell
wsl --list --verbose
```

- **--list** ou **-l**: Lista todas as distribuições Linux instaladas no sistema.
- **--verbose** ou **-v**: Mostra detalhes adicionais, como a versão do WSL utilizada por cada distribuição.

Este comando mostrará todas as distribuições instaladas e suas respectivas versões (1 ou 2).

Caso queira mudar a versão de uma distribuição específica para o WSL2, execute:

```powershell
wsl --set-version <nome_da_distribuicao> 2
```

- **--set-version**: Define a versão do WSL para uma distribuição específica.
- **<nome_da_distribuicao>**: Substitua pelo nome da distribuição que deseja alterar (ex.: `Ubuntu`).

Exemplo:

```powershell
wsl --set-version Ubuntu 2
```

## Passo 7: Iniciar a Distribuição Linux

Para iniciar a distribuição Linux instalada (como o Ubuntu), você pode usar o comando:

```powershell
wsl -d Ubuntu
```

- **-d** ou **--distribution**: Especifica qual distribuição Linux você deseja iniciar. Neste exemplo, estamos iniciando o Ubuntu.

Outra maneira de iniciar o Ubuntu é simplesmente digitar `wsl` no **PowerShell** ou **Prompt de Comando**, o que iniciará a distribuição padrão (se você tiver apenas uma, será o Ubuntu).

## Passo 8: Atualizar Pacotes do Sistema

Depois de iniciar o Ubuntu pela primeira vez, é recomendável atualizar os pacotes do sistema para garantir que tudo esteja na versão mais recente:

1. Execute os seguintes comandos no terminal do Ubuntu:

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

   - **sudo**: Permite executar comandos como administrador.
   - **apt update**: Atualiza a lista de pacotes disponíveis.
   - **apt upgrade -y**: Atualiza todos os pacotes instalados para a versão mais recente. O `-y` confirma automaticamente as atualizações.

## Passo 9: Acessar o Sistema de Arquivos do Windows e Linux

No WSL2, você pode acessar os arquivos do Windows a partir do Linux e vice-versa:

- Para acessar arquivos do Windows no Linux, utilize o caminho `/mnt/c/...`. Por exemplo:

  ```bash
  cd /mnt/c/Users/SeuUsuario/Documentos
  ```

- Para acessar arquivos do Linux no Windows, você pode usar o Explorador de Arquivos do Windows e digitar na barra de endereços:

  ```
  \wsl$\Ubuntu
  ```

Isso permite navegar pelos arquivos da distribuição Ubuntu diretamente do Windows.

## Passo 10: Atualizar o Kernel do WSL2 (Opcional)

Para garantir que você tenha a última versão do kernel do WSL2, baixe e instale o pacote de atualização do kernel a partir do site oficial da [Microsoft WSL2 Kernel Update](https://aka.ms/wsl2kernel).

## Passo 11: Instalar Ferramentas Básicas de Desenvolvimento (Opcional)

Para facilitar o desenvolvimento, você pode instalar algumas ferramentas básicas no Ubuntu:

```bash
sudo apt install git curl -y
```

- **git**: Sistema de controle de versão.
- **curl**: Ferramenta para transferir dados de ou para um servidor.

## Conclusão

Com esses passos, você deve ter o **WSL2** instalado e configurado no seu sistema Windows, pronto para usar uma distribuição Linux. O WSL2 oferece uma excelente forma de trabalhar com ferramentas e tecnologias Linux diretamente no Windows, facilitando o desenvolvimento e a integração entre os dois sistemas.

Para mais informações, consulte:
- [Documentação oficial do WSL](https://docs.microsoft.com/pt-br/windows/wsl/)
- [Guia para Iniciantes no WSL](https://docs.microsoft.com/pt-br/windows/wsl/basic-commands)
