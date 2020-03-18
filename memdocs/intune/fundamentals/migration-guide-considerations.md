---
title: Considerações especiais sobre a migração
titleSuffix: Microsoft Intune
description: Este artigo fornece considerações especiais sobre a migração antes de iniciar uma campanha de migração para o Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f29d2894-e98b-4f2c-b444-a8ccc1b7efdd
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a954732b2df5824d7116dc10e035b10290c0290
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331245"
---
# <a name="special-migration-considerations"></a>Considerações especiais sobre a migração

Existem considerações especiais sobre a migração que podem ser aplicáveis, dependendo do ambiente do fornecedor de MDM existente.

## <a name="wipe-for-apples-device-enrollment-program-dep"></a>Limpeza para programa de inscrição de dispositivos da Apple (DEP)

O Programa de Inscrição de Dispositivos (DEP) da Apple define configurações do dispositivo que não podem ser removidas pelo utilizador final. Para manter as funcionalidades da gestão avançada do DEP, o dispositivo tem de voltar ao estado inicial (novo) através da eliminação dos dados do mesmo para a inscrição no Intune.

Para continuar a utilizar o DEP para gerir os dispositivos em Intune, configurar a inscrição do [dispositivo iOS/iPadOS com o Programa de Inscrição](../enrollment/device-enrollment-program-enroll-ios.md)de Dispositivos .

## <a name="next-steps"></a>Próximos passos

[Fase 2: campanha de migração](migration-guide-campaign.md)
