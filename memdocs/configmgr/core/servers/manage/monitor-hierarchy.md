---
title: Monitorize a hierarquia
titleSuffix: Configuration Manager
description: Aprenda a monitorizar a sua infraestrutura no Gestor de Configuração utilizando o espaço de trabalho de Monitorização na consola.
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66fc6744ef7d1aaf90a5e7339cc9a5174c0d33f6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713703"
---
# <a name="monitor-the-hierarchy"></a>Monitorize a hierarquia

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para monitorizar a sua hierarquia no Gestor de Configuração, utilize o espaço de trabalho **de Monitorização** na consola 'Gestor de Configuração'.  

> [!NOTE]  
> A exceção a este local é quando os locais de migração. Monitorizou este processo no **nó** migratório do espaço de trabalho da **Administração.** Para mais informações, consulte Operações para migrar para o gerente de [configuração.](../../migration/operations-for-migration.md)  

Juntamente com a utilização da consola 'Gestor de Configuração' para monitorização, utilize as seguintes funcionalidades:

- [Introdução aos relatórios](introduction-to-reporting.md)
- [Ficheiros de registo](../../plan-design/hierarchy/log-files.md).  

Quando monitorizar sites, procure sinais que indiquem problemas que exijam uma ação da sua parte. Por exemplo:  

- Uma acumulação de ficheiros em servidores de site e sistemas de sites.  

- Mensagens de estado que indiquem um erro ou um problema.  

- Falha de comunicações intra-site.  

- Mensagens de erro e aviso no registo de eventos do sistema dos servidores.  

- Mensagens de erro e aviso no registo de erros do Microsoft SQL Server.  

- Sites ou clientes que não reportam o estado há muito tempo.  

- Resposta lenta da base de dados do SQL Server.  

- Sinais de falha de hardware.  

Se as tarefas de monitorização revelarem sinais de problemas, investigue a origem do problema. Em seguida, repara-o rapidamente para minimizar o risco de uma falha no local.  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a>Monitorizar tarefas comuns de gestão

O Gestor de Configuração fornece monitorização incorporada a partir da consola Do Gestor de Configuração.

### <a name="alerts"></a>Alertas

Para mais informações, consulte [monitor alertas](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts).  

### <a name="compliance-settings"></a>Definições de compatibilidade

Para mais informações, consulte [Como monitorizar as definições de conformidade](../../../compliance/deploy-use/monitor-compliance-settings.md).

### <a name="content"></a>Conteúdo

Para obter informações gerais sobre a monitorização de conteúdos, consulte Gerir a [infraestrutura](../deploy/configure/manage-content-and-content-infrastructure.md)de conteúdos e conteúdos.  

Para obter mais informações sobre a monitorização de tipos específicos de conteúdo:

