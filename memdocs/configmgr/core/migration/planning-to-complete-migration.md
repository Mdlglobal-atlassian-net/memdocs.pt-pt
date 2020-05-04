---
title: Concluir a migração
titleSuffix: Configuration Manager
description: Saiba como terminar a migração para uma hierarquia de destino de ramificação atual do Gestor de Configuração depois de uma hierarquia de origem já não ter dados.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76cf6b57a4bc1439f2aa9c2e0484271987f85748
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713010"
---
# <a name="plan-to-complete-migration-in-configuration-manager"></a>Plano para completar a migração em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Com o Gestor de Configuração, pode completar o processo de migração quando uma hierarquia de origem já não tem dados que pretende migrar para a sua hierarquia de destino. A conclusão da migração inclui os seguintes passos gerais:  

-   Certifique-se de que os dados necessários migraram. Antes de completar a migração de uma hierarquia de origem, certifique-se de que emigrou com sucesso todos os recursos da hierarquia de origem que necessita na hierarquia de destino. Isto pode incluir dados e clientes.  

-   Pare de recolher dados de sites de origem. Para completar a migração de uma hierarquia de origem, tem primeiro de parar de recolher dados de sites de origem.  

-   Limpe os dados da migração. Depois de deixar de recolher dados de todos os sites de origem numa hierarquia de origem, pode remover dados sobre o processo de migração e a hierarquia de origem da base de dados da hierarquia de destino.  

-   Desmantelar a hierarquia de origem. Depois de completar a migração de uma hierarquia de origem e que a hierarquia já não tem recursos que gere, pode desativar os locais na hierarquia de origem e remover as infraestruturas relacionadas do seu ambiente. Para obter informações sobre como desativar sites e hierarquias de origem, consulte a documentação para essa versão do Gestor de Configuração.  

Utilize as seguintes secções para o ajudar a planear completar a migração a partir de uma hierarquia de origem, interrompendo a recolha de dados e limpando os dados de migração:  

-   [Plano para parar de recolher dados](#Plan_to_Stop_Data_Gath)  

-   [Plano para limpar dados de migração](#Plan_to_clean_up)  

##  <a name="plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a>Plano para parar de recolher dados  
 Antes de completar a migração e limpar os dados da migração, deve parar de recolher dados de cada site de origem na hierarquia de origem. Para parar de recolher dados de cada site de origem, deve executar o comando **Stop Gathering Data** nos sites de origem de nível inferior e, em seguida, repetir o processo em cada site-mãe. O site de nível superior da hierarquia de origem terá de ser o último em que a recolha de dados é interrompida. Tem de parar a recolha de dados em cada local da criança antes de executar este comando num site dos pais. Normalmente, só se para de recolher dados quando está pronto para terminar o processo de migração.  

 Depois de deixar de recolher dados de um site de origem, os pontos de distribuição partilhados desse site já não estão disponíveis como locais de conteúdo para clientes na hierarquia de destino. Por isso, certifique-se de que qualquer conteúdo migrado que os clientes da hierarquia de destino exijam acesso aos restos mortais através de uma das seguintes opções:  

-   Na hierarquia do destino, distribua o conteúdo para pelo menos um ponto de distribuição.  

-   Antes de parar de recolher dados de um site de origem, atualize ou reatribua pontos de distribuição partilhados que tenham o conteúdo necessário. Para mais informações sobre a atualização ou reatribuição de pontos de distribuição partilhados, consulte as secções aplicáveis no Planeamento de uma estratégia de migração de implementação de [conteúdos.](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

Depois de deixar de recolher dados de cada site de origem na hierarquia de origem, pode limpar os dados da migração. Até limpar os dados da migração, cada trabalho de migração que tenha sido executado ou que esteja programado para ser executado permanece acessível na consola Do Gestor de Configuração.  

Para mais informações sobre sites de origem e recolha de dados, consulte O Planeamento de uma estratégia de [hierarquia de origem.](../../core/migration/planning-a-source-hierarchy-strategy.md)  

##  <a name="plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a>Plano para limpar dados de migração  
 O último passo necessário para acabar com a migração é limpar os dados da migração. Pode utilizar o comando **Clean Up Migration Data** depois de ter parado de recolher dados para cada site de origem na hierarquia de origem. Esta ação opcional remove dados sobre a atual hierarquia de origem da base de dados da hierarquia de destino.  

 Quando se limpa ma dados de migração, a maioria dos dados sobre a migração são removidos da base de dados da hierarquia de destino. No entanto, os detalhes sobre os objetos migrados são retidos. Com estes detalhes, pode utilizar o espaço de trabalho **migratório** para reconfigurar a hierarquia de origem que tem os dados que foram migrados para retomar a migração daquela hierarquia de origem, ou para rever os objetos e a propriedade do local dos objetos que anteriormente migraram.  
