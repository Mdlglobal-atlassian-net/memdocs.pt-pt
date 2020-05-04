---
title: Início Rápido – criar um utilizador no Intune
description: Início Rápido – criar um utilizador no Intune.
services: microsoft-intune
author: ErikjeMS
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 01/17/2020
ms.author: erikje
ms.manager: dougeby
ms.assetid: 820fcb18-0927-4ebd-be79-dce92b51c261
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf5c76e276722fb9bab2b5d6fac511f0b22ae1f2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330749"
---
# <a name="quickstart-create-a-user-in-intune-and-assign-the-user-a-license"></a>Quickstart: Criar um utilizador em Intune e atribuir uma licença ao utilizador

Neste arranque rápido, irá criar um utilizador e, em seguida, atribuir ao utilizador uma licença Intune. Quando utiliza o Intune, cada pessoa que deseja ter acesso aos dados da empresa deve ter a sua própria conta de utilizador. Os administradores intune podem configurar os utilizadores mais tarde para gerir o controlo de acesso.

## <a name="prerequisites"></a>Pré-requisitos

- Uma subscrição do Microsoft Intune. [Inscreva-se para uma conta de teste gratuita.](../fundamentals/free-trial-sign-up.md)

## <a name="sign-in-to-intune-in-microsoft-endpoint-manager"></a>Inscreva-se no Intune no Microsoft Endpoint Manager

Inscreva-se no [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) como [administrador global ou administrador de serviço intune](users-add.md#types-of-administrators). Se criou uma subscrição de teste Intune, a conta com a qual criou a subscrição é o administrador global.

## <a name="create-a-user"></a>Criar um utilizador

Um utilizador deve ter uma conta de utilizador para se inscrever na gestão do dispositivo Intune. Para criar um novo utilizador:

1. No Microsoft Endpoint Manager, selecione ![ **Utilizadores** > Todos os **utilizadores** > Novos **utilizadores**: No Microsoft Endpoint Manager, selecione Novo utilizador](./media/quickstart-create-user/create-user.png)
2. Na caixa **Nome,** introduza um nome, como ![ *Dewey Kellum*: Adicione detalhes do utilizador](./media/quickstart-create-user/create-user-02.png)
3. Na caixa de **nomes do Utilizador,** Dewey@contoso.onmicrosoft.comintroduza um identificador de utilizador, como .

    > [!NOTE]
    > Se não configurar o nome de domínio do cliente, utilize o nome de domínio verificado utilizado para criar a subscrição Intune (ou [teste gratuito).](free-trial-sign-up.md#sign-up-for-a-microsoft-intune-free-trial) 

4. Selecione **Mostrar palavra-passe** e lembre-se da senha gerada automaticamente para que possa iniciar sessão num dispositivo de teste.
5. Selecione **Criar**.

## <a name="assign-a-license-to-the-user"></a>Atribuir uma licença ao utilizador

Depois de ter criado um utilizador, deve utilizar o centro de administração microsoft [365](https://go.microsoft.com/fwlink/p/?LinkId=698854) para atribuir uma licença Intune ao utilizador. Se não atribuir uma licença ao utilizador, não conseguirão inscrever o dispositivo no Intune.

Para atribuir uma licença Intune a um utilizador:

1. Inscreva-se no centro de administração da [Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854) com as mesmas credenciais que usou para iniciar sessão no Intune.
2. Selecione **Utilizadores** > **Ativos utilizadores**e, em seguida, selecione o utilizador que acabou de criar.
3. Selecione o separador **Licenças e Aplicações.**
4. Em **caso de Select localização**, selecione uma localização para o utilizador, se ainda não estiver definida.
2. Selecione a caixa de verificação **Intune** na secção **Licenças.** Se outra licença incluir Intune, pode selecionar essa licença. O nome do [produto](https://docs.microsoft.com/azure/active-directory/users-groups-roles/licensing-service-plan-reference) apresentado é usado como plano de serviço na gestão azure.

    ![Selecione a localização e a licença Intune](./media/quickstart-create-user/create-user-03.png)

   > [!NOTE]
   > Esta definição utiliza uma das suas licenças para o utilizador. Se estiver a usar um ambiente experimental, irá posteriormente reatribuir esta licença a um verdadeiro utilizador num ambiente ao vivo.

6. Selecione **Guardar alterações**.

O novo utilizador ativo intune irá agora mostrar que está a usar uma licença **Intune.**

## <a name="clean-up-resources"></a>Limpar recursos

Se já não necessitar deste utilizador, pode eliminar o utilizador indo para o centro de [administração da Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854) e selecionando **os Utilizadores** > *o utilizador* > eliminar*o utilizador* > Delete**user** > **Close**.

   ![Selecione o ícone de exclusão](./media/quickstart-create-user/create-user-04.png)

## <a name="next-steps"></a>Passos seguintes

Neste arranque rápido, criou um utilizador e atribuiu uma licença Intune a esse utilizador. Para obter mais informações sobre como adicionar utilizadores ao Intune, veja [Adicionar utilizadores e conceder permissões administrativas no Intune](users-add.md).

Para continuar esta série de quickstarts Intune, vá para o próximo quickstart:

> [!div class="nextstepaction"]
> [Início Rápido: criar um grupo para gerir utilizadores](quickstart-create-group.md)
