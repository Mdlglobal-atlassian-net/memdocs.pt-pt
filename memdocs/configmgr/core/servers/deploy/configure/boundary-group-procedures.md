---
title: Procedimentos para os grupos de limites
titleSuffix: Configuration Manager
description: Configure grupos de fronteira supéro para organizar logicamente locais de rede relacionados chamados limites.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715796"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Como configurar grupos de limites para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo inclui procedimentos sobre como configurar grupos de fronteira. Antes de começar, certifique-se de compreender os conceitos de grupo de fronteiras. Para mais informações, consulte [os grupos de fronteira](boundary-groups.md).



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a>Criar um grupo de fronteiras  

1.  Na consola de Configuração Manager, vá ao espaço de trabalho da **Administração,** expanda a **Configuração da Hierarquia**e selecione o nó dos **Grupos de Fronteira.**  

2.  No separador **Home,** no grupo **Criar,** selecione **Create Boundary Group**.  

3.  Na caixa de diálogo **do Grupo Criar** Fronteiras, no separador **Geral,** especifique um **Nome** para este grupo de fronteira. Opcionalmente inclua uma **Descrição**.  

4.  Selecione **OK** para salvar o novo grupo de fronteiras, ou continue para a secção seguinte para configurar o grupo de fronteira.  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a>Configurar um grupo de fronteiras  

1.  Na consola de Configuração Manager, vá ao espaço de trabalho da **Administração,** expanda a **Configuração da Hierarquia**e selecione o nó dos **Grupos de Fronteira.**  

2.  Selecione o grupo de limites que pretende modificar e selecione **Propriedades** na fita. Esta ação abre a janela do grupo de fronteira Propriedades.  

Configure as seguintes definições:  
- [Adicionar ou remover limites](#bkmk_add)  
- [Configure a atribuição do site e selecione servidores de sistemas de site](#bkmk_references)  
- [Configurar comportamento de recuo](#bkmk_bg-fallback)  
- [Configure as opções de grupo de limites](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a>Adicionar ou remover limites

Na janela do grupo de fronteiraS Propriedades, utilize o separador **Geral** para modificar os limites que são membros deste grupo de fronteira:  

- Para adicionar limites, selecione **Adicionar**. Na janela Adicionar Limites, selecione a caixa de verificação para um ou mais limites e selecione **OK**.  

- Para remover limites, selecione o limite da lista e selecione **Remover**.  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a>Configure a atribuição do site e selecione servidores de sistemas de site

Para modificar a atribuição do site e configuração do servidor de servidor de site associado, mude para o separador **Referências** na janela propriedades do grupo de fronteira.  

- Para permitir que este grupo de limites seja utilizado pelos clientes para a atribuição do site, selecione **Use este grupo de limites para a atribuição do site**. Em seguida, selecione um site da lista de abandono do **site atribuído.** Para mais informações, consulte a [atribuição do Site.](boundary-groups.md#site-assignment)  

- Para associar servidores de sistema de site disponíveis com este grupo de limites, **selecione Adicionar**. A janela Add Site Systems apenas lista servidores que tenham suportado funções de sistema do site. Selecione a caixa de verificação para um ou mais servidores e selecione **OK**. Adiciona-os como servidores de sistema de site associados para este grupo de fronteira.  

    > [!NOTE]  
    >  Pode selecionar uma combinação de sistemas de sites disponíveis a partir de qualquer site na hierarquia. Os sistemas de site selecionados estão listados no separador **Sistemas** do Site nas propriedades de cada limite que é um membro deste grupo de fronteiras.  

- Para remover um servidor deste grupo de limites, selecione o servidor e, em seguida, **selecione Remover**.  

    > [!NOTE]  
    >  Para parar a utilização deste grupo de fronteira para associar sistemas de site, remova todos os servidores listados como servidores de sistema de site associados.  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a>Configurar comportamento de recuo

Para configurar o comportamento de recuo, mude para o separador **Relacionamentos** na janela propriedades do grupo de fronteira.  

- Criar uma relação com outro grupo de fronteiras:  

  - Selecione **Adicionar**. Na janela Dos Grupos de Fronteira de Fallback, selecione o grupo de limites para configurar.  

  - Desmarque um tempo de recuo para as seguintes funções do sistema do site:  
    - Ponto de distribuição  
    - Ponto de atualização de software  
    - Ponto de gestão  

      > [!Note]  
      > Por exemplo, abre a janela Propriedades para o grupo de fronteira seleções. Na janela dos Grupos de Fronteira seletivas, selecione o grupo de fronteira seletiva. Define o tempo de recuo `20`do ponto de distribuição para . Quando guardar esta configuração, os clientes do grupo de fronteira da Sucursal começarão a procurar conteúdo a partir dos pontos de distribuição do grupo de fronteira do Escritório Principal após 20 minutos.  

  - Para evitar o recuo para um grupo de limites específico, selecione o grupo de limites e, em seguida, selecione **Nunca recuo** para o tipo de função do sistema do site. Esta ação pode incluir o grupo de fronteira do *site padrão*.  

- Para modificar a configuração de uma relação existente, selecione o grupo de limites na lista e selecione **Change**. Esta ação abre a janela dos Grupos de Fronteira sancionadantes para apenas este grupo de fronteiras.  
 
- Para remover uma relação, selecione o grupo de limites na lista e selecione **Remover**.  

Para mais informações, consulte [Fallback.](boundary-groups.md#fallback) 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a>Configure as opções de grupo de limites
<!--1356193-->
A partir da versão 1806, para configurar opções adicionais para clientes neste grupo de fronteira, mude para o separador **Opções.** Para mais informações, consulte as opções do [grupo Boundary para downloads de pares](boundary-groups.md#bkmk_bgoptions).

- **Permitir transferências de pares neste grupo de limites**: Esta opção está ativada por padrão. O ponto de gestão fornece aos clientes uma lista de locais de conteúdo que inclui fontes de pares.  

    - **Durante os downloads dos pares, utilize apenas pares dentro da mesma sub-rede**: Esta definição depende da acima. Se ativar esta opção, o ponto de gestão apenas inclui na lista de dados de conteúdo fontes de pares que estão na mesma sub-rede que o cliente.  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a>Configure um site de recuo para atribuição automática do site  

Se os clientes não estiverem num grupo de fronteira com um site atribuído, atribua-os a este site quando estiverem instalados.

1.  Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2.  No separador **Home** da fita, no grupo **Sites,** selecione **Definições de Hierarquia**.  

3.  No separador **Geral,** selecione a caixa de verificação para **utilizar um site**de recuo . Em seguida, selecione um site da lista de drop-down do **site Fallback.**  

4.  Selecione **OK** para salvar a configuração.  

Para mais informações, consulte a [atribuição do Site.](boundary-groups.md#site-assignment)


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a>Permitir a utilização de pontos de gestão preferenciais  

Para mais informações, consulte [pontos de gestão preferenciais.](boundary-groups.md#bkmk_preferred)

1.  Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. No separador **Home** da fita, no grupo **Sites,** selecione **Definições de Hierarquia**.  

3. No separador **Geral,** os **clientes selecionados preferem utilizar pontos de gestão especificados em grupos de fronteira**.  

4. Selecione **OK** para salvar a configuração.  

