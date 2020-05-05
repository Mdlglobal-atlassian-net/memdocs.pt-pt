---
title: Gerir atualizações
titleSuffix: Configuration Manager
description: Gerencie os udpates que implementa e cria com o System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2cb1d1547c23357adbaa26e649e4e22a78e0f39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717812"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Gerir atualizações de software na Editora updates

*Aplica-se a: System Center Updates Publisher*     

No System Center Updates Publisher, utiliza o **Workspace updates** para gerir atualizações de software e pacotes que importou para o repositório.  

As tarefas de gestão incluem duplicação, edição e expiração ou reativação de atualizações e pacotes, e atribuir atualizações e pacotes a publicações. Também pode exportar catálogos personalizados para utilização com outras instalações da Updates Publisher.

Para obter atualizações que pode gerir:
-  [Adicione um catálogo](updates-publisher-catalogs.md#add-software-update-catalogs) de atualizações à sua instalação de Editor de Atualizações
-  [Importe](updates-publisher-catalogs.md#import-updates) as atualizações desse catálogo para o seu repositório.

Também pode [criar as suas próprias atualizações.](create-updates-with-updates-publisher.md)



## <a name="create-a-duplicate-of-an-update"></a>Criar uma duplicação de uma atualização
Pode criar duplicados, ou cópias, de atualizações que estão no seu repositório. Em seguida, pode modificar a cópia em vez de modificar a atualização original. Não é possível criar cópias de pacotes de atualização.

Para criar uma cópia, selecione uma atualização no Espaço de Trabalho das **Atualizações**e, em seguida, escolha **Duplicate**. A cópia da atualização aparece no mesmo local no Espaço de Trabalho de Atualizações com *Cópia adicionada* ao seu nome.

Uma nova cópia que cria tem um estatuto de **Não expirado,** mas de outra forma mantém as definições do original.

## <a name="edit-updates-and-bundles"></a>Editar atualizações e pacotes
Pode selecionar atualizações e pacotes que se encontram no seu repositório para modificá-las.

No **Workspace updates** selecione uma atualização ou pacote e, em seguida, **selecione Editar** a partir do separador **Home** para abrir o assistente de edição. Atualizações e pacotes cada um tem assistentes separados mas intimamente relacionados que apresentam as mesmas opções que os assistentes [Create Update](create-updates-with-updates-publisher.md#use-the-create-update-wizard) ou [Create Bundle.](create-updates-with-updates-publisher.md#use-the-create-bundle-wizard)

Ao editar, pode alterar qualquer detalhe disponível sobre a atualização ou pacote para que possa ser usado no seu ambiente. Por exemplo, pode editar as regras de aplicabilidade ou precedência, ou alterar o idioma. Também pode alterar o produto e o fornecedor para mover a atualização ou o pacote para uma pasta personalizada para atualizações de grupo para sua própria utilização.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Atribuir atualizações e pacotes para uma publicação
Pode selecionar atualizações e pacotes no Espaço de Trabalho de **Atualizações** e, em seguida, escolher **Atribuir** a partir do separador **Casa** da fita para adicioná-las a uma publicação. Isto inicia o assistente de atualizações de **software de atribuição.**
-  Consulte [atualizações e pacotes](#publish-updates-and-bundles-from-the-updates-workspace) de publicação para obter informações sobre como selecionar e publicar atualizações e pacotes como uma única tarefa.
-  Consulte as [publicações de Gestão](updates-publisher-publications.md) para obter informações sobre como gerir grupos de atualizações e pacotes como um único objeto. Depois de atribuir atualizações a uma publicação, pode gerir essa publicação, que por sua vez inclui todas as atualizações atribuídas.

Quando atribui atualizações a uma publicação:

-   Pode incluir atualizações e pacotes expirados e não expirados na mesma publicação.

-   Especifique o tipo de publicação:

    -   **Conteúdo Completo** – Isto publica o conteúdo completo da atualização para o seu Servidor WSUS. Isto inclui metadados e binários de atualização.

    -   **Metadados apenas** – Isto publica apenas os metadados; binários de atualização não são publicados. Pode escolher esta opção quando pretender recolher dados de conformidade.

    -   **Automático** – Este modo só está disponível quando tiver ligado atualizações Editora a Gestor de Configuração (Consulte a opção [ConfigMgr Server.)](updates-publisher-options.md#configmgr-server)

    Com este tipo, atualiza o Gestor de Configurações do Editor para determinar se as atualizações ou pacotes devem ser publicados com conteúdo completo ou apenas metadados. O conteúdo completo para uma atualização só é publicado quando essa atualização cumprir o limiar de contagem de **clientes solicitado** e o limiar de tamanho de fonte do **pacote,** que são especificados na página do **Servidor ConfigMgr** das opções do Editor de Atualizações.

-   Selecione uma publicação:

    -   Utilize a atualização de **software Atribua para publicações existentes** quando já criou uma publicação que pretende utilizar. Esta opção não está disponível até que exista pelo menos uma publicação.

    -   Utilize a **atualização** de software Atribuir a uma nova publicação quando não tiver uma publicação adequada. Isto criará uma nova publicação com o nome que especifica.

Depois de atribuir atualizações a uma publicação, pode utilizar o **Espaço de Trabalho** de Publicação para [publicar](updates-publisher-publications.md#publish-publications) ou [exportar](updates-publisher-publications.md#export-a-publication) a publicação em grupo.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publique atualizações e pacotes do Espaço de Trabalho de Atualizações
Quando publica atualizações e pacotes, o Updates Publisher adiciona informações sobre essas atualizações e pacotes (metadados) e possivelmente os binários para as atualizações (conteúdo completo), para um servidor de atualização para implementação para dispositivos.

Antes de ter a opção de publicar, tem de configurar a opção ['Atualizar servidor'](updates-publisher-options.md#update-server) para o Editor de Atualizações. Para abrir esta opção de configuração, vá ao **'Atualizações Workspace** &gt; **Overview'** e selecione **Configure WSUS e Certificado de Assinatura.** Também pode ir à página 'Atualizar servidor' nas opções do Editor de Atualizações.

Existem duas formas de publicar atualizações e pacotes:
-   Diretamente do Espaço de Trabalho das Atualizações. (Consulte o seguinte procedimento, *para publicar atualizações e pacotes*.)
-   Como [publicação](updates-publisher-publications.md#publish-publications) do Espaço de Trabalho das Publicações.  

> [!NOTE]   
> Atualizações A Editora só pode publicar atualizações com 375 megabytes (MB) ou menos em tamanho.

### <a name="to-publish-updates-and-bundles"></a>Para publicar atualizações e pacotes
1.  Vá ao **Workspace updates** e selecione uma ou mais atualizações e pacotes que pretende publicar. Em seguida, escolha **Publicar** a partir do separador **Home** da fita.

2.  Na página **Select** do assistente **publicar,** selecione como pretende publicar as atualizações. As opções são as mesmas que para a atribuição de [atualizações](#assign-updates-and-bundles-to-a-publication): **Conteúdo Completo,** **Apenas Metadados,** ou **Automática**.

    Também pode optar por assinar todas as atualizações com um novo certificado de publicação.

3.  Conclua o assistente.

Se a publicação falhar, é-lhe apresentado um link para o ficheiro UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-updates"></a>Atualizações das exportações
Pode exportar atualizações e pacotes do seu repositório Updates Publisher para criar um catálogo de atualizações personalizada. Em seguida, pode [adicionar](updates-publisher-catalogs.md#add-software-update-catalogs) [e,](updates-publisher-catalogs.md#import-updates) em seguida, importar esse catálogo para outra instância da Editora updates. (Também pode [exportar atualizações como publicação](updates-publisher-publications.md#export-a-publication).)

Para exportar diretamente, vá a **Atualizações Workspace** > **Todas as Atualizações** de Software e selecione uma ou mais atualizações e pacotes. Não é possível exportar um fornecedor ou pasta de produto, mas pode selecionar uma pasta e, em seguida, selecionar as atualizações nessa pasta para exportação.

Com uma ou mais atualizações selecionadas, escolha **exportar** a partir do separador **Home** da fita e, em seguida, forneça um caminho e nome de arquivo para a exportação do catálogo.

Terá a opção de exportar (incluir) atualizações de software dependentes.

## <a name="delete-updates-and-bundles"></a>Eliminar atualizações e pacotes
Pode eliminar atualizações e pacotes de atualizações para removê-las do repositório updates Publisher.

Vá a **Atualizações Workspace** > **Todas as Atualizações** de Software e selecione uma ou mais atualizações individuais. Em seguida, escolha **Apagar** a partir do separador **Inicial** da fita.

-   Se a sua seleção contiver apenas atualizações ou pacotes que não tenham sido publicados ou que tenham expirado, é-lhe pedido que confirme a eliminação antes de serem removidas.

-   Se a sua seleção incluir uma atualização ou pacote que tenha sido publicado e ainda não tenha expirado, é-lhe dado um aviso. Deve [expirar](updates-publisher-publications.md#expire-or-reactivate-updates-and-bundles) essas atualizações e, em seguida, publicar essa alteração antes de as apagar do repositório.  

Se eliminar uma atualização ou pacote de um fornecedor e, em seguida, importar novamente esse catálogo, essa atualização é restaurada no seu repositório.

## <a name="manage-vendor-and-product-folders"></a>Gerir as pastas do fornecedor e do produto
Para ver uma lista de fornecedores e produtos para cada fornecedor para o qual tenha importado ou criado atualizações, vá a Atualizações do **Workspace** > **Overview** > **Todas as Atualizações**de Software .

As pastas para fornecedores e produtos são criadas automaticamente pela Updates Publisher quando utiliza um assistente para importar ou criar uma atualização ou pacote de software. Também pode criar estas pastas manualmente.

-   Para criar uma pasta de fornecedor, no painel de navegação do Espaço de Trabalho das **Atualizações,** clique à direita em **Todas as Atualizações**de Software e, em seguida, escolha **Criar fornecedor**.

-   Para criar uma pasta de produto sob uma pasta do fornecedor, clique à direita na pasta do fornecedor e escolha **Criar produto**.

Além de criar pastas, pode mudar o nome ou eliminar qualquer remessa ou pasta de produto no seu repositório. Para isso, clique na pasta e escolha a opção que deseja, **Renomear** ou **Eliminar**. A eliminação de uma pasta remove todas as atualizações e pacotes dessa pasta e as suas pastas de produto do repositório Updates Publisher.

Pode mover atualizações entre o fornecedor e as pastas do produto, incluindo as pastas que cria. Para mover uma atualização ou um pacote para uma nova pasta, tem de selecionar e **editar** a atualização ou o pacote. Em seguida, na página **informação** do assistente de atualização editar pode reatribuir o fornecedor e o produto. Quando o assistente **de Atualização de Edição** estiver concluído, a alteração aplica-se e a atualização passa para a nova pasta.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Ver o XML de uma atualização ou pacote
Pode selecionar uma única atualização ou pacote no Espaço de Trabalho de **Atualizações** e, em seguida, escolher **o View** XML para exibir a estrutura XML dessa atualização. Não existem opções para editar a estrutura XML diretamente.
