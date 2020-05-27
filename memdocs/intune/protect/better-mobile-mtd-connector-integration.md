---
title: Configurar a integração do Better Mobile com o Intune
titleSuffix: Intune on Azure
description: Integração do conector Better Mobile com o Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6208c8f225cc3e54a61181960223f3f8cad8423d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989739"
---
# <a name="integrate-better-mobile-with-intune"></a>Integrar o Better Mobile com o Intune

Conclua os seguintes passos para integrar a solução Better Mobile Threat Defense com o Intune.

## <a name="before-you-begin"></a>Antes de começar

Os seguintes passos devem ser concluídos na [consola de administração Better Mobile](https://aad.bmobi.net) e permitirão uma ligação ao serviço da Better Mobile tanto para dispositivos matriculados intune (utilizando a conformidade do dispositivo) como para dispositivos não matriculados (utilizando políticas de proteção de aplicações).

Antes de iniciar o processo de integração do Better Mobile com o Intune, certifique-se de que tem os seguintes elementos:

- Subscrição do Microsoft Intune

- Credenciais de administrador do Azure Active Directory para conceder as seguintes permissões:

  - Iniciar sessão e ler o perfil de utilizador

  - Aceder ao diretório como o utilizador com sessão iniciada

  - Ler os dados do diretório

  - Enviar informações do dispositivo para o Intune

- Credenciais de administrador para aceder à consola de administração do Better Mobile.

### <a name="better-mobile-app-authorization"></a>Autorização da aplicação Better Mobile

O processo de autorização da aplicação Better Mobile consiste no seguinte:

- Permitir que o serviço do Better Mobile transmita informações relacionadas com o estado de funcionamento do dispositivo ao Intune.

- O Better Mobile sincroniza com a associação do Grupo de Inscrição do Azure AD para preencher a respetiva base de dados do dispositivo.

- Permitir que a consola de administração do Better Mobile utilize o Início de Sessão Único (SSO) do Azure AD.

- Permitir que a aplicação Better Mobile inicie sessão através do SSO do Azure AD.

## <a name="to-set-up-better-mobile-integration"></a>Para configurar a integração do Better Mobile

1. Aceda à [consola de administração do Better Mobile](https://aad.bmobi.net) e inicie sessão com as suas credenciais.
2. Escolha **a conta**de adicionar  >  **emM/MDM**de integração  >  **ADD ACCOUNT**.

     ![Imagem da consola de administração Better Mobile](./media/better-mobile-mtd-connector-integration/better_mobile_console.png)

3. Escolha **Intune**.
4. Junto a **ACCOUNT NAME** (NOME DA CONTA), escreva um descritor.
5. Na janela **Microsoft Sign in** (Início de Sessão Microsoft), introduza as suas credenciais do Intune.
6. Na janela **Permissions requested** (Permissões pedidas), selecione **Accept** (Aceitar).
7. Procure os Grupos de Segurança do Azure AD cujos dispositivos pretende que o Better Mobile sincronize e selecione-os a partir da lista. Em seguida, selecione **Continuar**.
8. Selecione **Done** (Concluído).
9. A página **Add account** (Adicionar conta) voltará a ser apresentada. Feche a página.

## <a name="next-steps"></a>Passos seguintes

- [Configurar aplicativos Better Mobile para dispositivos matriculados](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Configurar aplicativos Better Mobile para dispositivos não matriculados](mtd-add-apps-unenrolled-devices.md)
