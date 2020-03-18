---
title: Atualizações de software de resolução de problemas no Microsoft Intune - Azure Microsoft Docs
description: Resolva problemas de atualizações de software no Microsoft Intune.
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: d17b70f4-17b4-4d89-88fd-70fa4f34fbea
ROBOTS: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 851fea24f101d313dba3426e5d65c60c5f31fdb5
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330401"
---
# <a name="troubleshoot-software-updates-in-microsoft-intune"></a>Resolver problemas de atualizações de software no Microsoft Intune

Ajude a resolver problemas de atualização de software no Microsoft Intune. Para ver uma lista dos códigos e descrições de erros, aceda aos códigos de erro do agente de atualização de [Software no Microsoft Intune](../protect/software-update-agent-error-codes.md).

## <a name="windows-7-devices-with-many-superseded-updates-stop-reporting-to-intune"></a>Dispositivos do Windows 7 com muitas atualizações supersed deixam de reportar ao Intune

Os clientes da Microsoft Intune podem experimentar um ou mais dos seguintes sintomas:

- Os dispositivos de repente param de reportar ao Intune.  
- Os dispositivos experimentam uma alta utilização de CPU.
- As aplicações instalam-se lentamente quando instaladas através do Intune.
- O Microsoft Intune Center mostra o seguinte erro: `An error occurred while updating your computer. Error found: Code 0x800705b4`.
- A Intune Admin Console > Groups > All Devices > status shows: `One or more agents that are installed on this computer have errors. The information for this computer may not be accurate or up-to-date.`

Este problema pode ocorrer se as atualizações substituídas (as atualizações forem substituídas por outra atualização) não tiverem sido recusadas por um período prolongado. Durante certos processos, como a instalação de uma aplicação, o Windows verifica todas as atualizações supersed em sequência para que as atualizações e os seus sucessores sejam corretamente mapeados. Se a lista de atualizações supersed for demasiado grande, esta tarefa de verificação pode causar uma elevada utilização do CPU devido à carga de processamento e tempo necessários. Este problema afeta principalmente os dispositivos do Windows 7 devido ao grande número de atualizações supersed que estão disponíveis para o Windows 7. Os sistemas operativos mais recentes podem não ter tantas atualizações supersed disponíveis, e podem não ser suscetíveis a este problema.

**Resolução**

1. Inscreva-se em [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. Selecione **Atualizações de Software**.
3. Recuse todas as atualizações supersed que possam aplicar-se ao Windows 7 ou a aplicações, como o Microsoft Office, que foram instaladas nos clientes afetados.
4. Reinicie os clientes afetados.

Se estiver a executar o Windows 7, certifique-se de que a seguinte atualização está instalada:[3050265 Windows Update Client para windows 7: junho de 2015](https://support.microsoft.com/kb/3050265).

## <a name="next-steps"></a>Próximos passos

Obtenha [ajuda de suporte da Microsoft](get-support.md), ou use os [fóruns comunitários](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).