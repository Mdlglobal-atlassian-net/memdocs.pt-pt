---
title: Migrar dados
titleSuffix: Configuration Manager
description: Saiba como transferir dados de uma hierarquia de origem para uma hierarquia de destino do Gestor de Configuração.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718904"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Migrar dados entre hierarquias em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize a migração para transferir dados de uma hierarquia de origem suportada para a sua hierarquia de destino do Gestor de Configuração (filial atual). Quando se migra dados de uma hierarquia de origem:  

- Acede a dados das bases de dados do site na infraestrutura de origem e, em seguida, transfere esses dados para o seu ambiente atual.  

- A migração não altera os dados na hierarquia de origem. Em vez disso, descobre os dados e armazena uma cópia na base de dados da hierarquia de destino.  

Considere os seguintes pontos quando planeia a sua estratégia de migração:  

- Pode migrar uma infraestrutura SP2 de Configuração existente 2007 para O Gestor de Configuração (ramo atual).  

- Pode migrar alguns ou todos os dados suportados de um site de origem.  

- Pode migrar os dados de um único site de origem para vários sites diferentes da hierarquia de destino.  

- Pode mover dados de vários sites de origem para um único site da hierarquia de destino.  


O vídeo seguinte discute e demonstra dois [cenários comuns de migração.](#BKMK_MigrationScenarios) Também inclui opções para incluir o Microsoft Azure em planos de migração.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a>Conceitos  

 O Gestor de Configuração utiliza os seguintes conceitos e termos durante a migração.  

#### <a name="source-hierarchy"></a>Hierarquia de origem
Uma hierarquia que executa uma versão suportada do Gestor de Configuração e tem dados que pretende migrar. Ao configurar a migração, identifica-se a hierarquia de origem quando especifica o local de alto nível de uma hierarquia de origem. Após ter especificado uma hierarquia de origem, o site de nível superior da hierarquia de destino recolhe dados da base de dados do site de origem designado para identificar os dados que pode migrar. 

Para mais informações, consulte [as hierarquias source](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Sites de origem
Os sites da hierarquia de origem que contêm dados que pode migrar para a hierarquia de destino. 

Para mais informações, consulte [os sites Source](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Hierarquia de destino
Uma hierarquia de Gestor de Configuração (ramo atual) onde a migração corre para importar dados de uma hierarquia de origem.

#### <a name="data-gathering"></a>Recolha de dados
O processo contínuo de identificar informações numa hierarquia de origem que pode migrar para a sua hierarquia de destino. O Gestor de Configuração verifica a hierarquia de origem num horário. Este processo identifica quaisquer alterações à informação na hierarquia de origem que emigraram anteriormente e que poderá querer atualizar na hierarquia de destino.

Para mais informações, consulte a [recolha de dados.](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)

#### <a name="migration-jobs"></a>Tarefas de migração
O processo de configuração de objetos específicos para migrar e, em seguida, a gestão da migração desses objetos para a hierarquia de destino.

Para mais informações, consulte o Planeamento de uma estratégia de [trabalho de migração.](planning-a-migration-job-strategy.md)

#### <a name="client-migration"></a>Migração de clientes
O processo de transferência de informações utilizadas pelos clientes da base de dados do site de origem para a base de dados da hierarquia de destino. Esta migração de dados é seguida de uma atualização do software cliente em dispositivos para a versão de software cliente a partir da hierarquia de destino.

Para mais informações, consulte O Planeamento de uma estratégia de [migração de clientes.](planning-a-client-migration-strategy.md)

#### <a name="shared-distribution-points"></a>Pontos de distribuição partilhados
Os pontos de distribuição da hierarquia de origem que o Gestor de Configuração partilha com a hierarquia de destino durante o período de migração.

Durante o período de migração, os clientes atribuídos a sites na hierarquia de destino podem obter conteúdo a partir de pontos de distribuição partilhados.

Para mais informações, consulte pontos de [distribuição de partilha entre as hierarquias de origem e destino.](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)

#### <a name="monitoring-migration"></a>Monitorização da migração
O processo de monitorização de atividades de migração. Monitoriza o progresso migratório e o sucesso do nó **migratório** no espaço de trabalho da **Administração.**

Para obter mais informações, consulte [Planeamento para monitorizar a atividade migratória.](planning-to-monitor-migration-activity.md)

#### <a name="stop-gathering-data"></a>Parar a recolha de dados
O processo de interrupção da recolha de dados a partir de sites de origem. Quando já não tem dados para migrar de uma hierarquia de origem, ou se quiser parar as atividades relacionadas com a migração, pode configurar a hierarquia de destino para parar de recolher dados da hierarquia de origem.

Para mais informações, consulte a [recolha de dados.](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)

#### <a name="clean-up-migration-data"></a>Limpar dados de migração
O processo de conclusão da migração de uma hierarquia de origem através da remoção das informações sobre a migração da base de dados de hierarquias de destino.

Para mais informações, consulte [Planeamento para completar a migração.](planning-to-complete-migration.md)



## <a name="typical-workflow"></a>Fluxo de trabalho típico  

Para criar um fluxo de trabalho para a migração:

1.  Especifique uma hierarquia de origem suportada.  

2.  Configurar a recolha de dados. A recolha de dados permite ao Gestor de Configuração recolher informações sobre dados que possam migrar da hierarquia de origem.  

     O Gestor de Configuração repete automaticamente o processo para recolher dados num horário simples até que pare o processo de recolha de dados. Por padrão, o processo de recolha de dados repete-se a cada quatro horas para que o Gestor de Configuração possa identificar alterações aos dados na hierarquia de origem. A recolha de dados também é necessária para partilhar pontos de distribuição.  

3.  Crie tarefas de migração para migrar dados entre a hierarquia de origem e a hierarquia de destino.  

4.  Pode parar o processo de recolha de dados a qualquer momento utilizando a ação **Stop Gathering Data.** Quando para a recolha de dados, o Gestor de Configuração já não identifica alterações nos dados na hierarquia de origem e já não pode partilhar pontos de distribuição. Normalmente, utiliza esta ação quando já não pretende migrar dados nem partilhar pontos de distribuição da hierarquia de origem.  

5.  Opcionalmente, após a recolha de dados ter parado em todos os sites para a hierarquia de origem, você pode limpar os dados de migração usando a ação **Clean Up Migration Data.** Esta ação elimina os dados históricos sobre a migração de uma hierarquia de origem da base de dados da hierarquia de destino.  

Depois de migrar dados, e já não precisar da hierarquia de origem para gerir dispositivos no seu ambiente, pode desativar essa hierarquia de origem e infraestrutura.  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a>Cenários  

 O Gestor de Configuração suporta os seguintes cenários de migração:
- [Migração a partir de hierarquias do Configuration Manager 2007](#bkmk_2007)  
- [Migração do Gestor de Configuração 2012 ou de outra hierarquia do Gestor de Configuração](#bkmk_2012)

> [!NOTE]  
>  A expansão de uma hierarquia que tem um local autónomo numa hierarquia que tem um site de administração central não é classificada como uma migração. Para obter informações sobre a expansão da hierarquia, consulte [Expandir um local primário autónomo.](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a>Migração das hierarquias do Gestor de Configuração de 2007  

 Quando utiliza a migração para migrar dados do Gestor de Configuração de 2007, pode manter o seu investimento na infraestrutura do site existente e obter os seguintes benefícios:  

#### <a name="site-database-improvements"></a>Melhorias da base de dados do site
A base de dados do Gestor de Configuração (ramo atual) suporta o Unicode completo.

#### <a name="database-replication-between-sites"></a>Replicação da base de dados entre sites
A replicação no Gestor de Configuração (ramo atual) baseia-se no Microsoft SQL Server. Este comportamento melhora o desempenho da transferência de dados site-to-site.

#### <a name="user-centric-management"></a>Gestão centrada no utilizador
Os utilizadores são o foco das tarefas de gestão no Gestor de Configuração (ramo atual). Por exemplo, pode distribuir software a um utilizador mesmo que não saiba o nome do dispositivo para esse utilizador. Além disso, o Gestor de Configuração dá aos utilizadores muito mais controlo sobre o software instalado nos seus dispositivos e quando esse software está instalado.

#### <a name="hierarchy-simplification"></a>Simplificação da hierarquia
O Gestor de Configuração (ramo atual) permite-lhe construir uma hierarquia de site mais simples. Esta melhoria deve-se à introdução do tipo de site da administração central e às alterações ao comportamento dos sítios primários e secundários. O Gestor de Configuração (ramo atual) utiliza menos largura de banda de rede e requer menos servidores do que as versões anteriores.

#### <a name="role-based-administration"></a>Administração baseada em funções
Este modelo central de segurança no Gestor de Configuração (atual filial) oferece segurança e gestão em toda a hierarquia que correspondem aos seus requisitos administrativos e empresariais.

> [!NOTE]  
>  Devido às alterações de design que foram introduzidas pela primeira vez no System Center 2012 Configuration Manager, não é possível atualizar o Gestor de Configuração 2007 para o Gestor de Configuração (ramo atual). A atualização no local é suportada desde o System Center 2012 Configuration Manager até ao Gestor de Configuração (ramo atual).  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a>Migração do Gestor de Configuração 2012 ou de outra hierarquia do Gestor de Configuração  
 O processo de migração de dados de uma hierarquia do System Center 2012 do Gestor de Configuração ou do Gestor de Configuração é o mesmo. Este processo inclui a migração de dados de várias hierarquias de origem para uma hierarquia de destino único. Poderá utilizar este processo quando a sua empresa obtém recursos adicionais que já são geridos pelo Gestor de Configuração. Além disso, pode migrar dados de um ambiente de teste para o ambiente de produção do Seu Gestor de Configuração. Este processo permite manter o seu investimento no ambiente de teste do Gestor de Configuração.  



## <a name="see-also"></a>Consulte também  

-   [Planeamento para migração para Gestor de Configuração](planning-for-migration.md)  

-   [Configurar hierarquias de origem e locais de origem para migração](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operações de migração](operations-for-migration.md)  

-   [Segurança e privacidade da migração](security-and-privacy-for-migration.md)  

-   [Começar a utilizar o Configuration Manager](../servers/deploy/start-using.md)