- [Monitorizar aplicações](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Monitorizar pacotes e programas](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Monitorizar conteúdo para atualizações de software](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [Monitorizar o conteúdo das implementações de OS](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Endpoint Protection

Para mais informações, consulte [Como monitorizar a Proteção do Ponto Final](../../../protect/deploy-use/monitor-endpoint-protection.md).  

### <a name="os-deployment"></a>Implementação de SO

Para mais informações, consulte [as implementações do Monitor OS](../../../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="monitor-power-management"></a>Monitorizar a gestão de energia

Para mais informações, consulte [Como monitorizar e planear a gestão de energia.](../../clients/manage/power/monitor-and-plan-for-power-management.md)  

### <a name="monitor-software-metering"></a> Monitorizar a medição de software

Para obter mais informações, consulte o [uso da aplicação Monitor com a medição de software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

### <a name="monitor-software-updates"></a>Monitorizar atualizações de software

Para mais informações, consulte [as atualizações](../../../sum/deploy-use/monitor-software-updates.md)de software do Monitor .  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a>Monitorize a hierarquia do site

O nó da Hierarquia do **Site** do espaço de trabalho de **Monitorização** fornece-lhe uma visão geral da hierarquia do Gestor de Configuração e links interlocais. Pode utilizar duas vistas:  

- **Diagrama da hierarquia**: Exibe a sua hierarquia como um mapa de topologia simplificado que mostra apenas informações vitais. Para mais informações, consulte o [diagrama da Hierarquia.](#hierarchy-diagram)  

- **Vista Geográfica**: Exibe os seus sites num mapa geográfico mostrando as localizações do local que configura. Para mais informações, consulte [a vista geográfica.](#geographical-view)  

Utilize o nó **da Hierarquia** do Site para monitorizar a saúde de cada site. Monitorize também as ligações de replicação intersite e a sua relação com fatores externos, como uma localização geográfica.  

Tanto o estado do site como o estado de ligação intersite replicam-se como dados do site e não dados globais. Quando liga a consola do Gestor de Configuração a um site primário infantil, não é possível visualizar o site ou o estado de ligação para outros sites primários ou para os seus sites secundários infantis. Por exemplo, numa hierarquia com vários locais primários, quando liga a consola a um local primário, pode ver o estado dos sites secundários infantis, o local principal e o site da administração central. Nesta visão, não é possível ver o estado de outros sites abaixo do site da administração central.  

Para controlar o visor no nó da Hierarquia do **Site,** utilize a ação **Configurar Definições.** A hierarquia replica as definições que configura neste nó.  

### <a name="hierarchy-diagram"></a>Diagrama de Hierarquia

O diagrama da hierarquia apresenta os sites num mapa de topologia. Selecione um site e veja um resumo da mensagem de estado desse site. Percorra para visualizar mensagens de estado e aceda ao site **Propriedades**.  

Para ver o estado de alto nível de um site ou ligação de replicação entre os sites, passe o ponteiro do rato sobre o objeto. O estado da ligação de replicação não se replica globalmente. Para ver os detalhes da ligação de replicação entre todos os locais primários de uma hierarquia, ligue a consola ao site da administração central.  

As seguintes opções modificam o diagrama da hierarquia:  

#### <a name="groups"></a>Grupos

Configure o número de locais primários e locais secundários que desencadeiem uma mudança no diagrama da hierarquia. Esta alteração no visor combina os sites num único objeto. Em seguida, você vê o número total de sites e um alto nível de mensagens de estado e estado do site. As configurações de grupo não afetam a vista geográfica.  

#### <a name="favorite-sites"></a>Sites favoritos

Especifique sites individuais como um site favorito. Um ícone de estrela identifica um site favorito no diagrama da hierarquia. Os sites favoritos não são combinados com outros sites quando você usa grupos. São sempre exibidos individualmente.  

### <a name="geographical-view"></a>Vista Geográfica

A vista geográfica apresenta a localização de cada site num mapa geográfico. Apenas exibe sites que configura com uma localização. Ao selecionar um site nesta vista, mostra links de replicação para sites de pais ou filhos. Ao contrário da visão do diagrama da hierarquia, não é possível visualizar os detalhes da mensagem de estado do local ou da ligação de replicação nesta vista.  

> [!NOTE]  
> Para utilizar a vista geográfica, o computador a que a consola do Gestor de Configuração se liga deve ter o Internet Explorer instalado e poder aceder ao Bing Maps utilizando o protocolo HTTP.  

A seguinte opção altera a visão geográfica:  

#### <a name="site-location"></a>Localização do local

Especifique uma localização geográfica para cada local utilizando um dos seguintes tipos:

- Um endereço de rua
- Um nome de lugar como o nome de uma cidade
- Por latitude e longitude coordenadas

Por exemplo, para usar a latitude e longitude de Redmond, Washington, especificar **N 47 40 26.3572 W 122 7 17.4432** como a localização do local. Não é necessário especificar os símbolos para o grau, minutos ou segundos de latitude ou longitude. O Gestor de Configuração utiliza o Bing Maps para exibir a localização na vista geográfica. Então pode ver a sua hierarquia com as localizações geográficas. Esta visão fornece informações sobre questões regionais que podem afetar sites específicos ou replicação interlocal.  

Quando especificar uma localização, pode utilizar a caixa **Localização** para procurar um site específico na hierarquia. Com o site selecionado, introduza a localização como o nome de uma cidade ou morada na coluna **Localização** . O Gestor de Configuração utiliza o Bing Maps para resolver a localização.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>Passos seguintes

[Replicar a base de dados do monitor](monitor-replication.md)
