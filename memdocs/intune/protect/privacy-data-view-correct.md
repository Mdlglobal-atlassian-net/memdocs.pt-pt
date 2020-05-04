---
title: View and correct personal data (Ver e corrigir dados pessoais)
titleSuffix: Microsoft Intune
description: Saiba como ver e corrigir dados pessoais.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6cddd94400874c508a31b11b22fa4417798e2da
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084781"
---
# <a name="view-and-correct-personal-data"></a>View and correct personal data (Ver e corrigir dados pessoais)

Os administradores do Intune podem ver alguns dados pessoais com base nas respetivas permissões de acesso, mas apenas os utilizadores finais podem alterar os respetivos dados pessoais do dispositivo.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>Ver dados pessoais

Os administradores podem ver informações pessoais de utilizadores finais em vários painéis na IU do Intune. Os seguintes artigos explicam o que os administradores de informação fazem e não têm acesso a:
- [Veja os detalhes](../remote-actions/device-inventory.md) do dispositivo em Intune explica como pode rever detalhes sobre o dispositivo de um utilizador final.
- [Monitorizar informações e atribuições](../apps/apps-monitor.md) de aplicações explica como ver detalhes sobre aplicações instaladas no dispositivo de um utilizador final.
- O que a informação pode a [minha empresa ver quando inscrevi o meu dispositivo?](https://docs.microsoft.com/mem/intune/user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) É melhor dizer claramente aos seus utilizadores que tipo de dados está a recolher e por que está a recolhê-lo. Este artigo pode representar o primeiro passo para essa transparência.

### <a name="who-can-view-the-data"></a>Quem pode ver os dados?

A Microsoft utiliza controlos rigorosos para regular o acesso aos dados dos clientes ao conceder o nível mais baixo de acesso necessário para concluir tarefas essenciais e ao revogar o acesso quando este deixa de ser necessário. 

Pode proteger e controlar o acesso aos dados pessoais do utilizador final com o controlo de administração baseada em funções (RBAC). Para obter mais informações, veja [RBAC com o Microsoft Intune](../fundamentals/role-based-access-control.md).

Para saber mais sobre as práticas de dados da Microsoft, leia os Termos dos Serviços Online e a [Declaração de Privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409). 

## <a name="correct-end-user-personal-data"></a>Corrigir dados pessoais do utilizador final

Os administradores não podem atualizar informações específicas sobre dispositivos ou aplicações. Se o utilizador final quiser corrigir algum dado pessoal, por exemplo o nome do dispositivo, tem de o fazer diretamente no dispositivo. Essas alterações serão sincronizadas na próxima vez que o utilizador se ligar ao Intune.


## <a name="next-steps"></a>Passos seguintes

Saiba como [auditar, exportar ou eliminar](privacy-data-audit-export-delete.md) dados pessoais no Intune.
