---
title: Intune endpoint de teção e definição de resposta de fim de ponta / Microsoft Docs
description: Definições de definição e política de deteção e resposta de endpoint de segurança endpoint no Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
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
ms.openlocfilehash: dd53ec47435ba9dc416d2b152719b393d1647f90
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824001"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Definições de política de deteção e resposta de ponto final para segurança de ponto final em Intune

Ver as definições que pode configurar em perfis para a política de [deteção e resposta](../protect/endpoint-security-edr-policy.md) de Endpoint no nó de segurança de Ponto final de Intune.

Plataformas e perfis suportados:

- **Windows 10 e mais tarde**: Utilize esta plataforma para a política que implementa para dispositivos geridos com o Intune.
  - Perfil: **Deteção e resposta de ponto final (MDM)**

- **Windows 10 e Windows Server**: Utilize esta plataforma para a política que implementa para dispositivos geridos pelo Gestor de Configuração.
  - Perfil: **Deteção e resposta de ponto final (ConfigMgr) (Pré-visualização)**
  
  *Esta plataforma e perfil estão em Visualização Pública.*

## <a name="endpoint-detection-and-response-mdm"></a>Deteção e resposta de pontofinal (MDM)

**Deteção e resposta de pontofinal:**

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

## <a name="endpoint-detection-and-response-configmgr-preview"></a>Deteção e resposta de pontofinal (ConfigMgr) (Pré-visualização)

**Deteção e resposta de pontofinal:**

- **Partilha de amostras para todos os ficheiros**  

  Devoluções ou configurações do parâmetro de partilha de amostras de proteção de ameaças avançada do Microsoft Defender.  
  - **Não configurado** *(predefinido)*
  - **Sim**

- **Frequência de relatório de telemetria expedita**

  - **Não configurado** *(predefinido)*
  - **Sim** - Aumente a frequência de notificação de telemetria avançada de proteção contra ameaças do Microsoft Defender.

## <a name="next-steps"></a>Passos seguintes

[Política de segurança do ponto final para o EDR](../protect/endpoint-security-edr-policy.md)
