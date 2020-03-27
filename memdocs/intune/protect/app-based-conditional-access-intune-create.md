---
title: Configurar a política de acesso condicional baseada em aplicativos com o Intune
titleSuffix: Microsoft Intune
description: Aprenda a criar uma política de acesso condicional baseada em aplicativos com o Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 73b471d7eefa8e696b17a949756ce1395530c5f7
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80323199"
---
# <a name="set-up-app-based-conditional-access-policies-with-intune"></a>Configurar políticas de acesso condicional baseadas em aplicativos com intune

Configurar políticas de acesso condicional baseadas em aplicativos para apps que fazem parte da lista de aplicações aprovadas. A lista de aplicações aprovadas consiste em aplicações que foram testadas pela Microsoft.

Antes de poder utilizar as políticas de Acesso Condicional baseadas em aplicações, é necessário que as políticas de [proteção de aplicações Intune](../apps/app-protection-policies.md) se apliquem às suas apps.

> [!IMPORTANT]
> Este artigo percorre os passos para adicionar uma política de Acesso Condicional baseada em aplicativos. Pode utilizar os mesmos passos quando adicionar aplicações, como o SharePoint Online, Microsoft Teams e Microsoft Exchange Online a partir da lista de aplicações aprovadas.

## <a name="create-app-based-conditional-access-policies"></a>Criar políticas de acesso condicional baseadas em aplicativos

O Acesso Condicional é uma tecnologia do Azure Active Directory (Azure AD). O nó de Acesso Condicional a que acede a partir de *Intune* é o mesmo nó a que acede a partir de *Azure AD*. Como é o mesmo nó, não é preciso alternar entre Intune e Azure AD para configurar políticas.

Antes de poder criar políticas de Acesso Condicional a partir do centro de administração do Microsoft Endpoint Manager, deve ter uma licença Azure AD Premium.

### <a name="to-create-an-app-based-conditional-access-policy"></a>Para criar uma política de acesso condicional baseada em aplicativos

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Selecione **segurança endpoint** > **acesso condicional** > **Nova política.**

3. Introduza uma política **Nome**, e, em seguida, em *Atribuições,* selecione **Utilizadores e grupos**. Utilize as opções Incluir ou Excluir para adicionar os grupos à política e selecione **Concluído**.

4. Selecione **aplicações ou ações cloud**, e escolha quais aplicações proteger. Por exemplo, escolha **Selecionar aplicações** e selecione **Office 365 SharePoint Online** e **Office 365 Exchange Online**.

   Selecione **Concluído** para guardar as alterações.

5. Selecione **Condições** > **Aplicações do cliente** para aplicar a política a aplicações e browsers. Por exemplo, selecione **Sim** e, em seguida, ative **Browser** e **Aplicações móveis e clientes de ambiente de trabalho**.

   Selecione **Concluído** para guardar as alterações.

6. Sob *os controlos de Acesso,* selecione **Grant** para aplicar acesso condicional com base na conformidade do dispositivo. Por exemplo, selecione **Conceder acesso** > **Pedir que o dispositivo seja marcado como conforme**.

   Escolha **Selecionar** para guardar as alterações.

7. Para **ativar a política**, selecione **On**e, em seguida, selecione **Criar** para guardar as suas alterações.





## <a name="next-steps"></a>Próximos passos
[Bloquear aplicações que não tenham autenticação moderna](app-modern-authentication-block.md)

## <a name="see-also"></a>Veja também

[Proteger os dados da aplicação com políticas de proteção de aplicações](../apps/app-protection-policies.md)
[Acesso Condicional no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
