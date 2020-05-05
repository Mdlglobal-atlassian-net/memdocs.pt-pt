---
title: Pré-requisitos para a criação de relatórios
titleSuffix: Configuration Manager
description: Compreenda várias dependências que impactam o seu uso de relatórios no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e08833a5ef560a0f958fe68b4ade0d4717dffc73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720143"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Pré-requisitos para reporte no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O relatório em Configuração Gestor tem as seguintes dependências:

- SQL Server Reporting Services
- Ponto do Reporting Services
- Power BI Report Server (opcional, a partir da versão 2002)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Antes de poder utilizar relatórios no Gestor de Configuração, instale e configure os Serviços de Reporte do Servidor SQL.

Para obter mais informações sobre planeamento e implementação de Serviços de Reporte, consulte os Serviços de Relato do [Servidor SQL](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).

Instale a base de dados dos Serviços de Informação na instância predefinida ou numa instância nomeada de uma instalação do SQL Server de 64 bits. Colocaa a instância do Servidor SQL com o servidor do sistema do site ou configure-a num computador remoto.

O Gestor de Configuração suporta as mesmas versões do SQL Server para reportar como faz para a base de dados do site. Para mais informações, consulte [as versões Suportadas Do Servidor SQL](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Ponto do Reporting Services

Antes de poder utilizar relatórios no Configurmanager, configure a função do sistema de pontos de ponto de serviços de reporte.

Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint).

## <a name="power-bi-report-server"></a>Power BI Report Server

A partir da versão 2002, pode integrar relatórios com o Power BI Report Server. Para mais informações, incluindo pré-requisitos, consulte [Integrar com o Power BI Report Server](powerbi-report-server.md).

## <a name="next-steps"></a>Passos seguintes

[Configurar relatórios](configuring-reporting.md)
