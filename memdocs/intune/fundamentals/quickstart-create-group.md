---
title: Início Rápido – criar um grupo para gerir utilizadores
titleSuffix: Microsoft Intune
description: Neste início rápido, utilizará o Microsoft Intune para criar um grupo com base em utilizadores já existentes.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/17/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 723f4b4e-3090-4811-84ff-6af652abea5a
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7adb23f4709bf3ead07a01cb00d1b38fcb23c40
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330809"
---
# <a name="quickstart-create-a-group-to-manage-users"></a>Início Rápido: criar um grupo para gerir utilizadores

Neste início rápido, utilizará o Intune para criar um grupo com base num utilizador existente. Os grupos são utilizados para gerir os utilizadores e controlar o acesso dos seus funcionários aos recursos da sua empresa. Estes recursos podem fazer parte da intranet da sua empresa ou podem ser recursos externos, tais como sites do SharePoint, aplicações SaaS ou aplicações Web.

Se não tiver uma subscrição Intune, [inscreva-se numa conta de teste gratuita](free-trial-sign-up.md).

>[!NOTE]
>O Intune fornece os grupos **Todos os Utilizadores** e **Todos os Dispositivos** pré-criados na consola com otimizações incorporadas para sua comodidade.

## <a name="prerequisites"></a>Pré-requisitos

- Subscrição do Microsoft Intune – [inscreva-se numa conta de avaliação gratuita](../fundamentals/free-trial-sign-up.md).
- Para concluir este início rápido, terá de [criar um utilizador](quickstart-create-user.md).

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Inscreva-se no Intune no Microsoft Endpoint Manager

Inscreva-se no [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) como [administrador global ou administrador de serviço intune](users-add.md#types-of-administrators). Se criou uma Subscrição de avaliação do Intune, a conta com a qual criou a subscrição é de Administrador global.

## <a name="create-a-group"></a>Criar um grupo

Irá criar um grupo que será utilizado mais tarde nesta série de início rápido. Para criar um grupo:

1. Assim que abrir o **Microsoft Endpoint Manager,** selecione **Grupos** > **Novo grupo**.
2. Na caixa pendente **Tipo de grupo**, selecione **Segurança**.
3. No campo de **nome** sinuoso grupo, insira o nome para o novo grupo (por exemplo, **Testes De Contoso).**
4. Adicione uma **descrição** de Grupo para o grupo.
5. Defina o **Tipo de associação** para **Atribuído**. 
6. Em **Membros**, selecione o link e adicione um ou mais membros para o grupo da lista.

    ![Captura de ecrã da criação de um grupo no Microsoft Intune](./media/quickstart-create-group/quickstart-use-groups-01.png)

7. Clique em **Selecionar** > **Criar**.

Assim que tiver criado o grupo com êxito, este será apresentado na lista **Todos os grupos**. 

## <a name="next-steps"></a>Próximos passos

Neste início rápido, utilizou o Intune para criar um grupo com base num utilizador existente. Para obter mais informações sobre como adicionar grupos ao Intune, veja [Adicionar grupos para organizar utilizadores e dispositivos](groups-add.md).

Para seguir esta série de guias de início rápido do Intune, continue para o próximo guia de início rápido.

> [!div class="nextstepaction"]
> [Guia de Início Rápido: configurar a inscrição automática para dispositivos com o Windows 10](../enrollment/quickstart-setup-auto-enrollment.md)
