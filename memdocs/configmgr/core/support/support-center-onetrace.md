---
title: OneTrace do Centro de Suporte (Pré-visualização)
titleSuffix: Configuration Manager
description: OneTrace é um novo espectador de log com Centro de Suporte que tem melhorias sobre CMTrace.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723111"
---
# <a name="support-center-onetrace-preview"></a>OneTrace do Centro de Suporte (Pré-visualização)

<!--3555962-->

A partir da versão 1906, o OneTrace é um novo espectador de log com Support Center. Funciona da mesma forma com a CMTrace, com as seguintes melhorias:

- Uma vista atabáuada
- Janelas dockable
- Capacidades de pesquisa melhoradas
- Capacidade de ativar filtros sem sair da vista de registo
- Scrollbar sugere identificar rapidamente aglomerados de erros
- Abertura de registo rápido para ficheiros grandes

[![Screenshot do espectador de registo OneTrace](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

O OneTrace trabalha com muitos tipos de ficheiros de registo, tais como:

- Registos de clientes do Gestor de Configuração
- Registos de servidor do Gestor de Configuração
- Mensagens de estado
- Ficheiro de registo ETW do Windows Update no Windows 10
- Ficheiro de registo do Windows Update no Windows 7 & Windows 8.1

## <a name="prerequisites"></a>Pré-requisitos

- .NET Versão-quadro 4.6 ou posterior

## <a name="install"></a>Instalar

O OneTrace instala-se com o Centro de Suporte. Encontre o instalador do Centro de Suporte `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`no servidor do site no seguinte caminho: .

Por predefinição, a aplicação `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`OneTrace está instalada em .

> [!Note]  
> O Centro de Suporte e o OneTrace utilizam a Windows Presentation Foundation (WPF). Este componente não está disponível no Windows PE. Continue a utilizar o CMTrace em imagens de arranque com implementações de sequência de tarefas.  

## <a name="log-groups"></a>Grupos de registo

<!--5559993-->

A partir da versão 2002, o OneTrace suporta grupos de registo personalizáveis, semelhantes à funcionalidade no Support Center. Os grupos de registo permitem-lhe abrir todos os ficheiros de registo para um único cenário. O OneTrace inclui atualmente grupos para os seguintes cenários:

- Gestão de aplicações
- Definições de conformidade (também referidas como Gestão de Configuração Desejada)
- Atualizações de software

Para mostrar grupos de registo, vá ao menu **'Ver'** e selecione **grupos de registo**.

![Screenshot do grupo de log OneTrace para gestão de aplicações](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Personalizar grupos de registo

Pode personalizar estes grupos modificando a configuração XML, que `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`por padrão está no seguinte caminho: .

O exemplo seguinte é uma parte do ficheiro de configuração predefinido:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

O `GroupType` imóvel aceita os seguintes valores:

- `0`: Desconhecido ou outro
- `1`: Registos de clientes do Gestor de Configuração
- `2`: Registos de servidordo do Gestor de Configuração

A `GroupFilePath` propriedade pode incluir um caminho explícito para os ficheiros de registo. Se estiver em branco, o OneTrace baseia-se na configuração do registo para o tipo de grupo. Por exemplo, se `GroupType=1`definir, por padrão, o `C:\Windows\CCM\Logs` OneTrace procurará automaticamente os registos do grupo. Neste exemplo, não precisa de `GroupFilePath`especificar .

## <a name="see-also"></a>Consulte também

- [Espectador de registo do Centro de Suporte](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
