---
title: Utilizar o Centro de Software para implementar o Windows através da rede
titleSuffix: Configuration Manager
description: Pode implementar um sistema operativo no Software Center para atualizar um computador existente com uma nova versão do Windows ou para atualizar o Windows para a versão mais recente.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724217"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Use o Centro de Software para implementar o Windows sobre a rede com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode tornar disponível no Centro de Software a sequência de tarefas que instala um sistema operativo no Gestor de Configuração. Pode implantar um sistema operativo no Software Center com os seguintes cenários de implementação do sistema operativo:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)

Complete os passos num dos cenários de implementação do sistema operativo. Em seguida, utilize as seguintes secções para se preparar para implementações disponíveis no Centro de Software.

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
Para disponibilizar a implementação do sistema operativo no Centro de Software, configure a implementação. Pode configurar a implementação na página de Definições de **Implementação** do Assistente de Software de Implementação ou no separador Definições de **Implementação** nas propriedades para a implementação. Na definição **Tornar disponível para o seguinte** , configure **Apenas Clientes do Configuration Manager** ou **Clientes do Configuration Manager, suportes de dados e PXE**. Após a implementação do sistema operativo, o sistema operativo será apresentado no Centro de Software para os membros da recolha do alvo.

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> Implementar a sequência de tarefas nos computadores  
Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md). Quando implementar sistemas operativos para o Centro de Software, pode configurar se a implementação é necessária ou disponível.

-   **Implementação obrigatória**: as implementações obrigatórias disponibilizam o sistema operativo no Centro de Software, mas serão iniciadas automaticamente no agendamento de atribuição configurado.

-   **Implementação disponível**: o sistema operativo estará disponível no Centro de Software e o utilizador pode instalá-lo a pedido.
