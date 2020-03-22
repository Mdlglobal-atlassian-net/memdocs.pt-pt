---
title: Adicione as definições vpN aos dispositivos no Microsoft Intune - Azure  Microsoft Docs
description: Para administrador de dispositivos Android, Android Enterprise, iOS, iPadOS, macOS e dispositivos Windows, utilize configurações incorporadas para criar ligações de rede privada virtual (VPN) no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64356bf9be0c2c439c1f4fc296a9728a7937b001
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086565"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Criar perfis VPN para ligar aos servidores VPN em Intune

As redes privadas virtuais (VPNs) dão aos utilizadores acesso remoto seguro à sua rede de organização. Os dispositivos utilizam um perfil de ligação VPN para iniciar uma ligação com o servidor VPN. **Os perfis VPN** no Microsoft Intune atribuem definições de VPN a utilizadores e dispositivos na sua organização, para que possam ligar-se de forma fácil e segura à sua rede organizacional.

Por exemplo, pretende configurar todos os dispositivos iOS/iPadOS com as definições necessárias para se ligar a uma partilha de ficheiros na rede da organização. Cria um perfil VPN que inclui estas definições. Em seguida, atribui este perfil a todos os utilizadores que possuam dispositivos iOS/iPadOS. Os utilizadores veem a ligação VPN na lista de redes disponíveis e podem ligar-se sem esforço.

> [!NOTE]
> Pode utilizar políticas de [configuração personalizadas Intune](custom-settings-configure.md) para criar perfis VPN para as seguintes plataformas:
>
> * Android 4 e posterior
> * Dispositivos inscritos com Windows 8.1 e posterior
> * Windows Phone 8.1 e posterior
> * Computadores inscritos com o Windows 10
> * Windows 10 Mobile
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>Tipos de ligação VPN

Pode criar perfis VPN com os seguintes tipos de ligação:

- Automático
  - Windows 10

- Check Point Capsule VPN
  - Administrador de dispositivos Android
  - Perfis de trabalho android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Wnodows Phone 8.1

- Cisco AnyConnect
  - Administrador de dispositivos Android
  - Perfis de trabalho android Enterprise
  - Dono de dispositivo Android Enterprise (totalmente gerido)
  - iOS/iPadOS
  - macOS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Administrador de dispositivos Android
  - Perfis de trabalho Android Enterprise: Use a política de [configuração de aplicativos](../apps/app-configuration-policies-use-android.md)
  - Dono de dispositivo Android Enterprise (totalmente gerido): Utilize a política de configuração de [aplicações](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- VPN Personalizada
  - iOS/iPadOS
  - macOS

  Crie perfis VPN personalizados utilizando definições URI em [Criar um perfil com configurações personalizadas](custom-settings-configure.md).

- F5 Access
  - Administrador de dispositivos Android
  - Perfis de trabalho android Enterprise
  - Dono de dispositivo Android Enterprise (totalmente gerido)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Wnodows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Perfis de trabalho Android Enterprise: Use a política de [configuração de aplicativos](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Administrador de dispositivos Android
  - Perfis de trabalho android Enterprise
  - Dono de dispositivo Android Enterprise (totalmente gerido)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Wnodows Phone 8.1

- SonicWall Mobile Connect
  - Administrador de dispositivos Android
  - Perfis de trabalho android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Wnodows Phone 8.1

- Zscaler
  - Perfis de trabalho Android Enterprise: Use a política de [configuração de aplicativos](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS

> [!IMPORTANT]
> Para poder utilizar os perfis VPN atribuídos a um dispositivo, tem de instalar a aplicação VPN aplicável ao perfil. Para ajudá-lo a atribuir a app usando Intune, veja [o que é a gestão de aplicações no Microsoft Intune?](../apps/app-management.md)  

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Escolha a plataforma dos seus dispositivos. As opções são:
      - **Administrador de dispositivos Android**
      - **Android Enterprise** > **Dispositivo apenas proprietário**
      - **Android Enterprise** > **Work apenas perfil**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 e posterior**
      - **Windows 8.1 e posterior**
      - **Windows Phone 8.1**
    - **Perfil**: Selecione **VPN**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil VPN para toda a empresa**.
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.
7. Nas definições de **Configuração**, dependendo da plataforma que escolheu, as definições que pode configurar são diferentes. Selecione a sua plataforma para configurações detalhadas:

    - [Administrador de dispositivos Android](vpn-settings-android.md)
    - [Android Enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (incluindo Windows Holographic for Business)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. Selecione **Seguinte**.
9. Nas **etiquetas scope** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como `US-NC IT Team` ou `JohnGlenn_ITDepartment`. Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione o utilizador ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="secure-your-vpn-profiles"></a>Proteja os seus perfis VPN

Os perfis da VPN podem utilizar vários tipos de ligação e protocolos diferentes de fabricantes diferentes. Estas ligações são normalmente fixadas através dos seguintes métodos.

### <a name="certificates"></a>Certificados

Quando cria o perfil da VPN, pode escolher um perfil de certificado SCEP ou PKCS que tenha criado anteriormente no Intune. Este perfil é conhecido como certificado de identidade. É usado para autenticar contra um perfil de certificado fidedigno (ou *certificado raiz)* que cria para permitir a ligação do dispositivo do utilizador. O certificado fidedigno é atribuído ao computador que irá autenticar a ligação VPN (normalmente, o servidor VPN).

Para obter mais informações sobre como criar e utilizar perfis de certificado no Intune, veja [Como configurar certificados com o Microsoft Intune](../protect/certificates-configure.md).

### <a name="user-name-and-password"></a>Nome de utilizador e palavra-passe

O utilizador é autenticado no servidor VPN ao fornecer um nome de utilizador e uma palavra-passe.

## <a name="next-steps"></a>Próximos passos

O perfil não estará ativo assim que for criado. Em seguida, [atribua o perfil](device-profile-assign.md) a alguns dispositivos e [monitorize o seu estado](device-profile-monitor.md).

Também pode criar e utilizar VPNs por aplicação em [dispositivos Android/Android Enterprise](android-pulse-secure-per-app-vpn.md) e [iOS/iPadOS.](vpn-setting-configure-per-app.md)
