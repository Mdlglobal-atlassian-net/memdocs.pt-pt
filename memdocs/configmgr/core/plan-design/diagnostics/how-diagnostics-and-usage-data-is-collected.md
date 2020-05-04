---
title: Recolha de dados de diagnóstico
titleSuffix: Configuration Manager
description: Saiba como o Gestor de Configuração recolhe diagnósticos e dados de utilização sobre si mesmo.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709538"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Como o Gestor de Configuração recolhe dados de diagnóstico e de utilização

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para recolher dados de diagnóstico e utilização para O Gestor de Configuração, cada site primário executa consultas de Servidor SQL semanalmente. Numa hierarquia multilocal, os dados são replicados para o site de administração central.  

No local de alto nível de uma hierarquia, o ponto de ligação de serviço submete esta informação quando verifica as atualizações. O modo do ponto de ligação de serviço determina como os dados são transferidos:

- **Online**: Uma vez por semana, o ponto de ligação ao serviço envia automaticamente dados de diagnóstico e utilização para o serviço na nuvem.

- **Offline**: Transfere manualmente os diagnósticos e os dados de utilização com a ferramenta de [ligação](../../servers/manage/use-the-service-connection-tool.md)ao serviço .

Para mais informações, consulte sobre o ponto de [ligação ao serviço](../../servers/deploy/configure/about-the-service-connection-point.md).

> [!div class="nextstepaction"]
> [Como visualizar diagnósticos e dados de utilização](view-diagnostics-and-usage-data.md)
