---
title: Implementar atualizações de software
titleSuffix: Configuration Manager
description: Aprenda a implementar manualmente ou automaticamente atualizações de software na consola 'Gestor de Configuração'.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 00accfc5150226830b68beb194fa168c08148b84
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110428"
---
# <a name="deploy-software-updates"></a>Implementar atualizações de software  

*Aplica-se a: Gestor de Configuração (ramo atual)*

A fase de implementação da atualização de software é o processo de implementação de atualizações de software. Não importa como implemente atualizações de software, o site:
- Adiciona as atualizações a um grupo de atualizações de software
- Distribui o conteúdo da atualização para pontos de distribuição
- Implementa o grupo de atualização para clientes  

Depois de criar a implementação, o site envia uma política de atualização de software associada a clientes direcionados. Os clientes descarregam os ficheiros de conteúdo de atualização de software de uma fonte de conteúdo para a sua cache local. Os clientes na internet descarregam sempre conteúdos do serviço cloud microsoft Update. As atualizações de software estão então disponíveis para instalação pelo cliente.   

> [!Tip]  
>  Se um ponto de distribuição não estiver disponível, os clientes na intranet também podem descarregar atualizações de software a partir do Microsoft Update.  

> [!NOTE]  
>  Ao contrário de outros tipos de implementação, as atualizações de software são todas descarregadas para a cache do cliente. Isto é independentemente da definição máxima de tamanho de cache no cliente. Para obter mais informações sobre a definição de cache do cliente, consulte [Configurar a cache do cliente para clientes do Gestor de Configuração](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Se configurar uma implementação da atualização de software necessária, as atualizações de software são instaladas automaticamente no prazo agendado. Em alternativa, o utilizador no computador cliente pode agendar ou iniciar a instalação da atualização de software antes do termo do prazo. Após a instalação tentada, os computadores cliente enviam mensagens de estado de volta para o servidor de site para indicar se a instalação da atualização de software foi concluída com êxito. Para obter mais informações sobre implementações de atualização de software, veja [Fluxos de trabalho de implementação de atualizações de software](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Existem três cenários principais para a implementação de atualizações de software: 
- [Implementação manual](#BKMK_ManualDeployment)  
- [Implantação automática](#bkmk_auto)  
- [Implantação faseada](#bkmk_phased)  

Normalmente, começa-se por implementar manualmente atualizações de software para criar uma linha de base para os seus clientes, e depois gere atualizações de software nos clientes utilizando uma implementação automática ou faseada.  

> [!Note]  
> Não se pode usar uma regra de implantação automática com uma implantação faseada.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a>Implementar manualmente atualizações de software
Selecione atualizações de software na consola Do Gestor de Configuração e inicie manualmente o processo de implementação. Normalmente, utiliza este método de implantação para:  

- Obtenha os clientes atualizados com as atualizações de software necessárias antes de criar regras de implementação automáticaque gerem implementações mensais  

- Implementar atualizações de software fora da banda  


A lista seguinte apresenta o fluxo de trabalho geral para a implementação manual de atualizações de software:  

1. Filtre para atualizações de software que utilizam requisitos específicos. Por exemplo, forneça critérios que recuperem todas as atualizações de segurança ou software crítico que sejam necessárias em mais de 50 clientes.  

2. Crie um grupo de atualização de software que contém as atualizações de software.  

3. Transfira o conteúdo das atualizações de software no grupo de atualização de software.  

4. Implemente manualmente o grupo de atualização de software.  

Para obter mais informações e passos detalhados, consulte [Manualmente implementar atualizações](manually-deploy-software-updates.md)de software .

> [!Note]
> - A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver referências ao nome antigo na consola do Gestor de Configuração e documentação de suporte enquanto a consola está a ser atualizada.
> - Ao implementar manualmente as atualizações de clientes do Office 365, encontre-as no nó de **Atualizações do Office 365** no âmbito do **Office 365 Client Management** do espaço de trabalho da Biblioteca de **Software.** 

## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a>Implementar automaticamente atualizações de software

Configure a implementação automática de atualizações de software utilizando uma regra de implementação automática (ADR). Este método de implementação é comum para atualizações mensais de software (tipicamente conhecida como "Patch Tuesday") e para gerir atualizações de definição. Define os critérios para um ADR automatizar o processo de implantação. A lista seguinte fornece o fluxo de trabalho geral para implementar automaticamente atualizações de software:  

1.  Crie um ADR que especifique as definições de implementação.  

2.  O site adiciona as atualizações de software a um grupo de atualização de software.  

3.  O site implementa o grupo de atualização de software para os clientes na coleção de alvos.  

Primeiro, determine a sua estratégia automática de implementação de atualização de software. Por exemplo, criar o ADR para inicialmente visar uma coleção de clientes de teste. Depois de verificar se o grupo de teste instalou com sucesso as atualizações de software, adicione uma nova implementação à regra. Também pode alterar a coleção direcionada na implementação existente para uma que inclui um conjunto maior de clientes. Considere os seguintes comportamentos ao decidir sobre a estratégia a utilizar:  

- É capaz de modificar as propriedades dos objetos de atualização de software que o ADR cria.   

- O ADR implementa automaticamente atualizações de software para os clientes quando as adiciona à recolha do alvo.  

- Quando você ou o ADR adicionam novas atualizações de software ao grupo de atualização de software, o site implementa-as automaticamente para os clientes na coleção de alvos.  

- Ativar ou desativar as implementações a qualquer momento para o ADR.  


Depois de criar um ADR, adicione implementações adicionais à regra. Esta ação ajuda-o a gerir a complexidade de implementar diferentes atualizações para diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação.  

Cada nova implementação que adiciona:  

- Usa o mesmo grupo de atualização e pacote, que o ADR cria quando executa pela primeira vez  
- Pode visar uma coleção diferente  
- Suporta propriedades de implementação exclusivas, incluindo:  
  -   Hora de ativação  
  -   Prazo  
  -   Experiência de utilizador  
  -   Alertas separados para cada implantação  


Para mais informações e etapas detalhadas, consulte [Automaticamente implementar atualizações](automatically-deploy-software-updates.md) de software



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a>Implementar atualizações de software em fases

<!--1358146-->
A partir da versão 1810, criar implementações faseadas para atualizações de software. As implementações faseadas permitem-lhe orquestrar um lançamento coordenado e sequenciado de software com base em critérios e grupos personalizáveis.

Para mais informações, consulte [Criar implementações faseadas](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

