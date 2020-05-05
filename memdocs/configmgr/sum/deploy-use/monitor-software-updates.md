---
title: Monitorizar atualizações de software
titleSuffix: Configuration Manager
description: A consola 'Gestor de Configuração' fornece alertas e estados para monitorizar as atualizações e a conformidade.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110377"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>Monitorize atualizações de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração fornece muitas formas de o ajudar a monitorizar as atualizações de software de objetos, processos e informações de conformidade. Utilize as seguintes secções para monitorizar as atualizações de software.

## <a name="software-updates-dashboard"></a>Painel de atualizações de software

*(Introduzido na versão 1610)*

A partir da versão 1610 do Gestor de Configuração, pode utilizar o Dashboard de Atualizações de Software para ver o estado de conformidade atual dos dispositivos na sua organização e analisar rapidamente os dados para ver quais os dispositivos em risco. Para visualizar o dashboard, navegue para **monitorizar o** > **Painel de Atualizações**de Software de**Segurança** > de**Visão Geral** > .

## <a name="drill-through-required-updates"></a>Perfurar através de atualizações necessárias
<!--4224414-->
*(Introduzido na versão 1906)*

Pode perfurar as estatísticas de conformidade para ver quais os dispositivos que requerem uma atualização específica do software Microsoft 365 Apps. Para ver a lista do dispositivo, é necessário permissão para visualizar atualizações e as coleções a que os dispositivos pertencem. Para aprofundar a lista do dispositivo:

1. Vá a**Software Updates** > de **Software da Biblioteca** > de Software**Todas as Atualizações de Software**.
1. Selecione qualquer atualização que seja necessária por pelo menos um dispositivo.
1. Olhe para o separador **Resumo** e encontre o gráfico de tartes em **estatísticas.**
1. Selecione a hiperligação necessária para **ver** junto ao gráfico de tartes para aprofundar a lista do dispositivo.
1. Esta ação leva-o a um nó temporário em **Dispositivos** onde pode ver os dispositivos que necessitam da atualização. Você também pode tomar ações para o nó, como criar uma nova coleção a partir da lista.


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a>Alertas para atualizações de software  
 Pode configurar alertas para que as atualizações de software notifiquem os utilizadores administrativos sempre que os níveis de conformidade das implementações de atualizações de software se encontrem abaixo da percentagem configurada. Pode configurar alertas de implementações de atualizações de software nas seguintes localizações:  

-   Definição de ADR: pode configurar as definições de alertas no Assistente de Criação de Regra de Implementação Automática e nas propriedades da regra de implementação automática.  

-   Definição de implementação: pode configurar as definições de alertas no Assistente de Implementação de Atualização de Software e nas propriedades da implementação.  

Depois de configurar as definições de alerta, se ocorrerem as condições especificadas, o Gestor de Configuração gera um alerta. Poderá consultar os alertas de atualização de software nas seguintes localizações:  

1.  Consulte os alertas recentes no nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

2.  Efetue a gestão dos alertas configurados no nó **Alertas** da área de trabalho **Monitorização** .  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a>Software atualiza estado de sincronização  
 Depois de iniciar o processo de sincronização, pode monitorizar o processo de sincronização a partir da consola Do Gestor de Configuração para todos os pontos de atualização de software da sua hierarquia. Utilize o seguinte procedimento para monitorizar o processo de sincronização de atualizações de software.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para monitorizar o processo de sincronização de atualizações de software  

- Na consola do Gestor de Configuração, navegue para **monitorizar o** > estado de sincronização do ponto de**atualização**do software de**visão geral** > .  

    Os pontos de atualização de software na hierarquia do Gestor de Configuração são apresentados no painel de resultados. A partir desta vista, poderá monitorizar o estado de sincronização de todos os pontos de atualização de software. Para ver informações mais detalhadas sobre o processo de sincronização, pode rever o ficheiro wsyncmgr.log, que está localizado em <*ConfigMgrInstallationPath*>\Logs em cada servidor do site.  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a>Estado de implementação de atualização de software  
 Após implementar as atualizações de software de um grupo de atualização de software ou implementar uma atualização de software individual, poderá monitorizar o estado da implementação. Utilize o seguinte procedimento para monitorizar o estado de implementação de um grupo de atualização de software ou de uma atualização de software.  

#### <a name="to-monitor-deployment-status"></a>Para monitorizar o estado da implementação  

1.  Na consola 'Gestor de Configuração', navegue para **monitorizar** > **as implementações****de visão geral** > .  

2.  Clique no grupo de atualização de software ou na atualização de software cujo estado da implementação pretende monitorizar.  

