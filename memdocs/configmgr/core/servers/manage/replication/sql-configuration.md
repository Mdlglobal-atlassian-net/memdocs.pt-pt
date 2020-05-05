---
title: Configuração do SQL
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar a resolução de problemas da configuração SQL para O Gestor de Configuração
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723230"
---
# <a name="sql-configuration"></a>Configuração do SQL

Numa hierarquia multi-site, o Gestor de Configuração utiliza a replicação SQL para transferir dados entre sites. Para mais informações, consulte [a replicação da Base de Dados](../../../plan-design/hierarchy/database-replication.md).

Utilize o seguinte diagrama para iniciar a resolução de problemas da configuração SQL relacionada com o Corretor de ServiçoS SQL:

![Diagrama para resolução de problemas da configuração SQL](media/sql-configuration.svg)

## <a name="queries"></a>Consultas

Este diagrama tem as seguintes consultas e ações:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>Verifique se o SQL pode entregar mensagens SSB

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Ações de remediação

### <a name="remediate-the-issues-reported-from-transmission_status"></a>Remediar as questões reportadas a partir de transmission_status

Questões comuns:

- Configuração da firewall
- Configuração da rede
- Certificado SSB mal configurado

### <a name="run-sql-profiler-to-trace-ssb-events"></a>Executar o perfil SQL para rastrear eventos SSB

Executar o perfil SQL no CAS e na base de dados do site primário para rastrear eventos relacionados com o Corretor de ServiçoS SQL:

- **Login de corretor de auditoria**
- **Conversa de corretor de auditoria**
- Eventos na categoria **Broker**
