---
title: Monitorizar o estado de implantação do cliente
titleSuffix: Configuration Manager
description: Monitorize o estado de implementação do cliente no Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80cfa1576ae2cc4505147aee07a247e035b07ada
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713318"
---
# <a name="how-to-monitor-client-deployment-status-in-configuration-manager"></a>Como monitorizar o estado de implementação do cliente no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A implementação de clientes no seu site demora algum tempo e algumas instalações não são bem sucedidas à primeira vez. A consola Do Gestor de Configuração fornece uma forma de manter um olho nas implementações do cliente dentro de uma coleção, reportando o estado de implementação do cliente em tempo real.  

> [!NOTE]  
>  A melhor e mais fiável forma de monitorizar a implementação do cliente é com a consola Do Gestor de Configuração (como descrito neste artigo). A secção **Estado do Cliente** da área de trabalho **Monitorização** na consola mostra o estado da implementação do cliente com precisão e em tempo real. Pode monitorizar as implementações de cliente com outras ferramentas, como o Gestor de Servidores no Windows Server ou o System Center Operations Manager, mas pode receber alarmes da atividade normal de instalação de cliente. Devido à maneira como o programa de instalação de cliente (CCMSetup.exe) é executado em vários ambientes, estas outras ferramentas podem gerar alarmes e avisos falsos que não refletem com precisão o estado das implementações de cliente.  

 Na área de trabalho **Monitorização** da consola, pode monitorizar os seguintes estados para as implementações de cliente executadas numa coleção que especificar:  

- Compatível  

- Em curso  

- Não compatível  

- Falhou  

- Desconhecido  

  Os relatórios do Gestor de Configuração sobre implementações para clientes de produção ou de clientes de pré-produção. A consola do Configuration Manager também fornece um gráfico das implementações de cliente falhadas durante um determinado período de tempo para o ajudar a determinar se as ações que toma para resolver implementações estão a melhorar a taxa de sucesso de implementação com o tempo.  

## <a name="to-monitor-client-deployments"></a>Monitorizar as implementações do cliente  

- Na consola 'Gestor de Configuração', clique em **Monitorizar o** > **Estado do Cliente**.  

- Clique em **Implementação do Cliente de Produção** ou em **Implementação do Cliente de Pré-produção** consoante a versão do cliente que pretende monitorizar.  

- Reveja os gráficos do estado de implementação do cliente e de falha de implementação do cliente.  

- Se quiser alterar o âmbito do relatório, clique em **Navegar...** e escolha uma coleção diferente.  

  Para saber mais sobre as implementações de clientes pré-produção, consulte como testar as atualizações dos [clientes numa coleção pré-produção.](../../../core/clients/manage/upgrade/test-client-upgrades.md)

  > [!NOTE]
  > O estado de implementação em computadores que hospedam funções do sistema do site numa recolha pré-produção pode ser reportado como **não conforme** mesmo quando o cliente foi implementado com sucesso. Ao promover o cliente para produção, o estado de implementação é reportado corretamente.   

  Para monitorizar o estado dos clientes destacados, consulte [Como monitorizar os clientes](../../../core/clients/manage/monitor-clients.md)  

  Pode utilizar relatórios do Gestor de Configuração para saber mais informações sobre o estado dos clientes no seu site. Para obter mais informações sobre como executar relatórios, consulte [Introdução a relatórios](../../servers/manage/introduction-to-reporting.md).  
