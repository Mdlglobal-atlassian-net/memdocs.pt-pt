---
title: Reinicialização de dados globais
titleSuffix: Configuration Manager
description: Use este diagrama para começar a resolução de problemas de replicação SQL reinit para dados globais numa hierarquia do Gestor de Configuração
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713633"
---
# <a name="troubleshoot-global-data-reinit"></a>Resolução de problemas de dados globais reinit

Numa hierarquia multi-site, o Gestor de Configuração utiliza a replicação SQL para transferir dados entre sites. Para mais informações, consulte [a replicação da Base de Dados](../../../plan-design/hierarchy/database-replication.md).

Utilize o seguinte diagrama para iniciar a reinicialização da replicação SQL (reinit) para dados globais numa hierarquia do Gestor de Configuração:

![Diagrama para resolver problemas com a reinita de dados globais](media/global-data-reinit.svg)

## <a name="queries"></a>Consultas

Este diagrama utiliza as seguintes consultas:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Verifique se a replicação do site ainda não terminou de reinit

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Obtenha o Estado de & do TrackingGuid a partir do local principal

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Obtenha o Estado de & trackingGuid do CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>Verifique o estado do pedido para o ID de rastreio

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Passos seguintes

- [Mensagem em falta de reinicialização](reinit-missing-message.md)
