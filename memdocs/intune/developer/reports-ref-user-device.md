---
title: Associação de Dispositivos do Utilizador – Armazém de Dados do Intune
titleSuffix: Microsoft Intune
description: A entidade UserDeviceAssociation contém associações de dispositivos do utilizador na sua organização.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 777484A7-09CE-4409-987F-76B3F87DFE93
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6127b365a04ad48a9cbaa98bdef821c4d1334181
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79325573"
---
# <a name="reference-for-user-device-association-entity"></a>Referência para a entidade Associação de Dispositivo do Utilizador

A entidade **userDeviceAssociation** contém associações de dispositivos de utilizador na sua organização.

## <a name="userdeviceassociations"></a>userDeviceAssociations


|        Nome        |                                           Descrição                                            |        Exemplo         |
|--------------------|--------------------------------------------------------------------------------------------------|------------------------|
|      userKey       |              Identificador exclusivo do utilizador no armazém de dados. (Chave de substituição).               |          123           |
|     dispositivoChave      |                      Identificador exclusivo do dispositivo no armazém de dados.                      |          123           |
| criadoDateTimeUTC |           Data e hora em que a associação de dispositivos do utilizador foi criada. Utiliza o formato UTC.           | 11/23/2016 12:00:00 AM |
|     isDeleted      | Indica que o utilizador anulou a inscrição desse dispositivo e essa associação já não está atualizada. |       Verdadeiro/Falso       |
|  terminouDateTimeUTC  |              Data e hora em UTC em que a propriedade IsDeleted foi alterada para <strong>True</strong>.               | 23/06/2017 12:00:00 |

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre o [Intune Data Warehouse.](reports-nav-create-intune-reports.md)
