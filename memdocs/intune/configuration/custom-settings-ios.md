---
title: Adicione configurações personalizadas aos dispositivos iOS/iPadOS no Microsoft Intune - Azure Microsoft Docs
titleSuffix: ''
description: Exportar as definições de iOS e iPadOS a partir das ferramentas Apple Configurator ou Apple Profile Manager e, em seguida, importar estas definições para microsoft Intune. Estas definições podem criar, utilizar e controlar configurações personalizadas e funcionalidades em dispositivos iOS/iPadOS. Este perfil personalizado pode então ser atribuído ou distribuído para dispositivos iOS/iPadOS na sua organização para criar uma linha de base ou padrão.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/25/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ac931bf20140865e1185c4f401de0141273cdb3
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359416"
---
# <a name="use-custom-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Utilize configurações personalizadas para dispositivos iOS e iPadOS no Microsoft Intune

Utilizando o Microsoft Intune, pode adicionar ou criar configurações personalizadas para os seus dispositivos iOS/iPadOS utilizando "perfis personalizados". Os perfis personalizados são uma funcionalidade do Intune. Foram concebidos para adicionar definições e funcionalidades de dispositivos que não estão incorporadas Intune.

Ao utilizar dispositivos iOS/iPadOS, existem duas formas de obter configurações personalizadas em Intune:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Gestor de Perfis da Apple](https://support.apple.com/profile-manager)

Pode utilizar estas ferramentas para exportar definições para um perfil de configuração. Em Intune, importa este ficheiro e, em seguida, atribui o perfil aos utilizadores e dispositivos iOS/iPadOS. Uma vez atribuídas, as definições são distribuídas. Também criam uma linha de base ou padrão para iOS/iPadOS na sua organização.

Este artigo fornece algumas orientações sobre a utilização do Apple Configurator e do Apple Profile Manager, e descreve as propriedades que pode configurar.

## <a name="before-you-begin"></a>Antes de começar

[Criar o perfil.](custom-settings-configure.md)

## <a name="what-you-need-to-know"></a>O que tem de saber

- Ao utilizar o **Configurator Apple** para criar o perfil de configuração, certifique-se de que as definições que exporta são compatíveis com a versão iOS/iPadOS nos dispositivos. Para obter informações sobre como resolver definições incompatíveis, procure **Configuration Profile Reference** (Referência de Perfil de Configuração) e **Mobile Device Management Protocol Reference** (Referência do Protocolo de Gestão de Dispositivos Móveis) no site [Apple Developer](https://developer.apple.com/).

- Ao utilizar o **Gestor de Perfis da Apple**, certifique-se de que:

  - Ativa a [gestão de dispositivos móveis](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) no Gestor de Perfis.
  - Adicione [dispositivos iOS/iPadOS](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) no Profile Manager.
  - Depois de adicionar um dispositivo no Profile Manager, vá a **Under the Library** > **Devices** > selecione o seu dispositivo > **Definições**. Introduza as definições gerais para o dispositivo.

    Transfira e guarde este ficheiro. Irá introduzi-lo no perfil do Intune.

  - Certifique-se de que as definições que exporta do Apple Profile Manager são compatíveis com a versão iOS/iPadOS nos dispositivos. Para obter informações sobre como resolver definições incompatíveis, procure **Configuration Profile Reference** (Referência de Perfil de Configuração) e **Mobile Device Management Protocol Reference** (Referência do Protocolo de Gestão de Dispositivos Móveis) no site [Apple Developer](https://developer.apple.com/).

## <a name="custom-configuration-profile-settings"></a>Definições de perfil de configuração personalizada

- **Nome do perfil de configuração personalizado**: introduza um nome para o perfil. Este nome é apresentado no dispositivo e no estado do Intune.
- **Ficheiro de perfil de configuração**: navegue até ao perfil de configuração que criou com o Apple Configurator ou o Gestor de Perfis da Apple. O tamanho máximo `1000000` do ficheiro é bytes (pouco menos de 1MB). O ficheiro que importou é apresentado na área **Conteúdos do ficheiro**.

  Também pode adicionar fichas de dispositivo aos seus ficheiros de configuração personalizados. As fichas do dispositivo são usadas para adicionar informações específicas do dispositivo. Por exemplo, para mostrar o `{{serialnumber}}`número de série, insira . No dispositivo, o texto `123456789ABC`mostra semelhante ao , que é único em cada dispositivo. Ao introduzir variáveis, certifique-se de `{{ }}`que utiliza suportes encaracolados . [Os tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) de configuração da aplicação incluem uma lista de variáveis que podem ser usadas. Também pode `deviceid` utilizar ou qualquer outro valor específico do dispositivo.

  > [!NOTE]
  > As variáveis não são validadas na UI, e são sensíveis ao caso. Como resultado, pode ver perfis guardados com entrada incorreta. Por exemplo, se `{{DeviceID}}` introduzir `{{deviceid}}`em vez de , então a corda literal é mostrada em vez do ID único do dispositivo. Certifique-se de introduzir a informação correta.

## <a name="next-steps"></a>Passos seguintes

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md).

Saiba como [criar o perfil em dispositivos macOS](custom-settings-macos.md). 
