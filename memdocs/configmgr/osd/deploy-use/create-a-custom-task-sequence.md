---
title: Criar uma sequência de tarefas personalizada
titleSuffix: Configuration Manager
description: Editar uma sequência de tarefas personalizada no Gestor de Configuração para adicionar passos à sequência de tarefas.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9107e9787cf7f12cab624101c37344ea20684112
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720619"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Criar uma sequência de tarefas personalizada com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando cria uma sequência de tarefas personalizada no Gestor de Configuração, não contém passos de sequência de tarefas. Depois de criar a sequência de tarefas, edite-a e adicione os passos de sequência de tarefas de que necessita.  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a> Criar uma sequência de tarefas personalizada

Utilize o seguinte procedimento para criar uma sequência de tarefas personalizada:

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

1. No separador **Home** da fita, no grupo **Criar,** selecione Criar sequência de **tarefas**. Esta ação inicia o Assistente de Sequência de Tarefas Create.  

1. Na página **Criar uma Nova Sequência de Tarefas** , selecione **Criar uma nova sequência de tarefas personalizada**.  

1. Na página **informação** sobre a sequência de tarefas, especifique:

    - Um nome para a sequência de tarefas
    - Uma descrição da sequência de tarefas
    - Uma imagem de arranque opcional para a sequência de tarefas a utilizar

Depois de completar o Assistente de Sequência de Tarefas Create, o Diretor de Configuração adiciona a sequência de tarefas personalizada ao nó de sequências de **tarefas.** Pode agora editar esta sequência de tarefas para lhe adicionar passos de sequência de tarefas.  

## <a name="see-also"></a>Consulte também

Para obter uma lista dos passos de sequência de tarefas disponíveis, consulte [os passos](../understand/task-sequence-steps.md)da sequência de tarefas .  

Para obter mais informações sobre como editar uma sequência de tarefas, consulte [Utilize o editor da sequência de tarefas](../understand/task-sequence-editor.md).  

Na maioria das vezes, utilizará sequências de tarefas para automatizar tarefas para a implementação do OS, mas pode criar uma sequência de tarefas personalizada para automatizar diferentes tipos de tarefas. Para obter mais informações, consulte Criar uma sequência de [tarefas para implementações não-S](create-a-task-sequence-for-non-operating-system-deployments.md).

A partir da versão 2002, instale aplicações complexas utilizando sequências de tarefas através do modelo de aplicação. Adicione um tipo de implementação a uma aplicação que é uma sequência de tarefas, quer para instalar ou desinstalar a aplicação. Para mais informações, consulte [Create Windows aplicações](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

## <a name="next-steps"></a>Passos seguintes

[Implementar a sequência de tarefas](deploy-a-task-sequence.md)
