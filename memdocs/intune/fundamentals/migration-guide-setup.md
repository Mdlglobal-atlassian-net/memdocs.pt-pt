---
title: Configuração básica do Microsoft Intune
description: Este artigo fornece os passos necessários para configurar o Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60cfa440-0723-4ea0-bacf-3c5d26f9a1d3
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b7784d4ad86e3418259f85ca1c4577d2289dc86
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331193"
---
# <a name="basic-setup"></a>Configuração básica

Depois de avaliar o seu ambiente, é hora de configurar o Microsoft Intune.

## <a name="external-dependencies-for-an-intune-deployment"></a>Dependências externas para uma implementação do Intune

### <a name="identity"></a>Identidade

O Intune precisa do Azure Active Directory (AAD) como o fornecedor de identidades e de agrupamentos de utilizadores. Saiba mais sobre:

- [Requisitos de identidade](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview#design-considerations-overview)

- [Requisitos de sincronização do diretório](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements)

- [Multi-Factor Authentication (MFA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks)

- [Planear os grupos de utilizadores e de dispositivos](users-add.md)

- [Como criar grupos de utilizadores e dispositivos](groups-get-started.md)

Se a sua organização já estiver a utilizar o Office 365, o Intune terá de utilizar o mesmo ambiente do Azure Active Directory.

### <a name="pki-optional"></a>PKI (opcional)

Se estiver a planear utilizar a autenticação baseada em certificados para perfis vpn, Wi-Fi ou e-mail com intune, terá de se certificar de que tem uma infraestrutura PKI suportada [no local,](../protect/certificates-configure.md)pronta para criar e implementar perfis de certificado. Saiba mais sobre a configuração de certificados no Intune:

- [Como configurar a infraestrutura de certificados para o SCEP](/intune/certificates-scep-configure)

- [Como configurar a infraestrutura de certificados para PFX](/intune/certficates-pfx-configure).

## <a name="task-list-for-an-intune-setup"></a>Lista de tarefas para uma configuração do Intune

### <a name="task-1-intune-subscription"></a>Tarefa 1: Subscrição do Intune

Antes de poder migrar para Intune, primeiro precisa de uma [subscrição Intune](account-sign-up.md).

### <a name="task-2-assign-intune-user-licenses"></a>Tarefa 2: Atribuir licenças de utilizador do Intune

- Saiba [como atribuir licenças de utilizador do Intune](licenses-assign.md).

- Se tiver criado um novo inquilino do Azure Active Directory, saiba [como criar novos utilizadores ou sincronizar o utilizador a partir do seu Active Directory (AD) no local.](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)

### <a name="task-3-set-your-mdm-authority-to-intune"></a>Tarefa 3: Definir a autoridade MDM para o Intune

Recomendamos que gere o Intune utilizando o centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Defina a sua autoridade de MDM para **Insinton .** A utilização de uma autoridade MDM diferente permite ao Intune transferir a gestão de MDM para consolas de gestão da Microsoft alternativas. Estes casos são pouco comuns.

> [!IMPORTANT]
> Se estiver a transferir a gestão de dispositivos móveis para o Intune pela primeira vez, deverá definir a autoridade MDM para o Intune.

Saiba [como definir a autoridade de gestão móvel](mdm-authority-set.md).

## <a name="next-step"></a>Passo seguinte

Configure as políticas de gestão de [dispositivos e aplicações.](migration-guide-configure-policies.md)