3.  No separador **Home Page** , no grupo **Implementação** , clique em **Ver Estado**.  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> Relatórios de atualizações do software  
 As mensagens de estado relativas a atualizações de software disponibilizam informações sobre a conformidade das atualizações de software e sobre o estado de avaliação e de imposição das implementações de atualizações de software. Pode executar relatórios de atualizações de software para ver estas mensagens de estado. Estão disponíveis mais de 30 relatórios de atualização de software predefinidos. Estão organizados em várias categorias e podem ser usados para reportar informações específicas sobre atualizações e implementações de software. Além de utilizar os relatórios pré-configurados, também pode criar relatórios de atualização de software personalizados, adequados às necessidades da sua empresa. Para mais informações, consulte [Operações e manutenção para reportagem](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Relatórios de atualizações de software recomendados
Seguem-se alguns dos relatórios que são úteis na identificação de potenciais problemas: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Conformidade 9 - Saúde e conformidade globais (a partir da versão 1806)
O relatório inclui as seguintes partes:

- **Clientes Saudáveis vs Clientes Totais**: Este gráfico de barras compara os clientes "saudáveis" que comunicaram com o site no período de tempo especificado com o número total de clientes na coleção especificada.
- **Visão geral de conformidade**: Este gráfico de tartes mostra o estado de conformidade geral para o grupo específico de atualização de software sobre clientes ativos na coleção especificada.
- **Top 5 Não Conforme pelo ID do artigo**: Este gráfico de barras apresenta as cinco principais atualizações de software do grupo especificado que não são compatíveis com clientes ativos na recolha especificada.
- A parte inferior do relatório é uma tabela com mais detalhes, que lista as atualizações de software no grupo especificado.

#### <a name="management-2---updates-required-but-not-deployed"></a>Gestão 2 - atualizações obrigatórias mas não implementadas

Este relatório apresenta atualizações específicas do software do fornecedor numa classificação específica de atualizações que foram detetadas conforme exigido nos clientes, mas que não foram implementadas para uma coleção específica. 

#### <a name="troubleshooting-2---deployment-errors"></a>Resolução de problemas 2 - Erros de implantação

Este relatório devolve os erros de implementação no site e uma contagem de computadores que estão a experimentar cada erro. 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>Monitorizar o conteúdo  
 Pode monitorizar o conteúdo na consola Do Gestor de Configuração para rever o estado de todos os tipos de pacotes em relação aos pontos de distribuição associados. Estas informações podem incluir o estado de validação do conteúdo do pacote, o estado dos conteúdos atribuídos a um grupo específico de pontos de distribuição, o estado dos conteúdos atribuídos a um ponto de distribuição e o estado das funcionalidades opcionais de cada ponto de distribuição (validação de conteúdos, PXE e multicast).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a>Monitorização do estado do conteúdo  
 O nó **Estado do Conteúdo** da área de trabalho **Monitorização** disponibiliza informações sobre pacotes de conteúdos. Pode rever as informações gerais do pacote, o estado de distribuição do pacote e informações de estado detalhadas do pacote. Utilize o seguinte procedimento para ver o estado do conteúdo.  

#### <a name="to-monitor-content-status"></a>Para monitorizar o estado do conteúdo  

1.  Na consola do Gestor de Configuração, navegue para **monitorizar o** > estado do**Distribution Status** > **conteúdo**da distribuição de**visão geral** > . Os pacotes são apresentados.  

2.  Selecione o pacote cujas informações detalhadas de estado pretende visualizar.  

3.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações de estado detalhadas sobre o pacote.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Estado do grupo de pontos de distribuição  
 O nó **Estado do Grupo de Pontos de Distribuição** na área de trabalho **Monitorização** fornece informações acerca dos grupos de pontos de distribuição. Pode rever informações gerais sobre o grupo de pontos de distribuição, tais como o estado e a taxa de compatibilidade do grupo de pontos de distribuição, assim como informações de estado detalhadas sobre o grupo de pontos de distribuição. Utilize o seguinte procedimento para ver o estado do grupo de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para monitorizar o estado do grupo de pontos de distribuição  

1.  Na consola do Gestor de Configuração, navegue para **monitorizar o** > estado do ponto de distribuição do estado > **Distribution Status** > de**distribuição**de**visão geral**. Os grupos de pontos de distribuição são apresentados.  

2.  Selecione o grupo de pontos de distribuição cujas informações detalhadas de estado pretende visualizar.  

3.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações detalhadas de estado para o grupo de pontos de distribuição.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a>Estado de configuração do ponto de distribuição  
 O nó **Estado da Configuração do Ponto de Distribuição** na área de trabalho **Monitorização** fornece informações acerca do ponto de distribuição. Pode consultar quais os atributos que se encontram ativados no ponto de distribuição, incluindo PXE, Multicast e a validação de conteúdo. Também pode ver informações detalhadas de estado para o ponto de distribuição. Utilize o seguinte procedimento para ver o estado da configuração do ponto de distribuição.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorizar o estado da configuração do ponto de distribuição  

1.  Na consola do Gestor de Configuração, navegue para **monitorizar o** > estado de**configuração**do ponto de distribuição do**estado** > de distribuição de**visão geral** > . Os pontos de distribuição são apresentados.  

2.  Selecione o ponto de distribuição do qual pretende ver informações sobre o estado do ponto de distribuição.  

3.  No painel de resultados, clique no separador **Detalhes.** A informação do estado para o ponto de distribuição é apresentada.  

## <a name="next-steps"></a>Passos seguintes

- [Ficheiros de registo para atualizações de software](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Papel branco de gestão de atualizações de software](https://www.microsoft.com/download/confirmation.aspx?id=44578)
