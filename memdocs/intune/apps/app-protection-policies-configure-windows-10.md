---
title: Configurar políticas de proteção de aplicações para o Windows 10
titleSuffix: Microsoft Intune
description: Este tópico descreve como configurar políticas de proteção de aplicações (APP) para dispositivos Windows 10.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 949fddec-5318-4c9a-957e-ea260e6e05be
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75b988572a5c22e49547a7ba1521cfc3485f4f03
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326285"
---
# <a name="get-ready-to-configure-app-protection-policies-for-windows-10"></a>Preparar-se para configurar políticas de proteção de aplicações para o Windows 10 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Ative a gestão de aplicações móveis (MAM) para o Windows 10 ao definir o fornecedor de MAM no Azure AD. Definir um fornecedor de MAM no Azure AD permite-lhe definir o estado de inscrição ao criar uma nova política do Windows Information Protection (WIP) com o Intune. O estado de inscrição pode ser MAM ou gestão de dispositivos móveis (MDM).

## <a name="to-configure-the-mam-provider"></a>Para configurar o fornecedor de MAM

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Todos os serviços** e escolha o **M365 Azure Ative Directory** para trocar de dashboards.
3. Selecione **Diretório Ativo Azure**.
4. Selecione **Mobilidade (MDM e MAM)** no grupo **Gerir**.
5. Clique em **Microsoft Intune**.
6. Configure as definições no grupo **Derisque MAM URLs** no painel **Configure.**

   **Âmbito de utilizador MAM**  
   Utilize a inscrição automática MAM para gerir dados empresariais nos dispositivos Windows dos seus funcionários. A inscrição automática MAM será configurada para cenários de Bring Your Own Device.<ul><li>**Nenhum**<br>Selecione se nenhum utilizador pode ser inscrito na MAM.</li><li>**Alguns**<br>Selecione grupos do Azure AD que contenham utilizadores que serão inscritos na MAM.</li><li>**Todos**<br>Selecione se todos os utilizadores podem ser inscritos na MAM.</li></ul>

   **URL dos termos de utilização da MAM**  
   O URL dos termos de utilização da MAM não é suportado no Microsoft Intune. Esta caixa de introdução tem de ser deixada em branco para aplicar políticas de proteção.

   **URL de deteção da MAM**  
   O URL do ponto final de inscrição da MAM. O ponto final de inscrição é utilizado para inscrever dispositivos para gestão com a MAM.

   **URL de conformidade da MAM**  
   O URL de conformidade da MAM não é suportado no Microsoft Intune. Esta caixa de introdução tem de ser deixada em branco para aplicar políticas de proteção. 

7. Clique em **Guardar**.

## <a name="next-steps"></a>Próximos passos

[Criar uma política de proteção de aplicações WIP](windows-information-protection-policy-create.md)
