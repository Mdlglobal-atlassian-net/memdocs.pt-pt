---
title: Repor códigos de acesso de dispositivos com o Microsoft Intune – Azure | Microsoft Docs
description: Remova ou reponha o código de acesso com a ação Remover código de acesso nos dispositivos dos quais faça a gestão ou monitorização com o Intune.
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
ms.assetid: 47181d19-4049-4c7a-a8de-422206c4027e
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d7e5fc7d16212c40fbbe5c1486ed3be76d2738f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983105"
---
# <a name="reset-or-remove-a-device-passcode-in-intune"></a>Repor ou remover um código de acesso do dispositivo no Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Este documento discute tanto o reset de código de acesso do dispositivo como o reset de código de código de perfil de trabalho em dispositivos Android enterprise (anteriormente chamados Android for Work, ou AfW). É importante notar esta distinção como requisitos para cada um pode variar. Uma reposição de código de acesso ao nível do dispositivo repõe o código de acesso de todo o dispositivo. Uma redefinição da senha de perfil de trabalho repõe a senha apenas para o perfil de trabalho do utilizador em dispositivos empresariais Android.

## <a name="supported-platforms-for-device-level-passcode-reset"></a>Plataformas suportadas para reposição de códigos de acesso ao nível do dispositivo

| Plataforma | Suportada? |
| ---- | ---- |
| Dispositivos Android com a versão 6.X ou anterior | Yes |
| Dispositivos empresariais Android matriculados como Proprietário de Dispositivos | Yes |
| dispositivos iOS/iPadOS | Yes |
| dispositivos iOS/iPadOS matriculados com inscrição do utilizador | No |
| Dispositivos Android matriculados com um perfil de trabalho | No |
| Dispositivos Android com a versão 7.0 ou posterior | No |
| macOS | No |
| Windows | No |

Para dispositivos Android, isto significa que o reset da código de acesso ao nível do dispositivo só é suportado em dispositivos com 6.x ou anteriores, ou em dispositivos empresariais Android que executam no modo Quiosque. Isto porque a Google removeu o suporte para redefinir a senha/senha de um dispositivo Android 7 a partir de uma aplicação de Administrador de Dispositivos e aplica-se a todos os fornecedores de MDM.

## <a name="supported-platforms-for-android-enterprise-work-profile-passcode-reset"></a>Plataformas suportadas para reposição de códigos de acesso do perfil de trabalho do Android Enterprise

| Plataforma | Suportada? |
| ---- | ---- |
| Dispositivos Android Enterprise inscritos com um perfil de trabalho e com a versão 8.0 e posterior | Yes |
| Dispositivos Android Enterprise inscritos com um perfil de trabalho e com a versão 7.X e anterior | No |
| Dispositivos Android com a versão 7.X e anterior | No |

Para criar um novo código de acesso de perfil de trabalho, utilize a ação Repor Código de Acesso. Esta ação solicita uma reposição do código de acesso e cria um código de acesso novo e temporário apenas para o perfil de trabalho. 

## <a name="reset-a-passcode"></a>Repor um código de acesso


1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) com qualquer uma das seguintes funções: Azure Ative Directory Global Admin, Azure Ative Directory Intune Service Admin, Helpdesk Operator ou Role Administrator.
2. Selecione **Dispositivos** e, em seguida, selecione **Todos os dispositivos**.
3. A partir da lista de dispositivos que gere, selecione um dispositivo e escolha **a senha de reset**.

## <a name="reset-android-work-profile-and-device-owner-passcodes"></a>Redefinir o perfil de trabalho android e as códigos de acesso do proprietário do dispositivo

Os dispositivos Android Enterprise inscritos suportados com um perfil de trabalho recebem uma nova palavra-passe de desbloqueio do perfil gerido ou um desafio de perfil gerido para o utilizador final.

Para dispositivos de perfil de trabalho Android Enterprise que executam a versão 8.x ou posterior, os utilizadores finais são notificados para ativar a sua código de redefinição logo após a inscrição estar concluída. A notificação é apresentada se for necessário definir uma palavra-passe de perfil de trabalho. Após a entrada da sua senha, a notificação é rejeitada.

Para dispositivos android Enterprise ou dispositivos de perfil de trabalho que executam a versão 8.x ou posterior, após a reset da senha ser selecionada a partir da consola, o administrador MEM Intune é apresentado com uma senha temporária. A senha temporária deve ser inserida no aparelho. A senha temporária do dispositivo será exibida na consola durante 7 dias.


## <a name="remove-iosipados-passcodes"></a>Remova códigos de acesso iOS/iPadOS

Em vez de serem repostas, as códigos de acesso são removidas dos dispositivos iOS/iPadOS. Se estiver definida uma política de conformidade de código de acesso, o dispositivo pedirá ao utilizador para definir um novo código de acesso nas Definições.

## <a name="next-steps"></a>Passos seguintes

Para ver o estado da ação que acabou de realizar, em **Dispositivos**, selecione **Ações do dispositivo**.
