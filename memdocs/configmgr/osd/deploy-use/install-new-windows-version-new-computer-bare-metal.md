---
title: Instale o Windows num novo computador
titleSuffix: Configuration Manager
description: Utilize o Gestor de Configuração para instalar um sistema operativo num novo computador (metal nu) utilizando suportes PXE, OEM ou autónomos.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a70269839b4a550fbef4dc5cab1b7ff3d426d87
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711078"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Instale uma nova versão do Windows num novo computador (metal nu) com 'Configuração Manager'

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico fornece os passos gerais no Gestor de Configuração para instalar um sistema operativo num novo computador. Para este cenário, pode escolher de entre vários métodos de implementação diferentes, como PXE, OEM ou suportes de dados autónomos. Se não tiver a certeza de que este é o cenário de implementação do sistema operativo certo para si, consulte [cenários para implantar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md).  

Utilize as secções seguintes para atualizar um computador existente com uma nova versão do Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Plano  

-   **Planear e implementar requisitos de infraestrutura**  

     Existem vários requisitos de infraestrutura que devem estar em vigor antes de poder implementar sistemas operativos, tais como Windows ADK, Windows Deployment Services (WDS), configurações de discos rígidos suportados, etc. Para obter mais informações, consulte [os requisitos de infraestrutura para a implantação do sistema operativo.](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)

##  <a name="configure"></a><a name="BKMK_Configure"></a>Configurar  

1.  **Preparar uma imagem de arranque**  

     As imagens de arranque iniciam um computador com ambiente Windows PE (um sistema operativo mínimo com componentes e serviços limitados) que, em seguida, pode instalar o sistema operativo Windows completo no computador.   Quando implementar sistemas operativos, tem de selecionar uma imagem de arranque para utilizar e distribuir a imagem por um ponto de distribuição. Utilize o seguinte procedimento para preparar a imagem de arranque:  

    -   Para saber mais sobre imagens de arranque, consulte [Gerir imagens](../get-started/manage-boot-images.md)de arranque .  

    -   Para obter mais informações sobre como personalizar uma imagem de arranque, consulte [Personalizar imagens de arranque](../get-started/customize-boot-images.md).  

    -   Distribua a imagem de arranque por pontos de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparar uma imagem do sistema operativo**  

     A imagem do sistema operativo contém os ficheiros necessários para instalar o sistema operativo no computador de destino. Utilize o seguinte procedimento para preparar a imagem do sistema operativo:  

    -   Para saber mais sobre como criar uma imagem do sistema operativo, consulte [gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).

    -   Distribua a imagem do sistema operativo por pontos de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > As novas instalações do Windows também podem ser realizadas a partir de ficheiros de origem de instalação através de pacotes de upgrade de OS, mas utilizam imagens de OS como **instalar.wim.**
    >
    > A implementação de novas instalações do Windows através de pacotes de upgrade solado ainda é suportada, mas está dependente de que os condutores sejam compatíveis com este método. Ao instalar o Windows a partir de um pacote de atualização DES, os controladores são instalados enquanto ainda estão no Windows PE versus simplesmente serem injetados enquanto estão no Windows PE. Alguns condutores não são compatíveis com a instalação do Windows PE. Se os controladores não forem compatíveis com a instalação enquanto estiverem no Windows PE, utilize uma imagem de OS.  

3.  **Criar uma sequência de tarefas para implementar sistemas operativos na rede**  

     Utilize uma sequência de tarefas para automatizar a instalação do sistema operativo na rede. Utilize os passos em Criar uma sequência de [tarefas para instalar um sistema operativo](create-a-task-sequence-to-install-an-operating-system.md) para criar a sequência de tarefas para implantar o sistema operativo. Consoante o método de implementação que escolher, poderão existir outras considerações relativamente à sequência de tarefas.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Implantação  

-   Utilize um dos seguintes métodos de implementação para implementar o sistema operativo:  

    -   [Utilizar o PXE para implementar o Windows na rede](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Utilizar multicast para implementar o Windows na rede](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Criar uma imagem de um OEM de fábrica ou um depósito local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Utilizar suportes de dados de arranque para implementar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitorizar  

-   **Monitorizar a implementação da sequência de tarefas**  

     Para monitorizar a implementação da sequência de tarefas para instalar o sistema operativo, consulte [as implementações](monitor-operating-system-deployments.md)do sistema operativo Monitor .  
