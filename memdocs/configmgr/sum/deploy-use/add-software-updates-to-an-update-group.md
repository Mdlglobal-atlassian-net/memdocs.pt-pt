---
title: 'Adicione atualizações a um grupo de atualização '
titleSuffix: Configuration Manager
description: Adicione manualmente ou automaticamente atualizações de software a um grupo de atualização de software no seu ambiente.
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c38ed629e606d3f891a6473866d0e8eda40eade1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723909"
---
# <a name="add-software-updates-to-an-update-group"></a>Adicionar atualizações de software a um grupo de atualizações  

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Os grupos de atualizações de software proporcionam-lhe um método eficaz para organizar as atualizações de software no seu ambiente. Pode adicionar manualmente atualizações de software a um grupo de atualizações de software ou adicionar as atualizações de software automaticamente a um grupo de atualizações de software utilizando uma ADR. Também pode implementar um grupo de atualizações de software manualmente ou implementar o grupo automaticamente, utilizando uma ADR. Depois de implementar um grupo de atualização de software, pode adicionar novas atualizações de software ao grupo e o Gestor de Configuração irá implementá-las automaticamente. Utilize os seguintes procedimentos para adicionar atualizações de software a um grupo de atualizações de software novo ou existente.  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>Para adicionar atualizações de software a um novo grupo de atualizações de software  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software**e, em seguida, clique em **Todas as Atualizações de Software**.  

3.  Selecione as atualizações de software a serem adicionadas ao novo grupo de atualizações de software.  

4.  No separador **Home Page** , no grupo **Atualizar** , clique em **Criar Grupo de Atualização de Software**.  

5.  Especifique o nome para o grupo de atualizações de software e, opcionalmente, forneça uma descrição. Utilize um nome e uma descrição que forneçam informações suficientes para determinar qual o tipo de atualizações de software que fazem parte do grupo de atualizações de software. Para continuar, clique em **Criar**.  

6.  Clique em **Grupos de Atualização de Software** para apresentar o novo grupo de atualização de software.  

7.  Selecione o grupo de atualização de software e, no separador **Home Page** , no grupo **Atualizar** , clique em **Mostrar Membros** para apresentar uma lista das atualizações de software que estão incluídas no grupo.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Para adicionar atualizações de software a um grupo de atualização de software existente  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software**e, em seguida, clique em **Todas as Atualizações de Software**.  

3.  Selecione as atualizações de software que pretende adicionar ao novo grupo de atualizações de software.  

    > [!NOTE]  
    >  No nó **de Atualizações** de Software, o Gestor de Configuração apresenta todas as atualizações, exceto as da classificação de **Upgrades** e da classificação do produto **cliente do Office 365.**  

4.  No separador **Home Page** , no grupo **Atualizar** , clique em **Editar Associação**.  

5.  Selecione o grupo de atualizações de software ao qual pretende adicionar as atualizações de software.  

6.  Clique no nó **Grupos de Atualização de Software** para apresentar o grupo de atualização de software.  

7.  Selecione o grupo de atualizações de software e, no separador **Home Page** , no grupo **Atualizar** , clique em **Mostrar Membros** para apresentar uma lista das atualizações de software que estão incluídas no grupo de atualizações de software.  
