---
title: Modelo de dados do Armazém de Dados
titleSuffix: Microsoft Intune
description: O Armazém de Dados do Microsoft Intune copia dados diariamente para fornecer uma apresentação do histórico do seu ambiente móvel em contínua mudança.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4D04D3D9-4B6C-41CD-AAF8-466AF8FA6032
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf5ab63f72484ddbbf311810e232404ab643d2d2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331713"
---
# <a name="microsoft-intune-data-warehouse-data-model"></a>Microsoft Intune Data Warehouse modelo de dados

O Armazém de Dados do Intune copia dados diariamente para fornecer uma apresentação do histórico do ambiente de dispositivos móveis em contínua mudança. A apresentação é composta por entidades relacionadas no tempo.

## <a name="entities-entity-sets"></a>Entidades: conjuntos de entidades

O armazém expõe dados nas seguintes áreas de nível superior:

- Utilização e aplicações com proteção de aplicações ativada
- Dispositivos inscritos, propriedades e inventário
- Inventário de aplicações e software
- Políticas de conformidade e de configuração de dispositivos

Estas áreas contêm as entidades com significado para o ambiente do Intune. Encontrará detalhes sobre os conjuntos de entidades nos seguintes tópicos:

- [Aplicação](reports-ref-application.md)
- [Date](reports-ref-date.md)
- [Dispositivos](reports-ref-devices.md)
- [Extensão de Gestão do Intune](reports-ref-intunemanagementextension.md)
- [Policy](reports-ref-policy.md)
- [Mobile App Management (MAM)](../apps/app-management.md)
- [Utilizador](reports-ref-user.md)
- [Associações de Dispositivos do Utilizador](reports-ref-user-device.md)

## <a name="relationships-star-schema-model"></a>Relações: modelo de esquema de estrela

O armazém organiza as entidades em relações com significado para o tipo de questões que pretende esclarecer. Por exemplo, pode rever o número de instalações de uma aplicação Android desenvolvida internamente. A estrutura do armazém de dados permite-lhe obter informações sobre o seu ambiente móvel. Por sua vez, as ferramentas de análise, como o Microsoft Power BI, podem utilizar o modelo de dados do Armazém de Dados para criar visualizações e dashboards dinâmicos.

As entidades e as relações utilizam um modelo de esquema de estrela. Um esquema de estrela correlaciona os factos ao longo da dimensão de tempo. Um *facto* no contexto do modelo é uma medida quantitativa, como o número de dispositivos, número de aplicações ou momento de inscrição. As tabelas de factos armazenam uma grande quantidade de dados. As tabelas podem atingir grandes volumes e, por isso, limitam normalmente as informações a 30 dias. Uma *dimensão* fornece o contexto para os factos. Enquanto os factos medem o que aconteceu, as dimensões indicam a quem aconteceu. As tabelas de dimensão, tal como a tabela **Utilizador**, são mais pequenas e podem conservar dados por períodos de tempo mais longos, comparativamente às tabelas de factos.

Um modelo de esquema de estrela é otimizado para flexibilidade e análise de dados para que possa criar os relatórios necessários para compreender o seu ambiente móvel em evolução.

## <a name="time-daily-snapshots"></a>Hora: instantâneos diários

O armazém fica a jusante dos dados do Intune. O Intune cria um instantâneo diário à meia-noite (UTC) e guarda-o no armazém. A duração da retenção dos instantâneos varia conforme as tabelas de factos. Algumas podem reter os dados durante sete dias, outras 30 dias e algumas durante períodos mais longos.

## <a name="next-steps"></a>Passos seguintes

- Para saber mais sobre como o armazém de dados controla a duração de um utilizador no Intune, veja [Representação da duração do utilizador no Armazém de Dados do Intune](reports-ref-user-timeline.md).
- Para saber mais sobre trabalhar com armazéns de dados, veja [Create First Data WareHouse](https://www.codeproject.com/Articles/652108/Create-First-Data-WareHouse) (Criar Primeiro Armazém de Dados).
- Para saber mais sobre como trabalhar com o Power BI e um armazém de dados, veja [Create a new Power BI report by importing a dataset (Criar um novo relatório do Power BI através da importação de um conjunto de dados)](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/). 
