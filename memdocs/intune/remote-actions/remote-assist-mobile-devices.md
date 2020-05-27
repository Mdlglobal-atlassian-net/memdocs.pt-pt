---
title: Assista remotamente dispositivos móveis geridos por Intune
description: Pode utilizar quatro opções diferentes para ajudar remotamente os utilizadores com os seus dispositivos móveis.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34f88d4e7aefe9a32238bb6d14203de0defd65ef
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988254"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Assista remotamente a dispositivos móveis geridos pelo Microsoft Endpoint Manager

Existem quatro opções disponíveis para administrar remotamente dispositivos geridos pelo Microsoft Endpoint Manager:

- [O Microsoft Teams](https://products.office.com/microsoft-teams/) é o centro de trabalho em equipa onde podes conversar, conhecer e colaborar independentemente de onde estejas.
- [Quick Assist](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) é uma aplicação do Windows 10 que permite a duas pessoas partilhar um dispositivo sobre uma ligação remota.
- [TeamViewer](https://www.teamviewer.com/) é um programa de terceiros que compra separadamente. Fornece um conjunto abrangente de capacidades de acesso e suporte remotos. A integração Intune e [TeamViewer](teamviewer-support.md) permite suporte remoto utilizando teamViewer e o conector é gerido diretamente em Intune.
- [O controlo remoto](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) está incluído no Microsoft Endpoint Configuration Manager. É usado para administrar remotamente, fornecer assistência ou visualizar qualquer computador de grupo de trabalho e computador de domínio.

| Funcionalidades, Plataformas, Licenciamento | **Teams** | Assistência Rápida | TeamViewer (Intune) | Controlo remoto (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Vista e controlo remoto |![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Chat |![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Transferência de ficheiros |![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Acesso administrativo elevado |||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Acesso não acompanhado |||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Controlo remoto simultâneo |![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Suporte para múltiplos utilizadores |||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Ações remotas ||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Suporte over-the-internet |![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Relatórios de auditoria |![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Suporte para todas as plataformas (Windows, iOS, Android, macOS) |![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Integrado com o Windows 10 – não é necessária nenhuma aplicação adicional ||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Requer que o dispositivo seja cogerido pelo Gestor de Configuração e pelo Intune ||||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Requer licenciamento adicional\* |![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)||![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificação](../enrollment/media/enrollment-method-capab/checkmark.png)|

\*As equipas exigem o licenciamento O365 ou M365. A utilização do TeamViewer e intune requer o licenciamento tanto do TeamViewer como do Intune. Controlo Remoto é uma funcionalidade do Gestor de Configuração e requer licenciamento do Gestor de Configuração.
