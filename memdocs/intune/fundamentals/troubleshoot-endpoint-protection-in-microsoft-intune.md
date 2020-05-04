---
title: Mensagens comuns de proteção de pontofinal no Microsoft Intune - Azure Microsoft Docs
description: Consulte mensagens comuns e possível solução ao utilizar e resolver problemas de proteção de pontos finais e Microsoft Defender no Microsoft Intune.
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/13/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e31df2d2-bb1b-491b-9a71-04e0b18829c1
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 16b7cc65ae043fb48b7f500bfcd65195c7ff7561
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330437"
---
# <a name="endpoint-protection-issues-and-possible-solutions-in-microsoft-intune"></a>Problemas de proteção de endpoint e possíveis soluções no Microsoft Intune

Este artigo lista e descreve potenciais causas e soluções para alguns erros e advertências. Utilize a informação para ajudar a resolver problemas ao utilizar a proteção do ponto final.

## <a name="microsoft-defender-error-codes"></a>Códigos de erro do Microsoft Defender

Reveja os registos de eventos e códigos de erro para [resolver problemas com](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/troubleshoot-windows-defender-antivirus)o Microsoft Defender AV .

## <a name="common-intune-errors-and-possible-resolutions"></a>Erros insintonizados comuns e possíveis resoluções

### <a name="endpoint-protection-engine-unavailable"></a>Motor do Endpoint Protection indisponível

**Causa potencial**: O motor de proteção do ponto final Intune foi corrompido ou eliminado.

**Soluções possíveis:**

- Se a proteção de pontofinal for corrupta ou não atualizar, em seguida, atualize ou reinstale o programa.
- Forçar uma atualização imediata. No programa de cliente de proteção de pontofinal (possivelmente na barra de tarefas), escolha **Atualização**.
- Nos programas > painel de controlo, selecione **Microsoft Intune Endpoint Protection Agent**. Desinstale a aplicação.
- Durante a próxima sincronização de atualizações, o Gestor de Atualizações do Microsoft Online Management deteta o programa em falta e reinstala-o na hora de instalação agendada.

### <a name="features-are-disabled"></a>As funcionalidades são desativadas

Pode receber uma mensagem de que algumas funcionalidades estão desativadas. Estas mensagens podem acontecer se a proteção de pontofinal Intune ou o Microsoft Defender forem desativados por um administrador utilizando um perfil de configuração. Ou é desativado por um utilizador final no dispositivo. Mensagens possíveis:

`Endpoint Protection disabled`  
`Real-time protection disabled`  
`Download scanning disabled`  
`File and program activity monitoring disabled`  
`Behavior monitoring disabled`  
`Script scanning disabled`  
`Network Inspection System disabled`  

**Soluções possíveis**: Ativar estas funcionalidades. Para orientação, consulte:

- [Adicione definições de proteção de pontofinal](../protect/endpoint-protection-configure.md)
- [Antivírus Do Microsoft Defender](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)
- [Utilizadores finais: Ligue a proteção em tempo real para aceder aos recursos da empresa](../user-help/turn-on-defender-windows.md)

### <a name="malware-definitions-out-of-date"></a>Definições de software maligno desatualizadas

Este estado mostra quando as definições de malware no dispositivo estão desatualizadas por 14 dias ou mais. Por exemplo, a mensagem pode mostrar se o dispositivo está desligado da Internet, ou se as definições de malware estão desatualizadas.

**Soluções possíveis**: Se as definições de malware estiverem desatualizadas, atualize as definições utilizando o [Antivírus Do Microsoft Defender](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).

### <a name="full-scan-overdue-or-quick-scan-overdue"></a>Varredura completa atrasada ou exame rápido atrasado

Uma tomografia completa ou uma varredura rápida não está concluída há 14 dias. Este cenário pode acontecer se o dispositivo recomeçar durante uma varredura completa.

**Soluções possíveis**: Se um exame estiver atrasado, pode fazer uma varredura única ou agendar exames recorrentes. Ver [Microsoft Defender Antivírus](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).

### <a name="another-endpoint-protection-application-running"></a>Outra aplicação de Endpoint Protection em execução

Outra aplicação de proteção de ponto final está em execução, e o dispositivo é saudável.

**Soluções possíveis**: Se for instalada outra aplicação de proteção de pontofinal e o Intune detetar essa aplicação, o dispositivo pode tornar-se instável.

## <a name="next-steps"></a>Passos seguintes

Obtenha [ajuda de suporte da Microsoft](get-support.md), ou use os [fóruns comunitários](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
