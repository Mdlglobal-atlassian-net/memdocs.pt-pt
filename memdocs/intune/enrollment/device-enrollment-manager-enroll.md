---
title: Inscrever dispositivos com uma conta do gestor de inscrição de dispositivos
titleSuffix: Microsoft Intune
description: Utilize a conta do gestor de inscrição de dispositivos para inscrever dispositivos no Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb5dec2fd96c5b5dfe0b82bb30bf653250786c95
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986771"
---
# <a name="enroll-devices-in-intune-by-using-a-device-enrollment-manager-account"></a>Inscreva dispositivos em Intune utilizando uma conta de gestor de inscrição de dispositivos

Pode inscrever até 1000 dispositivos móveis com uma única conta do Azure Active Directory ao utilizar uma conta do gestor de inscrição de dispositivos (DEM). O DEM é uma permissão do Intune que pode ser aplicada a uma conta de utilizador do AAD e que permite que o utilizador inscreva até 1000 dispositivos. Uma conta DEM é útil para cenários onde os dispositivos são inscritos e preparados antes de serem distribuídos aos utilizadores. Por design, há um limite de 150 contas de Gestor de Inscrição de Dispositivos (DEM) no Microsoft Intune.

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>Limitações dos dispositivos inscritos com uma conta DEM

As contas de utilizador DEM e os dispositivos que estão inscritos com uma conta de utilizador DEM têm as seguintes limitações:

- Um utilizador de conta DEM deve ser atribuído a uma licença Intune.
- A limpeza não pode ser feita a partir do Portal da Empresa. A limpeza de um dispositivo inscrito por uma conta de utilizador DEM pode ser feita no portal do Azure a partir do Intune.
- Apenas o dispositivo local é apresentado na aplicação Portal da Empresa ou do site.
- As contas de utilizador de DEM não podem utilizar aplicações do Apple Volume Purchase Program (VPP) com licenças de utilizador Apple VPP devido aos requisitos de ID da Apple por utilizador para a gestão de apps.
- As contas DEM não podem ser utilizadas ao inscrever dispositivos através da Inscrição automática de Dispositivos da Apple (ADE).
- Os dispositivos podem instalar as aplicações VPP se tiverem licenças do dispositivo Apple VPP.
- Os dispositivos estão bloqueados para acesso condicional, com exceção do Windows 10 1803+
- Todos os dispositivos matriculados nas contas DEM têm de ser devidamente licenciados para serem geridos pela Intune. A licença pode ser uma licença de utilizador Intune ou uma licença de dispositivo Intune.
- Se estiver [a inscrever dispositivos](android-work-profile-enroll.md) de perfil de trabalho Android Enterprise utilizando uma conta DEM, existe um limite de 10 dispositivos que podem ser matriculados por conta.
- [A inscrição de dispositivos geridos pela Android Enterprise com](android-fully-managed-enroll.md) contas DEM não é suportada.
- A aplicação de uma restrição de dispositivo AD Azure a uma conta DEM impedirá que atinja o limite de 1.000 dispositivos que a conta DEM pode inscrever.

## <a name="enrollment-methods-supported-by-dem-accounts"></a>Métodos de inscrição suportados pelas contas DEM

Pode utilizar os seguintes métodos para inscrever dispositivos utilizando contas DEM:

- [Windows Autopilot](enrollment-autopilot.md)
- [Inscrições a granel dos dispositivos Windows](windows-bulk-enroll.md)
- DEM iniciado via Portal da Empresa

## <a name="add-a-device-enrollment-manager"></a>Adicionar um gestor de inscrição de dispositivos

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha os **gestores**de inscrição de  >  **dispositivos de dispositivos de**  >  **inscrição**de dispositivos .

2. Selecione **Adicionar**.

3. No painel **Adicionar Utilizador**, introduza um nome principal para o utilizador DEM e selecione **Adicionar**. O utilizador DEM é adicionado à lista de utilizadores DEM.

## <a name="permissions-required-to-create-dem-accounts"></a>Permissões necessárias para criar contas DEM

As funções de Administrador Global ou Administrador de Serviço do Intune no Azure AD são necessárias para:
- Atribuir uma permissão de DEM a uma conta de utilizador do Azure AD
- Ver todos os utilizadores DEM

Se um utilizador não tiver uma função de Administrador Global ou Administrador de Serviço do Intune atribuída, mas tiver permissões de leitura ativadas para a função de Gestores de Inscrição de Dispositivos atribuída ao mesmo, só poderá ver os utilizadores DEM que criou.

## <a name="remove-device-enrollment-manager-permissions"></a>Remover as permissões de gestor de inscrição de dispositivos

A remoção de um gestor de inscrição de dispositivos não afeta os dispositivos inscritos.

**Para remover um gestor de inscrição de dispositivos**

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha os **gestores**de inscrição de  >  **dispositivos de dispositivos de**  >  **inscrição**de dispositivos .
2. No painel **Gestores de inscrições de dispositivos**, selecione o gestor de inscrição de dispositivos e selecione **Eliminar**.

