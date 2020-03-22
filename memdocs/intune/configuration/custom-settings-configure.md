---
title: Utilizar definições personalizadas do dispositivo no Microsoft Intune – Azure | Microsoft Docs
description: Adicione ou crie um perfil para utilizar configurações personalizadas para windows Phone, Windows 8.1, Windows 10 e posteriormente, administrador de dispositivos Android, Android Enterprise, macOS e dispositivos iOS/iPadOS utilizando o Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083991"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Criar um perfil com definições personalizadas no Intune

O Microsoft Intune inclui várias definições incorporadas para controlar diferentes funcionalidades num dispositivo. Também pode criar perfis personalizados, que são criados semelhantes aos perfis incorporados. Os perfis personalizados são úteis se pretender utilizar definições e funcionalidades de dispositivos que não estão incorporadas no Intune. Estes perfis incluem funcionalidades e definições que pode controlar em dispositivos na sua organização. Por exemplo, pode criar um perfil personalizado que define a mesma funcionalidade para cada dispositivo iOS/iPadOS.

As definições personalizadas são configuradas de forma diferente para cada plataforma. Por exemplo, para controlar as funcionalidades em dispositivos Android e Windows, pode introduzir valores Open Mobile Alliance Uniform Resource Identifier (OMA-URI). Para dispositivos Apple, pode importar um ficheiro que criou no [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) ou no [Gestor de Perfis da Apple](https://support.apple.com/profile-manager).

Para obter mais informações sobre perfis de configuração, veja [O que são os perfis de dispositivos do Microsoft Intune?](device-profiles.md)

Este artigo mostra-lhe como criar um perfil personalizado para administrador de dispositivos Android, Android Enterprise, iOS/iPadOS, macOS e Windows. Também pode ver todas as definições disponíveis para as diferentes plataformas.

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política é **Windows 10: Perfil personalizado que permite o OMA-URI personalizado allowVPNOverCellular**.
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione a plataforma dos seus dispositivos. As opções são:

      - **Administrador de dispositivos Android**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 e posterior**
      - **Windows 8.1 e posterior**

    - **Tipo de perfil**: Selecione **Personalizado**.

4. As definições são diferentes para cada plataforma. Para ver as definições de uma plataforma específica, selecione a sua plataforma:

    - [Administrador de dispositivos Android](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. Quando terminar, selecione **Criar perfil** > **Criar**.

O perfil é criado e mostrado na lista de perfis **(configuração** do dispositivo > **Perfis).**

## <a name="next-steps"></a>Próximos passos

Depois que o perfil é criado, está pronto para ser atribuído. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).
