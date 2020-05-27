---
title: Utilizar definições personalizadas do dispositivo no Microsoft Intune – Azure | Microsoft Docs
description: Adicione ou crie um perfil para utilizar configurações personalizadas para windows Phone, Windows 8.1, Windows 10 e posteriormente, administrador de dispositivos Android, Android Enterprise, macOS e dispositivos iOS/iPadOS utilizando o Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ddbb82d3cd5c86ff32917013edd4f16b303678fe
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990091"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Criar um perfil com definições personalizadas no Intune

O Microsoft Intune inclui várias definições incorporadas para controlar diferentes funcionalidades num dispositivo. Também pode criar perfis personalizados, que são criados semelhantes aos perfis incorporados. Os perfis personalizados são úteis se pretender utilizar definições e funcionalidades de dispositivos que não estão incorporadas no Intune. Estes perfis incluem funcionalidades e definições que pode controlar em dispositivos na sua organização. Por exemplo, pode criar um perfil personalizado que define a mesma funcionalidade para cada dispositivo iOS/iPadOS.

As definições personalizadas são configuradas de forma diferente para cada plataforma. Por exemplo, para controlar as funcionalidades em dispositivos Android e Windows, pode introduzir valores Open Mobile Alliance Uniform Resource Identifier (OMA-URI). Para dispositivos Apple, pode importar um ficheiro que criou no [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) ou no [Gestor de Perfis da Apple](https://support.apple.com/profile-manager).

Para obter mais informações sobre perfis de configuração, veja [O que são os perfis de dispositivos do Microsoft Intune?](device-profiles.md)

Este artigo mostra-lhe como criar um perfil personalizado para administrador de dispositivos Android, Android Enterprise, iOS/iPadOS, macOS e Windows. Também pode ver todas as definições disponíveis para as diferentes plataformas.

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Escolha a plataforma dos seus dispositivos. As opções são:  

        - **Android device administrator (Administrador de dispositivos Android)**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 e posterior**
        - **Windows Phone 8.1**

    - **Perfil**: Selecione **Personalizado**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política é **Windows 10: Perfil personalizado que permite o OMA-URI personalizado allowVPNOverCellular**.
    - **Descrição**: Insira uma descrição para a apólice. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Nas definições de **Configuração**, dependendo da plataforma que escolheu, as definições que pode configurar são diferentes. Escolha a sua plataforma para configurações detalhadas:

    - [Android device administrator (Administrador de dispositivos Android)](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. Selecione **Seguinte**.
9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como ou `US-NC IT Team` `JohnGlenn_ITDepartment` . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="example"></a>Exemplo

No seguinte exemplo, a definição **Conectividade/PermitirVPNAtravésDeRedeMóvel** está ativada. Esta definição permite que um dispositivo com o Windows 10 abra uma ligação VPN através de uma rede móvel.

> [!div class="mx-imgBorder"]
> ![Exemplo de uma política personalizada que contém definições VPN em Intune e Endpoint Manager](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Passos seguintes

O perfil é criado, mas pode ainda não estar a fazer nada. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).
