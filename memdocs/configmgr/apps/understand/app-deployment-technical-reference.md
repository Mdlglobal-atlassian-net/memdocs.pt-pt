---
title: Referência técnica de implementação de aplicações de resolução de problemas
titleSuffix: Configuration Manager
description: Referência técnica para implementação de aplicações de resolução de problemas no Gestor de Configuração.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709818"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Referência técnica para implementação de aplicações no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Neste artigo, você vai aprender como as implementações de aplicações funcionam.

## <a name="before-you-begin"></a>Antes de Começar

Ao resolver implementações de aplicações de resolução de problemas, existem vários itens que podem ser úteis ao rever os registos dos clientes. Estes itens incluem:

- Id CI de aplicação
- Id exclusivo da aplicação
- Id único do tipo de implementação
- Id exclusivo de implementação de aplicações (também conhecido como ID exclusivo de atribuição)
- Finalidade de implementação de aplicações
- Id exclusivo do conteúdo
- ID e nome da coleção
- Tipo de recolha

Para simplificar a resolução de problemas, pode executar uma consulta SQL semelhante à abaixo contra a base de dados do Gestor de Configuração para obter as informações listadas acima.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> Quando executa esta consulta, **deve** utilizar o Nome da Aplicação listado no separador Informação Geral das Propriedades da Aplicação, em vez de utilizar o nome de aplicação localizado listado no separador Software Center das propriedades da Aplicação.

## <a name="next-steps"></a>Passos Seguintes

- [Política de Implementação de Aplicações](deployment-policy-technical-reference.md)
