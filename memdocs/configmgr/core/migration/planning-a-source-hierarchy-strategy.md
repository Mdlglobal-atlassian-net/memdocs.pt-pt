---
title: Estratégia de hierarquia de origem
titleSuffix: Configuration Manager
description: Configure uma hierarquia de origem e recolha dados de um site de origem antes de configurar um trabalho de migração do Gestor de Configuração.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28960753da06058ef181f94a5d11d9f2327ebf56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719681"
---
# <a name="plan-a-source-hierarchy-strategy-in-configuration-manager"></a>Planeie uma estratégia de hierarquia de origem no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de configurar um trabalho de migração no ambiente do Seu Gestor de Configuração, deve configurar uma hierarquia de origem e recolher dados de pelo menos um site de origem nessa hierarquia. Utilize as seguintes secções para o ajudar a planear configurar hierarquias de origem, configurar sites de origem e determinar como o Gestor de Configuração recolhe informações dos sites de origem na hierarquia de origem. 

##  <a name="source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a>Hierarquias de origem  
Uma hierarquia de origem é uma hierarquia do Gestor de Configuração que tem dados que pretende migrar. Quando configura a migração e especifica uma hierarquia de origem, especifica o local de alto nível da hierarquia de origem. Este site é também designado por site de origem. Sites adicionais de que pode migrar dados na hierarquia de origem também são chamados de sites de origem.  

-   Quando cria um trabalho de migração para migrar dados de uma hierarquia de origem do Gestor de Configuração de 2007, configura-os para migrar dados de um ou mais sítios de origem específicos na hierarquia de origem.  

-   Quando configura um trabalho de migração para migrar dados de uma hierarquia de origem que gere o System Center 2012 Configuration Manager ou mais tarde, basta especificar o site de alto nível.  

Só se pode criar uma hierarquia de origem de cada vez.  

-   Se criaruma nova hierarquia de origem, essa hierarquia torna-se automaticamente a atual hierarquia de origem substituindo a hierarquia de origem anterior.  

-   Quando configurar uma hierarquia de origem, deve especificar o site de alto nível da hierarquia de origem e especificar credenciais para o Gestor de Configuração usar para se ligar ao Fornecedor SMS e à base de dados do site de origem.  

-   O Gestor de Configuração utiliza estas credenciais para executar a recolha de dados para recuperar informações sobre os objetos e pontos de distribuição do site de origem.  

-   Como parte do processo de recolha dados, são identificados os sites subordinados na hierarquia de origem.  

-   Se a hierarquia de origem for uma hierarquia de Configuração 2007, pode configurar esses sites adicionais como sites de origem com credenciais separadas para cada site de origem.  

Embora possa criar várias hierarquias de origem sucessivamente, a migração está ativa para apenas uma hierarquia de origem de cada vez.  

-   Se criar uma hierarquia de origem adicional antes de completar a migração da atual hierarquia de origem, o Gestor de Configuração cancela quaisquer postos de trabalho de migração ativos e adia quaisquer trabalhos de migração programados para a atual hierarquia de origem.  

-   A hierarquia de origem recentemente configurada torna-se então a atual hierarquia de origem, e a hierarquia de origem original está agora inativa.  

-   Em seguida, pode criar credenciais de ligação, locais de origem adicionais e trabalhos de migração para a nova hierarquia de origem.  

Se restaurar uma hierarquia de origem inativa e não tiver usado previamente dados de migração de **limpeza,** pode ver os trabalhos de migração previamente configurados para essa hierarquia de origem. No entanto, para poder prosseguir a migração a partir dessa hierarquia terá de reconfigurar as credenciais para estabelecer ligação aos sites de origem aplicáveis na hierarquia e, em seguida, reagendar as tarefas de migração que não tenham sido concluídas.  

> [!CAUTION]  
>  Se migrar dados de mais do que uma hierarquia de origem, cada hierarquia de origem adicional terá de conter um conjunto exclusivo de códigos de site.  
> As hierarquias de origem e destino também requerem diferentes códigos de site.

Para mais informações sobre a configuração de uma hierarquia de origem, consulte a configuração de hierarquias de [origem e locais de origem para migração para o ramo atual do Gestor](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md) de Configuração  

##  <a name="source-sites"></a><a name="BKMK_Source_Sites"></a>Sites de origem  
 Os sites de origem são os sites da hierarquia de origem que contêm os dados que pretende migrar. O site de nível superior da hierarquia de origem é sempre o primeiro site de origem. Quando a migração recolhe dados do primeiro site de origem de uma nova hierarquia de origem, deteta informações sobre os sites adicionais dessa hierarquia.  

 Após a conclusão da recolha de dados do site de origem inicial, as ações seguintes a efetuar dependem da versão de produto da hierarquia de origem.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Sites de origem com o Configuration Manager 2007 SP2  
 Após a recolha de dados a partir do local de origem inicial da hierarquia SP2 do Gestor de Configuração 2007, não é preciso criar locais de origem adicionais antes de criar empregos de migração. No entanto, antes de poder migrar dados de sites adicionais, deve configurar sites adicionais como sites de origem, e o Gestor de Configuração deve recolher com sucesso dados desses sites.  

 Para recolher dados de sites adicionais, configura individualmente cada site como um site de origem. Isto requer que especifique as credenciais para o Gestor de Configuração ligar-se ao Fornecedor SMS e à base de dados do site de cada site de origem. Depois de configurar as credenciais para um site de origem, inicia-se o processo de recolha de dados para esse site.  

 Quando configurar sites de origem adicionais numa hierarquia de origem SP2 2007, tem de configurar os sites de origem de cima para baixo, o que significa que configura os sites de nível inferior. Pode configurar sites de origem num ramo da hierarquia a qualquer momento, mas deve configurar um site como um site de origem antes de configurar qualquer um dos seus sites infantis como locais de origem.  

