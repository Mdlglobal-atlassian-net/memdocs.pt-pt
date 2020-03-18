---
title: Atualizar para o Windows Holographic for Business
titleSuffix: Microsoft Intune
description: Saiba como atualizar os dispositivos com o Windows Holographic para o Windows Holographic for Business
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e809a888fc2696e54540ee6baa2271d7340579
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332085"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Atualizar os dispositivos com o Windows Holographic para o Windows Holographic for Business

O Microsoft Intune inclui muitas definições para ajudar a gerir e proteger os seus dispositivos. Este artigo lista e descreve as definições para atualizar os dispositivos Holográficos do Windows para o Windows Holographic for Business. Estas definições são criadas num perfil de configuração de upgrade em Intune que são empurrados ou implantados para dispositivos.

Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para atualizar os seus dispositivos Holográficos Windows. Para os HoloLens da Microsoft, pode adquirir a Suite Comercial para obter a licença necessária para a atualização. Para obter mais informações, veja [Desbloquear as funcionalidades do Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Para mais informações sobre esta funcionalidade, consulte [as edições do Upgrade Windows 10 ou ativar](edition-upgrade-configure-windows-10.md)o modo S .

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [configuração do dispositivo](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Atualização de edição

- **Edição para upgrade para**: Selecione **O Holográfico do Windows 10 para Negócios**.
- **Ficheiro de Licença**: Navegue e selecione o ficheiro de licença XML que lhe foi fornecido.

  ![Introduza o nome de ficheiro XML que inclui o Holographic para informações de licença de negócios](./media/holographic-upgrade/Holographic-edition-upgrade.png)
 
## <a name="next-steps"></a>Próximos passos

O perfil é criado, mas pode ainda não estar a fazer nada. Certifique-se de [atribuir o perfil](device-profile-assign.md)e monitorizar [o seu estado](device-profile-monitor.md).

Também pode criar perfis de upgrade de edição para [windows 10 e](edition-upgrade-windows-settings.md) dispositivos posteriores.
