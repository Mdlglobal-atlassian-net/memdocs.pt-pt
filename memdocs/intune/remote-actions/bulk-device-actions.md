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
ms.openlocfilehash: 5f33198e71fd4250ee93207e571bc535abd1c95f
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325374"
---
# <a name="use-bulk-device-actions"></a>Use bulk device actions (Utilizar ações do dispositivo em massa)

Pode utilizar ações de dispositivos a granel para as seguintes ações remotas:
- [Reset do piloto automático](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Notificações personalizadas](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Eliminar](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Mudar o nome](device-rename.md)
- [Reiniciar](device-restart.md)
- [Sincronização](device-sync.md)
- [Eliminação](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Utilize uma ação de dispositivo a granel

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Escolha **dispositivos** > **Todos os dispositivos** > as ações do dispositivo a **granel**.
![ações do dispositivo Bulk](./media/bulk-device-actions/bulk-device-actions.png)
3. Na página de ação do **dispositivo Bulk,** selecione uma ação **DE Os** e **Dispositivo**. Algumas ações do dispositivo têm opções ou campos adicionais para povoar. Escolha **Seguinte**.
4. Na página **Dispositivos,** selecione de 1 a 100 dispositivos > **Next**.
5. Na página **Review + criar,** selecione **Criar**.

## <a name="next-steps"></a>Próximos passos
[Visão geral da gestão do dispositivo.](device-management.md)
