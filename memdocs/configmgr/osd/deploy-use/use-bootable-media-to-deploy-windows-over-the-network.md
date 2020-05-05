---
title: Utilizar suportes de dados de arranque para implementar o Windows na rede
titleSuffix: Configuration Manager
description: Utilize implementações de suportes de arranque no Gestor de Configuração para implementar o sistema operativo quando o computador de destino começar.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724364"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Utilize suportes sinuosos para implantar o Windows sobre a rede com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode implantar o sistema operativo quando o computador de destino começar a utilizar uma implementação de suporte sinuoso. Os meios de comunicação contêm um ponteiro para a sequência de tarefas, a imagem do sistema operativo e outros conteúdos necessários da rede. Quando o computador de destino começa, o computador recupera os itens referenciados no ponteiro. Com os meios de comunicação sem funcionação isentos de conteúdo, pode atualizar o alvo sem ter de o substituir nos meios de comunicação.

Pode implantar sistemas operativos através da rede utilizando multicast nos seguintes cenários de implementação do sistema operativo:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir definições](replace-an-existing-computer-and-transfer-settings.md)  

Conclua os passos num dos cenários de implementação do sistema operativo e, em seguida, utilize as secções seguintes para utilizar suportes de dados de arranque para implementar o sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
Quando utilizar os meios de arranque para iniciar o processo de implementação do sistema operativo, configure a implementação para disponibilizar o sistema operativo aos meios de comunicação. Pode definir esta opção na página de Definições de **Implementação** do Assistente de Software de Implementação ou no separador Definições de **Implementação** nas propriedades para a implementação. Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:

-   Clientes, meios de comunicação e PXE do Gestor de Configuração

-   Apenas suportes de dados e PXE

-   Apenas suportes de dados e PXE (oculto)

## <a name="create-the-bootable-media"></a>Criar suportes de dados de arranque
Pode especificar se os suportes de arranque são uma pen USB ou um conjunto de CD/DVD. O computador que inicia o suporte deve suportar a opção que escolher como uma unidade de arranque. Para mais informações, consulte [Criar meios de sapateado.](create-bootable-media.md)  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Instalar o sistema operativo a partir de suportes de dados de arranque  
Insira o suporte de dados numa unidade de arranque no computador e ligue-o para instalar o sistema operativo.
