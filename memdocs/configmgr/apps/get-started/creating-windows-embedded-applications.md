---
title: Criar aplicações Windows Embedded
titleSuffix: Configuration Manager
description: Veja quais as considerações que deve ter em conta quando cria e implementa aplicações para dispositivos Incorporados windows.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bec9765e5152863bb8b55a0b75f1e5c2fc580550
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710497"
---
# <a name="create-windows-embedded-applications-with-configuration-manager"></a>Criar aplicações incorporadas ao Windows com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Além dos outros requisitos e procedimentos do Gestor de Configuração para a criação de uma aplicação, deve também ter em conta as seguintes considerações quando cria e implementa aplicações para dispositivos Incorporados no Windows.  

## <a name="general-considerations"></a>Considerações gerais  

-   Quando implementa aplicações para dispositivos Incorporados do Windows que estão habilitados para a filtragem de escrita, pode especificar se deve desativar o filtro de escrita no dispositivo durante a implementação da aplicação. Em seguida, pode optar por reiniciar o filtro de escrita após a implementação da aplicação. Se o filtro de escrita não for desativado, o software é implantado para uma sobreposição temporária. Isto significa que, a menos que outra implementação mude para persistir, o software deixará de ser instalado quando o dispositivo recomeçar.  

-   Ao implementar uma aplicação num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Desta forma, poderá gerir a desativação e a ativação do filtro de escrita, bem como o reinício do dispositivo.  

-   A definição que controla o comportamento do filtro de escrita é uma caixa de verificação chamada **Cometer alterações no prazo ou durante uma janela de manutenção (requer reinício)**.  

## <a name="tips-for-deploying-applications"></a>Sugestões para implementar aplicações  

**Utilize aplicações necessárias em vez de aplicações disponíveis para dispositivos Incorporados windows que tenham filtros de escrita ativados.** Uma vez que os utilizadores não podem instalar aplicações do Software Center num dispositivo Windows Embedded que tenha filtros de escrita ativados, implementa sempre aplicações com um propósito **de** implementação necessário e não **disponível** para estes dispositivos. Normalmente, isto não é um problema porque os computadores que executam um sistema operativo Windows Embedded muitas vezes executam uma única aplicação que deve funcionar da mesma forma para vários utilizadores. Por este motivo, estes dispositivos são altamente geridos e bloqueados pelo departamento de TI. As aplicações necessárias são ideais para este cenário.

 No entanto, se os utilizadores executarem mais de uma aplicação em dispositivos incorporados quando os filtros de escrita estiverem ativados, informe estes utilizadores sobre as seguintes limitações:  

-   Os utilizadores não podem instalar o software necessário a partir do Centro de Software.  

-   Os utilizadores não podem alterar o seu horário comercial no separador Opções do Centro de Software.  

-   Os utilizadores não podem adiar a instalação de uma aplicação necessária.  

Além disso, os utilizadores de baixos direitos não podem iniciar sessão durante um período de manutenção se o Gestor de Configuração estiver a cometer alterações para instalações e atualizações de software. Durante este período, os utilizadores veem uma mensagem a informá-los de que o dispositivo não está disponível porque está em manutenção.  

**Não implemente aplicações para dispositivos Incorporados do Windows que tenham filtros de escrita ativados se as aplicações exigirem que o utilizador aceite os termos da licença.** Quando os filtros de escrita são desativados para que o Gestor de Configuração possa instalar software em dispositivos incorporados, os utilizadores de baixos direitos não podem iniciar sessão no dispositivo. Se a instalação exigir que o utilizador aceite os termos de licenciamento, isto não será possível e a instalação falhará. Certifique-se de que não implementa software em dispositivos Windows Embedded se a instalação exigir a interação do utilizador. Pode utilizar a lista Plataformas Aplicáveis para filtrar estes sistemas operativos.  
