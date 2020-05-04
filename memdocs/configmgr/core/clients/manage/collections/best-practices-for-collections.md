---
title: Coleções boas práticas
titleSuffix: Configuration Manager
description: Obtenha as melhores práticas para coleções em 'Gestor de Configuração'.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714291"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Boas práticas para coleções em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as seguintes melhores práticas para coleções em 'Gestor de Configuração'.  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a>Não utilize atualizações incrementais com muitas coleções

Quando ativa a opção **Utilizar atualizações incrementais para esta coleção** , esta configuração poderá causar atrasos de avaliação se a ativar em muitas coleções. O limite é de cerca de 200 coleções na sua hierarquia. O número exato depende dos seguintes fatores:  

- O número total de coleções  

- A frequência de novos recursos a ser adicionados e alterados na hierarquia  

- O número de clientes na hierarquia  

- A complexidade das regras de associação de coleções na hierarquia  

## <a name="maintenance-window-size-for-software-updates"></a>Tamanho da janela de manutenção para atualizações de software

Pode configurar janelas de manutenção para recolhas de dispositivos para restringir as vezes que o Gestor de Configuração pode instalar software nestes dispositivos. Se configurar a janela de manutenção demasiado pequena, o cliente poderá não ser capaz de instalar atualizações críticas de software, o que deixa o cliente vulnerável ao ataque atenuado pela atualização de software.

> [!Tip]
> Considerações importantes a ter em mente ao planear as janelas de manutenção:
>
> - O tempo máximo de execução da atualização de software padrão é de 60 minutos.
> - Quando o Gestor de Configuração calcula se uma atualização pode instalar-se, adiciona cinco minutos ao tempo máximo de execução para responder a um reinício.
> - A duração remanescente de uma janela de manutenção deve ser mais longa do que o tempo máximo de execução da atualização do software mais cinco minutos.
