---
title: Reinit de replicação SQL
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar a reinicialização da replicação sQL entre os sites do Gestor de Configuração
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6207ed4eeeef892de38c85096d2cc80189214d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078566"
---
# <a name="sql-replication-reinit"></a>Reinit de replicação SQL

Numa hierarquia multi-site, o Gestor de Configuração utiliza a replicação SQL para transferir dados entre sites. Para mais informações, consulte [a replicação da Base de Dados](../../../plan-design/hierarchy/database-replication.md).

Utilize o seguinte diagrama para iniciar a reinicialização da replicação SQL (reinit):

![Diagrama para resolução de problemas de replicação SQL reinit](media/sql-replication-reinit.svg)

## <a name="queries"></a>Consultas

Este diagrama utiliza as seguintes consultas:

### <a name="check-if-site-is-in-maintenance-mode"></a>Verifique se o site está em modo de manutenção

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>Verifique qual grupo de replicação ainda não completou o reinit

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>Verifique os dados globais

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>Verifique os dados do site

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Passos seguintes

- [Reinicialização de dados globais](global-data-reinit.md)
- [Reinicialização de dados de sites](site-data-reinit.md)
- [Configuração do SQL](sql-configuration.md)
