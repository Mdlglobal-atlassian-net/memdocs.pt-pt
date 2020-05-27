---
title: Mude o nome de um dispositivo com microsoft Intune - Azure Microsoft Docs
description: Mude o nome de um dispositivo utilizando o Microsoft Intune.
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
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8beb69178c6f845592caa9890bc8ed9759eb2e23
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983037"
---
# <a name="rename-a-device-in-intune"></a>Mude o nome de um dispositivo em Intune

A ação do **dispositivo Rename** permite-lhe renomear um dispositivo que está matriculado em Intune. O nome do dispositivo é alterado em Intune e no dispositivo.

Pode renomear os seguintes tipos de dispositivos:
- Windows corporativo 
- iOS/iPadOS supervisionado
- MacOS 10 de propriedade corporativa

Esta funcionalidade não suporta atualmente renomear dispositivos híbridos Azure AD Windows.

## <a name="rename-a-device"></a>Mudar o nome de um dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Escolha **Dispositivos**  >  **Todos os dispositivos** > escolha um dispositivo > **...**  >  **Dispositivo de renomear**.
4. Na lâmina do **dispositivo Rename,** digite o novo nome na caixa de texto. Pode usar letras, números e hífenes. O nome deve conter pelo menos uma letra ou hífen.
5. Se pretender reiniciar o dispositivo depois de o renomear, escolha **Sim** ao lado do **Restart após o renome .**
6. Escolha **Mudar o nome**.

## <a name="windows-device-rename-rules"></a>Regras de renome do dispositivo Windows
Ao renomear um dispositivo Windows, o novo nome deve seguir estas regras:
- 15 caracteres ou menos (deve ser inferior ou igual a 63 bytes, sem incluir o nulo de rasto)
- Não é nulo ou uma corda vazia
- ASCII permitido: Letras (a-z, A-Z), números (0-9) e hífenes
- Unicode permitido: os caracteres >= 0x80, devem ser uTF8 válidos, devem ser idn-mappable (isto é, RtlIdnToNameprepUnicode consegue; ver RFC 3492)
- Os nomes não devem conter apenas números
- Sem espaços no nome
- Caracteres proibidos: { ~ ~ [ ] [ ] [ ] < = >? &@ " # $ % ` ( ) + / , . _ *)


## <a name="next-steps"></a>Passos seguintes

Para ver o estado da ação do dispositivo **Renomear,** verifique a página **'Visão Geral'** do dispositivo.
