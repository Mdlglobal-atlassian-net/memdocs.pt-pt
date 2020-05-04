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
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325374"
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

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Escolha **dispositivos** > **Todas as** > ações**do dispositivo**a granel .
![Ações de dispositivos a granel](./media/bulk-device-actions/bulk-device-actions.png)
3. Na página de ação do **dispositivo Bulk,** selecione uma ação **DE Os** e **Dispositivo**. Algumas ações do dispositivo têm opções ou campos adicionais para povoar. Escolha **Seguinte**.
4. Na página **dispositivos,** selecione de 1 a 100 dispositivos > **Seguinte**.
5. Na página **Review + criar,** selecione **Criar**.

## <a name="next-steps"></a>Passos seguintes
[Visão geral da gestão do dispositivo.](device-management.md)
