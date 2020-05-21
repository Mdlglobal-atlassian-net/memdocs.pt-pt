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
ms.openlocfilehash: 3a94b71bb479fcb84e998a4e4b7c3ad91e2e3043
ms.sourcegitcommit: d8dc05476ecd5db7ecb36dc649b566b349ba263d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83732912"
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
> Para dispositivos macOS, defina um PIN de recuperação de 6 dígitos. Se o dispositivo estiver bloqueado, a **Descrição geral do dispositivo** apresenta o PIN até que seja enviada outra ação de dispositivo. Certifique-se de que anota o pino, uma vez que só estará disponível durante 7 dias após o envio do comando de bloqueio remoto. Após os 7 dias, Intune deixará de ter o PIN. Além disso, não volte a iniciar este comando para o mesmo dispositivo até que o pino original seja utilizado para desbloquear o dispositivo com sucesso. Deve enviar este comando, anote o pino e até o utilizar para entrar no dispositivo macOS com sucesso, não envie este comando para o mesmo dispositivo novamente.  


## <a name="remote-lock-a-device"></a>Bloquear remotamente um dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecione **Dispositivos**  >  **Todos os dispositivos**.
4. Na lista de dispositivos, selecione um dispositivo e, em seguida, selecione a ação **Bloqueio remoto**.

## <a name="next-steps"></a>Próximos passos

- Para ver o estado desta ação, selecione as ações do Dispositivo **Intune**  >  **Devices**  >  **Device actions**microsoft . 
- Para obter mais ações que podem ajudá-lo a gerir os seus dispositivos, veja [Ações disponíveis](device-management.md).
