---
title: Ferramenta de transferência de biblioteca de conteúdo
titleSuffix: Configuration Manager
description: Utilize a ferramenta de transferência de biblioteca de conteúdo para transferir conteúdo de uma unidade de disco para outra num ponto de distribuição do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720087"
---
# <a name="content-library-transfer-tool"></a>Ferramenta de transferência de biblioteca de conteúdo

*Aplica-se a: Gestor de Configuração (ramo atual)*

A ferramenta de transferência da Biblioteca de Conteúdos é uma das ferramentas do Gestor de [Configuração.](tools.md) Transfere o conteúdo de uma unidade de disco para outra. A ferramenta foi concebida para funcionar em sistemas de locais de ponto de distribuição. Suporta pontos de distribuição colocalizados com um site ou sistemas de site remoto.  

A ferramenta é útil para o cenário quando a unidade de disco que hospeda a biblioteca de conteúdos fica cheia. Primeiro adicione ou identifique outro disco rígido com espaço suficiente para acolher a biblioteca de conteúdos. Em seguida, utilize **ContentLibraryTransfer.exe** para transferir conteúdo do disco rígido cheio antigo para o novo disco vazio.
 
Uma vez concluída a transferência, o conteúdo é acessível aos computadores clientes a partir da nova localização.



## <a name="usage"></a>Utilização 

Executar **ContentLibraryTransfer.exe** como um utilizador com permissões administrativas no ponto de distribuição. 

#### <a name="syntax"></a>Sintaxe 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Exemplo
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Limitações

- Executar a ferramenta localmente no ponto de distribuição. Não se pode executá-lo a partir de um computador remoto.  

- Use-o apenas quando os clientes não acedem ativamente ao ponto de distribuição. Se executar a ferramenta enquanto os clientes acedem a conteúdos, a biblioteca de conteúdos na unidade de destino pode ter dados incompletos. A transferência de dados pode falhar completamente levando a uma biblioteca de conteúdos inutilizável.  

- Não distribua o conteúdo para o ponto de distribuição quando executar a ferramenta. Se executar a ferramenta enquanto o conteúdo está a ser escrito para o ponto de distribuição, a biblioteca de conteúdos na unidade de destino pode ter dados incompletos. A transferência de dados pode falhar completamente levando a uma biblioteca de conteúdos inutilizável.



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [A biblioteca de conteúdos](../plan-design/hierarchy/the-content-library.md)
