---
title: Resolver problemas do BitLocker
titleSuffix: Configuration Manager
description: Saiba como resolver problemas com a gestão do BitLocker no Gestor de Configuração
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723923"
---
# <a name="troubleshoot-bitlocker"></a>Resolver problemas do BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as informações deste artigo para ajudá-lo a resolver problemas com a gestão do BitLocker no Gestor de Configuração.

## <a name="server-error-in-self-service"></a>Erro do servidor no self-service

Ao tentar abrir o portal`https://webserver.contoso.com/SelfService`de autosserviço pela primeira vez, vê a seguinte mensagem de erro:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Para corrigir este problema, certifique-se de que instalou o [pré-requisito](../../plan-design/bitlocker-management.md#prerequisites) para o **Microsoft ASP.NET MVC 4.0** no servidor web.

## <a name="see-also"></a>Consulte também

Para mais informações sobre a utilização de registos de eventos BitLocker, consulte os [registos do evento BitLocker](about-event-logs.md).

Para obter uma lista de erros conhecidos e possíveis causas para entradas de registo de eventos, consulte os seguintes artigos:

- [Registo de eventos de clientes](client-event-logs.md)
- [Registos de eventos do servidor](server-event-logs.md)

Para entender por que razão os clientes estão a reportar não conformes com a política de gestão bitLocker, consulte [códigos de incumprimento](non-compliance-codes.md).
