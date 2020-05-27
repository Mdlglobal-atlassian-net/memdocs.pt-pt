---
title: Inicie sessão com o utilizador de um dispositivo iOS/iPadOS
titleSuffix: Microsoft Intune
description: Saiba como iniciar sessão no utilizador atual de um dispositivo iOS/iPadOS com Intune."
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 702bc46c-1a6f-4689-bd53-3b778a447baa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e151110a39e28d00a2a98cd6ea3c3fc9214ef4a0
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983475"
---
# <a name="logout-the-current-user-on-intune-managed-iosipados-devices"></a>Inicie o logout do utilizador atual em dispositivos iOS/iPadOS geridos por Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A ação **Terminar sessão do utilizador atual** termina a sessão do utilizador atual num dispositivo iPad partilhado. 

## <a name="supported-platforms"></a>Plataformas suportadas

- Windows – não suportado
- Windows Phone – não suportado
- iOS/iPadOS - Suportado no iOS/iPadOS 9.3 e posteriormente (apenas dispositivos de iPad partilhados)
- macOS – não suportado
- Android – não suportado

## <a name="how-to-log-out-the-current-user"></a>Como terminar a sessão do utilizador atual

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selecione Dispositivos Todos os **Devices**  >  **dispositivos**.
2. Escolha um dispositivo iOS/iPadOS > **...**  >  Utilizador atual de **logout**.

## <a name="next-steps"></a>Passos seguintes

Para ver o estado da ação que acabou de realizar, no painel **Dispositivos e grupos**, escolha **Ações de Dispositivos**.
