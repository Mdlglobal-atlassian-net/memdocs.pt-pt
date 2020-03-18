---
title: Utilize as ações do dispositivo a granel no dispositivo Microsoft Intune.
titleSuffix: ''
description: Utilize as ações do dispositivo remoto a granel.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c50f5495aa593dc8904fe6a9120ecd29de693ee
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328421"
---
# <a name="use-bulk-device-actions"></a>Utilize ações de dispositivos a granel

Pode utilizar ações de dispositivos a granel para as seguintes ações remotas:
- [Reset do piloto automático](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Notificações personalizadas](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Eliminar](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Mudar o nome](device-rename.md)
- [Reiniciar](device-restart.md)
- [Sincronização](device-sync.md)
- [Eliminação](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Utilize uma ação de dispositivo a granel

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Escolha **dispositivos** > **Todos os dispositivos** > as ações do dispositivo a **granel**.
![ações do dispositivo Bulk](./media/bulk-device-actions/bulk-device-actions.png)
3. Na página de ação do **dispositivo Bulk,** selecione uma ação **DE Os** e **Dispositivo**. Algumas ações do dispositivo têm opções ou campos adicionais para povoar. Selecione **Next**.
4. Na página **Dispositivos,** selecione de 1 a 100 dispositivos > **Next**.
5. Na página **Review + criar,** selecione **Criar**.

## <a name="next-steps"></a>Próximos passos
[Visão geral da gestão do dispositivo.](device-management.md)
