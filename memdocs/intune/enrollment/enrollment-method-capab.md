---
title: Funcionalidades do método de inscrição do Intune para dispositivos Windows
titleSuffix: Microsoft Intune
description: Funcionalidades de cada método de inscrição para dispositivos Windows.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/21/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b9dca2303d960937a529a902391d6c05539fc9d4
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331549"
---
# <a name="intune-enrollment-method-capabilities-for-windows-devices"></a>Funcionalidades do método de inscrição do Intune para dispositivos Windows
[!INCLUDE[azure_portal](../includes/azure_portal.md)]

Existem vários métodos para inscrever os dispositivos da sua força de trabalho em Intune. Cada método possui diferentes funcionalidades e melhores práticas, conforme demonstrado nas tabelas abaixo.

## <a name="best-practices-by-enrollment-method"></a>Melhores práticas por método de inscrição
| **Melhores práticas** | **[Azure AD associado](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Microsoft Azure AD associado ao Autopilot (Modo orientado pelo utilizador)](enrollment-autopilot.md)** |**[Microsoft Azure AD associado ao Autopilot (Modo de implementação automática)](enrollment-autopilot.md)** |**[Em massa](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Cogestão](https://docs.microsoft.com/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Utilizados habitualmente no Intune for Education|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Dispositivos que podem ser utilizados como dispositivos partilhados|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Dispositivos pessoais que têm de aceder a recursos da empresa|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Gestão personalizada de aplicações|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>Funcionalidades por método de inscrição

| **Capacidades** | **[Azure AD associado](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Microsoft Azure AD associado ao Autopilot (Modo orientado pelo utilizador)](enrollment-autopilot.md)** |**[Microsoft Azure AD associado ao Autopilot (Modo de implementação automática)](enrollment-autopilot.md)** |**[Em massa](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Cogestão](https://docs.microsoft.com/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Acesso Condicional                                      |![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)\*\*|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|
|O utilizador é associado ao dispositivo                    |![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|
|Requer o Azure AD Premium                               |![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|
|O dispositivo pode avaliar os recursos protegidos por AC             |![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|
|Os utilizadores não podem ser administradores dos respetivos dispositivos               |![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Capacidade de configurar a experiência de configuração do dispositivo        |![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Capacidade de inscrever dispositivos sem a interação do utilizador      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|
|Capacidade de executar scripts do PowerShell                       |![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/checkmark.png)\*| 
|Suporta a inscrição automática após a associação a um domínio do AD      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|
|Suporta a inscrição automática após a associação a um domínio do Azure AD Híbrido|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|
|Suporta a inscrição automática após a associação a um domínio do Azure AD       |![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![Marca de verificação](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|

\*As cargas de trabalho das aplicações de clientes no Diretor de Configuração devem ser transferidas para Intune Pilot ou Intune.

\** [Os dispositivos estão bloqueados para acesso condicional, com exceção do Windows 10 1803+.](device-enrollment-manager-enroll.md)

## <a name="next-steps"></a>Passos seguintes

[Configurar a inscrição para dispositivos Windows](windows-enroll.md)

