---
title: Remova um utilizador de um dispositivo iOS/iPadOS com o Microsoft Intune
titleSuffix: ''
description: Aprenda a remover um utilizador de um dispositivo iOS/iPadOS partilhado com intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08a6ccb30d4397ce5d06483556579c32f3eb2819
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328369"
---
# <a name="remove-a-user-from-a-shared-iosipados-device"></a>Remova um utilizador de um dispositivo iOS/iPadOS partilhado


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A ação **Remover utilizador** elimina um utilizador selecionado da cache local num dispositivo iPad partilhado. O dispositivo iPad deve ser configurado para gerir a aplicação iOS/iPadOS Classroom utilizando um perfil de [educação iOS/iPadOS](../fundamentals/education-settings-configure-ios.md). 

## <a name="supported-platforms"></a>Plataformas suportadas

- Windows – não suportado
- Windows Phone – não suportado
- iOS/iPadOS - Suportado no iOS/iPadOS 9.3 e posteriormente (apenas dispositivos de iPad partilhados)
- macOS – não suportado
- Android – não suportado

## <a name="remove-a-user"></a>Remover um utilizador

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > **Todos os dispositivos**.
3. Na lista de dispositivos que gere, selecione um dispositivo iOS/iPadOS.
4. No painel do dispositivo, selecione **Utilizadores**.
5. Na lista, clique com o botão direito do rato no utilizador que pretende remover e, em seguida, selecione **Remover utilizador**.

## <a name="next-steps"></a>Próximos passos

- Para ver o estado da ação **Remover utilizador**, selecione **Dispositivos** > **Ações do dispositivo**.
