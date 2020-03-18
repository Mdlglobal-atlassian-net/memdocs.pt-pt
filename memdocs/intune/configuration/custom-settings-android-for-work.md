---
title: Adicionar definições personalizadas a dispositivos Android Enterprise no Microsoft Intune – Azure | Microsoft Docs
description: Adicionar ou criar um perfil personalizado para dispositivos Android Enterprise, para criar definições personalizadas no Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4724d6e5-05e5-496c-9af3-b74f083141f8
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 827b5eb8b65aa59212b9ef990def3c5f191baf7c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323893"
---
# <a name="use-custom-settings-for-android-enterprise-devices-in-microsoft-intune"></a>Utilizar definições personalizadas para dispositivos Android Enterprise no Microsoft Intune

Utilizando o Microsoft Intune, pode adicionar ou criar configurações personalizadas para os seus dispositivos Android Enterprise Work Profile utilizando um "perfil personalizado". Os perfis personalizados são uma funcionalidade do Intune. Foram concebidos para adicionar definições e funcionalidades de dispositivos que não estão incorporadas Intune.

Os perfis personalizados do Android Enterprise utilizam as definições Open Mobile Alliance Uniform Resource Identifier (OMA-URI) para controlar funcionalidades em dispositivos Android Enterprise. Estas definições são normalmente utilizadas por fabricantes de dispositivos móveis para controlar essas funcionalidades.

Intune suporta o seguinte número limitado de perfis personalizados Android Enterprise:

- ./Fornecedor/MSFT/WiFi/Profile/SSID/Settings: [Criar um perfil Wi-Fi com uma chave pré-partilhada](wi-fi-profile-shared-key.md) tem alguns exemplos.
- ./Fornecedor/MSFT/VPN/Profile/Name/PackageList: [Criar um perfil VPN por aplicação](android-pulse-secure-per-app-vpn.md) tem alguns exemplos.
- ./Fornecedor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste: Consulte o [exemplo](#example) neste artigo. Esta definição também está disponível na interface do utilizador. Para mais informações, consulte [as definições do dispositivo Android Enterprise para permitir ou restringir funcionalidades.](device-restrictions-android-for-work.md)

Se precisar de configurações adicionais, consulte [OEMConfig para Android Enterprise](android-oem-configuration-overview.md).

Este artigo mostra-lhe como criar um perfil personalizado para dispositivos Android Enterprise. Fornece também um exemplo de um perfil personalizado que bloqueia a funcionalidade de copiar e colar.

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes definições:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil personalizado Android Enterprise.**
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **Android Enterprise**.
    - **Tipo de perfil**: Selecione **Personalizado**.

4. Em **Definições OMA-URI Personalizadas**, selecione **Adicionar**. Introduza as seguintes definições:

    - **Nome**: introduza um nome exclusivo para a definição OMA-URI, para poder encontrá-la facilmente.
    - **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
    - **OMA-URI**: introduza o OMA-URI que quer utilizar como uma definição.
    - Tipo de **dados:** Selecione o tipo de dados que utilizará para esta definição OMA-URI. As opções são:

      - Cadeia
      - Cadeia (ficheiro XML)
      - Data e Hora
      - Número inteiro
      - Vírgula flutuante
      - Booleano
      - Base64 (ficheiro)

    - **Valor**: introduza o valor de dados que pretende associar à definição OMA-URI que introduziu. O valor depende do tipo de dados que selecionou. Por exemplo, se selecionar **Data e Hora,** selecione o valor de um apanhador de datas.

    Depois de adicionar algumas definições, pode selecionar **Exportar**. A opção **Exportar** cria uma lista de todos os valores que adicionou num ficheiro de valores separados por vírgulas (.csv).

5. Selecione **OK** para guardar as alterações. Continue a adicionar mais definições conforme necessário.
6. Quando terminar, selecione **OK** > **Criar** para criar o perfil Intune. Quando estiver concluído, o seu perfil é mostrado na lista de perfis de configuração - **Configuração.**

## <a name="example"></a>Exemplo

Neste exemplo, irá criar um perfil personalizado que restringe as ações de copiar e colar entre aplicações de trabalho e pessoais em dispositivos Android Enterprise.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes definições:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, introduza o perfil personalizado de colar de **cópia sinuoso**do bloco android .
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **Android Enterprise**.
    - **Tipo de perfil**: Selecione **Personalizado**.

4. Em **Definições OMA-URI Personalizadas**, selecione **Adicionar**. Introduza as seguintes definições:

    - **Nome**: introduza algo como `Block copy and paste`.
    - **Descrição**: introduza algo como `Blocks copy/paste between work and personal apps`.
    - **OMA-URI**: introduza `./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste`.
    - **Tipo**de dados : Selecione **Boolean para** que o valor para este OMA-URI seja **verdadeiro** ou **falso**.
    - **Valor**: Selecione **True**.

5. Depois de introduzir as definições, o seu ambiente deverá ter um aspeto semelhante à imagem seguinte:

    ![Bloquear a funcionalidade Copiar e Colar para perfis de trabalho do Android.](./media/custom-settings-android-for-work/custom-policy-afw-copy-paste.png)

Ao atribuir este perfil aos dispositivos Android Enterprise que gere, a funcionalidade Copiar e Colar é bloqueada entre aplicações nos perfis de trabalho e pessoais.

## <a name="next-steps"></a>Próximos passos

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Criar um [perfil personalizado em dispositivos Android.](custom-settings-android.md)
