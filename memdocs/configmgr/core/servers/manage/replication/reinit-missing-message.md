---
title: Mensagem em falta de reinicialização
titleSuffix: Configuration Manager
description: Use este diagrama para começar a resolver uma mensagem em falta com reinit de replicação SQL no Gestor de Configuração
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720465"
---
# <a name="reinit-missing-message"></a>Mensagem em falta de reinicialização

Numa hierarquia multi-site, o Gestor de Configuração utiliza a replicação SQL para transferir dados entre sites. Para mais informações, consulte [a replicação da Base de Dados](../../../plan-design/hierarchy/database-replication.md).

Utilize o diagrama seguinte para começar a resolver uma mensagem em falta com reinicialização da replicação SQL (reinita):

![Diagrama para resolução de problemas reinite mensagem em falta](media/reinit-missing-message.svg)

## <a name="queries"></a>Consultas

Este diagrama utiliza as seguintes consultas:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Verifique se a replicação do site ainda não terminou de reinit

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>Obtenha o Status de & TrackingGuid a partir do site do assinante

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>Obtenha o Status de & TrackingGuid a partir do site editorial

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Ações de remediação

### <a name="version-1902-and-later"></a>Versão 1902 e mais tarde

Para detetar o problema e reinitar, execute o Analisador de Ligação de [Replicação](../monitor-replication.md#BKMK_RLA).

### <a name="version-1810-and-earlier"></a>Versão 1810 e mais cedo

Faça a seguinte consulta SQL `ReplicationGroupID`para obter o :

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Em seguida, utilize o `InitializeData` método na classe `SMS_ReplicationGroup` WMI com os seguintes valores:

- ReplicationGroupID: a partir da consulta SQL acima
- SiteCode1: site dos pais
- SiteCode2: site infantil

Para obter mais informações, consulte o [método InitializeData na classe SMS_ReplicationGroup](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md).

#### <a name="example"></a>Exemplo

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Passos seguintes

- [Reinicialização da replicação do SQL](sql-replication-reinit.md)
