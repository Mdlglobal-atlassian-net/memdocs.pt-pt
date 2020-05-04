---
title: Inscrever dispositivos Android no Intune
titleSuffix: Microsoft Intune
description: Saiba como inscrever dispositivos Android no Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/23/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f276d98c-b077-452a-8835-41919d674db5
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d3d179af4a531134a543b070e5e70731231eda2c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79325489"
---
# <a name="enroll-android-devices"></a>Inscrever dispositivos Android

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Como administrador intune, pode inscrever dispositivos Android das seguintes formas:
- Android Enterprise (oferecendo um conjunto de opções de inscrição que fornecem aos utilizadores as funcionalidades mais atualizadas e seguras):
    - [**Perfil de trabalho android Enterprise**](android-work-profile-enroll.md): Para dispositivos pessoais, foi autorizada a aceder a dados corporativos. Os administradores podem gerir contas de trabalho, apps e dados. Os dados pessoais do dispositivo são mantidos separados dos dados de trabalho e os administradores não controlam as definições ou dados pessoais. 
    - [**Android Enterprise dedicado**](android-kiosk-enroll.md): Para dispositivos de uso único, propriedade corporativa, como sinalização digital, impressão de bilhetes ou gestão de inventário. Os administradores bloqueiam a utilização de um conjunto limitado de aplicações e ligações Web num dispositivo. Além disso, também impede os utilizadores de adicionarem outras aplicações ou de efetuarem outras ações no dispositivo.
    - [**Android Enterprise totalmente gerido**](android-fully-managed-enroll.md): Para dispositivos de utilizador único e corporativos usados exclusivamente para trabalho e não para uso pessoal. Os administradores podem gerir todo o dispositivo e impor controlos políticos indisponíveis para perfis de trabalho. 
- [**Administrador de dispositivos Android**](android-enroll-device-administrator.md), incluindo dispositivos Samsung Knox Standard e [dispositivos Zebra.](../configuration/android-zebra-mx-overview.md) 

## <a name="prerequisites"></a>Pré-requisitos

Para se preparar para gerir dispositivos móveis, tem de definir a autoridade de gestão de dispositivos móveis (MDM) para o **Microsoft Intune**. Veja [Set the MDM authority (Definir a autoridade de MDM)](../fundamentals/mdm-authority-set.md) para obter instruções. Este item só é definido uma vez, quando está a configurar pela primeira vez o Intune para a gestão de dispositivos móveis.

Para dispositivos fabricados pela Zebra Technologies, poderá ser necessário conceder ao Portal da Empresa permissões adicionais dependendo das capacidades do dispositivo específico. [Extensões de Mobilidade em dispositivos Zebra](../configuration/android-zebra-mx-overview.md) tem mais detalhes.

Para os dispositivos Samsung Knox Standard, existem [mais pré-requisitos.](android-samsung-knox-mobile-enroll.md)

## <a name="next-steps"></a>Passos seguintes

- [Configurar as inscrições de perfil de trabalho do Android Enterprise](android-work-profile-enroll.md)
- [Configurar inscrições de dispositivos dedicados ao Android Enterprise](android-kiosk-enroll.md)
- [Configurar as matrículas do Android Enterprise totalmente geridas](android-fully-managed-enroll.md)
- [Configurar a inscrição do administrador do dispositivo Android](android-enroll-device-administrator.md)

