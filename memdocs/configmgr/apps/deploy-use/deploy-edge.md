---
title: Implementar e atualizar Microsoft Edge, versão 77 e mais tarde
titleSuffix: Configuration Manager
description: Como implementar e atualizar o Microsoft Edge, versão 77 e mais tarde com O Gestor de Configuração
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2c3a542355dfa01e5f4f5be12f7b1bac10f30250
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710273"
---
# <a name="microsoft-edge-management"></a>Gestão microsoft edge

*Aplica-se a: Gestor de Configuração (Ramo Atual)*

O novo Microsoft Edge está pronto para o negócio. A partir da versão 1910 do 'Gestor de Configuração', já pode implementar o [Microsoft Edge, a versão 77 e mais tarde](https://docs.microsoft.com/deployedge/) para os seus utilizadores. Um script PowerShell é usado para instalar a construção Edge selecionada. O script também desliga atualizações automáticas para Edge para que possam ser geridas com O Gestor de Configuração.

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a>Implementar microsoft edge
<!--4561024-->
Os administradores podem escolher o canal Beta, Dev ou Estável, juntamente com uma versão do cliente do Microsoft Edge para implementar. Cada lançamento incorpora aprendizagens e melhorias dos nossos clientes e comunidade.

### <a name="prerequisites-for-deploying"></a>Pré-requisitos para a implantação

Para clientes visados com uma implementação do Microsoft Edge:

- A Política de [Execução](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) powerShell não pode ser definida para restrições.
  - PowerShell é executado para executar a instalação.

O dispositivo que executa a consola Do Gestor de Configuração precisa de ter acesso aos seguintes pontos finais:

|Localização|Utilizar|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Informações sobre lançamentos do Microsoft Edge|
|`http://dl.delivery.mp.microsoft.com`|Conteúdo para lançamentos do Microsoft Edge|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a>Verifique as políticas de atualização do Microsoft Edge

#### <a name="configuration-manager-version-1910"></a>Versão do Gestor de Configuração 1910

Na versão 1910, quando o Microsoft Edge é implementado, o script de instalação desliga as atualizações automáticas para o Microsoft Edge para que possam ser geridos com o Gestor de Configuração. Pode alterar este comportamento usando a Política de Grupo. Para mais informações, consulte [Plan a sua implementação das](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) políticas de [atualização](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies)do Microsoft Edge e Microsoft Edge .

#### <a name="configuration-manager-version-2002-and-later"></a>Versão de Gestor de Configuração 2002 e posterior
<!--4561024-->
A partir da versão 2002, pode criar uma aplicação Microsoft Edge que está configurada para receber atualizações automáticas em vez de ter atualizações automáticas desativadas. Esta alteração permite-lhe optar por gerir as atualizações para o Microsoft Edge com o 'Configuração', ou permitir que o Microsoft Edge atualize automaticamente. Ao criar a aplicação, selecione Permitir que **o Microsoft Edge atualize automaticamente a versão do cliente no dispositivo do utilizador final** na página de Definições do Microsoft **Edge.** Se usou anteriormente a Política de Grupo para alterar este comportamento, a Política de Grupo suporá a definição feita pelo Gestor de Configuração durante a instalação do Microsoft Edge.

[![Definição de atualização automática do Microsoft Edge](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>Criar uma implantação

Crie uma aplicação Microsoft Edge utilizando a experiência de aplicação incorporada, o que torna o Microsoft Edge mais fácil de gerir:

1. Na consola, sob a **Software Library,** há um novo nó chamado **Microsoft Edge Management**.
1. Selecione Criar a **Aplicação Microsoft Edge** a partir da fita ou clicando à direita no nó de Gestão microsoft **edge.**

   ![Ação do nó de clique direito do microsoft Edge Management](./media/4561024-create-microsoft-edge-application.png)

1. Na página **de Definições** de Aplicação do assistente, especifique um nome, descrição e localização para o conteúdo da aplicação. Certifique-se de que a pasta de localização do conteúdo que especifica está vazia.
1. Na página definições do **Microsoft Edge,** selecione:
   - O canal para implantar
   - A versão para implantar
   - Se pretender permitir que **o Microsoft Edge atualize automaticamente a versão do cliente no dispositivo do utilizador final** (adicionado na versão 2002)
1. Na página **de Implementação,** decida se pretende implementar a aplicação. Se selecionar **Sim,** pode especificar as definições de implementação da aplicação. Para obter mais informações sobre as definições de implementação, consulte [aplicações de implementação](deploy-applications.md#bkmk_deploy-general).
1. No **Software Center** no dispositivo cliente, o utilizador pode ver e instalar a aplicação.

   ![Página de Definições do Microsoft Edge no assistente de implementação](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>Ficheiros de registo para implementação

|Localização|Registar|Utilizar|
|---|---|---|
| Servidor do site|SMSProv.log|Mostra detalhes se a criação da app ou implementação falhar.|
| [Varia](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| Mostra detalhes se o download de conteúdo falhar|
| Cliente|  AppEnforce.log|Mostra informações de instalação|

## <a name="update-microsoft-edge"></a>Atualizar Microsoft Edge
<!--4831871-->

A partir da versão 1910 do Configuration Manager, verás um nó chamado **Todas as atualizações do Microsoft Edge** no Microsoft Edge **Management**. Este nó ajuda-o a gerir atualizações para todos os canais Do Microsoft Edge.<!--initial edge updates released Jan 15,2020-->

1. Para obter atualizações para o Microsoft Edge, certifique-se de que tem a classificação **de Atualizações** e o produto **Microsoft Edge** selecionado [para sincronização](../../sum/get-started/configure-classifications-and-products.md).

   [![Selecione Microsoft Edge como produto em propriedades de ponto de atualização de software](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. No espaço de trabalho da Biblioteca de **Software,** expanda a **Microsoft Edge Management** e clique no nó all Microsoft Edge **Updates.**

1. Se necessário, clique em **Synchronize Software Updates** na fita para iniciar uma sincronização. Para mais informações, consulte as atualizações de [software Synchronize](../../sum/get-started/synchronize-software-updates.md).

   ![Todos os nó de atualizações do Microsoft Edge](./media/4831871-all-microsoft-edge-updates.png)

1. Gerir e implementar atualizações do Microsoft Edge como qualquer outra atualização, como adicioná-las à sua [regra de implementação automática](../../sum/deploy-use/automatically-deploy-software-updates.md). Algumas das tarefas comuns de atualizações que pode fazer a partir do nó de **Todas as Atualizações** do Microsoft Edge incluem:

   - [Criar uma implementação faseada](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [Implementar manualmente atualizações de software](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [Transferir atualizações de software](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a>Painel de instrumentos da Microsoft Edge Management
<!--3871913-->
*(Introduzido na versão 2002)*

A partir do 'Configuration Manager' 2002, o painel de instrumentos da Microsoft Edge Management fornece-lhe informações sobre a utilização do Microsoft Edge e de outros navegadores. Neste painel, pode:

- Veja quantos dos seus dispositivos têm Microsoft Edge instalado
- Veja quantos clientes têm versões diferentes do Microsoft Edge instaladas.
   - Este gráfico não inclui o Canal Canário.
- Tenha uma visão dos navegadores instalados em todos os dispositivos
- Tenha uma visão do navegador preferido por dispositivo <!--5907383-->
   - Atualmente para o lançamento de 2002, este gráfico estará vazio.

### <a name="prerequisites-for-the-dashboard"></a>Pré-requisitos para o painel de instrumentos

Ative as seguintes propriedades nas classes de inventário de [hardware](../../core/clients/manage/inventory/extend-hardware-inventory.md) abaixo para o dashboard Microsoft Edge Management:

- **Software Instalado - Inteligência de Ativos (SMS_InstalledSoftware)**
   - Código de Software
   - Nome do Produto
   - Versão do produto

- **Navegador Padrão (SMS_DefaultBrowser)**
   - ID do programa do navegador

- **SMS_BrowserUsage (SMS_BrowserUsage)**
   - Nome do navegador
   - UtilizaçãoPercentagede

### <a name="view-the-dashboard"></a>Ver o dashboard

A partir do espaço de trabalho da Biblioteca de **Software,** clique na **Microsoft Edge Management** para ver o painel de instrumentos. Altere a recolha para os dados do gráfico clicando em **Navegar** e escolhendo outra coleção. Por defeito, as suas cinco maiores coleções estão na lista de lançamentos. Quando seleciona uma coleção que não está na lista, a coleção recém-seleccionada ocupa o lugar de baixo da sua lista de drop-down.

[![Painel de instrumentos da Microsoft Edge Management](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="next-steps"></a>Passos seguintes

[Monitorizar aplicações](monitor-applications-from-the-console.md)

[Monitorizar atualizações de software](../../sum/deploy-use/monitor-software-updates.md)

[Gerir e monitorizar as implementações faseadas](../../osd/deploy-use/manage-monitor-phased-deployments.md)
