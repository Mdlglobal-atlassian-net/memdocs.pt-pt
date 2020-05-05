---
title: Gerir publicações
titleSuffix: Configuration Manager
description: Gerir grupos de atualizações de software como uma publicação com system center updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0b79e0ec67fa7c1d7ede0af1549c8cda4dd3ee3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717707"
---
# <a name="manage-publications-in-updates-publisher"></a>Gerir publicações em Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Pode utilizar publicações para gerir grupos de atualizações e pacotes como um único objeto. Isto inclui a publicação das atualizações num servidor de gestão e a exportação da publicação como grupo para utilização com outra instalação da Updates Publisher.

## <a name="create-publications"></a>Criar publicações
As publicações são criadas de duas formas:

-   Quando gere atualizações e pacotes no Espaço de Trabalho de **Atualizações,** pode [atribuí-los](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) a uma nova publicação que é criada nessa altura.

-   No Espaço de Trabalho das **Publicações,** pode utilizar o botão **Criar** no separador **Publicação** da fita. Este método permite criar uma publicação para uso futuro. Mais tarde, ao atribuir atualizações, pode utilizar esta publicação.

## <a name="rename-a-publication"></a>Renomear uma publicação
Para renomear uma publicação, selecione a publicação a partir do Espaço de Trabalho das **Publicações**, e, em seguida, no separador **Publicação** da fita, escolha **Editar**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Alterar o tipo de publicação de atualizações numa publicação
A partir do Espaço de Trabalho de **Publicação,** pode modificar o tipo de **publicação** de atualizações e pacotes que são atribuídos a uma publicação.

1. Selecione a publicação que contém as atualizações que pretende modificar e, ** &lt;** em seguida, selecione uma ou mais atualizações ou pacotes da lista de atualizações> membro.

2. Em seguida, no separador **Home,** escolha uma das seguintes opções. As opções disponíveis dependem do tipo de publicação das atualizações selecionadas.

   -   **Automático**
   -   **Conteúdo completo**
   -   **Apenas metadados**

Depois de fazer uma mudança, poderá ter de refrescar a visão da publicação para ver os novos valores.

Para obter informações sobre os diferentes tipos de publicação, consulte [as atualizações e pacotes de atribuição para uma publicação](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Quando define o tipo de publicação de um pacote, todas as atualizações de software nesse pacote são publicadas com o tipo de publicação desse pacote.

## <a name="remove-updates-from-a-publication"></a>Remover atualizações de uma publicação
Para remover atualizações ou pacotes de uma publicação, no **Workspace publicações** selecione a publicação que pretende modificar e, em seguida, selecione as atualizações e pacotes que pretende remover. Em seguida, no separador **Casa** da fita, escolha **Remover**.

Após as atualizações serem removidas de uma publicação, permanecem disponíveis no repositório updates Publisher.

## <a name="publish-publications"></a>Publicar publicações
Quando publica atualizações e pacotes, o Updates Publisher adiciona informações sobre essas atualizações e pacotes (metadados) e possivelmente os binários para as atualizações (conteúdo completo), para um servidor de atualização para implementação para dispositivos.

Antes de ter a opção de publicar, tem de configurar a opção ['Atualizar servidor'](updates-publisher-options.md#update-server) para o Editor de Atualizações. Para abrir esta opção de configuração, vá ao **'Atualizações Workspace** &gt; **Overview'** e selecione **Configure WSUS e Certificado de Assinatura.** Também pode ir à página 'Atualizar servidor' nas opções do Editor de Atualizações.

> [!NOTE]   
> Atualizações A Editora só pode publicar atualizações com 375 megabytes (MB) ou menos em tamanho.

### <a name="to-publish-a-publication"></a>Publicar uma publicação

1. Vá ao Espaço de Trabalho das **Publicações**e, em seguida, selecione uma publicação que contenha o grupo de atualizações e pacotes que pretende publicar ou exportar. Em seguida, escolha **Publicar** a partir do separador **Home** da fita.

2. Na página **Select** do assistente **publicar** pode optar por assinar todas as atualizações com um novo certificado de publicação, mas não pode alterar o tipo de publicação.

3. Conclua o assistente.

   Se a publicação falhar, é-lhe apresentado um link para o ficheiro UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-a-publication"></a>Exportar uma publicação
Pode exportar uma publicação do seu repositório Updates Publisher. Ao fazê-lo exporta as atualizações e pacotes que são atribuídos a essa publicação e cria um catálogo de atualizações. Em seguida, pode [adicionar](updates-publisher-catalogs.md#add-software-update-catalogs) [e,](updates-publisher-catalogs.md#import-updates) em seguida, importar esse catálogo para outra instância da Editora updates. Também pode [exportar atualizações](manage-updates-with-updates-publisher.md#export-updates) que não fazem parte de uma publicação.

Para exportar uma publicação, vá ao Espaço de Trabalho das **Publicações** e selecione a publicação que contém atualizações que pretende exportar. Só é possível selecionar uma publicação de cada vez.

Com a publicação selecionada, escolha **exportar** a partir do separador **Home** da fita e, em seguida, forneça um caminho e nome de arquivo para a exportação do catálogo.

Também tem a opção de exportar (incluir) atualizações de software dependentes como parte da exportação.

## <a name="rename-a-publication"></a>Renomear uma publicação
Para renomear uma publicação, selecione a publicação do Espaço de Trabalho das **Publicações**e, em seguida, escolha **Editar** a partir do separador **Publicação** da fita.

## <a name="delete-a-publication"></a>Apagar uma publicação
Para eliminar uma publicação, selecione a publicação o Espaço de Trabalho das **Publicações**e, em seguida, escolha **Apagar** a partir do separador **Publicação** da fita.

Após a publicação ser removida da Updates Publisher, as atualizações que estavam na publicação permanecem disponíveis no repositório updates Publisher.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Expire ou reative atualizações e pacotes
Pode utilizar o Espaço de Trabalho de **Atualizações** para selecionar e, em seguida, expirar ou reativar atualizações e pacotes. Pode expirar e reativar atualizações e pacotes quantas vezes quiser.

-   **Para expirar atualizações ou pacotes,** no Workspace updates selecione uma ou mais atualizações ou pacotes que não estejam expirados, e depois escolha **Expirar** a partir do separador **Home.** Até publicar a atualização ou o pacote expirado para o Gestor de Configuração, pode reativa-lo.

    Antes de poder remover (eliminar) uma atualização ou pacote personalizado do Gestor de Configuração, tem de expirar e publicar esse estado caducado no 'Gestor de Configuração'. Depois de expiradas atualizações ou pacotes no 'Gestor de Configuração', já não pode implementar ou reativar a atualização ou o pacote.

-   **Para reativar atualizações ou pacotes,** no Workspace de atualizações selecione uma ou mais atualizações que estão caducadas e, em seguida, escolha **Reativar** a partir do separador **Home** da fita. Se a atualização expirada foi previamente publicada como expirada para O Gestor de Configuração, não poderá reativa-la.
