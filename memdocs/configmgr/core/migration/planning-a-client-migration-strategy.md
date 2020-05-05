---
title: Planear a migração de clientes
titleSuffix: Configuration Manager
description: Conheça as tarefas que migram os clientes de uma hierarquia de origem para uma hierarquia de destino de ramificação atual do Gestor de Configuração.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720913"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>Planeie uma estratégia de migração de clientes em 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para migrar clientes da hierarquia de origem para uma hierarquia de destino de ramificação atual do Gestor de Configuração, você deve fazer duas tarefas. Tem de migrar os objetos que estão associados ao cliente e, em seguida, tem de reinstalar ou reatribuir os clientes da hierarquia de origem à hierarquia de destino. Deve migrar primeiro os objetos para que estejam disponíveis quando os clientes forem migrados. Os objetos associados ao cliente são migrados utilizando tarefas de migração. Para obter informações sobre como migrar os objetos que estão associados ao cliente, consulte Planeamento de uma estratégia de trabalho de [migração.](../../core/migration/planning-a-migration-job-strategy.md)  

 Utilize as secções seguintes como auxílio para planear a migração dos clientes para a hierarquia de destino.  

-   [Plano para migrar clientes para a hierarquia de destino](#Planning_for_Client_Agent_Migration)  

-   [Planear o processamento dos dados mantidos nos clientes durante a migração](#Planning_for_Client_Data_Migration)  

-   [Plano de inventário e dados de conformidade durante a migração](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> Planear a migração dos clientes para a hierarquia de destino  
 Quando migra clientes de uma hierarquia de origem, o software cliente no computador cliente atualiza para corresponder à versão do produto da hierarquia de destino.  

-   Uma hierarquia de fonte de Gerente de **Configuração de 2007:** Quando migra clientes de uma hierarquia de origem que executa uma versão suportada do Gestor de Configuração, o software do cliente atualiza para a versão cliente para a hierarquia de destino.  

-   Um Gestor de **Configuração do System Center 2012 ou hierarquia de origem posterior:** Quando migra clientes entre hierarquias que são da mesma versão do produto, o software do cliente não muda nem atualiza. Em vez disso, o cliente é reatribuído a partir da hierarquia de origem a um site na hierarquia de destino.  

    > [!NOTE]  
    >  Quando a versão de produto de uma hierarquia não for suportada para migração para a hierarquia de destino, atualize todos os sites e clientes da hierarquia de origem para uma versão de produto compatível. Depois da atualização da hierarquia de origem para uma versão de produto suportada, pode migrar entre as hierarquias. Para mais informações, consulte [versões do Gestor de Configuração que são suportadas para migração](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) em [pré-requisitos para migração](../../core/migration/prerequisites-for-migration.md).  

Utilize as informações seguintes para planear a migração de clientes:  

-   Para atualizar ou reatribuir clientes de um site de origem a um site de destino, pode utilizar qualquer método de implementação de clientes que seja suportado para implementar clientes na hierarquia de destino. Os métodos de implementação de clientes típicos incluem a instalação push de cliente, a distribuição de software, a Política de Grupo e a instalação de cliente baseada em atualização de software. Para mais informações, consulte os métodos de [instalação do Cliente.](../../core/clients/deploy/plan/client-installation-methods.md)  

-   Certifique-se de que o dispositivo que executa o software do cliente na hierarquia de origem cumpre os requisitos mínimos de hardware e executa um sistema operativo que é suportado pela versão do Gestor de Configuração na hierarquia de destino.  

-   Antes de migrar um cliente, faça um trabalho de migração para migrar a informação que o cliente utilizará na hierarquia de destino.  

-   Os clientes que atualizam mantêm o seu histórico de execução para implementações. Isto impede que as implantações voltem a funcionar desnecessariamente na hierarquia do destino.  

    -   Para clientes de Configuração Manager 2007, o histórico de execução de anúncios é mantido.  

    -   Para clientes do System Center 2012 Configuração Manager ou Configuração Manager atual, o histórico de execução de implementação é mantido.  

-   Pode migrar os clientes de sites da hierarquia de origem por qualquer ordem à escolha. No entanto, considere migrar um número limitado de clientes em fases em vez de migrar um grande número de clientes em um único momento. Uma migração faseada reduz os requisitos de largura de banda da rede e o processamento do servidor quando cada cliente recém-atualizado submeter os respetivos dados de inventário e compatibilidade completos iniciais ao site atribuído.  

-   Quando migra clientes do Gestor de Configuração 2007, o software cliente existente é desinstalado a partir do computador cliente e o novo software cliente está instalado.  

-   O Gestor de Configuração não pode migrar um cliente do Gestor de Configuração de 2007 que tenha o cliente App-V instalado a menos que a versão do cliente App-V seja 4.6 SP1 ou posterior.  

Pode monitorizar o processo de migração do cliente no nó **migratório** do espaço de trabalho da **Administração** na consola Do Gestor de Configuração.  

Depois de migrar o cliente para a hierarquia de destino, já não consegue gerir esse dispositivo utilizando a sua hierarquia de origem, devendo considerar retirar o cliente da hierarquia de origem. Embora isto não seja um requisito quando migra hierarquias, pode ajudar a evitar a identificação de um cliente migrado num relatório da hierarquia de origem ou uma contagem incorreta de recursos entre as duas hierarquias durante a migração. Por exemplo, quando um cliente migrado permanece na base de dados do site de origem, poderá executar um relatório de atualizações de software que identifique incorretamente o computador como um recurso não gerido, quando é agora gerido pela hierarquia de destino.  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a>Plano para lidar com dados mantidos sobre clientes durante a migração  
Quando migra um cliente da respetiva hierarquia de origem para a hierarquia de destino, algumas informações são mantidas no dispositivo, enquanto outras deixam de estar disponíveis no dispositivo após a migração.  

As informações seguintes são mantidas no dispositivo cliente:  

-   O identificador único (GUID), que associa um cliente à sua informação na base de dados do Gestor de Configuração.  

-   O histórico de anúncios ou implementações, que impede que os clientes executem de novo implementações ou anúncios desnecessários na hierarquia de destino.  

As informações seguintes não são mantidas no dispositivo cliente:  

-   Os ficheiros da cache do cliente. Se o cliente necessitar destes ficheiros para instalar software, o cliente transfere-os novamente da hierarquia de destino.  

-   Informações da hierarquia de origem sobre quaisquer anúncios ou implementações que ainda não foram executados. Se pretender que o cliente execute as implementações ou os anúncios após a migração, tem de implementá-los de novo no cliente na hierarquia de destino.  

-   Informações sobre o inventário. O cliente reenvia esta informação para o seu site atribuído na hierarquia de destino após a migração do cliente e os novos dados do cliente foram gerados.  

-   Dados de compatibilidade. O cliente reenvia esta informação para o seu site atribuído na hierarquia de destino após a migração do cliente e os novos dados do cliente foram gerados.  

Quando um cliente migra, a informação armazenada no registo do cliente do Gestor de Configuração e no caminho dos ficheiros não é retida. Após a migração, volte a aplicar estas definições. As definições típicas incluem as seguintes:  

-   Esquemas de energia  

-   Definições de registo  

-   Definições da política local  

Além disso, poderá ter de reinstalar algumas aplicações.  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Planear os dados de inventário e de compatibilidade durante a migração  
Os dados de inventário e compatibilidade do cliente não são guardados quando migra um cliente para a hierarquia de destino. Em vez disso, esta informações são recriadas na hierarquia de destino quando um cliente envia pela primeira vez as respetivas informações para o site atribuído. Para ajudar a reduzir os requisitos de largura de banda da rede e o processamento do servidor resultantes, considere migrar um pequeno número de clientes em fases, em vez de um grande número de clientes de uma só vez.  

 Além disso, não é possível migrar personalizações do inventário de hardware a partir de uma hierarquia de origem. Tem de as introduzir na hierarquia de destino, em separado da migração. Para obter informações sobre como alargar o inventário de hardware, consulte [como configurar o inventário](../../core/clients/manage/inventory/configure-hardware-inventory.md)de hardware .  
