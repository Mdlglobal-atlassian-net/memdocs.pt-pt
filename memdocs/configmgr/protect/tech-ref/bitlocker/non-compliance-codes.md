---
title: Códigos de não conformidade
titleSuffix: Configuration Manager
description: Uma referência técnica para os possíveis códigos de um cliente do Gestor de Configuração que não está em conformidade com a política do BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722054"
---
# <a name="non-compliance-codes"></a>Códigos de não conformidade

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

O WMI no cliente fornece os seguintes códigos de incumprimento. Também descreve as razões pelas quais um determinado dispositivo relata como incompatível.

Existem vários métodos para visualizar o WMI. Por exemplo, utilize o seguinte comando PowerShell:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Se o dispositivo estiver em conformidade, este comando não devolve nada.
>
> Também pode verificar `Compliant` o atributo desta `1` classe, que é se o dispositivo estiver em conformidade.

|Código de incumprimento|Razão para o incumprimento|
|--- |--- |
|0|Força cifra, não AES 256.|
|1|A política bitLocker requer que este volume seja encriptado, mas não é.|
|2|A política bitLocker exige que este volume *não* seja encriptado, mas é.|
|3|A política bitLocker requer que este volume use um protetor TPM, mas não o faz.|
|4|A política BitLocker requer que este volume utilize um protetor TPM+PIN, mas não o faz.|
|5|A política bitLocker não permite que as máquinas não-TPM apresentem relatórios como conformes.|
|6|O volume tem um protetor TPM, mas o TPM não é visível.|
|7|A política bitLocker requer que este volume utilize um protetor de senha, mas não tem uma.|
|8|A política bitLocker requer que este volume *não* utilize um protetor de palavra-passe, mas tem um.|
|9|A política bitLocker requer que este volume utilize um protetor de desbloqueio automático, mas não tem um.|
|10|A política bitLocker requer que este volume *não* utilize um protetor de desbloqueio automático, mas tem um.|
|11|O BitLocker deteta um conflito político, o que o impede de reportar este volume como conforme.|
|12|É necessário um volume de sistema para encriptar o volume de S, mas não está presente.|
|13|A proteção está suspensa pelo volume.|
|14|O protetor de desbloqueio automático não é seguro a menos que o volume de S seja encriptado.|
|15|A política requer a força mínima da cito é xTS-AES-128 bit, a força real da cito é mais fraca.|
|16|A política requer a força mínima da cito é xTS-AES-256 bit, a força real da cito é mais fraca.|
