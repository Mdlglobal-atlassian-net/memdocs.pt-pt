---
title: Restringir funcionalidades de dispositivos utilizando a política no Microsoft Intune - Azure [ Microsoft Docs
description: Adicione um perfil de dispositivo para restringir funcionalidades no administrador de dispositivos Android, Android Enterprise, macOS, iOS, iPadOS, Windows Phone e Dispositivos Windows 10 no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 716925f077b7433eab06a6ea2f557c7653d0b03d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551433"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Configurar definições de restrição de dispositivos no Microsoft Intune

Intune inclui políticas de restrição de dispositivos que ajudam os administradores a controlar dispositivos Android, iOS/iPadOS, macOS e Windows. Estas restrições permitem controlar uma vasta gama de configurações e funcionalidades para proteger os recursos da sua organização. Por exemplo, os administradores podem:

- Permite ou bloqueia a câmara do dispositivo.
- Controle o acesso ao Google Play, lojas de aplicações, documentos de visualização e jogos.
- Bloqueie aplicações incorporadas ou crie uma lista de aplicações que permitissem ou proibissem.
- Permitir ou evitar o backup de ficheiros para contas de cloud e armazenamento.
- Detete um comprimento mínimo de senha e bloqueie senhas simples.

Estas funcionalidades estão disponíveis em Intune e são configuráveis pelo administrador. Intune usa "perfis de configuração" para criar e personalizar estas configurações para as necessidades da sua organização. Depois de adicionar estas funcionalidades num perfil, pode então empurrar ou implementar o perfil para dispositivos da sua organização.

Este artigo mostra-lhe como criar um perfil de restrições de dispositivos. Também pode ver todas as definições disponíveis para as diferentes plataformas.

> [!NOTE]
> A interface de utilizador Intune (UI) está a atualizar-se para uma experiência completa de ecrã, podendo demorar várias semanas. Até que o seu inquilino receba esta atualização, terá um fluxo de trabalho ligeiramente diferente quando criar ou editar configurações descritas neste artigo.

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione perfis de**configuração** > de **dispositivos** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Escolha a plataforma dos seus dispositivos. As opções são:  

        - **Administrador de dispositivos Android**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 e posterior**
        - **Windows 8.1 e posterior**
        - **Windows Phone 8.1**

    - **Perfil**: Selecione **restrições do dispositivo**.

        Para criar um perfil de restrições de dispositivos para dispositivos da Equipa Windows 10, como o Surface Hub, escolha as restrições do **Dispositivo (Windows 10 Team)**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política é **iOS/iPadOS: Bloquear a câmara nos dispositivos**.
    - **Descrição**: Insira uma descrição para a apólice. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Nas definições de **Configuração**, dependendo da plataforma que escolheu, as definições que pode configurar são diferentes. Escolha a sua plataforma para configurações detalhadas:

    - [Administrador de dispositivos Android](device-restrictions-android.md)
    - [Android Enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 e mais recente](device-restrictions-windows-10.md)
    - [Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. Selecione **Seguinte**.
9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para `US-NC IT Team` `JohnGlenn_ITDepartment`filtrar o perfil a grupos de TI específicos, tais como ou . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="next-steps"></a>Passos seguintes

Depois que o perfil é criado, está pronto para ser atribuído. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
