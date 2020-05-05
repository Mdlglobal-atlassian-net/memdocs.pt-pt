---
title: Desinstalar aplicações
titleSuffix: Configuration Manager
description: Desinstalar uma aplicação utilizando o Gestor de Configuração
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d9b5152c094ecc1470f748c57f2831cfdd66474
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075851"
---
# <a name="uninstall-applications-with-configuration-manager"></a>Desinstalar aplicações com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


Tome as seguintes ações para desinstalar uma aplicação que já implementou anteriormente.

-   Especifique a linha de comando para desinstalar o conteúdo do tipo de implementação na página de **Conteúdo** do Assistente do Tipo de Implementação Create.  

-   Implemente a aplicação utilizando uma ação de implementação de **Desinstalar**.  

> [!IMPORTANT]  
> Alguns tipos de aplicações não suportam a desinstalação.  

 Esta lista dá-lhe mais informações sobre como a desinstalação da aplicação funciona:  

-   Quando desinstala uma aplicação de 'Gestor de Configuração' (Gestor de Configuração), quaisquer aplicações dependentes não são automaticamente desinstaladas.  

-   Se implementar uma aplicação que utilize uma ação de **desinstalação** para um utilizador, e a aplicação foi instalada para todos os utilizadores do computador, a desinstalação poderá falhar se a conta do utilizador não tiver permissões para desinstalar a aplicação.  

-   Se remover um utilizador ou um dispositivo de uma coleção que tenha uma aplicação implantada, a aplicação não é automaticamente removida do dispositivo.  

-   Uma implementação com o objetivo de implementação de **Desinstalar** não verifica as regras de requisitos. Se a aplicação estiver instalada no computador em que é executada a implementação, será desinstalada.  

> [!IMPORTANT]  
> Para implementar a aplicação com a ação Desinstalar, deve primeiro eliminar quaisquer implementações de aplicações existentes, implementações simuladas ou implementações de sequência de tarefas que incluam esta aplicação. 

 Para obter mais informações sobre como criar um tipo de implementação, consulte [Criar aplicações](../../apps/deploy-use/create-applications.md).  

 Para obter mais informações sobre como implementar uma aplicação, consulte [aplicações de implementação](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Desinstalar uma aplicação  

1.  Configure o tipo de implementação da aplicação com a linha de comandos de desinstalação utilizando um dos seguintes métodos:  

    -   Na página **geral** do Assistente de Implementação Create, selecione a opção **Identifique automaticamente informações sobre este tipo de implementação a partir de ficheiros de instalação**. Se as informações estiverem disponíveis nos ficheiros de instalação, a linha de comandos de desinstalação é automaticamente adicionada às propriedades do tipo de implementação.  

    -   Na página **de Conteúdo** do Assistente do Tipo de Implementação Create, no campo de **desinstalação** do programa, especifique a linha de comando para desinstalar a aplicação.  

        > [!NOTE]  
        >  A página **'Conteúdo'** só é apresentada se selecionar a opção **Especificar manualmente as informações** do tipo de implementação na página **geral** do Assistente do Tipo de Implementação Create.  

    -   No separador **Programas** do ** <nome do tipo de *implementação*>** caixa de diálogo Properties, especifique a linha de comando para desinstalar a aplicação no campo do **programa Desinstalar.**  

2.  Implemente a aplicação e, em seguida, selecione a ação de implementação **Desinstalar** na página de Definições de **Implementação** do Assistente de Software de Implementação.  

    > [!NOTE]  
    >  Quando selecionar uma ação de implementação de **Desinstalar**, o objetivo de implementação é automaticamente configurado como **Necessário**.  
