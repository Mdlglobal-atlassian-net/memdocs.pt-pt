---
title: Personalizar um perfil VPN por aplicação para Android
titleSuffix: Microsoft Intune
description: Saiba como criar um perfil VPN por aplicação para dispositivos Android geridos pelo Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9fbcf60d3707097a323a05bf36d2cfe3902d5214
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325609"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Utilizar um perfil personalizado do Microsoft Intune para criar um perfil VPN por aplicação para dispositivos Android

Pode criar um perfil VPN por aplicação para dispositivos Android 5.0 e posteriores geridos pelo Intune. Em primeiro lugar, crie um perfil VPN que utilize o tipo de ligação Pulse Secure ou Citrix. Em seguida, crie uma política de configuração personalizada que associe o perfil de VPN a aplicações específicas.

> [!NOTE]
> Para utilizar VPN por aplicação em dispositivos Android Enterprise, também pode utilizar estes passos. Mas, recomenda-se usar uma política de configuração de [aplicações](../apps/app-configuration-policies-use-android.md) para a sua aplicação de cliente VPN.

Depois de atribuir a política ao seu dispositivo Android ou grupos de utilizadores, os utilizadores devem iniciar o cliente de VPN do Pulse Secure ou Citrix. O cliente de VPN permite apenas tráfego das aplicações especificadas para utilizar a ligação VPN aberta.

> [!NOTE]
>
> Apenas os tipos de ligação Pulse Secure e Citrix são suportados para este perfil.

## <a name="step-1-create-a-vpn-profile"></a>Passo 1: criar um perfil de VPN

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil VPN Android por app para toda**a empresa .
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **Android**.
    - **Tipo de perfil**: Selecione **VPN**.

4. Escolha **Definições** > **Configurar**. Em seguida, configure o perfil VPN. Para mais informações, consulte [como configurar as definições](vpn-settings-configure.md) de VPN e [configurações intune VPN para dispositivos Android](vpn-settings-android.md).

Tome nota do valor **Nome da Ligação** que especificar ao criar o perfil de VPN. Esse nome será necessário no próximo passo. Por exemplo, **MyAppVpnProfile**.

## <a name="step-2-create-a-custom-configuration-policy"></a>Passo 2: criar uma política de configuração personalizada

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil personalizado. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil VPN Android Personalizado OMA-URI para toda**a empresa .
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **Android**.
    - **Tipo de perfil**: Selecione **Personalizado**.

4. Escolha **Definições** > **Configurar**.
5. No painel **Definições OMA-URI Personalizadas**, selecione **Adicionar**.
    - **Nome**: Introduza um nome para a sua definição.
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **OMA-URI**: Introduza `./Vendor/MSFT/VPN/Profile/*Name*/PackageList`, onde o *nome* é o nome de ligação que observou no passo 1. Neste exemplo, a corda é `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`.
    - **Tipo de dados**: Enter **String**.
    - **Valor**: Introduza uma lista de pacotes separados pelo ponto e vírgula para associar ao perfil. Por exemplo, se quiser que o Excel e o navegador Google Chrome utilizem a ligação VPN, introduza `com.microsoft.office.excel;com.android.chrome`.

![Exemplo de política personalizada de VPN por aplicação Android](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Definir a lista de aplicações como lista de bloqueados ou lista de permitidos (opcional)

Utilize o valor **BLACKLIST** para introduzir uma lista de aplicações que *não podem* utilizar a ligação VPN. Todas as outras aplicações são ligadas através da VPN. Ou, use o valor **WHITELIST** para introduzir uma lista de aplicações que *podem* usar a ligação VPN. As aplicações que não estão na lista não se ligam através da VPN.

1. No painel **Definições OMA-URI Personalizadas**, selecione **Adicionar**.
2. Introduza um nome para a definição.
3. Em **OMA-URI,** insira `./Vendor/MSFT/VPN/Profile/*Name*/Mode`, onde o *nome* é o nome de perfil VPN que observou no Passo 1. No nosso exemplo, a corda é `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`.
4. No **tipo de Dados,** introduza **string**.
5. Em **Valor**, introduza **BLACKLIST** ou **WHITELIST**.

## <a name="step-3-assign-both-policies"></a>Passo 3: atribuir ambas as políticas

[Atribuir os perfis do dispositivo](device-profile-assign.md) aos utilizadores ou dispositivos necessários.
