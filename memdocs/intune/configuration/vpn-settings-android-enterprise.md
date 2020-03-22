---
title: Utilize as definições VPN para Android Enterprise no Microsoft Intune - Azure Microsoft Docs
description: Consulte todas as definições para criar ligações VPN em dispositivos Android Enterprise no Microsoft Intune. Introduza o nome de ligação, endereço IP ou FQDN do servidor VPN, escolha como os utilizadores autenticam e escolha os tipos de ligação Citrix, SonicWall, Check Point Capsule e Pulse Secure.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8bc627e7b9efb68e8d5cb777b5d8e659b06cab92
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086811"
---
# <a name="android-enterprise-device-settings-to-configure-vpn-in-intune"></a>Configurações do dispositivo Android Enterprise para configurar VPN em Intune

Este artigo lista e descreve as diferentes definições de ligação VPN que pode controlar em dispositivos Android Enterprise. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para criar uma ligação VPN, escolha como a VPN autentica, selecione um tipo de servidor VPN e muito mais.

Como administrador intune, pode criar e atribuir configurações VPN aos dispositivos Android Enterprise. 

Para saber mais sobre perfis VPN em Intune, consulte [perfis VPN](vpn-settings-configure.md).

> [!NOTE]
> Para configurar vpN sempre ligado, precisa de criar um perfil VPN e também criar um perfil de restrições de [dispositivocom](device-restrictions-android-for-work.md#connectivity) a definição de VPN sempre ligado configurada.

## <a name="before-you-begin"></a>Antes de começar

[Crie um perfil](vpn-settings-configure.md)de configuração do dispositivo , e escolha **o Android Enterprise.**

## <a name="device-owner-only"></a>Proprietário do dispositivo apenas

- **Nome da ligação**: introduza um nome para esta ligação. Os utilizadores finais verão este nome quando procurarem no dispositivo as ligações VPN disponíveis. Por exemplo, introduza `Contoso VPN`.
- **Endereço IP ou FQDN**: introduza o endereço IP ou nome de domínio completamente qualificado (FQDN) do servidor VPN ao qual os dispositivos são ligados. Por exemplo, introduza **192.168.1.1** ou **vpn.contoso.com**.

  - **Método de autenticação**: selecione como os dispositivos serão autenticados no servidor VPN. As opções são:
  
    - **Certificados**: selecione um perfil de certificado SCEP ou PKCS existente para autenticar a ligação. [Configurar certificados](../protect/certificates-configure.md) lista os passos para criar um perfil de certificado.
    - **Nome de utilizador e palavra-passe**: Ao iniciar sessão no servidor VPN, os utilizadores finais são solicitados a introduzir o seu nome de utilizador e palavra-passe.

- **Tipo de ligação**: selecione o tipo de ligação VPN. As opções são:

  - **Cisco AnyConnect**
  - **Acesso F5**
  - **Pulse Secure**

## <a name="work-profile-only"></a>Apenas perfil de trabalho

- **Nome da ligação**: introduza um nome para esta ligação. Os utilizadores finais verão este nome quando procurarem no dispositivo as ligações VPN disponíveis. Por exemplo, introduza `Contoso VPN`.
- **Endereço IP ou FQDN**: introduza o endereço IP ou nome de domínio completamente qualificado (FQDN) do servidor VPN ao qual os dispositivos são ligados. Por exemplo, introduza **192.168.1.1** ou **vpn.contoso.com**.

  - **Método de autenticação**: selecione como os dispositivos serão autenticados no servidor VPN. As opções são:
  
    - **Certificados**: selecione um perfil de certificado SCEP ou PKCS existente para autenticar a ligação. [Configurar certificados](../protect/certificates-configure.md) lista os passos para criar um perfil de certificado.
    - **Nome de utilizador e palavra-passe**: Ao iniciar sessão no servidor VPN, os utilizadores finais são solicitados a introduzir o seu nome de utilizador e palavra-passe.

- **Tipo de ligação**: selecione o tipo de ligação VPN. As opções são:

  - **Cisco AnyConnect**
  - **Acesso F5**
  - **Pulse Secure**
  - **SonicWall Mobile Connect**
  - **Check Point Capsule VPN**

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode criar perfis VPN para [dispositivos Android](vpn-settings-android.md), [iOS/iPadOS,](vpn-settings-ios.md) [macOS,](vpn-settings-macos.md) [Windows 10 e posteriormente](vpn-settings-windows-10.md), [Windows 8.1](vpn-settings-windows-8-1.md)e [Windows Phone 8.1.](vpn-settings-windows-phone-8-1.md)
