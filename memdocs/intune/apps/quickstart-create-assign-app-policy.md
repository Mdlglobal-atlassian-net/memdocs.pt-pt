---
title: 'Guia de Início Rápido: criar e atribuir uma política de proteção de aplicações'
titleSuffix: Microsoft Intune
description: Neste guia de início rápido, utilizará o Microsoft Intune para criar e atribuir uma política de proteção de aplicações.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2586fce0-5dca-4686-b9c4-791778838401
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb8b5eae3c88664caff76da597fc3ab9111f989c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79326793"
---
# <a name="quickstart-create-and-assign-an-app-protection-policy"></a>Guia de Início Rápido: criar e atribuir uma política de proteção de aplicações

Neste guia de início rápido, irá utilizar o Intune para criar e atribuir uma política de proteção de aplicações a uma aplicação cliente no dispositivo de um utilizador final. Intune usa políticas de proteção de aplicações para confirmar que as suas aplicações estão a cumprir os requisitos de proteção de dados da sua organização.

Se não tiver uma subscrição Intune, [inscreva-se numa conta de teste gratuita](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Pré-requisitos

- Para concluir este guia de início rápido, tem de [criar um utilizador](../fundamentals/quickstart-create-user.md), [criar um grupo](../fundamentals/quickstart-create-group.md), [inscrever um dispositivo](../enrollment/quickstart-setup-auto-enrollment.md) e [adicionar e atribuir uma aplicação](quickstart-add-assign-app.md).

## <a name="sign-in-to-intune"></a>Iniciar sessão no Intune

Inicie sessão no [Intune](https://aka.ms/intuneportal) enquanto [Administrador Global ou um Administrador de Serviços do Intune](../fundamentals/users-add.md#types-of-administrators). Se criou uma Subscrição de Avaliação do Intune, a conta com a qual criou a subscrição é de Administrador global.

## <a name="create-an-app-protection-policy"></a>Criar uma política de proteção de aplicações

Utilize os seguintes passos para criar uma política de proteção de aplicações:

1. [Intune](https://aka.ms/intuneportal), selecione **Apps** > App As políticas > de**proteção****create Policy**. 
2. Introduza os seguintes detalhes:

    - **Nome**: *Proteção de conteúdo do Windows 10*
    - **Descrição**: *Os utilizadores associados a esta política não conseguirão cortar, copiar nem colar conteúdos entre a aplicação atribuída e outras aplicações não geridas no dispositivo.*
    - **Plataforma**: *Windows 10*
    - **Estado da inscrição**: *Com inscrição*

3. Selecione **Aplicações protegidas** para selecionar as aplicações que têm de cumprir esta política.
4. Clique em **Adicionar aplicações**.
5. Em **Aplicações recomendadas**, selecione **Word Mobile**.
5. Clique **ok** > **OK**. 
6. Selecione **Definições necessárias** para configurar a aplicação.
7. Clique em **Permitir Substituições** para definir o modo do Windows Information Protection. A seleção desta opção impedirá que os dados empresariais saiam da aplicação protegida.
8. Clique em **CRIAR OK** > **.**

Agora verá a política de proteção de aplicações em Intune.

### <a name="assign-the-app-protection-policy"></a>Atribuir a política de proteção de aplicações

Depois de criar uma política de proteção de aplicações no Intune, pode atribuí-la a grupos. 

Siga os seguintes passos para atribuir uma política de proteção de aplicações:

1. [Intune](https://aka.ms/intuneportal), selecione **Intune** > **Apps** > **App Protection policies**. 
2. Selecione a política de proteção de aplicações que criou anteriormente. Neste guia de início rápido, a política é **Proteção de conteúdo do Windows 10**.
3. Selecione **Atribuições**.
4. Clique **Selecionar grupos para incluir** no separador **Incluir**.
5. Selecione **Técnicos de Teste da Contoso** como o grupo a incluir.
6. Clique em > **Selecione Guardar**. **Select** 

Agora já atribuiu a política de proteção de aplicações.

> [!NOTE]
> As políticas de proteção de aplicações só podem ser aplicadas a grupos que contenham utilizadores e não dispositivos.

## <a name="next-steps"></a>Passos seguintes

Neste guia de início rápido, criou e atribuiu uma política de proteção de aplicações. Os utilizadores da aplicação aos quais foi atribuída esta política não conseguirão cortar, copiar nem colar conteúdos entre a aplicação atribuída e outras aplicações não geridas no dispositivo. Este tipo de proteção ajudará a proteger os dados da sua organização. Para obter mais informações sobre políticas de proteção de aplicações no Intune, veja [What are app protection policies?](app-protection-policy.md) (O que são as políticas de proteção de aplicações?).

Para seguir esta série de guias de início rápido do Intune, continue para o próximo guia de início rápido.

> [!div class="nextstepaction"]
> [Guia de Início Rápido: criar e atribuir uma função personalizada](../fundamentals/create-custom-role.md)
