---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Use system center Updates Publisher para gerir atualizações personalizadas
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717700"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Aplica-se a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) é uma ferramenta autónoma que permite a fornecedores de software independentes ou desenvolvedores de aplicações line-of-business gerir atualizações personalizadas. Esta gestão de atualizações personalizadas inclui atualizações que têm dependências, como motoristas e pacotes de atualizações.

Utilizando a Editora updates, pode:

-   Importa atualizações de catálogos externos (catálogos de atualizações não Microsoft).
-   Modificar definições de atualização, incluindo aplicabilidade, e metadados de implementação.
-   Atualizações de exportação para catálogos externos.
-   Publique atualizações num servidor de atualização.

Depois de publicar atualizações num servidor de atualização, pode então utilizar o 'Gestor de Configuração' para detetar e implementar essas atualizações nos seus dispositivos geridos.

## <a name="workspaces"></a>Áreas de Trabalho
Ao abrir atualizações Editora, este descorre para o nó de visão geral do Espaço de Trabalho de *Atualizações.*

![Atualiza a consola da Editora](media/console1.png)


Updates Publisher tem quatro espaços de trabalho para ajudar a organizá-lo.


**Atualizao Espaço de Trabalho:** Utilize este espaço de trabalho para [criar](create-updates-with-updates-publisher.md) e [gerir](manage-updates-with-updates-publisher.md) atualizações de software e atualizar pacotes. Este espaço de trabalho inclui a atribuição de atualizações e pacotes para uma publicação, publicação e exportação para outro repositório updates Publisher.

**Publicações Espaço de trabalho:** Este espaço de trabalho é onde [gere publicações.](updates-publisher-publications.md) Uma publicação é um grupo de atualizações que cria para simplificar a exportação e publicação das atualizações.

A gestão de publicações inclui a publicação de atualizações para um servidor para que os seus clientes possam encontrá-las e instalá-las, exportando atualizações e pacotes para utilização por outras instalações da Editora de Atualizações, ou modificando o conteúdo ou detalhes de uma publicação.

**Regras Espaço de trabalho:** Aqui é onde gere regras de [aplicabilidade](updates-publisher-applicability-rules.md) que podem ser guardadas e depois usadas com atualizações que implementa. Existem dois tipos de regras:

-   Regras instaladas – Estas regras ajudam a determinar se um cliente deve instalar uma atualização.
-   Regras instaladas – Estas regras verificam se uma atualização já está instalada.

Espaço de trabalho dos **catálogos:** Utilize este espaço de trabalho para adicionar e [gerir catálogos](updates-publisher-catalogs.md)de atualizações de software. Este espaço de trabalho inclui a importação de atualizações de software desses catálogos para o repositório Updates Publisher.

## <a name="whats-new-in-system-center-updates-publisher"></a>Quais as novidades na Editora de Atualizações do System Center

>[!NOTE] 
> A versão mais recente do System Center Updates Publisher foi lançada a 6 de novembro de 2019. Para mais informações, consulte a secção de História do [Lançamento.](#release-history)

Existe um novo modo de autor System Center Updates Publisher para ajudá-lo a autorar as suas atualizações. Quando ativa o modo de autoria, é adicionado um Espaço de Trabalho de **Categorias** ao ecrã de início. Um novo botão **Detectoid** também é adicionado ao Espaço de Trabalho de **Atualizações** quando o modo de autor está ativado.

### <a name="to-enable-authoring-mode"></a>Para ativar o modo de autoria

1. No canto superior esquerdo da consola, clique no separador **Atualizações Publisher** **Properties** e, em seguida, escolha **Opções**.
1. Vá às opções **de Autor.**
1. Verifique a caixa para **ativar**o modo de autor .

![Ativar o modo de autoria para atualizações da Editora](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Sobre as categorias espaço de trabalho

O espaço de trabalho das categorias permite aos autores da atualização organizar atualizações que pertencem uma si. Por exemplo, se for um OEM, poderá desejar organizar as suas atualizações com base em modelos ou linhas de produtos. Pode definir várias categorias e categorias infantis, mas não categorias de crianças, uma vez que está limitado a dois níveis.

![Screenshot do espaço de trabalho das categorias](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Atribuir uma atualização a uma categoria

Uma vez que tenha sido autor da sua atualização, pode atribuí-la a uma categoria selecionando a atualização e clicando no botão **Categorize.** Também pode clicar na atualização e selecionar **Categorize**.

![Screenshot de categorizar uma atualização](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>Sobre os detectóides

Uma vez ativado o modo de autor, pode criar detectóides para atualizações. Os detectóides são úteis quando tem várias atualizações que usam a mesma regra (ou um conjunto de regras) para determinar a aplicabilidade. Nesses casos, criaria um detectóide e atribuía-o como pré-requisito para uma atualização. Pode atribuir vários detectóides a uma atualização de autoria.


### <a name="create-a-detectoid"></a>Criar um detectóide

1. Abra o espaço de trabalho das **atualizações.**
1. Na fita, clique no botão **Detectóide.**
1. Siga as instruções no assistente para criar o seu detectóide.



![Atualizar pré-requisitos utilizando um detectóide](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>História de lançamento

- [Versão RTW 2019 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Lançado novembro, 6 de novembro de 2019
- [Versão de rollup atualizada 6.0.283.0 a partir de KB4462765](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Lançado a 7 de setembro de 2018.
- [Versão RTW de 2017 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Lançado a 26 de março de 2018.


## <a name="next-steps"></a>Passos seguintes
Para começar, primeiro [instale](install-updates-publisher.md), e depois [configure as opções](updates-publisher-options.md) para updates Publisher.
