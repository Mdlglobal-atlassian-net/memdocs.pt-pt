---
title: Registos de eventos do BitLocker
titleSuffix: Configuration Manager
description: Saiba como trabalhar com informações do BitLocker no Windows Event Log para resolver problemas
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4875e7875321294d815bfcd8a25a805d3e085aab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722103"
---
# <a name="bitlocker-event-logs"></a>Registos de eventos do BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

O agente de gestão BitLocker e os serviços web utilizam registos de eventos do Windows para gravar mensagens. No Espectador de Eventos, aceda a Registos de **Aplicações e Serviços,** **Microsoft,** **Windows**. O canal de registo (nó) varia consoante o computador e o componente:

- **MBAM**: Agente de gestão BitLocker num computador cliente
- **MBAM-Web**:
  - Serviço de recuperação no ponto de gestão
  - Portal self-service
  - Site de administração e monitorização

Para obter mais informações sobre mensagens específicas nestes registos, consulte os seguintes artigos:

- [Registo de eventos de clientes](client-event-logs.md)
- [Registos de eventos do servidor](server-event-logs.md)

Em cada nó, por defeito verá dois canais de registo: **Administrador** e **Operacional**. Para obter informações mais detalhadas sobre resolução de problemas, também pode mostrar [registos de análise e depuração.](#bkmk_debug)

## <a name="log-properties"></a>Propriedades de log

No Windows Event Viewer, selecione um registo específico. Por exemplo, **Administrador.** Vá ao menu **Ação** e selecione **Propriedades**. Configure as seguintes definições:

- Tamanho máximo do **registo (KB)**: `1028` por defeito, esta definição é (1 MB) para todos os registos.
- Quando o tamanho máximo do registo do **evento for atingido:** por padrão, os registos de **administração** e **operacionais** são definidos para **substituir os eventos conforme necessário (eventos mais antigos primeiro)**.

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a>Troncos analíticos e depurados

Pode ativar registos mais detalhados para fins de resolução de problemas. No Espectador de Eventos, vá ao menu **'Ver'** e selecione **Registos Denalíticos e Debug**. Agora, quando navegar para o canal de registo, verá dois registos adicionais: **Analytic** e **Debug**.

> [!TIP]
> Por predefinição, estes registos têm as seguintes propriedades:
>
> - Tamanho máximo do tronco `1028` **(KB)**: (1 MB)
> - **Não sobrepor os eventos (limpe os registos manualmente)**

## <a name="export-logs-to-text"></a>Registos de exportação para texto

Especialmente com os [registos analíticos e dedebugs,](#bkmk_debug)poderá ser mais fácil rever as entradas de registonum único ficheiro de texto. Utilize os seguintes comandos PowerShell para exportar as entradas de registo de eventos para ficheiros de texto:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
