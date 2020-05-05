---
title: Instalações de avaliação de upgrade
titleSuffix: Configuration Manager
description: Saiba como atualizar uma instalação de avaliação para uma instalação completa do Gestor de Configuração.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8a42b2538ff1baaceb6895d371081ac2a444c5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718001"
---
# <a name="upgrade-an-evaluation-installation-of-configuration-manager-to-a-full-installation"></a>Atualize uma instalação de avaliação do Gestor de Configuração para uma instalação completa

*Aplica-se a: Gestor de Configuração (ramo atual)*

Se instalou o Gestor de Configuração como uma versão de avaliação, após 180 dias, a consola 'Gestor de Configuração' torna-se apenas de leitura até ativar o produto a partir da página de Manutenção do **Site** na Configuração. Em qualquer momento antes ou depois do período de 180 dias, tem a opção de atualizar uma instalação de avaliação para uma instalação completa.  

> [!NOTE]  
>  Quando liga uma consola do Gestor de Configuração a uma instalação de avaliação do Gestor de Configuração, a barra de título da consola apresenta o número de dias que permanecem até que a instalação de avaliação expire. O número de dias não é automaticamente atualizado e só atualiza quando se faz uma nova ligação a um site.  

 Pode atualizar os seguintes sites que executam uma instalação de avaliação:  

-   Site de administração central  
-   Site primário  

Como os locais secundários não são tratados como instalações de avaliação, não é necessário modificar um local secundário após o seu principal local principal atualizar para uma instalação completa.  

Pré-requisitos para atualizar uma versão de avaliação para uma versão licenciada:  

-   Deve ter um produto válido para utilizar durante a atualização.  
-   A sua conta deve ter direitos **de administrador** no computador onde o site está instalado.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Para atualizar uma versão de avaliação do Gestor de Configuração para uma versão licenciada  

1.  No servidor do site, executar **Setup.exe** (configuração do Gestor de Configuração) a partir da pasta de instalação do Gestor de Configuração **(%path%\BIN\X64**). Tem de executar a cópia da Configuração que está localizada no servidor do site na pasta 'Gestor de Configuração', uma vez que as opções de manutenção do site não estão disponíveis quando executa a Configuração a partir de suportes de instalação.  
2.  Na página **Antes de Começar,** selecione **Seguinte**.  
3.  Na página **Getting Started,** selecione **Executar a manutenção do site ou redefinir o Site**, e, em seguida, selecione **Next**.  
4.  Na página de Manutenção do **Site,** selecione **Atualizar a edição de avaliação para uma edição licenciada,** introduzir uma chave de produto válida e, em seguida, selecionar **Next**.  
5.  Na página De Termos de Licença de Software da **Microsoft,** leia e aceite os termos da licença e, em seguida, selecione **Next**.  
6.  Na página **de Configuração,** selecione **Fechar** para completar o assistente.  

    > [!NOTE]  
    >  A barra de título de uma consola De Configuração Manager que permanece ligada ao site que atualiza pode indicar que o site ainda é uma versão de avaliação até voltar a ligar a consola ao site.  
