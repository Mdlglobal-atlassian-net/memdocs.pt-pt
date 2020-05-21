---
title: Intune endpoint de teção e definição de resposta de fim de ponta / Microsoft Docs
description: Definições de definição e política de deteção e resposta de endpoint de segurança endpoint no Microsoft Intune
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
ms.openlocfilehash: dd41cfc0d08771c461e6f681ed18791535202bef
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431315"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Definições de política de deteção e resposta de ponto final para segurança de ponto final em Intune

Ver as definições que pode configurar em perfis para a política de *deteção e resposta* de Endpoint no nó de segurança de Ponto final de Intune como parte de uma política de [segurança endpoint](../protect/endpoint-security-policy.md).

Plataformas e perfis suportados:

- **Windows 10 e mais tarde:**
  - Perfil: **Deteção e resposta de ponto final**

## <a name="endpoint-detection-and-response-profile"></a>Perfil de deteção e resposta de ponto final

### <a name="endpoint-detection-and-response"></a>Endpoint detection and response (Deteção e resposta de pontos finais)

- **Tipo de pacote de pacote de configuração do cliente MICROSOFT Defender ATP**

  Faça o upload de um pacote de configuração assinado que será usado para embarcar no cliente ATP do Microsoft Defender.

  - **Não configurado** *(predefinido)*
  - **Bolha de embarque**  
  - **Bolha offboarding**  

  Quando definido para *a blob Onboarding,* pode configurar as seguintes definições:

  - **Proteção avançada contra ameaças no embarque blob**  
    Clique **em Selecionar ficheirode embarque** para abrir o painel de ficheiros de embarque *Select,* onde especifica um `.onboarding` ficheiro.

  Quando definido para *offboarding blob,* pode configurar as seguintes definições:
  
  - **Avançado de proteção contra ameaças offboarding blob**  
     Clique em **Selecionar ficheiro offboarding** para abrir o painel de *ficheiros offboarding Select,* onde especifica um `.offboarding` ficheiro.

- **Partilha de amostras para todos os ficheiros**  

  Devoluções ou configurações do parâmetro de partilha de amostras de proteção de ameaças avançada do Microsoft Defender.  
  - **Não configurado** *(predefinido)*
  - **Sim**

- **Frequência de relatório de telemetria expedita**

  - **Não configurado** *(predefinido)*
  - **Sim** - Aumente a frequência de notificação de telemetria avançada de proteção contra ameaças do Microsoft Defender.

## <a name="next-steps"></a>Próximos passos

[Política de segurança do ponto final para o EDR](../protect/endpoint-security-edr-policy.md)
