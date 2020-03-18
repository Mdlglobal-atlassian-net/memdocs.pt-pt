---
title: Configuração De Inscrição Intune para dispositivos geridos pela Android Enterprise
titleSuffix: Microsoft Intune
description: Saiba como inscrever dispositivos geridos pelo Android Enterprise em Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: c4fb6adadb4e0dbf593bbbe3d9ee51ed5783e152
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325481"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-fully-managed-devices"></a>Configurar a inscrição intune de dispositivos geridos totalmente pela Android Enterprise 

Os dispositivos geridos totalmente pelo Android Enterprise são dispositivos corporativos associados a um único utilizador e utilizados exclusivamente para trabalho e não para uso pessoal. Os administradores podem gerir todo o dispositivo e impor controlos políticos indisponíveis para perfis de trabalho, tais como:
- Permita a instalação de aplicações apenas a partir do Managed Google Play.
- Bloquear a desinstalação de aplicações geridas.
- Evite que os utilizadores reacendam dispositivos de reposição de fábrica, e assim por diante.

Intune ajuda-o a implementar aplicações e configurações para dispositivos Android Enterprise, incluindo dispositivos geridos pelo Android Enterprise. Para obter detalhes específicos sobre o Android Enterprise, veja [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) (Requisitos empresariais do Android).

## <a name="technical-requirements"></a>Requisitos técnicos

Você deve ter um inquilino autónomo Intune para gerir dispositivos android enterprise totalmente geridos. A gestão de dispositivos totalmente gerida não está disponível na antiga consola de gestão Silverlight.

Os dispositivos devem satisfazer estes requisitos para serem geridos como um dispositivo Android Enterprise totalmente gerido:

- Android OS versão 6.0 ou superior.
- Os dispositivos devem executar uma construção do Android que tenha conectividade Google Mobile Services (GMS). Os dispositivos têm de ter os GMS disponíveis e têm de conseguir ligar-se aos mesmos.

Não existe qualquer restrição ao fabricante do dispositivo/OEM se os requisitos acima referidos forem cumpridos.

## <a name="set-up-android-enterprise-fully-managed-device-management"></a>Configurar a gestão completa de dispositivos do Android Enterprise

Para configurar a gestão completa do dispositivo Android Enterprise, siga estes passos:

1. Para se preparar para gerir dispositivos móveis, tem de definir a autoridade de gestão de [dispositivos móveis (MDM) para o **Microsoft Intune**](../fundamentals/mdm-authority-set.md). Este item só é definido uma vez, quando está a configurar pela primeira vez o Intune para a gestão de dispositivos móveis.
2. [Ligue a sua conta do inquilino do Intune à sua conta do Android Enterprise](connect-intune-android-enterprise.md).
3. [Ativar dispositivos de utilizador corporativos](#enable-corporate-owned-user-devices)
4. [Inscreva os dispositivos totalmente geridos](#enroll-the-fully-managed-devices).

### <a name="enable-corporate-owned-user-devices"></a>Ativar dispositivos de utilizador corporativos

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) e escolha **dispositivos** ** > ** android > **android  > ** dispositivos de utilizador **totalmente geridos.**
2. Em **Permitir que os utilizadores matriculem dispositivos de utilizador corporativos,** escolha **Sim**.

> [!NOTE]
> Se tiver uma política de Acesso Condicional Azure AD definida que utiliza o *dispositivo necessário para ser marcado como* controlo conforme e se aplica a **aplicações All Cloud**, **Android** e **Browsers** – deve excluir desta política a aplicação cloud **Microsoft Intune.** Isto porque os processos de configuração do Android utilizam um separador Chrome para autenticar os seus utilizadores durante a inscrição. Para mais informações, consulte a Documentação de [Acesso Condicional da Azure AD.](https://docs.microsoft.com/azure/active-directory/conditional-access/)

Quando esta definição está definida para **Sim,** ele fornece-lhe um token de inscrição (uma corda aleatória) e um código QR para o seu inquilino Intune. Este token de inscrição única é válido para todos os seus utilizadores e não expirará. Dependendo do Sistema Operativo Android e versão do dispositivo, pode utilizar o código token ou QR para inscrever o dispositivo.

## <a name="enroll-the-fully-managed-devices"></a>Inscreva os dispositivos totalmente geridos
Agora pode [inscrever os seus dispositivos totalmente geridos.](android-dedicated-devices-fully-managed-enroll.md)

## <a name="next-steps"></a>Próximos passos
- [Adicione as políticas de configuração de dispositivos totalmente geridas pelo Android Enterprise](../configuration/device-restrictions-android-for-work.md#device-owner-only)
- [Configure políticas de configuração de aplicativos para dispositivos geridos totalmente pelo Android Enterprise](../apps/app-configuration-policies-use-android.md)

