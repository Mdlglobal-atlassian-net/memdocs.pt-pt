---
title: Preparar a gestão de atualizações de software
titleSuffix: Configuration Manager
description: Para se preparar para gerir as atualizações, complete estas tarefas para exibir dados de avaliação de conformidade na consola Do Gestor de Configuração.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ab22fdcacf7574884f7cfd21859cb4b1aeb8e23f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717273"
---
# <a name="prepare-for-software-updates-management"></a>Preparar a gestão de atualizações de software

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes dos dados de avaliação de conformidade da atualização de software, na consola do Gestor de Configuração e antes de poder implementar atualizações de software para computadores clientes, tem de completar os passos nas seguintes secções.

## <a name="step-1-install-a-software-update-point"></a>Passo 1: Instale um ponto de atualização de software  
O ponto de atualização do software é necessário no site da administração central, ou site primário autónomo, e em sites primários para permitir a avaliação de conformidade de atualizações de software e implementar atualizações de software para os clientes. O ponto de atualização de software é opcional em site secundários. Para mais detalhes, consulte Instalar um ponto de [atualização](install-a-software-update-point.md) de software  

## <a name="step-2-synchronize-software-updates"></a>Passo 2: Sincronizar Atualizações de Software
A sincronização das atualizações de software é o processo de recuperação dos metadados de atualizações de software que satisfaz os critérios que configura. As atualizações de software não são apresentadas na consola Do Gestor de Configuração até sincronizar as atualizações de software. Para mais detalhes, consulte as atualizações de [software Synchronize](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Passo 3: Configurar classificações e produtos para sincronizar
Realize esta configuração no site de administração central ou site primário autónomo. Depois de sincronizar as atualizações de software pela primeira vez, o Gestor de Configuração recupera uma lista atualizada de classificações e produtos. Agora, pode selecionar entre as novas opções nas propriedades do Componente de Ponto de Atualização de Software. Depois de configurar as novas classificações e produtos, repita o passo 2 para iniciar a sincronização de atualizações de software para recuperar os metadados de atualizações de software para os novos critérios. Para mais detalhes, consulte [classificações e produtos da Configuração para sincronizar](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Passo 4: Gerir as definições para atualizações de software
Depois de sincronizar as atualizações de software, verifique as definições do cliente do Gestor de Configuração, configurações de políticas de grupo e configurações de atualizações de software antes de implementar atualizações de software. Para mais detalhes, consulte ['Gerir as definições' para atualizações](manage-settings-for-software-updates.md)de software .
