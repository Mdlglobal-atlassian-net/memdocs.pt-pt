---
title: Inscrever-se ou iniciar sessão no Microsoft Intune
description: Como se inscrever para uma subscrição do Microsoft Intune ou iniciar a sua subscrição.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f3ce07a-b718-42a9-bace-f99a8b8abd94
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: ad73f89ff4dccd3151bd3123cd4bb54483aaae30
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332737"
---
# <a name="sign-up-or-sign-in-to-microsoft-intune"></a>Inscrever-se ou iniciar sessão no Microsoft Intune

Este tópico informa os administradores de sistema acerca da inscrição numa conta do Intune.

Antes de se inscrever no Intune, confirme se já tem uma conta do Microsoft Online Services, um Contrato Enterprise ou contrato de licenciamento em volume equivalente. Um contrato de licenciamento em volume da Microsoft ou outra subscrição dos serviços cloud da Microsoft, como o Office 365, geralmente inclui uma conta escolar ou profissional.

Se já tiver uma conta escolar ou profissional, **inicie sessão** com a mesma e adicione o Intune à sua subscrição. Caso contrário, pode **inscrever-se** numa conta nova e utilizar o Intune para a sua organização.

>[!WARNING]
>Não pode combinar uma conta escolar ou profissional existente após inscrever-se numa conta nova.

## <a name="how-to-sign-up-for-intune"></a>Como se inscrever no Intune

1. Visite a página [Inscrição no Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20).

   ![Captura de ecrã da página Web de inscrição numa conta de Avaliação do Microsoft Intune](./media/account-sign-up/account-sign-up-site.png)

2. Na página Inscrição, inicie sessão ou inscreva-se para gerir uma nova subscrição do Intune.

## <a name="post-sign-up-considerations"></a>Considerações de pós-inscrição

Depois de se inscrever numa nova subscrição, recebe uma mensagem de e-mail com as informações da sua conta para o endereço de e-mail que indicou durante o processo de inscrição. Este e-mail confirma que a sua subscrição está ativa.

Depois de concluir o processo de inscrição, é direcionado para o centro de administração da Microsoft 365, utilizado para adicionar utilizadores e atribuir-lhes licenças. Se tiver apenas contas baseadas na cloud com o seu nome de domínio onmicrosoft.com predefinido, pode adicionar utilizadores e atribuir licenças neste momento. Contudo, se planear utilizar o [nome de domínio personalizado](custom-domain-name-configure.md) da sua organização ou as [informações de conta de utilizador sincronizada](users-add.md#sync-active-directory-and-add-users-to-intune) do Active Directory no local, pode fechar essa janela do browser.

## <a name="sign-in-to-microsoft-intune"></a>Inscreva-se na Microsoft Intune

Uma vez que se tenha inscrito no Intune, pode utilizar qualquer dispositivo com um [browser suportado](supported-devices-browsers.md#intune-supported-web-browsers) para iniciar sessão no [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) para administrar o serviço.

Por predefinição, a sua conta deve ter uma das seguintes permissões em Azure AD:

- Administrador Global
- Administrador de Serviço Intune (também conhecido como Administrador Intune)

Para conceder acesso à administração do serviço para utilizadores com outras permissões, consulte o Controlo de [Acesso Baseado em Funções](role-based-access-control.md)

### <a name="intune-admin-portal-url"></a>URL do portal de administração intune

Microsoft 365 Admin Center: https://devicemanagement.microsoft.com

Portal Intune Azure: https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade

Intune for Education: https://intuneeducation.portal.azure.com

Intune classic portal: https://manage.microsoft.com O portal clássico Intune é usado apenas para gerir dispositivos matriculados com o cliente de software Intune PC

### <a name="urls-for-intune-services-provided-by-office-365"></a>URLs para serviços Intune prestados pelo Office 365

Microsoft 365 Business: https://portal.microsoft.com/adminportal

Office 365 Mobile Device Management: https://portal.office.com/adminportal/home#/MifoDevices

## <a name="see-also"></a>Veja também

[Não pode entrar no Office 365, Azure ou Intune](https://support.microsoft.com/help/2412085)
