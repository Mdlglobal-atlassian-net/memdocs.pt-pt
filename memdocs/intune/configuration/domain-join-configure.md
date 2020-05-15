---
title: Domínio junta definições de perfil para Windows 10 no Microsoft Intune - Azure Microsoft Docs
description: Crie um perfil de configuração de dispositivo de união de domínio para dispositivos híbridos azure aD. Utilize este perfil para implementar informações de domínio ative diretório no local para dispositivos aprovisionados com o Windows Autopilot e microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b2fd0bac1532b20aac35d36a24831c658f24761
ms.sourcegitcommit: b94415467831517f2aeab9c7c8a13fe8db8bc8ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401646"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Configuração Domain Junte as definições para dispositivos híbridos Azure AD em Microsoft Intune

Muitos ambientes usam no local O Diretório Ativo (AD). Quando os dispositivos adenantes de domínio também são unidos ao Azure AD, eles são chamados dispositivos híbridos Azure AD. Utilizando o Windows Autopilot, pode [inscrever dispositivos híbridos Azure AD](../enrollment/windows-autopilot-hybrid.md) em Intune. Para se inscrever, também precisa de um perfil de configuração **de Domain Join.**

Um perfil de configuração **de 'Ajoin' de domínio** de domínio inclui informações de domínio de diretório ativo no local. Quando os dispositivos estão a fornecer (e normalmente offline), este perfil implementa os detalhes do domínio AD para que os dispositivos saibam qual o domínio no local a aderir. Se não criar um perfil de adesão ao domínio, estes dispositivos podem não ser implementados.

Esta funcionalidade aplica-se a:

- Windows 10 e mais recente
- Dispositivos híbridos associados ao Azure AD
- Implantação híbrida com Piloto Automático + Intune

Este artigo mostra-lhe como criar um perfil de adesão de domínio para uma implementação híbrida do Autopilot. Também pode ver as definições disponíveis.

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
    - **Perfil**: Selecione **'Select Domain Join' (pré-visualização)**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política é **Windows 10: Perfil de adesão de domínio do domínio do domínio que inclui informações de domínio no local para inscrever dispositivos híbridos ad com o Windows Autopilot**.
    - **Descrição**: Insira uma descrição para a apólice. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.
7. Nas definições de **Configuração,** introduza as seguintes propriedades:

    - **Prefixo de nome do computador**: Introduza um prefixo para o nome do dispositivo. Os nomes do computador têm 15 caracteres. Após o prefixo, os restantes 15 caracteres são gerados aleatoriamente.
    - **Nome de domínio**: Introduza o nome de domínio totalmente qualificado (FQDN) os dispositivos devem aderir. Por exemplo, inserir`americas.corp.contoso.com.`
    - **Unidade organizacional** (opcional): Insira o caminho completo[(nome distinto)](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)para a unidade organizacional (OU) as contas do computador devem ser criadas. Por exemplo, introduza `"CN=Users,DC=Contoso,DC=com"`. Se não introduzir um valor, é utilizado um recipiente de objetos de computador bem conhecido.

      Para obter mais informações e conselhos sobre esta definição, consulte [dispositivos híbridos azure ad- joined](../enrollment/windows-autopilot-hybrid.md).

8. Selecione **Seguinte**.

9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como ou `US-NC IT Team` `JohnGlenn_ITDepartment` . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupo de utilizadores que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

Está agora pronto para [implementar dispositivos híbridos azure ad-join, utilizando Intune e Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Passos seguintes

Depois de [atribuído](device-profile-assign.md)o perfil, [monitorize o seu estado](device-profile-monitor.md).

[Implemente dispositivos híbridos de AD com](../enrollment/windows-autopilot-hybrid.md)a utilização de Intune e Windows Autopilot .
