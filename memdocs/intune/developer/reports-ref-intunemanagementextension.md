---
title: Entidade IntuneManagementExtension
titleSuffix: Microsoft Intune
description: Tópico de referência para a categoria da Entidade IntuneManagementExtension das coleções de entidades na API do Armazém de Dados do Intune.
keywords: Armazém de Dados do Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 73DF3B90-6D52-4EF6-AFFD-1873A18C7421
ms.reviewer: dariusz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f8152eb12779376e1885d0a2b2898cd602aa825d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331689"
---
# <a name="reference-for-intune-management-extensions"></a>Referência para extensões de gestão intune

A categoria **intuneManagementExtensions** contém entidades para dispositivos móveis que rastreiam informações como:

- Versões de uma IntuneManagementExtension
- Estado da instalação de uma IntuneManagementExtension

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions

A entidade **intuneManagementExtensionVersion** lista todas as versões utilizadas por intuneManagementExtensions.

| Propriedade  | Descrição | Exemplo |
|---------|------------|--------|
| extensãoVersionKey |Identificador único da versão intuneManagementExtensions. | 1 |
| extensãoVersão |O número da versão de quatro dígitos. |1.0.2.0 |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates

O **intuneManagementExtensionHealthState** lista todos os possíveis estados de saúde das extensões intuneManagementExtensions.

| Propriedade  | Descrição | Exemplo |
|---------|------------|--------|
| extensãoStateKey |Identificador exclusivo do estado de funcionamento. | 2 |
| extensãoEstado |Estado de funcionamento de uma IntuneManagementExtension. | Healthy |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions

A **intuneManagementExtension** lista a saúde intuneManagementExtensions em cada dispositivo Windows 10 por dia.
Os dados são mantidos relativamente aos últimos 60 dias. 


|      Propriedade       |                         Descrição                         | Exemplo |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               Identificador exclusivo da Data.                |   123   |
|      inquilinoChave      |              Identificador exclusivo do Inquilino.               |   456   |
|      dispositivoChave      |              Identificador exclusivo do Dispositivo.               |   789   |
| extensãoVersionKey | Identificador único da versão intuneManagementExtension. |    1    |
|  extensãoStateKey  |             Identificador exclusivo do estado de funcionamento.              |    2    |

