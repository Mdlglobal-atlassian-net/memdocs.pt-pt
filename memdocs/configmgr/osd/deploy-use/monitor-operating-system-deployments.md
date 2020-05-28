---
title: Monitorizar implementações do sistema operativo
titleSuffix: Configuration Manager
description: Para ajudá-lo a monitorizar os objetos de implementação do sistema operativo, a consola Do Gestor de Configuração fornece alertas, relatórios e vários indicadores de estado.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7afab9fbbb443b2f9fb4af15a3805c0b7df7a014
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802171"
---
# <a name="monitor-operating-system-deployments-in-configuration-manager"></a>Monitorizar implementações do sistema operativo no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A consola 'Gestor de Configuração' fornece as seguintes formas de o ajudar a monitorizar os objetos de implementação do sistema operativo.  


##  <a name="alerts-for-operating-system-deployments"></a><a name="BKMK_OSDAlerts"></a> Alertas para implementações de sistema operativo  
 Pode configurar um alerta nas definições de implementação de sequência de tarefas para notificar os utilizadores administrativos quando os níveis de conformidade da implementação estiverem abaixo da percentagem configurada.  

 Depois de configurar as definições de alerta, se ocorrerem as condições especificadas, o Gestor de Configuração gera um alerta. Pode rever os alertas de implementação da sequência de tarefas nas seguintes localizações:  

1.  Reveja os alertas recentes no nó **Sistemas Operativos** da área de trabalho **Biblioteca de Software** .  

2.  Efetue a gestão dos alertas configurados no nó **Alertas** da área de trabalho **Monitorização** .  

##  <a name="task-sequence-deployment-status"></a><a name="BKMK_TSDeployStatus"></a>Estado de implantação da sequência de tarefas  
 Depois de implementar uma sequência de tarefas, pode monitorizar o estado de implementação. Utilize o procedimento seguinte para monitorizar o estado de implementação de uma sequência de tarefas.  

#### <a name="to-monitor-deployment-status"></a>Para monitorizar o estado da implementação  

1.  Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2.  Na área de trabalho Monitorização, clique em **Implementações**.  

3.  Clique na sequência de tarefas para a qual pretende monitorizar o estado de implementação.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Ver Estado**.  

> [!NOTE]  
> Quando uma atualização é iniciada, a mensagem de estado 52200 é gerada. Isto contém o utilizador que fez a atualização.  

##  <a name="operating-system-deployment-reports"></a><a name="BKMK_TSReports"></a>Relatórios de implantação do sistema operativo  
 Existem muitos relatórios de implementação do sistema operativo predefinidos disponíveis. Estes relatórios estão organizados em várias categorias e podem ser utilizados para reportar informações específicas sobre migração de estado e implementações de sequências de tarefas. Além de utilizar os relatórios pré-configurados, também pode criar relatórios de atualização de software personalizados, adequados às necessidades da sua empresa. Para mais informações, consulte [Operações e manutenção para reportagem](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>Monitorizar o conteúdo  
 Pode monitorizar o conteúdo na consola Do Gestor de Configuração para rever o estado de todos os tipos de pacotes em relação aos pontos de distribuição associados. Estas informações podem incluir o estado de validação do conteúdo do pacote, o estado dos conteúdos atribuídos a um grupo específico de pontos de distribuição, o estado dos conteúdos atribuídos a um ponto de distribuição e o estado das funcionalidades opcionais de cada ponto de distribuição (validação de conteúdos, PXE e multicast).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a>Monitorização do estado do conteúdo  
 O nó **Estado do Conteúdo** da área de trabalho **Monitorização** disponibiliza informações sobre pacotes de conteúdos. Pode rever as informações gerais do pacote, o estado de distribuição do pacote e informações de estado detalhadas do pacote. Utilize o seguinte procedimento para ver o estado do conteúdo.  

#### <a name="to-monitor-content-status"></a>Para monitorizar o estado do conteúdo  

1.  Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2.  Na área de trabalho Monitorização, expanda **Estado da Distribuição**e clique em **Estado do Conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote cujas informações detalhadas de estado pretende visualizar.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações de estado detalhadas sobre o pacote.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Estado do grupo de pontos de distribuição  
 O nó **Estado do Grupo de Pontos de Distribuição** na área de trabalho **Monitorização** fornece informações acerca dos grupos de pontos de distribuição. Pode rever informações gerais sobre o grupo de pontos de distribuição, tais como o estado e a taxa de compatibilidade do grupo de pontos de distribuição, assim como informações de estado detalhadas sobre o grupo de pontos de distribuição. Utilize o seguinte procedimento para ver o estado do grupo de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para monitorizar o estado do grupo de pontos de distribuição  

1.  Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2.  Na área de trabalho de monitorização, expanda **Estado de Distribuição**e, em seguida, clique em **Estado do Grupo de Pontos de Distribuição**. Os grupos de pontos de distribuição são apresentados.  

3.  Selecione o grupo de pontos de distribuição cujas informações detalhadas de estado pretende visualizar.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações detalhadas de estado para o grupo de pontos de distribuição.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a>Estado de configuração do ponto de distribuição  
 O nó **Estado da Configuração do Ponto de Distribuição** na área de trabalho **Monitorização** fornece informações acerca do ponto de distribuição. Pode consultar quais os atributos que se encontram ativados no ponto de distribuição, incluindo PXE, Multicast e a validação de conteúdo. Também pode ver informações detalhadas de estado para o ponto de distribuição. Utilize o seguinte procedimento para ver o estado da configuração do ponto de distribuição.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorizar o estado da configuração do ponto de distribuição  

1.  Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2.  Na área de trabalho de monitorização, expanda **Estado de Distribuição**e, em seguida, clique em **Estado da Configuração do Ponto de Distribuição**. Os pontos de distribuição são apresentados.  

3.  Selecione o ponto de distribuição do qual pretende ver informações sobre o estado do ponto de distribuição.  

4.  No painel de resultados, clique no separador **Detalhes.** A informação do estado para o ponto de distribuição é apresentada.  
