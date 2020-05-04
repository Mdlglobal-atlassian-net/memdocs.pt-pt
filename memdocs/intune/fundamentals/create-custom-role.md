---
title: Criar um papel personalizado em Intune
description: Aprenda a criar um papel personalizado no Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6633682a9572ba36f41f42e77c5aa64403e0e209
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81440582"
---
# <a name="create-a-custom-role-in-intune"></a>Criar um papel personalizado em Intune

Pode criar uma função intune personalizada que inclua quaisquer permissões necessárias para uma função de trabalho específica. Por exemplo, se um grupo do departamento de TI gerir aplicações, políticas e perfis de configuração, pode juntar todas essas permissões numa só função personalizada. Depois de criar uma função personalizada, pode [atribuí-la](assign-role.md) a todos os utilizadores que necessitem dessas permissões.

Para criar, editar ou atribuir funções, a sua conta tem de ter uma das seguintes permissões no Azure AD:
- **Administrador Global**
- **Administrador de Serviços do Intune**

## <a name="to-create-a-custom-role"></a>Para criar uma função personalizada

1. No [centro de administração do Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha**funções** > de **administração** > do Inquilino**Todas as funções** > **Criam**.

2. Na página **Basics,** introduza um nome e descrição para o novo papel e, em seguida, escolha **Next**.

3. Na página **Permissões,** escolha as permissões que pretende utilizar com esta função.

4. Na página **Scope (Tags),** escolha as etiquetas para este papel. Quando esta função é atribuída a um utilizador, esse utilizador pode aceder a recursos que também possuam estas etiquetas. Escolha **Seguinte**.

5. Na página **Review + criar** página, quando terminar, escolha **Criar**. O novo papel é apresentado na lista nas **funções Intune - Todas as funções.**

## <a name="copy-a-role"></a>Copiar um papel

Também pode copiar um papel existente.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha**funções** > de **administração** > do Inquilino Todas as**funções** > selecionar a caixa de verificação para um papel na lista > **Duplicate**.

2. Na página **Basics,** insira um nome. Certifique-se de usar um nome único.

3. Todas as permissões e etiquetas de âmbito do papel original já serão selecionadas. Posteriormente, pode alterar o **nome**, **descrição,** **permissões**e **âmbito**da função duplicada .

4. Depois de ter feito todas as alterações que deseja, escolha **Next** para chegar à página **Review + criar.** Selecione **Criar**. 

## <a name="next-steps"></a>Passos seguintes
- [Atribuir uma função a um utilizador](assign-role.md)
- [Saiba mais sobre o controlo de acesso baseado em papéis em Intune](role-based-access-control.md)


