# Guia de Instalação do WSL2 no Windows

Este guia descreve como instalar o **WSL2 (Windows Subsystem for Linux 2)** no Windows passo a passo.

## Requisitos

- **Windows 10** (versão 2004 ou superior) ou **Windows 11**
- Conta de administrador no sistema
- Conexão com a internet para baixar as atualizações necessárias

## Passo 1: Habilitar o WSL

Abra o **PowerShell** como **administrador** e execute o seguinte comando para habilitar o WSL:

```powershell
wsl --install
```

Este comando instala o WSL e define o **WSL2** como a versão padrão. Ele também instala a distribuição Linux Ubuntu por padrão.

Caso deseje apenas habilitar o recurso, sem instalar automaticamente uma distribuição, execute:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

## Passo 2: Habilitar a Plataforma de Máquina Virtual

Habilite a **Plataforma de Máquina Virtual**, necessária para o WSL2. No **PowerShell** como administrador, execute:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Após a execução, reinicie o computador para aplicar as alterações.

## Passo 3: Definir o WSL2 como Versão Padrão

Abra o **PowerShell** como administrador e defina o **WSL2** como a versão padrão para novas distribuições:

```powershell
wsl --set-default-version 2
```

## Passo 4: Instalar uma Distribuição Linux

Para instalar uma distribuição Linux, abra a **Microsoft Store** e procure por uma distribuição de sua escolha, como **Ubuntu**, **Debian** ou **Fedora**.