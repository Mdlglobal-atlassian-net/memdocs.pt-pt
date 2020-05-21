---
title: Gerir as definições de proteção de contas de ataque com políticas de segurança de ponto final no Microsoft Intune / Microsoft Docs
description: Configure e implemente políticas para dispositivos que gere com definições de política de proteção de conta de segurança final no Microsoft Endpoint Manager.
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
ms.openlocfilehash: 6fb5702b7c809c7810004a53d084f19fa94dea9e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431367"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Política de proteção de contas para segurança de pontofinal em Intune

Utilize políticas de segurança intune endpoint para proteção de conta para proteger a identidade e contas dos seus utilizadores. A política de proteção de conta está focada nas definições para Windows Hello e Credential Guard, que faz parte da identidade do Windows e gestão de acesso.

- *O Windows Hello for Business* substitui as palavras-passe por uma autenticação forte de dois fatores em Computadores e dispositivos móveis.
- *A Guarda Credencial* ajuda a proteger credenciais e segredos que usa com os seus dispositivos.

Para saber mais, consulte [a gestão de Identidade e acesso](https://docs.microsoft.com/windows/security/identity-protection/) na documentação de identidade e gestão de acesso do Windows.

Encontre as políticas de segurança de ponto final para a proteção da conta sob *gestão* no nó de **segurança Endpoint** do centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Ver definições para perfis de [proteção de conta](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-account-protection-profiles"></a>Pré-requisitos para perfis de proteção de conta

- Windows 10 ou mais tarde

## <a name="account-protection-profiles"></a>Perfis de proteção de conta

Os perfis de *proteção de conta estão em Pré-visualização*.

**Perfis do Windows 10:**

- **Proteção de conta** *(Pré-visualização)* – As definições para as políticas de proteção de conta ajudam-no a proteger as credenciais dos utilizadores.

## <a name="next-steps"></a>Próximos passos

[Configure políticas de segurança de Endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
