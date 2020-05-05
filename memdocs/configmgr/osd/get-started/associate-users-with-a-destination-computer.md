---
title: " Associar utilizadores a um computador"
titleSuffix: Configuration Manager
description: Configure o Gestor de Configuração para associar os utilizadores aos computadores de destino ao implementar sistemas operativos.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724203"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Associar os utilizadores a um computador de destino no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando utiliza o Gestor de Configuração para implementar sistemas operativos, pode associar os utilizadores ao computador de destino. Esta opção funciona se um único utilizador ou vários utilizadores são os principais utilizadores do computador de destino.  

A afinidade dispositivo/utilizador suporta a gestão centrada no utilizador para a implementação de aplicações. Quando associa um utilizador ao computador de destino para instalar um SISTEMA, pode posteriormente implementar aplicações a esse utilizador, e as aplicações instalam-se automaticamente no computador de destino. Embora possa configurar o suporte para a afinidade do dispositivo de utilizador durante a implementação do SISTEMA, não é possível utilizar a afinidade do dispositivo do utilizador para implementar o SISTEMA.  

Para obter mais informações sobre a finção do dispositivo do utilizador, consulte [os utilizadores e dispositivos do Link com a finidade](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .  

Existem vários métodos através dos quais pode integrar a afinidade do dispositivo do utilizador nas suas implementações de SO. É possível integrar a afinidade dispositivo/utilizador em implementações de PXE, implementações de suportes de dados de arranque e implementações de suportes de dados pré-configurados.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Criar uma sequência de tarefas que inclui a variável **SMSTSAssignUsersMode**

Adicione a variável **SMSTSAssignUsersMode** ao início da sua sequência de tarefas utilizando o passo variável da sequência de [tarefas definida.](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) Esta variável especifica o modo como a sequência de tarefas processa as informações do utilizador.

Para obter mais informações, consulte variáveis de sequência de [tarefas](../understand/task-sequence-variables.md#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Criar um comando de pré-início que reúne as informações do utilizador

O comando prestart pode ser um VBScript com uma caixa de entrada. Pode também ser uma aplicação HTML (HTA) que valida os dados do utilizador em que entram. 

Este comando prestart deve definir a variável **SMSTSUDAUsers** que é usada quando a sequência de tarefas é executado. Esta variável pode ser definida num computador, numa coleção ou numa variável de sequência de tarefas.

Para obter mais informações, consulte variáveis de sequência de [tarefas](../understand/task-sequence-variables.md#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Configurar o modo como os pontos de distribuição e os suportes de dados associam o utilizador ao computador de destino

O ponto de distribuição ou suporte de suporte suporta a associação dos utilizadores com o computador de destino onde o SISTEMA está implantado. Utilize um dos seguintes métodos: 

- [Configure um ponto de distribuição para aceitar pedidos de arranque pXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [Criar meios de comunicação sabotáveis](../deploy-use/create-bootable-media.md)  
- [Criar meios pré-encenados](../deploy-use/create-prestaged-media.md)  


Configurar o suporte de afinidade do dispositivo do utilizador não tem um método incorporado para validar a identidade do utilizador. Este comportamento é importante quando um técnico está a fornecer o computador e introduz a informação em nome do utilizador. Além de definir como a sequência de tarefas lida com as informações do utilizador, configurar estas opções no ponto de distribuição e os meios de comunicação proporcionam a capacidade de restringir as implementações que são iniciadas a partir de uma bota PXE ou de um tipo específico de mídia.
