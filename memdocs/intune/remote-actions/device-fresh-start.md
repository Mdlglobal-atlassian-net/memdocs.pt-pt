---
title: Repor dispositivos Windows 10 com o Microsoft Intune – Azure | Microsoft Docs
description: Utilize a funcionalidade Começar do Zero para remover ou desinstalar aplicações de PCs com Windows 10 com o Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5aa5cfa3-c483-4099-b40f-578ff8dca425
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6d409f3ba1dc91815ce3dc67a2d65e5703c7268
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80322555"
---
# <a name="use-fresh-start-to-reset-windows-10-devices-with-intune"></a>Utilizar a funcionalidade Começar do Zero para repor dispositivos Windows 10 com o Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A ação de dispositivo **Começar do Zero** remove todas as aplicações instaladas num PC com a versão 1703 ou posterior do Windows 10. A funcionalidade Começar do Zero ajuda a remover aplicações que vêm geralmente pré-instaladas (OEM) num PC novo. 

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selecione **Dispositivos** > **todos os dispositivos**.
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
