---
title: Iniciar uma campanha de migração do Intune
titleSuffix: Microsoft Intune
description: Este artigo fornece orientações sobre como iniciar uma campanha de migração para o Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f781b029-50f2-46ee-8ff7-03b4a6719e80
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a15bc7c1fd74aa3741a9bd699778795cbf3faab
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82080033"
---
# <a name="phase-2-migration-campaign"></a>Fase 2: campanha de migração

Selecione uma abordagem de migração mais adequada às necessidades da sua organização e ajuste as táticas de implementação com base nos seus requisitos específicos. O restante deste guia irá dotá-lo das ferramentas necessárias para atingir o objetivo de inserir os dispositivos dos seus utilizadores no Intune.

## <a name="keys-to-a-successful-migration"></a>Aspetos essenciais para uma migração com êxito

Baseie-se nestes pontos essenciais para concluir uma migração com êxito a partir de um fornecedor de MDM de terceiros no Intune:

- As comunicações claras e pertinentes podem minimizar o período de inatividade e a insatisfação do utilizador final.

- Confirme se tem instruções de migração específicas e concretas.

- A inscrição de todos os dispositivos geridos tem de ser anulada a partir do seu fornecedor de MDM existente antes de estes serem inscritos no Intune.

- Forneça orientações do fornecedor de MDM existente aos utilizadores finais sobre como anular a inscrição dos respetivos dispositivos.

- Utilize uma abordagem faseada. Comece com um pequeno grupo de utilizadores piloto e adicione de forma incremental mais grupos de utilizadores até chegar à implementação de escala completa.

- Monitorize o êxito das inscrições e dos carregamentos do suporte técnico de cada ciclo. Deixe tempo na agenda para garantir que os critérios de êxito podem ser avaliados para cada grupo antes de migrar a próxima. A implementação piloto deve validar o seguinte:

  - Se as taxas de êxito e de falha da inscrição estão dentro das expectativas.

  - Produtividade do utilizador:

    - Se os recursos da empresa, tais como VPN, Wi-Fi, e-mail e certificados, estão a trabalhar.

    - Se as aplicações aprovisionadas estão acessíveis.

  - Segurança de dados:

    - Se os relatórios de conformidade estão a ser realizados.

    - Se as proteções de aplicações móveis estão impostas.

Quando estiver satisfeito com a primeira fase de migrações, repita o [ciclo de migração](migration-guide-cycle.md) para a fase seguinte.

- Repita os ciclos faseados até todos os utilizadores terem migrado para o Intune.

- Confirme que a equipa de suporte técnico está pronta para suportar os utilizadores finais ao longo da campanha de migração. Execute uma migração voluntária até poder fazer uma estimativa da carga de trabalho de chamadas de suporte.

- Não estabeleça prazos para inscrição até que a restante população possa ser tratada pelo seu helpdesk

> [!IMPORTANT]
> Não configure o Intune e a sua solução de MDM de terceiros existente para aplicar controlos de acesso a recursos, tais como o Exchange ou o SharePoint Online. Além disso, só deve inscrever os dispositivos numa solução de cada vez.

## <a name="next-steps"></a>Passos seguintes

Crie o seu [plano de comunicação](migration-guide-communication-plan.md).
