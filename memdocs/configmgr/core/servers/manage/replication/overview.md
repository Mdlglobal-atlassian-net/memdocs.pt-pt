---
title: Resolver problemas de replicação do SQL
titleSuffix: Configuration Manager
description: Use estes diagramas para ajudar a compreender e resolver problemas a replicação do SQL entre sites do Gestor de Configuração
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720472"
---
# <a name="troubleshoot-sql-replication"></a>Resolver problemas de replicação do SQL

Numa hierarquia multi-site, o Gestor de Configuração utiliza a replicação SQL para transferir dados entre sites. Para mais informações, consulte [a replicação da Base de Dados](../../../plan-design/hierarchy/database-replication.md).

Para melhor compreender e ajudar a resolver problemas com a replicação do SQL, use estes diagramas.

- [Replicação do SQL](sql-replication.md)
- [Configuração do SQL](sql-configuration.md)
- [Desempenho do SQL](sql-performance.md)
- [Reinicialização da replicação do SQL](sql-replication-reinit.md)
- [Reinicialização de dados globais](global-data-reinit.md)
- [Reinicialização de dados de sites](site-data-reinit.md)
- [Mensagem em falta de reinicialização](reinit-missing-message.md)

Estes diagramas de resolução de problemas estão interligados. Use o seguinte diagrama para entender as suas relações:

![Diagrama de visão geral do processo para resolução de problemas de replicação SQL](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Para mais informações, consulte as seguintes séries de blogs do Microsoft Support:

- [ConfigMgr DRS Synchronization Internals](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [ConfigMgr 2012 Serviço de Replicação de Dados (DRS) Desencadeado](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS – Perguntas de resolução de problemas](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [Internos de Inicialização configMgr 2012 DRS](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012: Problemas de certificado sql e corretor de serviços SQL](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
