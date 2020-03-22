---
title: definições de política antivírus macOS para o Antivírus Do Microsoft Defender para Intune  Microsoft Docs
description: Consulte uma lista das definições no perfil Antivírus Microsoft Defender para macOS. Este perfil faz parte da política antivírus de segurança endpoint para macOS no Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: 9a0687b9e3938c93cfaebe0e064fd994077a92af
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086280"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Definições para Microsoft Defender ATP para Mac no Microsoft Intune

Ver as definições de perfil *Antivírus* que pode configurar para o Microsoft Defender ATP para Mac no Microsoft Intune. Para obter mais informações sobre estas definições, consulte o [Microsoft Defender Advanced Threat Protection for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) na documentação do Windows.

**Microsoft Defender ATP**

- **Proteção em tempo real**  
  Exija que o Defender nos dispositivos macOS utilize a funcionalidade de Monitorização em tempo real. A monitorização em tempo real localiza e impede que o malware instale ou execute no seu dispositivo. Pode desligar esta definição por um curto período de tempo antes de voltar a ligar automaticamente.

  - **Não configurado** *(predefinido)* - A definição é restaurada à defeito do sistema
  - **Habilitado** - Impor a utilização da monitorização em tempo real. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Desativado** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.

- **Proteção entregue em nuvem**  
  Por padrão, o Defender envia informações à Microsoft sobre quaisquer problemas que encontre. A Microsoft analisa essa informação para saber mais sobre problemas que afetam o seu e outros clientes, para oferecer soluções melhoradas. A proteção funciona melhor quando a *submissão automática* da amostra é definida.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Ativado** - A proteção entregue em nuvem é ativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Desativado** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.

- **Submissão automática da amostra**  
  Envia ficheiros de amostras para a Microsoft para ajudar a proteger os utilizadores de dispositivos e a sua organização contra potenciais ameaças.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Ativado** - A proteção entregue em nuvem é ativada.  Os utilizadores do dispositivo não podem alterar esta definição.
  - **Desativado** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.

- **Recolha de dados de diagnóstico**

  Configure como os dados de diagnóstico e utilização são partilhados com a Microsoft.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Necessário**
  - **Opcional**

- **Pastas excluídas da varredura**  
  Selecione **Adicionar** e, em seguida, especificar pastas para ignorar durante uma varredura.

- **Ficheiros excluídos da varredura**  
  Selecione **Adicionar** e, em seguida, especificar ficheiros para ignorar durante uma varredura.

- **Tipos de ficheiros excluídos da varredura**  
  Selecione **Adicionar** e, em seguida, especificar extensões de ficheiros para ignorar durante uma varredura.

- **Processos excluídos da varredura**  
  Selecione **Adicionar** e, em seguida, especificar processos para ignorar durante uma varredura.
