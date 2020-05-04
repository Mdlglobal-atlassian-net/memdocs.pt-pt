---
title: Partilhar aplicações no Centro de Software
titleSuffix: Configuration Manager
description: Partilhe um link para uma aplicação no Software Center em 'Configuração Manager'.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710077"
---
# <a name="share-an-application-from-software-center"></a>Partilhar uma aplicação do Software Center

*Aplica-se a: Gestor de Configuração (ramo atual)* <!-- 1706 -->

Pode copiar uma hiperligação para uma ![aplicação no Software Center utilizando o botão](media/share15.png)**Share Share** na vista Dados da Aplicação.   Só pode partilhar hiperligações para aplicações. Se a aplicação ficar indisponível, o hiperlink abre uma janela com uma mensagem indisponível da aplicação.

1. Escolha **candidaturas**e, em seguida, escolha a aplicação.
2. Clique ![no](media/share15.png) botão **Partilhar.**
3. Clique em **Copiar** na janela.
4. Colá-lo num e-mail para partilhar a aplicação.  

> [!TIP]  
>  Para criar um link num e-mail do Outlook, prima **CTRL** + **K** e, em seguida, colhe o URL.  
>  
> Por padrão, o Outlook mostra um alerta de segurança para o protocolo do Centro de Software quando o destinatário clica no link. Evite isso no seu ambiente adicionando uma chave de protocolo de confiança ao registo. Por exemplo, `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
