---
title: Pré-requisitos de Inteligência de Ativos
titleSuffix: Configuration Manager
description: Obtenha os pré-requisitos para a Inteligência de Ativos no Gestor de Configuração.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a7f87336c35c236a9e07d531469d65958d5d14e0
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906592"
---
# <a name="prerequisites-for-asset-intelligence-in-configuration-manager"></a>Pré-requisitos para inteligência de ativos em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A Inteligência de Ativos no Gestor de Configuração tem dependências e dependências externas dentro do produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela seguinte fornece as dependências da Inteligência de Ativos que são externas ao Gestor de Configuração.  

|Dependência|Mais Informações|  
|----------------|----------------------|  
|Pré-requisitos da Auditoria de Eventos de Início de Sessão Bem-sucedidos|Quatro relatórios do Asset Intelligence apresentam informações recolhidas a partir de registos de eventos de Segurança do Windows em computadores cliente. Se as definições de registo de eventos de Segurança não estiverem configuradas para registar todos os eventos de início de sessão bem-sucedidos, estes relatórios não contêm dados, mesmo que esteja ativada a classe adequada de relatórios de inventário de hardware.<br /><br /> Os relatórios do Asset Intelligence seguintes dependem das informações de registo de eventos de Segurança do Windows recolhidas:<br /><br /> - Hardware 03A - Utilizadores de computador primários<br />- Hardware 03B - Computadores para um utilizador específico da consola primária<br />- Hardware 04A - Computadores partilhados (multiutilizadores)<br />- Hardware 05A - Utilizadores de consolas num computador específico<br /><br /> Para ativar o Agente do Cliente de Inventário de Hardware para inventariar as informações necessárias para suportar estes relatórios, primeiro tem de modificar as definições de registo de eventos de Segurança do Windows nos clientes para registar todos os eventos de início de sessão bem-sucedidos e ativar a classe de relatório de inventário de hardware **SMS_SystemConsoleUser** . Para mais informações sobre como modificar as definições de registo de eventos de Segurança para registar todos os eventos de início de sessão bem-sucedidos, consulte [Enable auditing of success logon events](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  A classe de relatórios de inventário de hardware **SMS_SystemConsoleUser** retém os dados de eventos de início de sessão bem-sucedidos durante apenas os últimos 90 dias do registo de eventos de Segurança, independentemente da duração do registo. Se o registo de eventos de Segurança tiver menos de 90 dias de dados, é lido todo o registo.  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependências Internas do Configuration Manager  
 A tabela seguinte fornece as dependências da Inteligência de Ativos que são internas ao Gestor de Configuração.  

|Dependência|Mais Informações|  
|----------------|----------------------|  
|Pré-requisitos do Agente do Cliente|Os relatórios do Asset Intelligence dependem das informações do cliente obtidas através de relatórios de inventário de hardware e software do cliente. Para obter as informações necessárias para todos os relatórios do Asset Intelligence, têm de estar ativados os seguintes agentes do cliente:<br /><br /> - Agente cliente de inventário de hardware<br />- Agente cliente de medição de software|  
|Dependências do Agente do Cliente de Inventário de Hardware|Para recolher os dados de inventário necessários para alguns relatórios do Asset Intelligence, o Agente do Cliente de Inventário de Hardware tem de estar ativado. Além disso, algumas classes de relatórios de inventário de hardware de que os relatórios do Asset Intelligence dependem têm de estar ativadas nos computadores de servidor do site primário.<br /><br /> Para obter informações sobre a habilitação do Agente cliente de inventário de hardware, consulte [como alargar o inventário de hardware](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Dependências do Agente do Cliente de Medição de Software|Vários relatórios de software do Asset Intelligence dependem do Agente do Cliente de Medição de Software para fornecer dados. Para obter informações sobre a habilitação do Agente cliente de medição de software, consulte o [uso da aplicação Monitor com a medição de software](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Os relatórios do Asset Intelligence seguintes dependem do Agente do Cliente de Medição de Software para fornecer dados:<br /><br /> - Software 07A - Executáveis recentemente utilizados por número de computadores<br />- Software 07B - Computadores que recentemente utilizaram um executível especificado<br />- Software 07C - Executáveis recentemente utilizados num computador específico<br />- Software 08A - Executáveis recentemente utilizados por número de utilizadores<br />- Software 08B - Utilizadores que recentemente utilizaram um executível especificado<br />- Software 08C - Executíveis recentemente utilizados por um utilizador especificado|  
|Pré-requisitos da Classe de Relatórios de Inventário de Hardware do Asset Intelligence|Os relatórios da Inteligência de Ativos no Gestor de Configuração dependem de aulas específicas de relatórios de inventário de hardware. Até as classes de relatórios de inventário de hardware estarem ativadas e os clientes terem reportado o inventário de hardware com base nestas classes, os relatórios do Asset Intelligence associados não irão conter nenhuns dados. Pode ativar as classes de relatórios de inventário de hardware seguintes para suportar os requisitos de relatórios do Asset Intelligence:<br /><br /> - SMS_SystemConsoleUsage<sup>1</sup><br />- SMS_SystemConsoleUser<sup>1</sup><br />- SMS_InstalledSoftware<br />- SMS_AutoStartSoftware<br />- SMS_BrowserHelperObject<br />- Win32_USBDevice<br />- SMS_InstalledExecutable<br />- SMS_SoftwareShortcut<br />- SoftwareLicensingService<br />- SoftwareLicensingProduct<br />- SMS_SoftwareTag<br /><br /> <sup>1</sup> Por predefinição, as classes de relatórios de inventário de hardware do Asset Intelligence **SMS_SystemConsoleUsage** e **SMS_SystemConsoleUser** estão ativadas.<br /><br /> Pode editar as classes de relatórios de inventário de hardware da Asset Intelligence na consola do Gestor de Configuração, no espaço de trabalho **de Ativos e Compliance,** quando clicar no nó de Inteligência de **Ativos.** Para mais informações, consulte a secção de relatórios de relatórios de hardware de [hardware enable Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) no tópico de Configuração de Inteligência de [Ativos.](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services tem de ser instalada para que os relatórios de atualização de software possam ser apresentados. Para obter mais informações sobre a criação de um ponto de serviços de reporte, consulte [a Configuração de relatórios](../../../servers/manage/configuring-reporting.md).|  
