---
title: Objetos migrados
titleSuffix: Configuration Manager
description: Aprenda a planear a migração de objetos entre hierarquias num ambiente de ramificação atual do Gestor de Configuração.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9777fb12a2d63a990587386ac33cb2749bf19a4e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719653"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Plano para a migração de objetos do Gestor de Configuração para o ramo atual do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Com o ramo atual do Gestor de Configuração, pode migrar muitos dos diferentes objetos que estão associados a diferentes funcionalidades encontradas num site de origem.

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a>Plano para migrar atualizações de software  
 Pode migrar objetos de atualização de software, como pacotes de atualização de software e implementações de atualizações de software.  

 Para migrar com sucesso objetos de atualização de software, tem primeiro de configurar a sua hierarquia de destino com configurações que correspondam ao ambiente da hierarquia de origem. Isso requer as seguintes ações:  

-   Implementar um ponto de atualização de software ativo na hierarquia do destino  

-   Configurar o catálogo de produtos e idiomas para corresponder à configuração da sua hierarquia de origem  

-   Sincronizar o ponto de atualização de software na hierarquia do destino com os Serviços de Atualização do Servidor do Windows (WSUS)  

Ao migrar atualizações de software, tenha em consideração:  

-   A migração de objetos de atualização de software pode falhar quando não sincronizou informação na hierarquia do seu destino para corresponder à configuração da sua hierarquia de origem.  

    > [!WARNING]  
    >  O Gestor de Configuração não suporta a utilização da ferramenta WSUSutil para sincronizar dados entre uma hierarquia de origem e destino.  

-   Não é possível migrar atualizações personalizadas que tenham sido publicadas utilizando o System Center Updates Publisher. Em vez disso, as atualizações personalizadas devem ser republicadas na hierarquia de destino.  

Quando se migra de uma hierarquia de origem do Gestor de Configuração de 2007, o processo de migração modifica alguns objetos de atualização de software para o formato utilizado pela hierarquia de destino. Utilize a tabela seguinte para o ajudar a planear a migração de objetos de atualização de software a partir do Configuração Manager 2007.  

|Objeto de Gestor de Configuração 2007|Nome do objeto após a migração|  
|-----------------------------------|---------------------------------|  
|Listas de atualização de software|As listas de atualização de software são convertidas em grupos de atualização de software.|  
|Implementações de atualizações de software|As implementações de atualização de software são convertidas em implementações e grupos de atualização.<br /><br /> Depois de migrar uma implementação de atualização de software do Diretor de Configuração 2007, deve ative-a na hierarquia de destino antes de a implementar.|  
|Pacotes de atualização de software|Os pacotes de atualização de software mantêm a mesma designação.|  
|Modelos de atualização de software|Os modelos de atualização de software mantêm a sua designação.<br /><br /> O valor **de duração** nos modelos de implementação do Gestor de Configuração de 2007 não migra.|  

Quando migra objetos de um System Center 2012 Configuration Manager ou de Configuração da hierarquia de origem do ramo atual, os objetos de atualização do software não são modificados.  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a>Plano para migrar conteúdo  
 É possível migrar conteúdo de uma hierarquia de origem suportada para a hierarquia de destino. Para uma hierarquia de origem do Gestor de Configuração de 2007, este conteúdo inclui pacotes e programas de distribuição de software e aplicações virtuais, como a Virtualização de Aplicações da Microsoft (App-V). Para o System Center 2012 Configuração Manager e Configuração De Gestão de hierarquias de fonte de filial, este conteúdo inclui aplicações e aplicações virtuais App-V. Quando se migra o conteúdo entre hierarquias, os ficheiros de origem comprimido migram para a hierarquia do destino.  

