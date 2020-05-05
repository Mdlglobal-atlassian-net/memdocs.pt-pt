---
title: Reinicialização de dados de sites
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar a resolução de problemas de replicação SQL reinit para dados do site numa hierarquia do Gestor de Configuração
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078600"
---
# <a name="troubleshoot-site-data-reinit"></a>Reinit de dados do site de resolução de problemas

Numa hierarquia multi-site, o Gestor de Configuração utiliza a replicação SQL para transferir dados entre sites. Para mais informações, consulte [a replicação da Base de Dados](../../../plan-design/hierarchy/database-replication.md).

Utilize o seguinte diagrama para iniciar a reinicialização da replicação SQL (reinit) para os dados do site numa hierarquia do Gestor de Configuração:

![Diagrama para resolver problemas de dados do site reinit](media/site-data-reinit.svg)

## <a name="queries"></a>Consultas

Este diagrama utiliza as seguintes consultas:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Verifique se a replicação do site ainda não terminou de reinit

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Obtenha o Estado de & trackingGuid do CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Obtenha o Estado de & do TrackingGuid a partir do local principal

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Verifique se o local primário não está em modo de manutenção

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>Verifique o estado do pedido para o ID de rastreio

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Passos seguintes

- [Mensagem em falta de reinicialização](reinit-missing-message.md)
- [Reinicialização de dados globais](global-data-reinit.md)
