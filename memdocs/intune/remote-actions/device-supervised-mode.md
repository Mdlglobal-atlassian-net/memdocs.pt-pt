---
title: Ligue o modo supervisionado iOS/iPadOS com o Microsoft Intune
titleSuffix: ''
description: Saiba como ativar o modo supervisionado iOS/iPadOS com o Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/15/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8190814-07f0-42d8-9b3a-87c67dd2b7ed
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: da02d51ce5860c3be0e0e51341b5f41f01245303
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983054"
---
# <a name="turn-on-iosipados-supervised-mode"></a>Ligue o modo supervisionado iOS/iPadOS


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

O modo supervisionado pela Apple iOS/iPadOS dá aos administradores mais opções na gestão dos dispositivos apple, tornando-o útil para dispositivos corporativos implementados em escala. Por exemplo, pode restringir o AirDrop ou impedir que os utilizadores alterem o nome do dispositivo. Para obter uma lista das definições que exigem o modo supervisionado, veja [Definições de restrição de dispositivos iOS no Intune](../configuration/device-restrictions-ios.md).

O Intune suporta o modo supervisionado como parte do [Programa de Registo de Aparelho (DEP)](../enrollment/device-enrollment-program-enroll-ios.md) da Apple.

Para obter uma lista de controlos da Apple que requerem supervisão, consulte a referência das definições de [Payload](http://help.apple.com/configurator/mac/2.4/#/cad5370d089)da Apple .

## <a name="turn-on-supervised-mode-during-enrollment"></a>Ativar o modo supervisionado durante a inscrição

No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)pode ligar o modo supervisionado para dispositivos quando criar um perfil de [inscrição da Apple no DEP](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile). Em **Definições da Gestão de Dispositivos**, selecione a caixa de verificação **Supervisionado**.

## <a name="turn-on-supervised-mode-after-enrollment"></a>Ativar o modo supervisionado após a inscrição

Após a inscrição, a única maneira de ligar o modo supervisionado é ligar um dispositivo iOS/iPadOS a um Mac e [utilizar o Configurador Apple](../enrollment/apple-configurator-enroll-ios.md) (que irá redefinir o dispositivo). Não é possível configurar um dispositivo para o modo Supervisionado em Intune após a inscrição.

## <a name="identify-a-supervised-device"></a>Identificar um dispositivo supervisionado

Para determinar se um dispositivo é supervisionado, consulte o ecrã de bloqueio ou a página **Acerca de**:
- No ecrã de bloqueio do dispositivo, estará escrito **Este iPhone é gerido pela "Nome da Empresa".**
- Na página **Sobre** do dispositivo, dirá que **este iPhone está supervisionado. O nome da empresa pode monitorizar o tráfego da Internet e localizar este dispositivo.**

## <a name="next-steps"></a>Passos seguintes

Para saber mais sobre outras opções de gestão de dispositivos, veja [O que é a gestão de dispositivos do Microsoft Intune?](device-management.md)
