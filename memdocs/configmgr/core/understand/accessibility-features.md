---
title: Acessibilidade
titleSuffix: Configuration Manager
description: Conheça as funcionalidades que tornam o Gestor de Configuração acessível a todos.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2ff86df999ab744d590b1ca120a8b566d18f446b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718561"
---
# <a name="accessibility-features-in-configuration-manager"></a>Funcionalidades de acessibilidade no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


O Gestor de Configuração inclui funcionalidades para ajudar a torná-lo acessível para todos.

> [!Note]  
> A partir da versão 1902, para melhorar as funcionalidades de acessibilidade da consola De Configuração Manager, atualize .NET para a versão 4.7 ou posteriormente no computador que executa a consola. <!-- SCCMDocs-pr issue #3228 -->  
> 
> Para obter mais informações sobre as alterações de acessibilidade efetuadas em .NET 4.7.1 e 4.7.2, consulte [as novidades na acessibilidade no .NET Framework](https://docs.microsoft.com/dotnet/framework/whats-new/whats-new-in-accessibility).  



## <a name="keyboard-shortcuts"></a>Atalhos de teclado

### <a name="console-workspaces"></a>Espaços de trabalho de consola

Para aceder a um espaço de trabalho, utilize os seguintes atalhos de teclado:  

|Atalho de teclado| Área de trabalho|
|--------|--------|  
|Ctrl + 1| Ativos e Conformidade|
|Ctrl + 2|  Biblioteca de Software|
|CTRL + 3|  Monitorização|
|Ctrl + 4|  Administração|


### <a name="other-keyboard-shortcuts"></a>Outros atalhos de teclado

|Atalho de teclado|  Objetivo|
|--------|--------|  
|Ctrl + M|Coloque o foco no painel principal (central).|
|Ctrl + T|Coloque o foco no nó superior no painel de navegação. Se o foco já estava naquele painel, o foco está definido para o último nó que visitou.|
|Ctrl+I|Coloque o foco na barra de migalhas de pão, abaixo da fita.|
|Ctrl + L|Detete o foco no campo **de pesquisa,** quando disponível.|
|Ctrl + D|Dete tede o foco para o painel de detalhes, quando disponível.|
|Alt     |Mude o foco dentro e fora da fita.|



## <a name="other-accessibility-features"></a>Outras funcionalidades de acessibilidade

- Para navegar no painel de navegação, digite as letras de um nome de nó.

- A navegação do teclado através da vista principal e a fita é circular.

- A navegação do teclado no painel de detalhes é circular. Para voltar ao objeto ou painel anterior, utilize Ctrl + D e, em seguida, Mude + TAB.

- Depois de refrescar uma vista workspace, o foco está definido para o painel principal desse espaço de trabalho.

- Para aceder a um menu espaço de trabalho, selecione a tecla Tab até que o ícone Expandir/Colapso esteja focado. Em seguida, selecione a tecla seta para baixo para aceder ao menu espaço de trabalho.  

- Para navegar através de um menu espaço de trabalho, use as teclas de seta.  

- Para aceder a diferentes áreas do espaço de trabalho, utilize a tecla Tab e as teclas Shift+Tab. Para navegar dentro de uma área do espaço de trabalho, como a fita, use as teclas de seta.  

- Para aceder à barra de endereços quando o seu foco estiver no nó da árvore, utilize o Shift+Tab três vezes.  

- Numa página de assistente ou propriedade, pode mover-se entre as caixas com atalhos de teclado. Selecione a tecla Alt mais o caracteres sublinhados (Alt+_) para selecionar uma caixa específica.     

- Para navegar para os diferentes nós de um espaço de trabalho, insira a primeira letra do nome de um nó. Cada tecla de pressão move o cursor para o próximo nó que começa com essa letra. Quando se está a utilizar um leitor de ecrã, o leitor lê o nome desse nó.



## <a name="see-also"></a>Consulte também

Para obter mais informações sobre os fundamentos da navegação nas interfaces de utilizador do Gestor de Configuração, consulte os seguintes artigos:
- [Usando a consola De Configuração Manager](../servers/manage/admin-console.md)  
- [Manual do utilizador do Software Center](software-center.md)

> [!NOTE]  
> As informações deste artigo podem aplicar-se apenas aos utilizadores que licenciam produtos da Microsoft nos Estados Unidos. Se obteve este produto fora dos Estados Unidos, pode utilizar o cartão de informação subsidiário que veio com o seu pacote de software ou visitar o [website da Microsoft Accessibility](https://go.microsoft.com/fwlink/?LinkId=8431) para obter informações de contacto para serviços de suporte da Microsoft. Pode contactar a sua subsidiária para saber se o tipo de produtos e serviços descritos nesta secção estão disponíveis na sua área. Encontram-se disponíveis informações sobre acessibilidade noutros idiomas, incluindo japonês e francês.  

