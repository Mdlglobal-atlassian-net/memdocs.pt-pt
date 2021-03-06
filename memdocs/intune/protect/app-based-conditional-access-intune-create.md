---
title: Configurar a política de acesso condicional baseada em aplicativos com o Intune
titleSuffix: Microsoft Intune
description: Aprenda a criar uma política de acesso condicional baseada em aplicativos com o Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: how-to
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
ms.openlocfilehash: 7d07b87bca934dac924f2d2c281ecb7b2a2e8a2c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989791"
---
# <a name="set-up-app-based-conditional-access-policies-with-intune"></a>Configurar políticas de acesso condicional baseadas em aplicativos com intune

Configurar políticas de acesso condicional baseadas em aplicativos para apps que fazem parte da lista de aplicações aprovadas. A lista de aplicações aprovadas consiste em aplicações que foram testadas pela Microsoft.

Antes de poder utilizar as políticas de Acesso Condicional baseadas em aplicações, é necessário que as políticas de [proteção de aplicações Intune](../apps/app-protection-policies.md) se apliquem às suas apps.

> [!IMPORTANT]
> Este artigo percorre os passos para adicionar uma simples política de acesso condicional baseada em aplicações. Pode utilizar os mesmos passos para outras aplicações em nuvem. Para mais informações, consulte a [implementação](https://docs.microsoft.com/azure/active-directory/conditional-access/plan-conditional-access) do Plano de Acesso Condicional

## <a name="create-app-based-conditional-access-policies"></a>Criar políticas de acesso condicional baseadas em aplicativos

O Acesso Condicional é uma tecnologia do Azure Active Directory (Azure AD). O nó de Acesso Condicional a que acede a partir de *Intune* é o mesmo nó a que acede a partir de *Azure AD*. Como é o mesmo nó, não é preciso alternar entre Intune e Azure AD para configurar políticas.

Antes de poder criar políticas de Acesso Condicional a partir do centro de administração do Microsoft Endpoint Manager, deve ter uma licença Azure AD Premium.

### <a name="to-create-an-app-based-conditional-access-policy"></a>Para criar uma política de acesso condicional baseada em aplicativos

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Selecione **segurança endpoint**  >  **Acesso condicional**Nova  >  **política**.

3. Introduza uma política **Nome**, e, em seguida, em *Atribuições,* selecione **Utilizadores e grupos**. Utilize as opções Incluir ou Excluir para adicionar os grupos à política e selecione **Concluído**.

4. Selecione **aplicações ou ações cloud**, e escolha quais aplicações proteger. Por exemplo, escolha **as aplicações Select**, e selecione **Office 365 (pré-visualização)**.

   Selecione **Concluído** para guardar as alterações.

5. Selecione **Conditions**  >  **Condições Aplicações cliente** para aplicar a política a apps e navegadores. Por exemplo, selecione **Sim** e, em seguida, ative **Browser** e **Aplicações móveis e clientes de ambiente de trabalho**.

   Selecione **Concluído** para guardar as alterações.

6. Sob *os controlos de Acesso,* selecione **Grant** para aplicar acesso condicional com base na conformidade do dispositivo. Por exemplo, selecione **Acesso ao Grant**Exigir  >  **aplicação de cliente aprovada** e exigir política de **proteção de aplicações (pré-visualização)** e, em seguida, selecione **Exigir um dos controlos selecionados**

   Escolha **Selecionar** para guardar as alterações.

7. Para **ativar a política**, selecione **On**e, em seguida, selecione **Criar** para guardar as suas alterações.





## <a name="next-steps"></a>Passos seguintes
[Bloquear aplicações que não tenham autenticação moderna](app-modern-authentication-block.md)

## <a name="see-also"></a>Consulte também

[Proteja os dados das aplicações com políticas](../apps/app-protection-policies.md) 
 de proteção de aplicações [Acesso Condicional no Diretório Ativo Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
