---
title: Configurar o inventário de hardware
titleSuffix: Configuration Manager
description: Configurar o inventário de hardware para todos os clientes ou para uma coleção em 'Gestor de Configuração'.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714438"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>Como configurar o inventário de hardware no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este procedimento configura as predefinições de cliente para inventário de hardware e aplica-se a todos os clientes na sua hierarquia. Se pretender que estas definições se apliquem apenas a determinados clientes, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os dispositivos que pretende que utilizem inventário de hardware. Ver [Como configurar as definições do cliente](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se um dispositivo cliente receber definições de inventário de hardware de vários conjuntos de definições de cliente, as classes de inventário de hardware de cada conjunto de definições serão intercaladas quando o cliente comunicar o inventário de hardware. Além disso, não verificar uma classe num ambiente de cliente personalizado com uma prioridade maior não desativa o cliente de inventariar essa classe. 

Para desativar uma classe específica de inventário de hardware na maioria dos sistemas, exceto alguns, a classe precisa de ser desmarcada nas definições padrão do cliente. Em seguida, crie uma definição personalizada do cliente para ativar a classe e implemente-a para os sistemas-alvo.


### <a name="to-configure-hardware-inventory"></a>Para configurar o inventário de hardware  

1.  Na consola 'Gestor de Configuração', escolha as**definições** > padrão do cliente de **'' ''' '',** > **configurações**padrão do cliente .  

4.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

5.  Na caixa de diálogo **Definições Predefinidas,** escolha inventário de **hardware**.  

6.  Na lista **Definições do Dispositivo** , configure as seguintes definições:  

    -   Ativar o inventário de **hardware nos clientes** - Selecione **Sim**.  

    -   **Calendário de inventário** de hardware - Clique em **Agenda** para especificar o intervalo em que os clientes recolhem inventário de hardware.  

7.  Configure outras definições de cliente de inventário de [hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) que você precisa.  

Os dispositivos cliente serão configurados com estas definições da próxima vez que transferirem a política de cliente. Para iniciar a recuperação de políticas para um único cliente, consulte [Como gerir os clientes.](../../../../core/clients/manage/manage-clients.md)  
