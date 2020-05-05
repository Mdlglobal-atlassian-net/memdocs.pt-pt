---
title: Substituir um computador existente e transferir definições
titleSuffix: Configuration Manager
description: No 'Gestor de Configuração', escolha entre métodos de implementação, tais como suportes de arranque, multicast ou Software Center, para substituir um computador existente por um novo computador.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b494fd5d9623af9de16d68e3d30e0e78a4ef338
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723776"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Substitua um computador existente e as definições de transferência por Configuração Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico fornece os passos gerais no Gestor de Configuração para substituir um computador existente por um novo computador. Para este cenário, pode escolher de entre vários métodos de implementação diferentes, como suporte de dados de arranque, multicast ou Centro de Software. Também pode optar por instalar um ponto de migração de estado para armazenar definições e, em seguida, restaurá-lo para o novo sistema operativo após a respetiva instalação. Se não tiver a certeza de que este é o cenário de implementação do sistema operativo certo para si, consulte [cenários para implantar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md).  

 Utilize as secções seguintes para atualizar um computador existente com uma nova versão do Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Plano  

-   **Planear e implementar requisitos de infraestrutura**  

     Existem vários requisitos de infraestrutura que devem estar em vigor antes de poder implementar sistemas operativos, tais como Windows ADK, User State Migration Tool (USMT), Windows Deployment Services (WDS), configurações de discos rígidos suportados, etc. Para mais informações, consulte [os requisitos de infraestrutura para a implantação do sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)  

-   **Instalar um ponto de migração de estado (necessário apenas se transferir definições)**  

     Quando pretender capturar definições do computador existente e, em seguida, restaurá-las para o novo sistema operativo, tem de instalar um ponto de migração de estado. Para mais informações, consulte [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="configure"></a><a name="BKMK_Configure"></a>Configurar  

1.  **Preparar uma imagem de arranque**  

     As imagens de arranque iniciam um computador com ambiente Windows PE (um sistema operativo mínimo com componentes e serviços limitados) que, em seguida, pode instalar o sistema operativo Windows completo no computador. Quando implementar sistemas operativos, tem de selecionar uma imagem de arranque para utilizar e distribuir a imagem por um ponto de distribuição. Utilize o seguinte procedimento para preparar a imagem de arranque:  

    -   Para saber mais sobre imagens de arranque, consulte [Gerir imagens](../get-started/manage-boot-images.md)de arranque .  

    -   Para obter mais informações sobre como personalizar uma imagem de arranque, consulte [Personalizar imagens de arranque](../get-started/customize-boot-images.md).  

    -   Distribua a imagem de arranque por pontos de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparar uma imagem do sistema operativo**  

     A imagem do sistema operativo contém os ficheiros necessários para instalar o sistema operativo no computador de destino. Utilize o seguinte procedimento para preparar a imagem do sistema operativo:  

    -   Para saber mais sobre como criar uma imagem do sistema operativo, consulte [gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).  

    -   Distribua a imagem do sistema operativo por pontos de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Criar uma sequência de tarefas para implementar sistemas operativos na rede**  

     Utilize uma sequência de tarefas para automatizar a instalação do sistema operativo na rede. Utilize os passos em Criar uma sequência de [tarefas para instalar um sistema operativo](create-a-task-sequence-to-install-an-operating-system.md) para criar a sequência de tarefas para implantar o sistema operativo. Consoante o método de implementação que escolher, poderão existir outras considerações relativamente à sequência de tarefas.  

    > [!NOTE]  
    >  Neste cenário, se capturar e restaurar as definições de utilizador e os ficheiros, pode optar por utilizar um ponto de migração de estado ou guarde os ficheiros localmente. Para mais informações, consulte Gerir o [estado do utilizador](../get-started/manage-user-state.md).  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Implantação  

-   Utilize um dos seguintes métodos de implementação para implementar o sistema operativo:  

    -   [Utilizar o Centro de Software para implementar o Windows através da rede](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Utilizar suportes de dados de arranque para implementar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Utilizar multicast para implementar o Windows na rede](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Criar uma imagem de um OEM de fábrica ou um depósito local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Monitorizar  

-   **Monitorizar a implementação da sequência de tarefas**  

     Para monitorizar a implementação da sequência de tarefas para instalar o sistema operativo, consulte [as implementações](monitor-operating-system-deployments.md)do sistema operativo Monitor .  
