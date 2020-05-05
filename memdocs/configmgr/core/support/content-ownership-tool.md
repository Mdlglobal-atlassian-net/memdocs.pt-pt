---
title: Ferramenta de Propriedade do Conteúdo
titleSuffix: Configuration Manager
description: Utilize a Ferramenta de Propriedade de Conteúdo para alterar a propriedade de pacotes órfãos no Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723391"
---
# <a name="content-ownership-tool"></a>Ferramenta de Propriedade do Conteúdo

*Aplica-se a: Gestor de Configuração (ramo atual)*

A Ferramenta de Propriedade de Conteúdo é uma das ferramentas do Gestor de [Configuração.](tools.md) Muda a propriedade de pacotes órfãos no Gestor de Configuração. Pacotes órfãos não têm um servidor de site próprio. Os pacotes podem ficar órfãos removendo o servidor do site enquanto ainda são propriedade deste servidor do site.

Execute a Ferramenta de Propriedade de Conteúdo em qualquer servidor de site na hierarquia do Gestor de Configuração. Inscreva-se como utilizador administrativo com permissões de pacote suficientes.  

> [!Tip]  
> Utilize **contentLibraryCleanup.exe** `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para *remover* conteúdo órfão de um ponto de distribuição. Para mais informações, consulte a ferramenta de [limpeza da biblioteca de conteúdos](../plan-design/hierarchy/content-library-cleanup-tool.md).  



## <a name="features"></a>Funcionalidades

- Mostrar todos os pacotes órfãos  

- Exiba todos os pacotes, mesmo que não estejam órfãos.  

- Ver o estado da ligação a um site  

- Filtrar pacotes por nome, código de site ou tipo de pacote  

- Ordenar por qualquer coluna exibida  

- Alterar a atribuição de um ou mais pacotes com uma única ação  

- Ver o progresso da atividade de transferência de propriedade  



## <a name="usage"></a>Utilização

Executar **ContentOwnershipTool.exe** para iniciar a ferramenta. As permissões do administrador local no computador não são necessárias para executar a ferramenta.

Não há parâmetros de linha de comando.

> [!Important]   
> Esta ferramenta altera a propriedade de um pacote órfão. O pacote em si não se move do ponto de distribuição em que está armazenado. Esta mudança de propriedade não faz com que o pacote atualize nos pontos de distribuição. Também não leva os clientes a reavaliar a política de implementação do pacote. Após as alterações de propriedade, certifique-se de que o novo servidor do site pode aceder aos ficheiros de origem. Deve ter, pelo menos, **ler** permissões aos ficheiros de origem de cada pacote. 



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [A biblioteca de conteúdos](../plan-design/hierarchy/the-content-library.md)
