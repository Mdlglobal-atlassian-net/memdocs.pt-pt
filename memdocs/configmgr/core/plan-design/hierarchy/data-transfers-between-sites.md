---
title: Transferências de dados entre sites
titleSuffix: Configuration Manager
description: Saiba como o Gestor de Configuração movimenta dados entre sites e como pode gerir a transferência dos dados através da sua rede.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720213"
---
# <a name="data-transfers-between-sites"></a>Transferências de dados entre sites

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração utiliza replicação baseada *em ficheiros* e *replicação* de bases de dados para transferir diferentes tipos de informação entre sites. Saiba como o Gestor de Configuração movimenta dados entre sites e como pode gerir a transferência de dados através da sua rede.  

## <a name="types-of-replication"></a>Tipos de replicação

### <a name="file-based-replication"></a><a name="bkmk_fileroute" />Replicação baseada em ficheiros

O Gestor de Configuração utiliza replicação baseada em ficheiros para transferir dados baseados em ficheiros entre sites da sua hierarquia. Estes dados incluem aplicações e pacotes que pretende implementar para pontos de distribuição em sites infantis. Também lida com os registos de dados de descoberta não processados que o site transfere para o seu site-mãe e, em seguida, processa.  

Para mais informações, consulte a [replicação baseada em Ficheiros](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" />Replicação de base de dados

A replicação da base de dados do Gestor de Configuração utiliza o Servidor SQL para transferir dados. Utiliza este método para fundir alterações na sua base de dados do site com a informação da base de dados de outros sites da hierarquia.

Para mais informações, consulte [a replicação da Base de Dados](database-replication.md).

Para obter ajuda na resolução de problemas da replicação DoQL, consulte a [replicação SQL](../../servers/manage/replication/overview.md)de Troubleshoot .

## <a name="see-also"></a>Consulte também

[Monitorizar a replicação](../../servers/manage/monitor-replication.md)
