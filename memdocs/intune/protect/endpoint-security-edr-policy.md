---
title: Gerir definições de deteção e resposta de ponto final com políticas de segurança de ponto final no Microsoft Intune / Microsoft Docs
description: Configure e implemente políticas para dispositivos que gere com a política de deteção e resposta final de ponto final no Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 3ca9d8f1db36856d9d696a2a1c3933ff4a54b7c3
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431307"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Política de deteção e resposta de ponto final para segurança de ponto final em Intune

Quando integra o Defender ATP com o Intune, pode utilizar as políticas de segurança de ponto final para deteção e resposta de pontofinal (EDR) para gerir as definições EDR e dispositivos de bordo para o Defender ATP.

As capacidades de deteção e resposta do AtP do Microsoft Defender fornecem deteções avançadas de ataques que estão perto do tempo real e asercionáveis. Os analistas de segurança podem priorizar os alertas de forma eficaz, ganhar visibilidade em todo o âmbito de uma violação e tomar medidas de resposta para remediar ameaças.

Encontre as políticas de segurança de ponto final para o EDR no *âmbito do Manage* no nó de segurança **Endpoint** do centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Ver definições para perfis de [deteção e resposta de Ponto Final](../protect/endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-profiles"></a>Pré-requisitos para perfis EDR

- Windows 10 ou mais tarde
- Para que a Intune gere as definições de deteção e resposta de pontofinal num dispositivo, deve embarcar no dispositivo com o Defender ATP.

## <a name="edr-profiles"></a>Perfis EDR

**Perfis do Windows 10:**

- **Deteção e resposta de ponto final** – Gerir as [definições para deteção e resposta de pontofinal ATP do Microsoft Defender](endpoint-security-edr-profile-settings.md).

  As capacidades de deteção e resposta do AtP do Microsoft Defender fornecem deteções avançadas de ataques que estão perto do tempo real e asercionáveis.

  Para saber mais, consulte a [deteção e resposta](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) do ponto final na documentação ATP do Microsoft Defender.

## <a name="next-steps"></a>Próximos passos

[Configure políticas de segurança de Endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
