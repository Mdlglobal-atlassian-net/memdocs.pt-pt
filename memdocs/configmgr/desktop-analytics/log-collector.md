---
title: Recoletor de registos
titleSuffix: Configuration Manager
description: Utilize a ferramenta de colecionador de registos para ajudar a resolver problemas no Desktop Analytics
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c101e45eb794ff73599e9612a5aec991be01ae6c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718883"
---
# <a name="desktop-analytics-log-collector"></a>Colecionador de registos desktop Analytics

Começando na versão 1906 do Gestor de Configuração, utilize a ferramenta **DesktopAnalyticsLogsCollector.ps1** do diretor de instalação do Gestor de Configuração para ajudar a resolver problemas de inscrição no dispositivo Desktop Analytics. Executa alguns passos básicos de resolução de problemas e recolhe os registos relevantes num único diretório de trabalho. Pode partilhar este conteúdo com o suporte da Microsoft.


## <a name="prerequisites"></a>Pré-requisitos

- Um cliente desktop Analytics com windows 10, Windows 8.1 ou Windows 7 com Service Pack 1

- Execute o script no dispositivo como um utilizador administrativo, e **Corra como Administrador**.

    > [!Tip]
    > Pode utilizar a funcionalidade **scripts** do Gestor de Configuração com esta ferramenta. Para mais informações, consulte [exemplo 5: Desdobrar script através de **Scripts**de Gestor](#bkmk_ex5)de Configuração .

- Para o Windows 7 com o Service Pack 1, a versão PowerShell 4.0 ou posterior
    - [.NET versão-quadro 4.6 ou posterior](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [versão 4.0](https://support.microsoft.com/help/2819745) (aka.ms/wmf4download) ou [versão 5.1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.ms/wmf5download)

## <a name="usage"></a>Utilização

Obtenha o script do conteúdo de instalação do Gestor de Configuração:`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parâmetros

### `-LogPath`

Especifica um caminho local ou unc para colocar o registo e outros ficheiros de saída.

**Valores:**

- Percurso local (comprimento máximo = 130), por exemplo:`c:\myfolder`

- Caminho da UnC (comprimento máximo = 130), por exemplo:`\\myserver\myfolder`

**Tipo**: Corda

**Posição**: 1

**Valor predefinido**: `$Env:SystemDrive\M365AnalyticsLogs` (Quando este parâmetro é espaço nulo, vazio ou branco, o script cria a pasta M365AnalyticsLogs sob a unidade do sistema.)

### `-LogMode`

Especifica o nível verboso dos troncos.

**Valores:**

- `0`: Registar mensagens de script apenas para a janela de comando PowerShell.

- `1`: Inicie as mensagens de script em ambos os ficheiros de registo sob a pasta de saída e a janela de comando PowerShell.

- `2`: Inicie sessão de mensagens de script para registar ficheiros apenas na pasta de saída.

**Tipo**: Int16

**Posição**: 2

**Valor predefinido**: `1` (Registar mensagens de script tanto no ficheiro de registo como na janela de comando PowerShell.)

### `-CollectNetTrace`

Especifica se o script recolhe o traço da rede.

**Valores:**

- `0`: Não ative o rastreio da rede.

- `1`(qualquer valor não nulo): Ativar o rastreio da rede e recolher resultados.

**Tipo**: Int16

**Posição**: 3

**Valor predefinido**: `0` (Não ative o rastreio da rede)

### `-CollectUTCTrace`

Especifica se o script recolhe o traço DO Windows UTC e executa o diagnóstico de conectividade.

**Valores:**

- `0`: Não ative o rastreio UTC nem faça o diagnóstico de conectividade.

- `1`(qualquer valor não nulo zero): Ativar o traço UTC, executar o diagnóstico de conectividade e recolher resultados.

**Tipo**: Int16

**Posição**: 4

**Valor predefinido**: `0` (Não ative o rastreio utc ou faça o diagnóstico de conectividade)


## <a name="output"></a>Saída

O script cria uma pasta de *trabalho* sob o caminho especificado. Por exemplo, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss.** Coloca todos os seus ficheiros de saída nesta pasta de trabalho.

Se ativar o script para escrever num ficheiro de *registo,* gera um na pasta de trabalho. Por exemplo, **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss.txt**.

O script também gera outros *ficheiros de diagnóstico* na pasta de trabalho. Por exemplo:

- `installedKBs.txt`: uma lista de atualizações do Windows instaladas no dispositivo
- `appcompat`: dados de compatibilidade de aplicações
- `Reg*.txt`: uma série de ficheiros com dados exportados do Registo do Windows


## <a name="examples"></a>Exemplos

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a>Exemplo 1: Executar script através da janela de comando PowerShell com valores predefinidos

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a>Exemplo 2: Executar script via janela de comando PowerShell com parâmetros especificados

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a>Exemplo 3: Executar script via janela de comando PowerShell com parâmetros especificados na posição

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a>Exemplo 4: Executar script através da janela de comando PowerShell com parâmetro siespecificado e mensagens verbosas

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a>Exemplo 5: Implementar script através de **scripts** de gestor de configuração

Para mais informações, consulte [Criar e executar scripts PowerShell a partir da consola Do Gestor de Configuração](../apps/deploy-use/create-deploy-scripts.md).

DesktopAnalyticsLogsCollector.ps1 é assinado digitalmente pela Microsoft. Pode ser necessário adicionar o seu certificado de assinatura de código Microsoft como um Editor Fidedigno no dispositivo alvo.

1. Abra as propriedades do script no Windows Explorer. Mude para o separador **Assinaturas Digitais** e selecione **Detalhes**.

2. No separador **Geral,** selecione **'Ver Certificado**' .

    > [!Note]
    > Para distribuir o certificado através de outros mecanismos, primeiro exporte o certificado para um ficheiro. Vá ao separador **Detalhes** e selecione **Copiar para Arquivar**.

3. Selecione **Certificado de Instalação**. Importar o certificado, colocando-o na loja **Trust Publishers.**


## <a name="see-also"></a>Consulte também

- [Resolver problemas da Análise de Computadores](troubleshooting.md)

- [Criar e executar scripts PowerShell a partir da consola De Configuração Manager](../apps/deploy-use/create-deploy-scripts.md)
