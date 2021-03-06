---
title: Repor dispositivos Windows 10 com o Microsoft Intune – Azure | Microsoft Docs
description: Utilize a funcionalidade Começar do Zero para remover ou desinstalar aplicações de PCs com Windows 10 com o Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5aa5cfa3-c483-4099-b40f-578ff8dca425
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7003bf0aa943eab6d884b55c511fea5dddeae8e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989920"
---
# <a name="use-fresh-start-to-reset-windows-10-devices-with-intune"></a>Utilizar a funcionalidade Começar do Zero para repor dispositivos Windows 10 com o Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A ação do dispositivo **Fresh Start** remove todas as aplicações instaladas num PC que executa o Windows 10, versão 1709 ou posterior. A funcionalidade Começar do Zero ajuda a remover aplicações que vêm geralmente pré-instaladas (OEM) num PC novo. 

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selecione **Devices**  >  **Dispositivos Todos os dispositivos**.
2. Na lista dos dispositivos que gere, selecione um computador com o Windows 10.
3. Clique em **Começar de Novo**. 
4. Selecione **Manter os dados de utilizador neste dispositivo** para:
   * Manter o dispositivo associado ao Azure AD
   * O dispositivo está novamente inscrito na gestão de dispositivos móveis quando um Diretório Ativo Azure ativo ativo iactivado os sinais do utilizador no dispositivo.
   * Manter os conteúdos da pasta Raiz do utilizador do dispositivo e remover as aplicações e definições

  > [!IMPORTANT]
 > Se não reter os dados do utilizador, o dispositivo será restaurado para o estado completo do OOBE (experiência fora da caixa) que retém a conta de administrador incorporada.
 > Os dispositivos BYOD não serão matriculados a partir da Azure AD e da gestão de dispositivos móveis.
 > Os dispositivos aderes à Azure AD voltarão a ser matriculados na gestão de dispositivos móveis quando um Diretório Ativo Do Azure ativado pelo utilizador entrar no dispositivo.
 
5. Clique em **OK**.   
6. Para ver o estado desta ação, volte a **Dispositivos** e clique em **Ações do dispositivo**.  
7. O dispositivo será restaurado no ecrã inicial de entrada.
