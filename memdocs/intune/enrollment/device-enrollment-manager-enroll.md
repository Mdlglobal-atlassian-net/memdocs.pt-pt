---
title: Inscrever dispositivos com uma conta do gestor de inscrição de dispositivos
titleSuffix: Microsoft Intune
description: Utilize a conta do gestor de inscrição de dispositivos para inscrever dispositivos no Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
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
ms.openlocfilehash: e6b0c901cd52edcd674a2d787bc703c371dcf519
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327142"
---
# <a name="enroll-devices-in-intune-by-using-a-device-enrollment-manager-account"></a>Inscrever dispositivos no Intune ao utilizar uma conta de Gestor de inscrição de dispositivos

Pode inscrever até 1000 dispositivos móveis com uma única conta do Azure Active Directory ao utilizar uma conta do gestor de inscrição de dispositivos (DEM). O DEM é uma permissão do Intune que pode ser aplicada a uma conta de utilizador do AAD e que permite que o utilizador inscreva até 1000 dispositivos. Uma conta DEM é útil para cenários onde os dispositivos são inscritos e preparados antes de serem distribuídos aos utilizadores. Por design, há um limite de 150 contas de Gestor de Inscrição de Dispositivos (DEM) no Microsoft Intune.

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>Limitações dos dispositivos inscritos com uma conta DEM

As contas de utilizador DEM e os dispositivos que estão inscritos com uma conta de utilizador DEM têm as seguintes limitações:

- Um utilizador de conta DEM deve ser atribuído a uma licença Intune.
- A limpeza não pode ser feita a partir do Portal da Empresa. A limpeza de um dispositivo inscrito por uma conta de utilizador DEM pode ser feita no portal do Azure a partir do Intune.
- Apenas o dispositivo local é apresentado na aplicação Portal da Empresa ou do site.
- As contas de utilizador de DEM não podem utilizar aplicações do Apple Volume Purchase Program (VPP) com licenças de utilizador Apple VPP devido aos requisitos de ID da Apple por utilizador para a gestão de apps.
- As contas DEM não podem ser utilizadas ao inscrever dispositivos através da Inscrição automática de Dispositivos da Apple (ADE).
- Os dispositivos podem instalar as aplicações VPP se tiverem licenças do dispositivo Apple VPP.
- Dispositivos estão bloqueados para o acesso condicional com a exceção do Windows 10 versão 1803 +
- Todos os dispositivos matriculados nas contas DEM têm de ser devidamente licenciados para serem geridos pela Intune. A licença pode ser uma licença de utilizador Intune ou uma licença de dispositivo Intune.
- Se estiver [a inscrever dispositivos](android-work-profile-enroll.md) de perfil de trabalho Android Enterprise utilizando uma conta DEM, existe um limite de 10 dispositivos que podem ser matriculados por conta.


## <a name="add-a-device-enrollment-manager"></a>Adicionar um gestor de inscrição de dispositivos

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), escolha **dispositivos** > **Inscrever dispositivos** > gestores de **inscrição do dispositivo**.

2. Selecione **Adicionar**.

3. No painel **Adicionar Utilizador**, introduza um nome principal para o utilizador DEM e selecione **Adicionar**. O utilizador DEM é adicionado à lista de utilizadores DEM.

## <a name="permissions-for-dem"></a>Permissões para DEM

As funções de Administrador Global ou Administrador de Serviço do Intune no Azure AD são necessárias para:
- Atribuir uma permissão de DEM a uma conta de utilizador do Azure AD
- Ver todos os utilizadores DEM

Se um utilizador não tiver uma função de Administrador Global ou Administrador de Serviço do Intune atribuída, mas tiver permissões de leitura ativadas para a função de Gestores de Inscrição de Dispositivos atribuída ao mesmo, só poderá ver os utilizadores DEM que criou.


## <a name="remove-device-enrollment-manager-permissions"></a>Remover as permissões de gestor de inscrição de dispositivos

A remoção de um gestor de inscrição de dispositivos não afeta os dispositivos inscritos.

**Para remover um gestor de inscrição de dispositivos**

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), escolha **dispositivos** > **Inscrever dispositivos** > gestores de **inscrição do dispositivo**.
2. No painel **Gestores de inscrições de dispositivos**, selecione o gestor de inscrição de dispositivos e selecione **Eliminar**.

