---
title: Portal de self-service BitLocker
titleSuffix: Configuration Manager
description: Como utilizar o portal de self-service do utilizador no Gestor de Configuração para recuperação bitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fda719aed4d70cd9783d158e17d546b698497997
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717406"
---
# <a name="bitlocker-self-service-portal"></a>Portal de self-service BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

Depois de [instalar o portal de self-service BitLocker](setup-websites.md), se o BitLocker trancar o dispositivo de um utilizador, pode aceder de forma independente aos seus computadores. O portal de auto-atendimento não necessita de assistência do pessoal do balcão de ajuda.

[![Screenshot do portal de self-service BitLocker padrão](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> Para obter uma chave de recuperação do portal de self-service, um utilizador deve ter assinado com sucesso no computador pelo menos uma vez. Este sinal de entrada deve ser local para o dispositivo, não numa sessão remota. Caso contrário, têm de contactar o balcão de ajuda para a recuperação da chave. Um administrador de mesa de ajuda pode usar o site de [administração e monitorização](helpdesk-portal.md) para solicitar a chave de recuperação.

O BitLocker pode bloquear o dispositivo nas seguintes situações:

- O utilizador esquece a sua senha bitLocker ou PIN

- Há uma alteração nos ficheiros OS do dispositivo, BIOS ou Módulo de Plataforma Fidedigna (TPM)

Para solicitar a chave de recuperação BitLocker do portal de self-service:

1. Quando o BitLocker bloqueia um dispositivo, exibe o ecrã de recuperação BitLocker durante o arranque. Escreva o ID da chave de recuperação BitLocker de 32 dígitos.

1. Noutro computador, vá ao portal de self-service no `https://webserver.contoso.com/SelfService`navegador web, por exemplo.

1. Leia e aceite o aviso.

1. No campo ID da **Chave de Recuperação,** introduza os primeiros oito dígitos do ID da chave de recuperação BitLocker. Se corresponder a várias teclas, introduza todos os 32 dígitos.

1. Escolha uma das seguintes opções para a **Razão** para este pedido:

    - BIOS/TPM alterado
    - Os arquivados modificados
    - PIN/frase-passe perdida

1. Selecione **Obter Tecla**. O portal de autosserviço exibe a chave de **recuperação BitLocker**de 48 dígitos .

1. Introduza este código de 48 dígitos no ecrã de recuperação BitLocker no seu computador.

> [!NOTE]
> O portal de autosserviço BitLocker pode esgotar-se após um período de inatividade. Por exemplo, após cinco minutos pode ver um aviso de tempo com um contador de 60 segundos.
>
> ![Aviso de tempo de tempo livre do portal bitLocker](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Se não responder à contagem regressiva, a sessão expirará.
>
> ![Página expirada do portal de self-service BitLocker](media/bitlocker-self-service-portal-session-expired.png)
