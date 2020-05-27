---
title: Perfil VPN personalizado por app para Android no Microsoft Intune - Azure Microsoft Docs
description: Saiba como criar um perfil VPN por aplicação para dispositivos de administrador de dispositivos Android geridos pelo Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
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
ms.openlocfilehash: 367ac927650ebf08c245b1ff554ad01db3bf3792
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990158"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Utilizar um perfil personalizado do Microsoft Intune para criar um perfil VPN por aplicação para dispositivos Android

Pode criar um perfil VPN por aplicação para dispositivos Android 5.0 e posteriores geridos pelo Intune. Em primeiro lugar, crie um perfil VPN que utilize o tipo de ligação Pulse Secure ou Citrix. Em seguida, crie uma política de configuração personalizada que associe o perfil de VPN a aplicações específicas.

> [!NOTE]
> Para utilizar VPN por aplicação em dispositivos Android Enterprise, também pode utilizar estes passos. Mas, recomenda-se usar uma política de configuração de [aplicações](../apps/app-configuration-policies-use-android.md) para a sua aplicação de cliente VPN.

Depois de atribuir a política ao seu dispositivo Android ou grupos de utilizadores, os utilizadores devem iniciar o cliente de VPN do Pulse Secure ou Citrix. Em seguida, o cliente VPN permite que apenas o tráfego das aplicações especificadas utilize a ligação VPN aberta.

> [!NOTE]
>
> Apenas os tipos de ligação Pulse Secure e Citrix são suportados para este perfil.

## <a name="step-1-create-a-vpn-profile"></a>Passo 1: criar um perfil de VPN

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **administrador de dispositivos Android**.
    - **Perfil**: Selecione **VPN**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é administrador de **dispositivo Android por perfil VPN para toda**a empresa .
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.
7. Nas definições de **Configuração,** configure as definições que deseja no perfil:

    - [Definições VPN para dispositivos de administrador](vpn-settings-android.md)de dispositivos Android .

    Tome nota do valor do Nome de **Ligação** que introduz ao criar o perfil VPN. Este nome é necessário no próximo passo. Neste exemplo, o nome da ligação é **MyAppVpnProfile**.

8. Selecione **Next**, e continue a criar o seu perfil. Para mais informações, consulte [Criar um perfil VPN](vpn-settings-configure.md#create-the-profile).

## <a name="step-2-create-a-custom-configuration-policy"></a>Passo 2: criar uma política de configuração personalizada

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil personalizado. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil VPN Android Personalizado OMA-URI para toda**a empresa .
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **administrador de dispositivos Android**.
    - **Tipo de perfil**: Selecione **Personalizado**.

4. Escolha **configurar definições**  >  **Configure**.
5. No painel **Definições OMA-URI personalizadas**, selecione **Adicionar**.
    - **Nome**: Introduza um nome para a sua definição.
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **OMA-URI**: Introduza, onde o nome é o nome de `./Vendor/MSFT/VPN/Profile/*Name*/PackageList` ligação que observou no passo 1. *Name* Neste exemplo, a corda é `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList` .
    - **Tipo de dados**: Enter **String**.
    - **Valor**: Introduza uma lista de pacotes separados pelo ponto e vírgula para associar ao perfil. Por exemplo, se quiser que o Excel e o navegador Google Chrome utilizem a ligação VPN, introduza `com.microsoft.office.excel;com.android.chrome` .

    > [!div class="mx-imgBorder"]
    >![Exemplo Android administrador de dispositivos por app VPN política personalizada](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Definir a lista de aplicações como lista de bloqueados ou lista de permitidos (opcional)

Utilize o valor **BLACKLIST** para introduzir uma lista de aplicações que *não podem* utilizar a ligação VPN. Todas as outras aplicações são ligadas através da VPN. Ou, use o valor **WHITELIST** para introduzir uma lista de aplicações que *podem* usar a ligação VPN. As aplicações que não estão na lista não se ligam através da VPN.

1. No painel **Definições OMA-URI personalizadas**, selecione **Adicionar**.
2. Introduza um nome para a definição.
3. Em **OMA-URI,** insira, `./Vendor/MSFT/VPN/Profile/*Name*/Mode` onde o *nome* é o nome de perfil VPN que observou no Passo 1. No nosso exemplo, a corda `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode` é.
4. No **tipo de Dados,** introduza **string**.
5. Em **Valor**, introduza **BLACKLIST** ou **WHITELIST**.

## <a name="step-3-assign-both-policies"></a>Passo 3: atribuir ambas as políticas

[Atribuir os perfis do dispositivo](device-profile-assign.md) aos utilizadores ou dispositivos necessários.

## <a name="next-steps"></a>Passos seguintes

- Para obter uma lista de todas as definições vpn do administrador do dispositivo Android, consulte as definições do [dispositivo Android para configurar VPN](vpn-settings-android.md).
- Para saber mais sobre as definições de VPN e Intune, consulte [configurar as definições de VPN no Microsoft Intune](vpn-settings-configure.md).
