---
title: Como funciona um ciclo de migração do Intune típico
titleSuffix: Microsoft Intune
description: Este artigo explica como um ciclo de migração do Microsoft Intune funciona e dá-lhe exemplos sobre como processar os ciclos de migração.
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
ms.assetid: 3688b724-9521-4210-bf4d-bcf47d8d4ca0
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: cdef53672c46fe4e49a5d21a22e585654c504f03
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075953"
---
# <a name="typical-migration-cycle"></a>Ciclo de migração típico

É comum uma organização iniciar a sua migração intune com um pequeno piloto, direcionando um subconjunto dos seus utilizadores no departamento de TI. Além disso, a sua organização poderá ter de discutir fatores como a vontade do grupo de mudança, número de utilizadores, complexidade, requisitos, localização e risco de negócio para ajudar na determinação do prazo de migração.

Aqui está um exemplo de como os seus grupos-alvo podem ser agendados:

  | **Grupos de destino da migração** | **Período de tempo 1** | **Período de tempo 2** | **Período de tempo 3** | **Período de tempo 4** | **...**
|:---:|:---:|:---:|:---:|:---:|:---:|
| Organização de TI Piloto Limitada (50 utilizadores) | Anunciar o Plano | Dar instrução para a inscrição | Dar um prazo | Impor acesso condicional |  |                                                        
| Organização de TI Piloto Expandida (200 utilizadores) |  | Anunciar o Plano | Dar instrução para a inscrição | Dar um prazo | Impor acesso condicional |
| Fase 1 da migração Utilizadores com grandes conhecimentos de tecnologia (2000) |  |  | Anunciar o Plano | Dar instrução para a inscrição | Dar um prazo |
| Fase 2 da migração Leste dos EUA |  |  |  | Anunciar o Plano | Dar instrução para a inscrição |
| Todas as Regiões |  |  |  |  | Anunciar o Plano |

## <a name="customer-migration-case-study"></a>Caso prático da migração do cliente

### <a name="adatum-corporation"></a>Adatum Corporation

Veja [como correu o processo de migração de um fornecedor de MDM de terceiros para o Intune da Adatum Corporation](https://gallery.technet.microsoft.com/Intune-migration-guide-893a95e3?redir=0).

## <a name="monitoring-migration"></a>Monitorização da migração

O Intune proporciona várias formas de monitorização da migração:

* Vistas do grupo de utilizadores do Intune

* Conjunto de relatórios incorporados

* Alertas na consola

Controle o número de utilizadores que têm dispositivos inscritos depois de cada fase para poder:

- Avaliar a eficácia do plano de comunicação.

- Estimar o impacto da aplicação do Acesso Condicional.


## <a name="post-migration"></a>Pós-migração

Extinga o fornecedor de MDM anterior e anule a subscrição do serviço após a migração para o Intune. Além disso, remova quaisquer requisitos de infraestrutura desnecessários seguindo as instruções do fornecedor do MDM.