### <a name="packages-and-programs"></a>Pacotes e programas  
 Ao migrar pacotes e programas, estes não são modificados pela migração. No entanto, antes de os migrar, tem de configurar cada pacote para utilizar um caminho da Convenção Universal de Nomeação (UNC) para a sua localização de ficheiros de origem. Como parte da configuração para migrar pacotes e programas, terá de atribuir um site na hierarquia de destino para gerir este conteúdo. O conteúdo não é migrado do site designado, mas após a migração, o site designado acede à localização original do ficheiro de origem utilizando o mapeamento da UnC.  

 Depois de migrar um pacote e programa para a hierarquia de destino, e enquanto a migração da hierarquia de origem permanece ativa, pode disponibilizar o conteúdo aos clientes nessa hierarquia utilizando um ponto de distribuição partilhado. Para utilizar um ponto de distribuição partilhado, o conteúdo terá de permanecer acessível no ponto de distribuição do site de origem. Para saber mais sobre pontos de distribuição partilhados, consulte pontos de [distribuição de partilha entre as hierarquias](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) de origem e destino no Plano de uma estratégia de migração de implementação de [conteúdos.](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

 Para conteúdos que tenham migrado, se a versão de conteúdo mudar na hierarquia de origem ou na hierarquia de destino, os clientes já não podem aceder ao conteúdo a partir do ponto de distribuição partilhada na hierarquia de destino. Neste cenário, é necessário remigrar o conteúdo para restaurar uma versão consistente do pacote entre a hierarquia de origem e a hierarquia de destino. Esta informação sincroniza durante o ciclo de recolha de dados.  

> [!TIP]  
>  Por cada pacote que migrar, atualize o pacote na hierarquia de destino. Esta ação pode evitar problemas na implementação do pacote nos pontos de distribuição na hierarquia de destino. No entanto, quando atualizar um pacote sobre o ponto de distribuição na hierarquia de destino, os clientes dessa hierarquia deixarão de poder obter esse pacote a partir de um ponto de distribuição partilhada. Para atualizar um pacote na hierarquia de destino, na consola do Gestor de Configuração, vá à Biblioteca de Software, clique no pacote e, em seguida, selecione Pontos de Distribuição de **Atualização**. Faça esta ação por cada pacote que migra.  

> [!TIP]  
> Utilize o Gestor de Conversão de Pacotes para converter pacotes e programas em aplicações de Gestor de Configuração. Para mais informações, consulte O Gestor de Conversão de [Pacotes](../../apps/pcm/package-conversion-manager.md).  

### <a name="virtual-applications"></a>Aplicações virtuais  
Ao migrar pacotes App-V de um site de Configuração 2007 suportado, o processo de migração converte-os em aplicações na hierarquia de destino. Além disso, com base em anúncios existentes para o pacote App-V, os seguintes tipos de implementação são criados na hierarquia de destino:  

-   Se não existirem anúncios, é criado um tipo de implementação que utilize as predefinições do tipo de implementação.  

-   Se existir um anúncio, é criado um tipo de implementação que utiliza as mesmas definições que o anúncio do Gestor de Configuração de 2007.  

-   Se existirem vários anúncios, é criado um tipo de implementação para cada anúncio do Gestor de Configuração de 2007, utilizando as definições para esse anúncio.  

> [!IMPORTANT]  
>  Se migrar um pacote app-V de Configuração 2007 anteriormente migrado, a migração falha porque os pacotes de aplicações virtuais não suportam o comportamento de migração de sobreposição. Neste cenário, terá de eliminar o pacote de aplicação virtual migrado da hierarquia de destino e, em seguida, criar uma nova tarefa de migração para migrar a aplicação virtual.  

> [!NOTE]  
>  Depois de migrar um pacote App-V, pode utilizar o assistente de conteúdo de atualização para alterar o caminho de origem para os tipos de implementação do App-V. Para saber mais sobre como atualizar os conteúdos para um tipo de implementação, consulte como gerir tipos de implementação em tarefas de [Gestão para aplicações de Gestor](../../apps/deploy-use/management-tasks-applications.md)de Configuração .  

Quando se migra de um System Center 2012 Configuration Manager ou de Configuração diretor a hierarquia de fonte de filial, pode migrar objetos para o ambiente virtual App-V, além de tipos e aplicações de implementação app-V. Para mais informações sobre ambientes App-V, consulte [aplicações virtuais App-V.](../../apps/get-started/deploying-app-v-virtual-applications.md)  

### <a name="advertisements"></a>Anúncios  
Você pode migrar anúncios de um site de origem suportado de Configuração 2007 para a hierarquia de destino usando migração baseada em recolha. Se atualizar um cliente, este manterá o histórico dos anúncios anteriormente executados, para impedir que o cliente volte a executar os anúncios migrados.  

> [!NOTE]  
>  Não é possível migrar anúncios para pacotes virtuais. Esta é uma exceção à migração de anúncios.  

### <a name="applications"></a>Aplicações  
 Pode migrar aplicações de um Gestor de Configuração suportado do System Center 2012 ou do Gestor de Configuração atual para uma hierarquia de destino. Se reatribuir um cliente da hierarquia de origem para a hierarquia de destino, o cliente manterá o histórico das aplicações anteriormente instaladas, para impedir que o cliente volte a executar as aplicações migradas.  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a>Plano para migrar coleções  
 Pode migrar os critérios para coleções a partir de um Gestor de Configuração suportado do System Center 2012 ou da hierarquia atual do Gestor de Configuração. Para isso, usa-se um trabalho de migração baseado em objetos. Ao migrar uma coleção migrará as respetivas regras, e não as informações sobre os membros da coleção nem as informações ou objetos relacionados com os membros da coleção.  

 A migração do objeto de recolha não é suportada quando se migra de uma hierarquia de origem do Gestor de Configuração de 2007.  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a>Plano para migrar implementações do sistema operativo  
É possível migrar os seguintes objetos de implementação de sistemas operativos a partir de uma hierarquia de origem suportada:  

-   Imagens e pacotes de sistemas operativos. O caminho de origem das imagens de arranque é atualizado para a localização de imagem padrão para o Kit de Instalação Administrativa do Windows (Windows AIK) no site do destino. Eis os requisitos e limitações da migração de imagens e pacotes de sistemas operativos:  

    -   Para migrar com sucesso ficheiros de imagem, a conta de computador do servidor SMS Provider para o site de alto nível da hierarquia de destino deve ter permissão **de Leitura** e **Escrita** para os ficheiros de fonte de imagem da localização do Windows AIK do site de origem.  

    -   Quando migrar um pacote de instalação do sistema operativo, certifique-se de que a configuração da embalagem no site de origem aponta para a pasta que tem o ficheiro WIM e não para o próprio ficheiro WIM. Se o pacote de instalação apontar para o ficheiro WIM, a migração do pacote de instalação falhará.  

    -   Quando migra um pacote de imagem de arranque de um site de origem do Gestor de Configuração de 2007, o id do pacote não é mantido no local do destino. O resultado é que os clientes da hierarquia de destino não poderão utilizar pacotes de imagens de arranque que estejam disponíveis em pontos de distribuição partilhados.  

-   Sequências de tarefas. Quando se migra uma sequência de tarefas que tem uma referência a um pacote de instalação de clientes, essa referência é substituída por uma referência ao pacote de instalação do cliente da hierarquia de destino.  

    > [!NOTE]  
    >  Quando se migra uma sequência de tarefas, o Gestor de Configuração pode migrar objetos que não são necessários na hierarquia do destino. Estes objetos incluem imagens de boot e pacotes de instalação de clientes de 2007.  

-   Controladores e pacotes de controladores. Quando migra os pacotes de condutores, a conta de computador do Fornecedor SMS na hierarquia de destino deve ter total controlo sobre a fonte do pacote.

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a>Plano para migrar a gestão de configuração desejada  
É possível migrar itens de configuração e linhas de base de configuração.  

> [!NOTE]  
>  Itens de configuração não interpretados das hierarquias de origem do Diretor de Configuração 2007 não são suportados para a migração. Não é possível migrar nem importar estes itens de configuração para a hierarquia de destino. Para saber mais sobre itens de configuração não interpretados, consulte itens de configuração não interpretados nos [itens de configuração sobre configuração no](https://go.microsoft.com/fwlink/?LinkId=103846) tópico de Gestão de Configuração Desejado na biblioteca de documentação de Configuração 2007.  

Pode importar Pacotes de Configuração 2007 do Gestor de Configuração. O processo de importação converte automaticamente os pacotes de configuração para serem compatíveis com o ramo atual do Gestor de Configuração.  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a>Plano para migrar fronteiras  
 É possível migrar limites entre hierarquias. Quando se migram fronteiras do Gestor de Configuração 2007, cada limite do local de origem migra ao mesmo tempo e é adicionado a um novo grupo de fronteiras que é criado na hierarquia de destino. Quando migra limites de um System Center 2012 Configuration Manager ou configuração hierarquia de filial atual, cada limite que selecionar é adicionado a um novo grupo de limites na hierarquia de destino.  

 Cada grupo de limites criado automaticamente está ativado para localização de conteúdo, mas não para atribuição de site. Deste modo, é evitada a sobreposição de limites para atribuição de sites entre as hierarquias de origem e de destino. Quando migra de um site de origem do Gestor de Configuração de 2007, isto ajuda a evitar que novos clientes do Gestor de Configuração 2007 que se instalam sejam incorretamente atribuídos à hierarquia de destino. Por predefinição, os clientes da filial atual do Gestor de Configuração não atribuem automaticamente aos sites do Gestor de Configuração 2007.  

 Durante a migração, se partilhar um ponto de distribuição com a hierarquia de destino, todos os limites associados a essa distribuição migram automaticamente para a hierarquia de destino. Na hierarquia do destino, a migração cria um novo grupo de fronteiras só para leitura para cada ponto de distribuição partilhado. Se alterar os limites do ponto de distribuição da hierarquia de destino, o grupo de limites da hierarquia de destino será atualizado com estas alterações durante o próximo ciclo de recolha de dados.  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a>Plano para migrar relatórios  
O Gestor de Configuração não suporta a migração de relatórios. Em alternativa, utilize o SQL Server Reporting Services Report Builder para exportar relatórios da hierarquia de origem e, em seguida, importá-los para a hierarquia de destino.  

> [!NOTE]  
>  Como existem alterações de esquemas para relatórios entre o Diretor de Configuração 2007 e o Diretor de Configuração da atual filial, teste cada relatório que importa de uma hierarquia do Gestor de Configuração de 2007 para garantir que funciona como esperado.  

Para mais informações sobre reportagens, consulte [Introdução à reportagem](../servers/manage/introduction-to-reporting.md).  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a>Plano para migrar pastas organizacionais e de pesquisa  
 É possível migrar pastas organizacionais e pastas de procura de uma hierarquia de origem suportada para uma hierarquia de destino. Além disso, a partir de um System Center 2012 Configuration Manager ou Configuração Manager atual hierarquia de fonte de filial, você pode migrar os critérios para uma pesquisa guardada para uma hierarquia de destino.  

 Por predefinição, o processo de migração mantém as estruturas de pastas de procura e de pastas administrativas de objetos e coleções. No entanto, no assistente create migration job, na página **Definições,** pode configurar um trabalho de migração para não migrar a estrutura organizacional para objetos, desverificando a caixa para esta opção. As estruturas organizacionais das coleções são sempre mantidas.  

 Uma exceção a esta regra é uma pasta de procura com aplicações virtuais. Quando um pacote App-V é migrado, o pacote App-V é transformado numa aplicação no Gestor de Configuração. Após a migração da pasta de pesquisa, apenas os pacotes restantes são encontrados, e a pasta de pesquisa não pode localizar um pacote App-V devido a esta conversão para uma aplicação quando o pacote App-V migra.  

 Quando migra uma pesquisa guardada de um System Center 2012 Configuration Manager ou configuração atual da hierarquia de fonte de filial, migra os critérios para a pesquisa, e não a informação sobre os resultados da pesquisa. A migração de uma pesquisa guardada não é aplicável a partir de um site de origem do Gestor de Configuração de 2007.  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a>Plano para migrar personalizações de Inteligência de Ativos  
 É possível migrar personalizações do Asset Intelligence de uma hierarquia de origem suportada para uma hierarquia de destino. Não existem alterações significativas na estrutura das personalizações de Inteligência de Ativos entre o Gestor de Configuração de 2007 e o atual ível do Gestor de Configuração.  

> [!NOTE]  
> O ramo atual do Gestor de Configuração não suporta a migração de objetos de Inteligência de Ativos a partir de um site do Gestor de Configuração de 2007 que está a usar o Serviço de Inteligência de Ativos 2.0 (AIS 2.0).  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a>Plano para migrar regras de medição de software personalizações  
 Não existem alterações significativas na medição de software entre o Diretor de Configuração de 2007 e o atual diretor de configuração. É possível migrar as regras de medição de software de uma hierarquia de origem suportada para uma hierarquia de destino.  

 Por predefinição, as regras de medição de software que migra para uma hierarquia de destino não estão associadas a um site específico da hierarquia de destino e, em vez disso, aplicam-se a todos os clientes da hierarquia. Para aplicar uma regra de medição de software a clientes de um site específico, tem de editar a regra de medição após a respetiva migração.  
