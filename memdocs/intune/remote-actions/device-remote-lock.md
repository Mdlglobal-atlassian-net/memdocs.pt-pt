---
title: Bloquear dispositivos com o Microsoft Intune – Azure | Microsoft Docs
description: Utilize a ação Bloqueio remoto no Microsoft Intune para bloquear um dispositivo protegido por um PIN ou palavra-passe.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 29b30d46fc5998c69059c743c3f469e198cee1ef
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325125"
---
# <a name="remotely-lock-devices-with-intune"></a>Bloquear remotamente dispositivos com o Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A ação **Bloqueio remoto** bloqueia o dispositivo. Para desbloquear o dispositivo, o proprietário do dispositivo introduz o código de acesso. Pode bloquear remotamente dispositivos que tenham um PIN ou uma palavra-passe definida. Os dispositivos que não tenham um PIN ou palavra-passe não podem ser bloqueados remotamente.

## <a name="supported-platforms"></a>Plataformas suportadas

**O bloqueio remoto** é suportado para as seguintes plataformas:

- Android
- Dispositivos de quiosque Android Enterprise
- Dispositivos com perfil de trabalho do Android Enterprise
- iOS
- macOS
- Windows 10 Mobile
- Windows Phone 8.1 e posterior

O **Bloqueio remoto** não é suportado para:
- Windows 10 Desktop

> [!NOTE]
> Para dispositivos macOS, defina um PIN de recuperação de 6 dígitos. Se o dispositivo estiver bloqueado, a **Descrição geral do dispositivo** apresenta o PIN até que seja enviada outra ação de dispositivo.

## <a name="remote-lock-a-device"></a>Bloquear remotamente um dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecione **Dispositivos** > **Todos os dispositivos**.
4. Na lista de dispositivos, selecione um dispositivo e, em seguida, selecione a ação **Bloqueio remoto**.

## <a name="next-steps"></a>Passos seguintes

- Para ver o estado desta ação, selecione as ações do**Devices** > **Dispositivo** **Intune** > microsoft . 
- Para obter mais ações que podem ajudá-lo a gerir os seus dispositivos, veja [Ações disponíveis](device-management.md).
