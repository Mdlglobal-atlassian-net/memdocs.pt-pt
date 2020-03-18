---
title: Adicione as definições vpN aos dispositivos no Microsoft Intune - Azure  Microsoft Docs
description: Para dispositivos Android, Android Enterprise, iOS, iPadOS, macOS e Windows, utilize configurações incorporadas para criar ligações de rede privada virtual (VPN) no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 453ce45c40370641f37527501a577876c9867acd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333025"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Criar perfis VPN para ligar aos servidores VPN em Intune



As redes privadas virtuais (VPNs) dão aos seus utilizadores acesso remoto seguro à sua rede de organização. Os dispositivos utilizam um perfil de ligação VPN para iniciar uma ligação com o servidor VPN. **Os perfis VPN** no Microsoft Intune atribuem definições de VPN a utilizadores e dispositivos na sua organização, para que possam ligar-se de forma fácil e segura à sua rede organizacional.

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

|Tipo de ligação|Platform|
|-|-|
|Automático|Windows 10|
|Check Point Capsule VPN|- Android<br/>- Perfis de trabalho android Enterprise<br/>- iOS/iPadOS<br/>- macOS<br/>- Windows 10<br/>- Windows 8.1<br/>- Windows Phone 8.1|
|Cisco AnyConnect|- Android<br/>- Perfis de trabalho android Enterprise<br/>- Proprietário de dispositivos Android Enterprise (totalmente gerido)<br/>- iOS/iPadOS<br/>- macOS|
|Cisco (IPSec)|iOS/iPadOS|
|Citrix SSO|- Android<br/>- Perfis de trabalho Android Enterprise: Utilize a política de [configuração de aplicativos](../apps/app-configuration-policies-use-android.md)<br/>- Proprietário de dispositivos Android Enterprise (totalmente gerido): Utilize a política de configuração de [aplicações](../apps/app-configuration-policies-use-android.md)<br/>- iOS/iPadOS<br/>- Windows 10|
|VPN Personalizada|- iOS/iPadOS<br/>- macOS|
|F5 Access|- Android<br/>- Perfis de trabalho android Enterprise<br/>- Proprietário de dispositivos Android Enterprise (totalmente gerido)<br/>- iOS/iPadOS<br/>- macOS<br/>- Windows 10<br/>- Windows 8.1<br/>- Windows Phone 8.1|
|IKEv2| - iOS/iPadOS<br/>- Windows 10|
|L2TP|Windows 10|
|Palo Alto Networks GlobalProtect|- Perfis de trabalho Android Enterprise: Utilize a política de [configuração de aplicativos](../apps/app-configuration-policies-use-android.md)<br/>- iOS/iPadOS<br/>- Windows 10|
|PPTP|Windows 10|
|Pulse Secure|- Android<br/>- Perfis de trabalho android Enterprise<br/>- Proprietário de dispositivos Android Enterprise (totalmente gerido)<br/>- iOS/iPadOS<br/>- macOS<br/>- Windows 10<br/>- Windows 8.1<br/>- Windows Phone 8.1|
|SonicWall Mobile Connect|- Android<br/>- Perfis de trabalho android Enterprise<br/>- iOS/iPadOS<br/>- macOS<br/>- Windows 10<br/>- Windows 8.1<br/>- Windows Phone 8.1|
|Zscaler|- Perfis de trabalho Android Enterprise: Utilize a política de [configuração de aplicativos](../apps/app-configuration-policies-use-android.md)<br/>- iOS/iPadOS|

> [!IMPORTANT]
> Para poder utilizar os perfis VPN atribuídos a um dispositivo, tem de instalar a aplicação VPN aplicável ao perfil. Pode utilizar as informações do artigo [O que é a gestão de aplicações do Microsoft Intune?](../apps/app-management.md) para ajudá-lo a atribuir a aplicação através do Intune.  

Saiba como criar perfis VPN personalizados com definições URI em [Criar um perfil com definições personalizadas](custom-settings-configure.md).

## <a name="create-a-device-profile"></a>Criar um perfil de dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil VPN para toda a empresa**.
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Escolha a plataforma dos seus dispositivos. As opções são:

      - **Android**
      - **Android Enterprise** > **Dispositivo apenas proprietário**
      - **Android Enterprise** > **Work apenas perfil**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows Phone 8.1**
      - **Windows 8.1 e posterior**
      - **Windows 10 e posterior**

    - **Tipo de perfil**: Selecione **VPN**.

4. Consoante a plataforma que escolheu, as definições que pode configurar variam. Consulte os seguintes artigos para obter definições detalhadas em cada plataforma:

    - [Definições do Android](vpn-settings-android.md)
    - [Configurações do Android Enterprise](vpn-settings-android-enterprise.md)
    - [definições iOS/iPadOS](vpn-settings-ios.md)
    - [Definições do macOS](vpn-settings-macos.md)
    - [Definições do Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)
    - [Definições do Windows 8.1](vpn-settings-windows-8-1.md)
    - [Definições do Windows 10](vpn-settings-windows-10.md) (incluindo o Windows Holographic for Business)

5. Assim que terminar, selecione **OK** > **Criar** para guardar as alterações.

O perfil é criado e apresentado na lista de perfis. Para atribuir este perfil a grupos, veja [atribuir perfis de dispositivo](device-profile-assign.md).

## <a name="secure-your-vpn-profiles"></a>Proteja os seus perfis VPN

Os perfis da VPN podem utilizar vários tipos de ligação e protocolos diferentes de fabricantes diferentes. Estas ligações são normalmente fixadas através dos seguintes métodos.

### <a name="certificates"></a>Certificados

Quando cria o perfil da VPN, pode escolher um perfil de certificado SCEP ou PKCS que tenha criado anteriormente no Intune. Este perfil é conhecido como certificado de identidade. É utilizado para autenticação em relação a um certificado fidedigno (ou um *certificado de raiz*) que deve criar para permitir que o dispositivo do utilizador estabeleça ligação. O certificado fidedigno é atribuído ao computador que irá autenticar a ligação VPN (normalmente, o servidor VPN).

Para obter mais informações sobre como criar e utilizar perfis de certificado no Intune, veja [Como configurar certificados com o Microsoft Intune](../protect/certificates-configure.md).

### <a name="user-name-and-password"></a>Nome de utilizador e palavra-passe

O utilizador é autenticado no servidor VPN ao fornecer um nome de utilizador e uma palavra-passe.

## <a name="next-steps"></a>Próximos passos

O perfil não estará ativo assim que for criado. Em seguida, [atribua o perfil](device-profile-assign.md) a alguns dispositivos.

Também pode criar e utilizar VPNs por aplicação em dispositivos [Android](android-pulse-secure-per-app-vpn.md) e [iOS/iPadOS.](vpn-setting-configure-per-app.md)