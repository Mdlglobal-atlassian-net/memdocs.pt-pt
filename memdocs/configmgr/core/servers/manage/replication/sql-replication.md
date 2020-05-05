---
title: Replicação do SQL
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar a resolução de problemas da replicação do SQL entre os sites do Gestor de Configuração
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717525"
---
# <a name="sql-replication"></a>Replicação do SQL

Numa hierarquia multi-site, o Gestor de Configuração utiliza a replicação SQL para transferir dados entre sites. Para mais informações, consulte [a replicação da Base de Dados](../../../plan-design/hierarchy/database-replication.md).

Utilize o seguinte diagrama para iniciar a resolução de problemas da replicação DoQL quando uma ligação falha:

![Diagrama para resolução de problemas da replicação do SQL](media/sql-replication.svg)

## <a name="queries"></a>Consultas

Este diagrama utiliza as seguintes consultas:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>Verifique se a ligação do grupo de replicação está em estado degradado ou falhado

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>Verifique se a ligação do grupo de replicação é calculada recentemente

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>Verifique o modo de manutenção SQL

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Passos seguintes

- [Reinicialização da replicação do SQL](sql-replication-reinit.md)
- [Desempenho do SQL](sql-performance.md)
- [Configuração do SQL](sql-configuration.md)
