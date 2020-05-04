---
title: Gerir clientes na Internet
titleSuffix: Configuration Manager
description: Saiba mais sobre gestão de clientes com gateway de gestão de nuvem e gestão de clientes baseado na Internet no Gestor de Configuração.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c00d480b993498c5fa27e2a4d91a5f2a3bc130ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710630"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gerir clientes na internet com O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Tipicamente no Gestor de Configuração, a maioria dos computadores e servidores geridos estão fisicamente na mesma rede interna que os servidores do sistema do site que desempenham funções de gestão. No entanto, pode gerir clientes fora da sua rede interna quando estão ligados à internet. Esta capacidade não requer que os clientes se conectem via VPN para chegar aos servidores do sistema do site.

O Gestor de Configuração fornece duas formas de gerir clientes ligados à Internet:

-   Gateway de gestão da cloud

-   Gestão de clientes baseada na Internet


## <a name="cloud-management-gateway"></a>Gateway de gestão da cloud

O portal de gestão de nuvem fornece a gestão de clientes baseados na Internet. Utiliza uma combinação de um serviço de nuvem Microsoft Azure e uma nova função do sistema de site que comunica com esse serviço. Os clientes baseados na Internet usam o serviço de nuvem para comunicar com o Gestor de Configuração no local.

#### <a name="advantages"></a>Vantagens  

-   Não são necessários investimentos adicionais em infraestruturas no local.  

-   Não expõe as infraestruturas no local à internet.  

-   As máquinas virtuais cloud que executam o serviço são totalmente geridas pelo Azure e não requerem manutenção.  

-   Configurar e configurar facilmente na consola 'Gestor de Configuração'.  

#### <a name="disadvantages"></a>Desvantagens  

-   Custo de subscrição em nuvem.  

-   Dados de gestão enviados através do serviço de nuvem.  

Para mais informações, consulte [Plan for cloud management gateway](cmg/plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Gestão de clientes baseada na Internet

Este método baseia-se em servidores de sistemas de sites virados para a Internet para os quais os clientes comunicam para fins de gestão. Requer que os clientes e servidores do sistema do site sejam configurados para gestão baseada na Internet.

#### <a name="advantages"></a>Vantagens  

-   Sem dependência de serviço na nuvem.  

-   Nenhum custo adicional associado a uma subscrição em nuvem.  

-   Controlo total dos servidores e funções que fornecem o serviço.  

#### <a name="disadvantages"></a>Desvantagens  

-   Requerem investimentos adicionais em infraestruturas.  

-   Despesas gerais e operacionais de infraestruturas adicionais.  

-   As infraestruturas devem ser expostas à internet.  

Para mais informações, consulte [Plano de gestão de clientes baseado na Internet.](plan-internet-based-client-management.md)  
