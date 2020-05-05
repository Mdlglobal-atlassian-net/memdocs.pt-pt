---
title: Utilizar multicast para implementar o Windows na rede
titleSuffix: Configuration Manager
description: Utilize o multicast no ambiente do Gestor de Configuração para que vários computadores possam simultaneamente descarregar a imagem do sistema operativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f81b23d3783d397d83a3925b98c0c8f601fa4012
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720122"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Utilize o multicast para implementar o Windows sobre a rede com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Multicast é um método de otimização de rede que pode utilizar no ambiente do Gestor de Configuração, onde é provável que vários clientes descarreguem a mesma imagem do sistema operativo ao mesmo tempo. Quando é utilizado o multicast, a imagem do sistema operativo é transferida em simultâneo por vários computadores à medida que é multidifundida pelo ponto de distribuição, em vez de ter um ponto de distribuição que envia uma cópia dos dados para cada cliente através de uma ligação separada.  

 Pode implementar sistemas operativos na rede através de multicast nos seguintes cenários de implementação de sistema operativo:  

- [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

  Execute os passos num dos cenários de implementação do sistema operativo e utilize as secções seguintes para suporte de multicast.  

##  <a name="configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> Configurar um ponto de distribuição para suportar multicast  
 Para utilizar multicast quando implementa sistemas operativos, tem de configurar um ponto de distribuição para suportar multicast. Para mais informações, consulte [Instalar e configurar pontos](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)de distribuição . Para obter uma lista de portas necessárias para suportar o multicast, consulte [Portos](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Preparar uma imagem do sistema operativo para implementações multicast  
 Para configurar o pacote de imagem do sistema operativo para suportar multicast, consulte [Prepare the operating system image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Implementar a sequência de tarefas  
 Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md).  
