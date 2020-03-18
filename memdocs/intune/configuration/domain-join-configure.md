---
title: Domínio junta definições de perfil para Windows 10 no Microsoft Intune - Azure Microsoft Docs
description: Crie um perfil de configuração de dispositivo de união de domínio para dispositivos híbridos azure aD. Utilize este perfil para implementar informações de domínio ative diretório no local para dispositivos aprovisionados com o Windows Autopilot e microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333113"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Configuração Domain Junte as definições para dispositivos híbridos Azure AD em Microsoft Intune

Muitos ambientes usam no local O Diretório Ativo (AD). Quando os dispositivos adenantes de domínio também são unidos ao Azure AD, eles são chamados dispositivos híbridos Azure AD. Utilizando o Windows Autopilot, pode [inscrever dispositivos híbridos Azure AD](../enrollment/windows-autopilot-hybrid.md) em Intune. Para se inscrever, também precisa de um perfil de configuração **de Domain Join.**

Um perfil de configuração **de 'Ajoin' de domínio** de domínio inclui informações de domínio de diretório ativo no local. Quando os dispositivos estão a fornecer (e normalmente offline), este perfil implementa os detalhes do domínio AD para que os dispositivos saibam qual o domínio no local a aderir. Se não criar um perfil de adesão ao domínio, estes dispositivos podem não ser implementados.

Esta funcionalidade aplica-se a:

- Windows 10 e mais recente
- Hybrid Azure AD aderiu a dispositivos
- Implantação híbrida com Piloto Automático + Intune

Este artigo mostra-lhe como criar um perfil de adesão de domínio para uma implementação híbrida do Autopilot. Também pode ver as definições disponíveis.

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política é **Windows 10: Perfil de adesão de domínio do domínio do domínio que inclui informações de domínio no local para inscrever dispositivos híbridos ad com o Windows Autopilot**.
    - **Descrição**: Insira uma descrição para a apólice. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
    - **Tipo de perfil:** Selecione **'Selecionar A dispor de domínio' (pré-visualização)** .

4. Selecione **Definições**. Introduza as seguintes propriedades:

    - **Prefixo de nome do computador**: Introduza um prefixo para o nome do dispositivo. Os nomes do computador têm 15 caracteres. Após o prefixo, os restantes 15 caracteres são gerados aleatoriamente.
    - **Nome de domínio**: Introduza o nome de domínio totalmente qualificado (FQDN) os dispositivos devem aderir. Por exemplo, introduza `americas.corp.contoso.com.`
    - **Unidade organizacional** (opcional): Insira o caminho completo[(nome distinto)](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)para a unidade organizacional (OU) as contas do computador devem ser criadas. Por exemplo, introduza `"CN=Users,DC=Contoso,DC=com"`. Se não introduzir um valor, é utilizado um recipiente de objetos de computador bem conhecido.

      Para obter mais informações e conselhos sobre esta definição, consulte [dispositivos híbridos azure ad- joined](../enrollment/windows-autopilot-hybrid.md).

5. Assim que terminar, selecione **OK** > **Criar** para guardar as alterações.

O perfil é criado e mostrado na lista de perfis. Está agora pronto para [implementar dispositivos híbridos azure ad-join, utilizando Intune e Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Próximos passos

Depois que o perfil é criado, está pronto para ser atribuído. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

[Implemente dispositivos híbridos de AD com](../enrollment/windows-autopilot-hybrid.md)a utilização de Intune e Windows Autopilot .
