---
title: On-premises MDM (MDM no local)
titleSuffix: Configuration Manager
description: Conheça a gestão de dispositivos móveis no local (MDM) no Gestor de Configuração
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721837"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>MDM no local em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração no local é uma solução de gestão de dispositivos que se baseia nas capacidades de gestão incorporadas do Windows. Esta funcionalidade baseia-se na norma Open Mobile Alliance (OMA) Device Management (DM). Utiliza a infraestrutura do Gestor de Configuração da sua organização para gerir e manter os dispositivos. A sua organização exige que as licenças Microsoft Intune utilizem esta funcionalidade, mas não requer qualquer ligação à nuvem. O Gestor de Configuração armazena todos os dados sobre os seus dispositivos na base de dados do site no local.

No local, o MDM difere da Microsoft Intune, que também depende das capacidades de DM Incorporadas da OMA. Todas as funções de gestão em Intune são entregues através de serviços na nuvem. No local, o MDM também difere da solução de gestão baseada no cliente tradicionalmente oferecida pelo Gestor de Configuração. Baseia-se em infraestruturas semelhantes, mas não utiliza software cliente instalado separadamente nos dispositivos que gere.  

## <a name="comparison"></a>Comparação

As seguintes secções enumeram as vantagens e desvantagens do MDM no local em comparação com a gestão tradicional baseada no cliente:  

### <a name="advantages"></a>Vantagens

- **Infraestrutura simplificada**: São necessárias menos funções no sistema de sítios.

- **Mais fácil de manter**: Como a funcionalidade de gestão está incorporada no dispositivo OS, não são necessárias novas versões do cliente do Gestor de Configuração quando novas funcionalidades de gestão são introduzidas no site.

- **No local:**- Toda a gestão e dados são mantidos no local.

### <a name="disadvantages"></a>Desvantagens

Menor funcionalidade de **gestão do cliente**: Sem orquestração, medição de software, integração de terceiros, sequenciação de tarefas ou suporte do Software Center.

- **Suporte limitado do dispositivo**: no local o MDM não suporta tantas versões DE como o cliente do Gestor de Configuração. Para mais informações, consulte [versões De SO suportadas para clientes e dispositivos.](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)

## <a name="next-step"></a>Passo seguinte

Saiba o que considerar na configuração da infraestrutura do Gestor de Configuração e planeamento para a inscrição de dispositivos no MDM no local.

> [!div class="nextstepaction"]
> [Plano de MDM no local](../plan-design/plan-on-premises-mdm.md)  
