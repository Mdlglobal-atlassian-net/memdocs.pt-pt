---
title: Início Rápido – criar e atribuir uma função personalizada no Intune
description: Início Rápido – criar e atribuir uma função personalizada a um gestor de dispositivos remotos.
services: microsoft-intune
author: ErikjeMS
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 03/26/2019
ms.author: erikje
ms.assetid: 0b3ac749-4a61-4717-bf08-e0e6a15c3b0a
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6cb0080a63c14c2a2fe4acd5906980e63e6b832c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079982"
---
# <a name="quickstart-create-and-assign-a-custom-role"></a>Início Rápido: criar e atribuir uma função personalizada

Neste início rápido do Intune, vai criar e atribuir uma função personalizada com permissões específicas a um serviço de segurança operacional. Em seguida, vai atribuir a função a um grupo desses operadores. Há várias funções predefinidas que pode utilizar de imediato. Contudo, ao criar funções personalizadas como esta, tem controlo de acesso preciso em relação a todas as partes de seu sistema de gestão de dispositivos móveis.

Se não tiver uma subscrição Intune, [inscreva-se numa conta de teste gratuita](free-trial-sign-up.md).

## <a name="prerequisites"></a>Pré-requisitos

- Para concluir este início rápido, terá de [criar um grupo](quickstart-create-group.md).

## <a name="sign-in-to-intune"></a>Iniciar sessão no Intune

Inicie sessão no [Intune](https://aka.ms/intuneportal) enquanto Administrador Global ou Administrador de Serviços do Intune. Se criou uma Subscrição de Avaliação do Intune, a conta com a qual criou a subscrição é de Administrador global.

## <a name="create-a-custom-role"></a>Criar uma função personalizada

Quando cria uma função personalizada, pode definir permissões para um amplo conjunto de ações. Para a função de operações de segurança, vamos definir algumas permissões de Leitura para que o operador possa rever as configurações e políticas de um dispositivo.

1. Intune, escolha **Papéis** > **Todos os papéis** > **Adicionar**.
![Browser](./media/quickstart-create-custom-role/add-custom-role.png)
2. Em **Adicionar função personalizada**, na caixa **Nome**, introduza *Operações de segurança*.
3. Na caixa **Descrição**, introduza *Esta função permite que um operador de segurança monitorize informações de configuração e compatibilidade de dispositivos*.
4. Escolha identificar**dispositivos corporativos** >  **Configurar** > **Sim** ao lado de **Ler** > **OK**.
![Browser](./media/quickstart-create-custom-role/corp-device-id-read.png)
5. Escolha **as políticas** > de conformidade do dispositivo**Sim** ao lado de **Ler** > **OK**.
6. Escolha **configurações** > do dispositivo**Sim** ao lado de **Ler** > **OK**.
7. Escolha **organização** > **Sim** ao lado de **Ler** > **OK**.
8. Escolha **OK** > **Criar**.

## <a name="assign-the-role-to-a-group"></a>Atribuir a função a um grupo

Antes de o seu operador de segurança poder utilizar as novas permissões, tem de atribuir a função a um grupo que contenha o utilizador de segurança.

1. Intune, escolha **Funções** > **Todas as funções** > **Operações de segurança**.
2. Em **Funções do Intune**, selecione **Atribuições** > **Atribuir**.
3. Na caixa **Nome da atribuição**, introduza *Operador de segurança*.
4. Escolha **Adicionar Membro (Grupos)** > **.**
5. Selecione o grupo **Técnicos de Teste da Contoso**.
6. Escolha **Selecione** > **OK**.
7. Escolha **Scope (Grupos)** > **Selecione grupos para incluir** > **Os Testers Contoso**.
8. Escolha **Selecione** > **OK** > **OK**.

Agora todos os elementos do grupo são membros da função *Operações de segurança* e podem rever as seguintes informações sobre um dispositivo: identificadores de dispositivo da empresa, políticas de conformidade do dispositivo, configurações do dispositivo e informações sobre a organização.

## <a name="clean-up-resources"></a>Limpar recursos

Se não quiser continuar a utilizar a nova função personalizada, pode eliminá-la. Escolha **papéis** > **Todas as funções** > escolher as elipses ao lado do papel > **Excluir**.

## <a name="next-steps"></a>Passos seguintes

Neste início rápido, criou uma função de operações de segurança personalizada e atribui-a a um grupo. Para obter mais informações sobre funções no Intune, veja [Controlo de administração baseada em funções (RBAC) com o Microsoft Intune](role-based-access-control.md).

Para seguir esta série de guias de início rápido do Intune, continue para o próximo guia de início rápido.

> [!div class="nextstepaction"]
> [Quickstart: Criar um perfil de dispositivo de e-mail para iOS/iPadOS](../configuration/quickstart-email-profile.md)
