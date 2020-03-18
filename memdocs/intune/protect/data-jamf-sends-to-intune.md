---
title: Data JAMF Pro envia para Intune
titleSuffix: Microsoft Intune
description: Reveja a lista de dados que o Jamf Pro envia para o Microsoft Intune quando integrar o Jamf Pro para gerir os Macs com o Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e9b943ca03f54a976061c19f4ce60a94283640c0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329441"
---
# <a name="data-jamf-pro-sends-to-intune"></a>Dados que o Jamf Pro envia para o Intune

Quando utiliza o [Jamf Pro](https://www.jamf.com) para gerir os seus Macs de utilizadores finais com o Intune, o Jamf Pro captura informações de inventário sobre dispositivos macOS geridos. 

## <a name="data"></a>Dados  
Para obter a lista de dados que o Jamf Pro partilha com o Intune, consulte [o Apêndice: Informações](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.9.0/Appendix__Inventory_Information_Shared_with_Microsoft_Intune.html) de inventário partilhadas com a Microsoft Intune na documentação técnica do Jamf Pro. 

<!--  
Jamf Pro reports the following information to Intune:  

* Device Azure AD ID
* JAMF Inventory State (inventory state of a computer checked in with Jamf Pro within the last 24 hours)
* OS Version
* User Azure AD ID
* Encrypted (FileVault 2)
* Gatekeeper Status
* Password: minimum number of character sets
* Password expiration (days)
* Password Type - simple, alphanumeric, or unknown
* Prevent Auto Login
* Required Passcode Length
* Password: number of previous passwords to prevent reuse
* System Integrity Protection
* Last Check-In Time
* Architecture Type
* Available RAM Slots
* Battery Capacity
* Boot ROM
* Bus Speed
* Cache Size
* Device Name
* Domain Join
* Jamf ID
* MAC address
* Make
* Model
* Model Identifier
* NIC Speed
* Number of Cores
* Number of Processors
* OS
* Platform
* Processor Speed
* Processor Type
* Secondary MAC Address
* Serial Number
* SMC Version
* Total RAM
* UDID
* User Email
--> 

<!-- 
You can remove a Jamf-managed device from the Intune console by selecting **Delete** in the **All devices** view. Bulk device deletion can be enabled by selecting multiple devices and clicking **Delete**.
-->

## <a name="next-steps"></a>Próximos passos
Obtenha informações sobre como remover um dispositivo gerido pelo [Jamf nos docs Jamf Pro](https://www.jamf.com/jamf-nation/articles/80/unmanaging-computers-while-preserving-their-inventory-information). Também pode apresentar um bilhete de apoio com suporte ao [Jamf](https://www.jamf.com/support/) para obter ajuda adicional. 

