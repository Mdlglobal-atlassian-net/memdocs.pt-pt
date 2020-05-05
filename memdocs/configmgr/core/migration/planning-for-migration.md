---
title: Planear a migração
titleSuffix: Configuration Manager
description: Conheça sites e hierarquias antes de migrar dados para uma hierarquia de destino de destino de ramificação do Gestor de Configuração.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719660"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Plano de migração para o ramo atual do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de migrar dados para uma hierarquia de destino de destino de ramificação atual do Gestor de Configuração, certifique-se de que está familiarizado com sites e hierarquias em Configuração Manager. Para mais informações sobre sites e hierarquias, consulte [Fundamentos de Gestor de Configuração](../../core/understand/fundamentals.md).  

Instale uma hierarquia de ramificação atual do Gestor de Configuração para ser a hierarquia de destino antes de migrar dados de uma hierarquia de origem suportada.  

Depois de instalar a hierarquia de destino, configurar as funcionalidades e funções de gestão que pretende utilizar na hierarquia do seu destino antes de começar a migrar dados.  

Além disso, poderá ter de planear a sobreposição entre a hierarquia de origem e a sua hierarquia de destino. Por exemplo, pode configurar a hierarquia de origem para utilizar os mesmos locais ou limites de rede que a sua hierarquia de destino, e depois instala novos clientes na sua hierarquia de destino e utiliza a atribuição automática do site. Neste cenário, uma vez que um cliente recém-instalado do Gestor de Configuração pode selecionar um site para aderir a qualquer hierarquia, o cliente pode atribuir incorretamente à sua hierarquia de origem. Por isso, planeie atribuir a cada novo cliente na hierarquia de destino um site específico nessa hierarquia em vez de usar a atribuição automática do site.  

Para mais informações sobre atribuições do site, consulte [considerações](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) de atribuição do site do Cliente na [Interoperabilidade entre diferentes versões do Gestor de Configuração](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

Use os seguintes artigos para ajudá-lo a planear como migrar uma hierarquia de origem apoiada para uma hierarquia de destino de Gestor de Configuração:

-   [Pré-requisitos de migração](../../core/migration/prerequisites-for-migration.md)  

-   [Listas de verificação de administrador para planeamento da migração](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determine se deve migrar dados para o ramo atual do Gestor de Configuração](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planear uma estratégia de hierarquia de origem](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Listas de verificação de administrador para planeamento da migração](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planeie uma estratégia de migração de clientes](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planear uma estratégia de migração de implementação de conteúdos](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Plano para a migração de objetos do Gestor de Configuração para o ramo atual do Gestor de Configuração](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Plano de monitorização da atividade migratória](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Plano para completar a migração](../../core/migration/planning-to-complete-migration.md)  