> [!NOTE]  
>  Apenas os locais primários de uma hierarquia SP2 de 2007 são apoiados para a migração.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Sites de origem que executam System Center 2012 Configuration Manager ou posteriormente  
 Após a recolha de dados a partir do site de origem inicial do System Center 2012 Configuration Manager ou posterior hierarquia, não é preciso criar sites de origem adicionais nessa hierarquia de origem. Isto porque, ao contrário do Gestor de Configuração de 2007, estas versões do Gestor de Configuração utilizam uma base de dados partilhada, e a base de dados partilhada permite identificar e depois migrar todos os objetos disponíveis a partir do site de origem inicial.  

 Quando configura as contas de acesso para recolher dados, poderá ter de conceder ao Source **Site Site SMS O** acesso a vários computadores da hierarquia de origem. Isto pode ser necessário quando o site de origem suporta múltiplas instâncias do Fornecedor de SMS, cada uma num computador diferente. Quando a recolha de dados é iniciada, o site de nível superior da hierarquia de destino contacta o site de nível superior da hierarquia de origem para identificar as localizações do Fornecedor de SMS desse site. Só é identificada a primeira instância do Fornecedor de SMS. Se o processo de recolha de dados não conseguir aceder ao Fornecedor de SMS na localização identificada, o processo falhará, não tentando estabelecer ligação a computadores adicionais que executem uma instância do Fornecedor de SMS desse site.  

##  <a name="data-gathering"></a><a name="BKMK_Data_Gathering"></a>Recolha de dados  
 Imediatamente após especificar uma hierarquia de origem, configurar credenciais para cada site de origem adicional numa hierarquia de origem, ou partilhar os pontos de distribuição para um site de origem, o Gestor de Configuração começa a recolher dados do site de origem.  

 Em seguida, o processo de recolha de dados repete-se numa agenda simples, para manter a sincronização com eventuais alterações dos dados do site de origem. Por predefinição, o processo é repetido a cada quatro horas. Pode alterar a programação para este ciclo editando as **Propriedades** do site de origem. O processo inicial de recolha de dados deve rever todos os objetos na base de dados do Gestor de Configuração e pode demorar muito tempo a terminar. Os processos de recolha de dados subsequentes identificam apenas as alterações dos dados, demorando menos tempo.  

 Para recolher os dados, o site de nível superior da hierarquia de destino estabelece ligação ao Fornecedor de SMS e à base de dados do site de origem para obter uma lista de objetos e pontos de distribuição. Estas ligações utilizam as contas de acesso do site de origem. Para obter informações sobre as configurações necessárias para recolher dados, consulte [pré-requisitos para a migração](../../core/migration/prerequisites-for-migration.md).  

 Pode iniciar e parar o processo de recolha de dados utilizando dados **de recolha agora** e parar de recolher **dados** na consola do Gestor de Configuração.  

 Depois de utilizar dados de recolha de **dados** para um site de origem por qualquer motivo, deve reconfigurar as credenciais para o site antes de poder recolher dados desse site novamente. Até reconfigurar o site de origem, o Gestor de Configuração não pode identificar novos objetos ou alterações em objetos previamente migrados nesse site.  

> [!NOTE]  
>  Antes de expandir um local primário autónomo para uma hierarquia com um site de administração central, deve parar todos os dados recolhidos. Pode reconfigurar a recolha de dados após a expansão do site.  

### <a name="gather-data-now"></a>Recolher Dados Agora  
 Após a execução do processo inicial de recolha de dados de um site, o processo é repetido para identificar os objetos que tenham sido atualizados desde o último ciclo de recolha de dados. Também pode utilizar a ação **Gather Data Now** na consola 'Gestor de Configuração' para iniciar imediatamente o processo e repor a hora de início do próximo ciclo.  

 Após a conclusão com êxito do processo de recolha de dados de um site de origem, poderá partilhar os pontos de distribuição do site de origem e configurar as tarefas de migração de dados do site. A recolha de dados é um processo de repetição para a migração, e continua até alterar a hierarquia de origem ou usar dados de **recolha** de dados para terminar o processo de recolha de dados para esse site.  

### <a name="stop-gathering-data"></a>Parar a Recolha de Dados  
 Pode utilizar dados de recolha de **dados** para terminar o processo de recolha de dados para um site de origem quando já não pretende que o Gestor de Configuração identifique objetos novos ou alterados a partir desse site. Esta ação também impede o Gestor de Configuração de oferecer aos clientes na hierarquia de destino quaisquer pontos de distribuição partilhadas da fonte como locais de conteúdo para o conteúdo que você emigraram.  

 Para parar de recolher dados de cada site de origem, deve executar dados de **recolha de dados** nos sites de origem de nível inferior e, em seguida, repetir o processo em cada site-mãe. O site de nível superior da hierarquia de origem terá de ser o último em que a recolha de dados é interrompida. Terá de interromper a recolha de dados em cada site subordinado antes de efetuar essa ação num site principal. Normalmente, apenas interromperá a recolha de dados quando estiver pronto para concluir o processo de migração.  

 Depois de deixar de recolher dados para um site de origem, as informações previamente recolhidas sobre objetos e coleções desse site permanecem disponíveis para serem usadas quando cria novos postos de trabalho migratórios. No entanto, não vê quaisquer novos objetos ou coleções, nem vê alterações que foram feitas aos objetos existentes. Se reconfigurar o site de origem e recomeçar a recolher dados, verá o estado e informações sobre os objetos anteriormente migrados.  
