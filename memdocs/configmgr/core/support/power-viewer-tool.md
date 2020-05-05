---
title: Ferramenta de Visualizador de Energia
titleSuffix: Configuration Manager
description: Utilize a Ferramenta power viewer para visualizar o estado da funcionalidade de gestão de energia num cliente do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723195"
---
# <a name="power-viewer-tool"></a>Ferramenta de Visualizador de Energia

*Aplica-se a: Gestor de Configuração (ramo atual)*

A ferramenta Power Viewer é uma das ferramentas do Gestor de [Configuração.](tools.md) Use-o para visualizar o estado da funcionalidade de gestão de energia num cliente do Gestor de Configuração.

Executar **PowerVwr.exe** como administrador. Quando a ferramenta é lançada, apresenta as capacidades de potência e as definições de potência do computador local no separador **Power Config.** 

Para visualizar os dados de gestão de energia de um computador remoto:  

1. Vá ao menu **'Ficheiro'** e clique em **Connect**. 

2. Introduza o nome do **Computador** e um **nome de utilizador** e **palavra-passe,** se necessário. 

Existem três separadores no Power Viewer:  

- **Power Config**: Ver as capacidades de potência e as definições de potência do computador-alvo.  

- **Atividade Diária**: Ver os gráficos de atividade diária do cliente, que inclui as seguintes informações:  

    - **Computador ligado**: O estado de potência do computador num dia. O modo de sono é considerado como desligado.  

    - **Monitor on**: On or off status of monitor in one day.  

    - **Ativo do utilizador**: Informação sobre a atividade do utilizador num dia.  

- **Power Events**: Veja todos os eventos diários de energia. O cliente resume estes eventos às 00:00. Esta resumidação gera dados para o gráfico de atividade diária.  
