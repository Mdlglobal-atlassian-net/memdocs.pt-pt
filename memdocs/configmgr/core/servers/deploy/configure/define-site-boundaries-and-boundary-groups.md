---
title: Utilizar limites e grupos de fronteira
titleSuffix: Configuration Manager
description: Utilize limites e grupos de fronteiras para definir localizações de rede e sistemas de site acessíveis para dispositivos que gere.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0b1a6bb6ff9fdffad65db884fe8c3b68d3fc3263
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711246"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Definir limites do site e grupos de fronteira

*Aplica-se a: Gestor de Configuração (ramo atual)*

*Os limites* no Gestor de Configuração definem as localizações da rede na sua intranet. Estas localizações incluem dispositivos que pretende gerir. *Os grupos de* fronteiras são grupos lógicos de limites que se configuram.

Uma hierarquia pode incluir qualquer número de grupos de fronteira. Cada grupo de limites pode conter qualquer combinação dos seguintes tipos de limites:  

- Sub-rede IP  
- Nome do site do Active Directory  
- Prefixo IPv6  
- Intervalo de endereços IP  

Os clientes na intranet avaliam a respetiva localização de rede atual e, em seguida, utilizam essa informação para identificar os grupos de limites a que pertencem.  

Os clientes utilizam grupos de limites para:  

- **Encontre um site atribuído:** Os grupos de fronteira permitem que os clientes encontrem um site primário para a atribuição do cliente. Este comportamento também é conhecido como atribuição automática do *site.*  

- **Encontre certas funções** do sistema do site que podem utilizar: Associe um grupo de fronteiras com determinadas funções do sistema do site. Em seguida, o site fornece aos clientes essa lista de sistemas de sites no grupo de fronteira. Os clientes utilizam estes sistemas de sites para ações como encontrar conteúdo ou um ponto de gestão próximo.  

Os clientes que estão na internet ou configurados como clientes apenas na Internet não usam informações de limites. Estes clientes não podem usar a atribuição automática do site. Eles podem descarregar conteúdo a partir de um ponto de distribuição baseado na Internet a partir do seu site designado ou de um ponto de distribuição baseado na nuvem.  

A partir da versão 1902, pode associar um gateway de gestão de nuvem (CMG) a um grupo de fronteiras. Para mais informações, consulte o [design da hierarquia da CMG.](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design)<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a>Recomendações

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Use uma mistura dos limites mais mínimos que atendem às suas necessidades

Utilize qualquer tipo ou tipo de limite que escolha que funcione para o seu ambiente. Para simplificar as suas tarefas de gestão, utilize tipos de limites que lhe permitam utilizar o menor número de limites que puder.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Evite sobrepor limites para a atribuição automática do site

Embora cada grupo de fronteira suporte tanto a atribuição do site como a referência do sistema do site, crie um conjunto separado de grupos de fronteira para usar apenas para a atribuição do site. Certifique-se de que cada limite de um grupo de fronteiras não é membro de outro grupo de fronteiras com uma missão de site diferente.

- Uma única fronteira pode ser incluída em vários grupos de fronteira  

- Cada grupo de limites pode ser associado a outro site primário para atribuição de sites  

- Para um limite que é membro de dois diferentes grupos de fronteira com diferentes atribuições de site, os clientes selecionam aleatoriamente um site para aderir. Este comportamento pode não ser para o site que quer que o cliente se junte. Esta configuração *chama-se limites sobrepostos.*  

    Sobrepor limites não é um problema para a localização do conteúdo. Pode ser uma configuração útil que fornece aos clientes recursos adicionais ou locais de conteúdo que possam usar.  


## <a name="next-steps"></a>Passos seguintes

- [Definir as localizações da rede como limites](boundaries.md)

- [Configure grupos de fronteira](boundary-groups.md)
