---
title: O que é a inscrição de dispositivos do Microsoft Intune
titleSuffix: Microsoft Intune
description: Conheça as inscrições para dispositivos iOS/iPadOS, Android e Windows.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 4/24/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d907aaac6c37cbe7cad71e850fbc44322c93841
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986387"
---
# <a name="what-is-device-enrollment"></a>O que é a inscrição de dispositivos?
[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune permite-lhe gerir os dispositivos e aplicações da sua força de trabalho e como acedem aos dados da sua empresa. Para utilizar esta gestão de dispositivos móveis (MDM), deve primeiro inscrever os dispositivos no serviço Intune. Quando um dispositivo está matriculado, é emitido um certificado de MDM. Este certificado é utilizado para comunicar com o serviço Intune.

Como pode ver nas seguintes tabelas, existem vários métodos para inscrever os dispositivos da sua força de trabalho. Cada método depende da propriedade do dispositivo (pessoal ou empresarial), do tipo de dispositivo (iOS, Windows, Android) e dos requisitos de gestão (reposições, afinidade, bloqueio).

Por predefinição, os dispositivos para todas as plataformas têm permissão para serem inscritos no Intune. No entanto, pode [restringir os dispositivos por plataforma](enrollment-restrictions-set.md#create-a-device-type-restriction).

## <a name="iosipados-enrollment-methods"></a>métodos de inscrição iOS/iPadOS

| **Método** | **Reposição obrigatória** | [**Afinidade de Utilizador**](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) | **Bloqueado** | **Detalhes** |
|:---:|:---:|:---:|:---:|:---:|
| | Os dispositivos são apagados durante a inscrição. | Associa cada dispositivo a um utilizador.| Se sim, os utilizadores não podem desinscrever dispositivos. | |
|**[BYOD](#bring-your-own-device)** | No| Yes | No | [Mais informações](apple-mdm-push-certificate-get.md)|
|**[DEM](#device-enrollment-manager)**| Não |Não |Não | [Mais informações](device-enrollment-manager-enroll.md)|
|**[ADE](#apple-automated-device-enrollment)**| Yes | Opcional | Opcional|[Mais informações](device-enrollment-program-enroll-ios.md)|
|**[USB-SA](#usb-sa)**| Yes | Opcional | No| [Mais informações](apple-configurator-enroll-ios.md)|
|**[USB-Direct](#usb-direct)**| Não | Não | Não|[Mais informações](apple-configurator-enroll-ios.md)|

## <a name="macos-enrollment-methods"></a>Métodos de inscrição do macOS
| **Método** |  **Reposição obrigatória** |  **Afinidade de Utilizador** | **Bloqueado** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#bring-your-own-device)** | No| Yes | No | [Mais informações](macos-enroll.md)|
|**[DEM](#device-enrollment-manager)**| Não |Não |Não  | [Mais informações](device-enrollment-manager-enroll.md)|
|**[ADE](#apple-automated-device-enrollment)**| Yes | Opcional | Opcional|[Mais informações](device-enrollment-program-enroll-macos.md)|

## <a name="windows-enrollment-methods"></a>Métodos de inscrição do Windows

| **Método** | **Reposição obrigatória** | **Afinidade de Utilizador** | **Bloqueado** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#bring-your-own-device)** | No | Yes | No | [Mais informações](windows-enroll.md)|
|**[DEM](#device-enrollment-manager)**| Não |Não |Não |[Mais informações](device-enrollment-manager-enroll.md)|
|**Inscrição automática** | No |Yes |No | [Mais informações](windows-enroll.md#enable-windows-10-automatic-enrollment)|
|**Piloto automático** |Sim |Sim |No | [Mais informações](enrollment-autopilot.md)
|**Inscrição em massa** |Não |Não |Não | [Mais informações](windows-bulk-enroll.md) |
|**Cogestão** |No |Yes |No | [Mais informações](https://docs.microsoft.com/configmgr/core/clients/manage/co-management-overview)
|**GPO** |No |Sim |No | [Mais informações](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)

## <a name="android-enrollment-methods"></a>Métodos de inscrição do Android

| **Pessoal** | **Métodos de Inscrição** | **Reposição obrigatória** | **Afinidade de Utilizador** | **Bloqueado** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**Admin de dispositivos Android**|**Utilizador iniciado via Portal da Empresa** | No | Sim | No | [Mais informações](https://docs.microsoft.com/mem/intune/user-help/enroll-device-android-company-portal)|
|**Perfil de trabalho da empresa android**|**Utilizador iniciado via Portal da Empresa**| No | Sim | No | [Mais informações](android-work-profile-enroll.md)|


| **Empresarial** | **Métodos de Inscrição** | **Reposição obrigatória** | **Afinidade de Utilizador** | **Bloqueado** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**Admin de dispositivos Android**|**[DEM](#device-enrollment-manager) iniciado via Portal da Empresa**| Não | Não | Não |[Mais informações](device-enrollment-manager-enroll.md)|
|**Admin de dispositivos Android**|**(IMEI ou SN pré-declarados) Utilizador iniciado via Portal da Empresa**| No | Sim | No | [Mais informações](corporate-identifiers-add.md)|
|**Administrador de dispositivos Android com extensões de mobilidade da zebra**|**Utilizador ou [DEM](#device-enrollment-manager) iniciado via Portal da Empresa**| No | Sim, se o utilizador iniciado, não se o [DEM](#device-enrollment-manager) iniciado | No | [Mais informações](../configuration/android-zebra-mx-overview.md)|
|**Android Enterprise Dedicado**|**NFC, Token, Código QR, Zero Touch**| Sim | No | Configurável através da política | [Mais informações](android-kiosk-enroll.md)|
|**Android Enterprise totalmente gerido**|**NFC, Token, Código QR, Zero Touch**| Yes | Sim, o que é que se está Não se [o DEM](device-enrollment.md#device-enrollment-manager) iniciado | Configurável através da política | [Mais informações](android-dedicated-devices-fully-managed-enroll.md)|


## <a name="bring-your-own-device"></a>Traga o seu próprio dispositivo
Os seus próprios dispositivos (BYOD) incluem telemóveis, tablets e computadores de propriedade pessoal. Os utilizadores instalam e executam a aplicação Portal da Empresa para inscrever BYODs. Este programa permite aos utilizadores aceder aos recursos da empresa tais como o e-mail.

## <a name="corporate-owned-device"></a>Dispositivo pertencentes à empresa
[Os dispositivos corporativos (COD)](corporate-identifiers-add.md) incluem telefones, tablets e computadores pertencentes à organização e distribuídos à força de trabalho. A inscrição COD suporta cenários de gestão, como inscrição automática, dispositivos partilhados ou requisitos de inscrição previamente autorizados. Uma forma habitual de inscrever CODs passa pela utilização do gestor de inscrição de dispositivos (DEM) por parte do administrador ou do gestor. Os dispositivos iOS/iPadOS podem ser matriculados diretamente através das ferramentas ADE que são fornecidas pela Apple. Os dispositivos com um número IMEI também podem ser identificados e marcados como pertencentes à organização.

### <a name="device-enrollment-manager"></a>Gestor de inscrição de dispositivos
A gestão de inscrição de dispositivos (DEM) é uma conta especial do utilizador que serve para inscrever e gerir múltiplos dispositivos pertencentes à empresa. Os gestores podem instalar o Portal da Empresa e inscrever muitos dispositivos sem utilizador. Estes tipos de dispositivo são ideais, por exemplo, para aplicações de utilitários ou ponto de venda, mas não para utilizadores que necessitem de aceder a recursos de e-mail ou da empresa. Saiba mais sobre o [DEM](device-enrollment-manager-enroll.md).

### <a name="apple-automated-device-enrollment"></a>Inscrição de dispositivo automatizado da Apple
A gestão de Inscrição automática de Dispositivos (ADE) da Apple permite criar e implementar a política "no ar" para dispositivos iOS/iPadOS e macOS que são comprados e geridos com ADE. O dispositivo é inscrito quando os utilizadores ligarem o dispositivo pela primeira vez e executarem o Assistente de Configuração. Este método suporta o modo supervisionado iOS/iPadOS, que permite configurar um dispositivo com funcionalidadeespecífica.

Saiba mais sobre a inscrição iOS/iPadOS ADE:

- [Escolha como inscrever dispositivos iOS/iPadOS](ios-enroll.md)
- [Inscreva dispositivos iOS/iPadOS utilizando programa de inscrição de dispositivos](device-enrollment-program-enroll-ios.md)

### <a name="usb-sa"></a>USB-SA
Os administradores de TI utilizam o Apple Configurator, através de USB, para preparar manualmente cada dispositivo pertencente à empresa para inscrição com o Assistente de Configuração. O administrador de TI cria um perfil de inscrição e exporta-o para o Apple Configurator. Quando os utilizadores recebem os seus dispositivos, é-lhes solicitado que executem o Assistente de Configuração para inscrever o seu dispositivo. Este método suporta o modo **supervisionado iOS,** que por sua vez permite as seguintes funcionalidades:
- Inscrição bloqueada
- Modo de Local Público e outras restrições e configurações avançadas

Saiba mais sobre a inscrição do iOS/iPadOS Apple Configurator com o Assistente de Configuração:

- [Decida como inscrever dispositivos iOS/iPadOS](ios-enroll.md)
- [Inscreva dispositivos iOS/iPadOS com Configurator e Assistente de Configuração](apple-configurator-enroll-ios.md)

### <a name="usb-direct"></a>USB-Direct
Para a inscrição direta, o administrador tem de inscrever cada dispositivo manualmente através da criação de uma política de inscrição e exportá-lo para o Apple Configurator. Os dispositivos ligados por USB pertencentes à empresa são inscritos diretamente e não necessitam de ser apagados. Os dispositivos são geridos como dispositivos sem utilizador. Não estão trancadas ou supervisionadas e não suportam acesso condicional, deteção de fugas de prisões ou gestão de aplicações móveis.

Para saber mais sobre a inscrição iOS/iPadOS, consulte:

- [Decida como inscrever dispositivos iOS/iPadOS](ios-enroll.md)
- [Inscreva dispositivos iOS/iPadOS com Configurator e inscrição direta](apple-configurator-enroll-ios.md)

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Limpeza de dispositivos móveis após a expiração do certificado MDM

O certificado MDM é renovado automaticamente quando os dispositivos móveis estão a comunicar com o serviço do Intune. Se os dispositivos móveis forem limpos ou não comunicarem com o serviço Intune durante algum tempo, o certificado MDM não é renovado. O dispositivo é removido do portal do Azure 180 dias depois da expiração do certificado MDM.
