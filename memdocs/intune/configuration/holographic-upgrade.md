---
title: Upgrade para Windows Holographic for Business in Microsoft Intune - Azure Microsoft Docs
description: Atualize para o Windows 10 Holographic for Business utilizando um perfil de configuração do dispositivo no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d561d2682cf90d5d7075640c260d8f21c8b891b1
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556120"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Atualizar os dispositivos com o Windows Holographic para o Windows Holographic for Business

O Microsoft Intune inclui muitas definições para ajudar a gerir e proteger os seus dispositivos. Este artigo lista e descreve as definições para atualizar os dispositivos Holográficos do Windows para o Windows Holographic for Business.

Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para atualizar os seus dispositivos Holográficos Windows. Para os HoloLens da Microsoft, pode adquirir a Suite Comercial para obter a licença necessária para a atualização. Para obter mais informações, veja [Desbloquear as funcionalidades do Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Como administrador intune, pode criar e atribuir estas definições aos seus dispositivos.

Para mais informações sobre esta funcionalidade, consulte [as edições do Upgrade Windows 10 ou ativar](edition-upgrade-configure-windows-10.md)o modo S .

## <a name="before-you-begin"></a>Antes de começar

[Crie um atualização de atualização da edição do Windows 10 e o perfil](edition-upgrade-configure-windows-10.md#create-the-profile)de configuração do dispositivo de comutação de modo .

Quando cria um perfil de configuração de upgrade e configuração de dispositivo de mudança de modo do Windows 10, existem mais definições do que as listadas neste artigo. As definições deste artigo são suportadas no Windows Holographic para dispositivos Empresariais.

## <a name="edition-upgrade"></a>Atualização de edição

- **Edição para upgrade para**: Selecione **O Holográfico do Windows 10 para Negócios**.
- **Ficheiro de Licença**: Navegue e selecione o ficheiro de licença XML que lhe foi fornecido.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="Intune, introduza o nome de ficheiro XML que inclui a informação holográfica para a licença de negócios.":::

## <a name="next-steps"></a>Próximos passos

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).

Também pode criar perfis de upgrade de edição para [windows 10 e](edition-upgrade-windows-settings.md) dispositivos posteriores.
