---
title: Configuração De Inscrição Intune para dispositivos geridos pela Android Enterprise
titleSuffix: Microsoft Intune
description: Saiba como inscrever dispositivos geridos pelo Android Enterprise em Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: how-to
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
ms.openlocfilehash: e270afc0c2ef84af0f44c0b9fc767319bdf2d30b
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990424"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-fully-managed-devices"></a>Configurar a inscrição intune de dispositivos geridos totalmente pela Android Enterprise 

Os dispositivos totalmente geridos do Android Enterprise são dispositivos pertencentes à empresa associados a um único utilizador e utilizados exclusivamente para o trabalho e não para uso pessoal. Os administradores podem gerir todo o dispositivo e impor controlos políticos indisponíveis para perfis de trabalho, tais como:
- Permita a instalação de aplicações apenas a partir do Managed Google Play.
- Bloquear a desinstalação de aplicações geridas.
- Evite que os utilizadores reacendam dispositivos de reposição de fábrica, e assim por diante.

Intune ajuda-o a implementar aplicações e configurações para dispositivos Android Enterprise, incluindo dispositivos geridos pelo Android Enterprise. Para mais detalhes sobre o Android Enterprise, consulte [os requisitos do Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

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

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e escolha **dispositivos**android  >  **android**  >  **de inscrição**   >  **corporate, dispositivos de utilizador totalmente geridos**.
2. Em **Permitir que os utilizadores matriculem dispositivos de utilizador corporativos,** escolha **Sim**.

> [!NOTE]
> Se tiver uma política de Acesso Condicional Azure AD definida que utilize o *dispositivo necessário para ser marcado como* controlo de Grant compatível ou uma política de Bloco e se aplica a **aplicações All Cloud**, **Android**e **Browsers**, deve excluir desta política a aplicação cloud **Microsoft Intune.** Isto porque o processo de configuração do Android utiliza um separador Chrome para autenticar os seus utilizadores durante a inscrição. Para mais informações, consulte [a documentação de Acesso Condicional azure AD.](https://docs.microsoft.com/azure/active-directory/conditional-access/)

Quando esta definição está definida para **Sim,** ele fornece-lhe um token de inscrição (uma corda aleatória) e um código QR para o seu inquilino Intune. Este token de inscrição única é válido para todos os seus utilizadores e não expirará. Dependendo do Sistema Operativo Android e versão do dispositivo, pode utilizar o código token ou QR para inscrever o dispositivo.

## <a name="enroll-the-fully-managed-devices"></a>Inscreva os dispositivos totalmente geridos
Agora pode [inscrever os seus dispositivos totalmente geridos](android-dedicated-devices-fully-managed-enroll.md) (mas não quando utilizar contas DEM).

## <a name="next-steps"></a>Passos seguintes
- [Adicione as políticas de configuração de dispositivos totalmente geridas pelo Android Enterprise](../configuration/device-restrictions-android-for-work.md#device-owner-only)
- [Configure políticas de configuração de aplicativos para dispositivos geridos totalmente pelo Android Enterprise](../apps/app-configuration-policies-use-android.md)

