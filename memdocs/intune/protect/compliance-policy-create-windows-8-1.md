---
title: Definições de conformidade do Windows 8.1 no Microsoft Intune – Azure | Microsoft Docs
description: Veja uma lista de todas as definições que pode utilizar quando define a conformidade para os seus dispositivos Windows 8.1 e Windows Phone 8.1 no Microsoft Intune. Verifique a conformidade da versão mínima e máxima do sistema operativo, defina o comprimento e as restrições das palavras-passe, ative a encriptação no armazenamento de dados e muito mais.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0189fea7f73b70286a6daf844a10806d4c1e8a5d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329669"
---
# <a name="windows-81-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Definições do Windows 8.1 para marcar dispositivos como conformes ou não conformes com o Intune

Este artigo apresenta e descreve as definições de conformidade diferentes que pode configurar em dispositivos Windows 8.1 no Intune. Como parte da solução de gestão de dispositivos móveis (MDM), utilize estas definições para bloquear palavras-passe simples, definir uma versão mínima e máxima do SO e muito mais.

Esta funcionalidade aplica-se a:

- Wnodows Phone 8.1
- Windows 8.1 e posterior

Enquanto administrador do Intune, utilize estas definições de conformidade para ajudar a proteger os recursos da sua organização. Para saber mais sobre as políticas de conformidade e para o que servem, veja a [introdução à conformidade de dispositivos](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Antes de começar

[Criar uma política de conformidade](create-compliance-policy.md#create-the-policy). Em **Plataforma**, selecione **Windows Phone 8.1**, **Windows 8.1 e posterior**.

## <a name="device-properties"></a>Device Properties

### <a name="operating-system-version"></a>Versão do Sistema Operativo

**Windows telefone 8.1 e mais tarde**
- **Versão mínima de OS para dispositivos móveis:**  
  introduza a versão mínima permitida. quando um dispositivo não cumpre o requisito de versão mínima do SO, será reportado como não conforme. É apresentada uma hiperligação com informações sobre como atualizar. O utilizador do dispositivo pode optar por atualizar o seu dispositivo e, em seguida, ter acesso aos recursos da empresa.

- **Versão máxima de OS para dispositivos móveis:**  
  introduza a versão máxima permitida. Quando um dispositivo está a utilizar uma versão S mais tarde do que a versão inserida na regra, o acesso aos recursos da organização é bloqueado. Pede-se ao utilizador do dispositivo que contacte o seu administrador de TI. O dispositivo não pode aceder aos recursos organizacionais até que uma regra mude para permitir a versão S.

**Windows 8.1 e posterior**
- **Versão mínima do SO**:  
  introduza a versão mínima permitida. quando um dispositivo não cumpre o requisito de versão mínima do SO, será reportado como não conforme. É apresentada uma hiperligação com informações sobre como atualizar. O utilizador do dispositivo pode optar por atualizar o seu dispositivo e, em seguida, ter acesso aos recursos da empresa.

- **Versão máxima do SO**:  
  introduza a versão máxima permitida. Quando um dispositivo está a utilizar uma versão S mais tarde do que a versão inserida na regra, o acesso aos recursos da organização é bloqueado. Pede-se ao utilizador do dispositivo que contacte o seu administrador de TI. O dispositivo não pode aceder aos recursos organizacionais até que uma regra mude para permitir a versão S.

Os PCs Windows 8.1 devolvem a versão **3**. Se a regra da versão do SO estiver definida como Windows 8.1 para o Windows, o dispositivo será reportado como não conforme, mesmo que tenha o sistema operativo Windows 8.1.

## <a name="system-security"></a>System Security

### <a name="password"></a>Palavra-passe

- **Exigir uma palavra-passe para desbloquear os dispositivos móveis**:  
  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.
  - **Exigir** - Os utilizadores devem introduzir uma palavra-passe antes de poderem aceder ao seu dispositivo.

- **Palavras-passe simples**:  
  - **Não configurado** *(predefinido)* - Os utilizadores podem criar senhas simples como **1234** ou **1111**.
  - **Bloco** - Os utilizadores não podem criar senhas simples, tais como **1234** ou **1111**.  

- **Comprimento mínimo da palavra-passe**:  
  introduza o número mínimo de dígitos ou carateres que a palavra-passe tem de ter.

  Para dispositivos que executam o Windows e são acedidos com uma conta Microsoft, a política de conformidade não avalia corretamente se uma das seguintes condições for satisfeita:  
  - O comprimento mínimo da palavra-passe é superior a oito caracteres
  - Número mínimo de conjuntos de caracteres é mais de dois

- **Tipo de palavra-passe**:  
  escolha se uma palavra-passe deve ter apenas carateres **Numéricos** ou se deve existir uma combinação de números e de outros carateres (**Alfanuméricos**).

  Quando definido para *Alphanumérico,* a seguinte definição está disponível.  

  - **Número de carateres não alfanuméricos na palavra-passe**:  
    Quando o tipo de *palavra-passe* for definido para **Alphanumérico,** especifique o número mínimo de conjuntos de caracteres que a palavra-passe deve conter. As opções incluem **0** a **4** conjuntos, com um padrão de **1**.
    
    Os quatro conjuntos de carateres são:
    - Letras minúsculas
    - Letras maiúsculas
    - Símbolos
    - Números

    Definir um número mais relevado exige que o utilizador crie uma palavra-passe mais complexa. Para dispositivos que são acedidos com uma conta Microsoft, a política de conformidade não avalia corretamente se uma das seguintes condições for satisfeita:

    - O comprimento mínimo da palavra-passe é superior a oito caracteres
    - Número mínimo de conjuntos de caracteres é mais de dois

- **Minutos de inatividade antes de a palavra-passe ser exigida**:  
  introduza o tempo de inatividade antes de o utilizador ter de reintroduzir a palavra-passe.

- **Expiração da palavra-passe (dias)** :  
  Selecione o número de dias antes da palavra-passe expirar e os utilizadores devem criar uma nova.

- **Número de palavras-passe anteriores para impedir a reutilização**:  
  introduza o número de palavras-passe utilizadas anteriormente que não podem ser utilizadas.

### <a name="encryption"></a>Encriptação

- **Encriptação do armazenamento de dados no dispositivo**:  
  - **Não configurado** *(predefinido)*
  - **Exigir** - Utilizar *o Necessário* para encriptar o armazenamento de dados nos seus dispositivos.


<!-- not on phone   
- **Require encryption on mobile device**: **Require** the device to be encrypted to connect to data storage resources.
--> 

## <a name="next-steps"></a>Próximos passos

- [Adicionar ações para dispositivos não conformes](actions-for-noncompliance.md) e [utilizar etiquetas de âmbito para filtrar políticas](../fundamentals/scope-tags.md).
- [Monitorizar as políticas de conformidade](compliance-policy-monitor.md).
- Veja as [definições de política de conformidade para dispositivos Windows 10 e mais recentes](compliance-policy-create-windows.md).