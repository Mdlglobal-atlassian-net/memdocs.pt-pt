---
title: Monitorizar conteúdo
titleSuffix: Configuration Manager
description: Compreenda como monitorizar os conteúdos distribuídos utilizando a consola 'Gestor de Configuração'.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fafcbffe3231af78ae3a079061accc9f112a181c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110020"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Monitorize o conteúdo que distribui com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize a consola 'Gestor de Configuração' para monitorizar os conteúdos distribuídos, incluindo:  

- O estado de todos os tipos de pacotes para os pontos de distribuição associados.  
- O estado de validação do conteúdo do conteúdo num pacote.  
- O estado dos conteúdos atribuídos a um grupo específico de pontos de distribuição.  
- O estado de conteúdo atribuído a um ponto de distribuição.  
- O estado das funcionalidades opcionais para cada ponto de distribuição (validação de conteúdos, PXE e multicast).  

> [!NOTE]  
> O Gestor de Configuração apenas monitoriza o conteúdo num ponto de distribuição que está na biblioteca de conteúdos. Não monitoriza os conteúdos armazenados no ponto de distribuição em pacotes ou ações personalizadas.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a>Monitorização do estado do conteúdo

O nó **Estado do Conteúdo** da área de trabalho **Monitorização** disponibiliza informações sobre pacotes de conteúdos. Na consola Do Gestor de Configuração, reveja informações como:  

- Nome, tipo e ID do pacote
- Quantos pontos de distribuição um pacote foi enviado para
- Taxa de conformidade
- Quando o pacote foi criado
- Versão fonte

Também encontra informações detalhadas sobre o estado de qualquer pacote, incluindo:  

- Estado de distribuição
- O número de falhas
- Distribuição pendente  
- O número de instalações

Também pode gerir distribuições que permanecem em curso até um ponto de distribuição, ou que não conseguiram distribuir conteúdo com sucesso para um ponto de distribuição:  

- A opção de cancelar ou redistribuir conteúdo está disponível quando visualiza a mensagem de estado de implementação de um trabalho de distribuição para um ponto de distribuição no painel de Detalhes do **Ativo.** Este painel pode ser encontrado no separador **In Progress** ou no separador **Error** do nó de **Status Status.**  
- Além disso, os detalhes do trabalho mostram a percentagem do trabalho que completou quando vê os detalhes de um trabalho no separador **In Progress.** Os detalhes do trabalho também mostram o número de repetições que permanecem para um trabalho. Quando vê os detalhes de um trabalho no separador **Error,** mostra quanto tempo até que ocorra o próximo novo retry.  

Quando cancela uma implementação que ainda não esteja concluída, o trabalho de distribuição para transferir esse conteúdo para:  

- O estado da implementação atualiza-se então para indicar que a distribuição falhou e que foi cancelada por uma ação do utilizador.  
- Este novo estado aparece no separador **Error.**  

> [!NOTE]  
> Quando uma implementação está quase concluída, é possível que a ação para cancelar essa distribuição não seja processada antes da distribuição para o ponto de distribuição estar concluída. Quando isto ocorre, a ação de cancelamento da implantação é ignorada e o estado dos ecrãs de implantação é bem sucedido.  
>
> Embora possa selecionar a opção de cancelar uma distribuição para um ponto de distribuição que está localizado num servidor de site, isso não tem qualquer efeito. Este comportamento deve-se ao facto de o servidor do site e o ponto de distribuição num servidor de site partilharem a mesma loja de conteúdos de instância única. Não há nenhum trabalho de distribuição para cancelar.  

Quando redistribui conteúdo que anteriormente não foi transferido para um ponto de distribuição, o Gestor de Configuração começa imediatamente a reimplantar esse conteúdo para o ponto de distribuição. O Gestor de Configuração atualiza o estado da implementação para refletir o estado em curso dessa reimplantação.  

### <a name="tasks-to-monitor-content"></a>Tarefas para monitorizar o conteúdo

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de monitorização,** expanda o Estado de **Distribuição**e, em seguida, selecione o nó de Status de **Conteúdo.** Este nó exibe as embalagens.  

2. Selecione o pacote que pretende gerir.  

3. No separador **Casa** da fita, no grupo **Conteúdo,** selecione **'Ver Status**. A consola apresenta informações detalhadas sobre o estado do pacote.

Continue a uma das seguintes secções para ações adicionais:

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Cancelar uma distribuição que continua em curso  

1. Mude para o separador **In Progress.**

2. No painel de Detalhes do **Ativo,** clique à direita na entrada para a distribuição que pretende cancelar e selecione **Cancelar**.  

3. Selecione **Sim** para confirmar a ação e cancelar o trabalho de distribuição para esse ponto de distribuição.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Redistribuir conteúdo que não distribuiu  

1. Mude para o separador **Error.**

2. No painel de Detalhes do **Ativo,** clique à direita na entrada para a distribuição que pretende redistribuir e selecione **Redistribuir**.  

3. Selecione **Sim** para confirmar a ação e iniciar o processo de redistribuição nesse ponto de distribuição.  


## <a name="distribution-point-group-status"></a> Estado do grupo de pontos de distribuição

O nó **Estado do Grupo de Pontos de Distribuição** na área de trabalho **Monitorização** fornece informações acerca dos grupos de pontos de distribuição. Pode rever informações como:  

- O nome, descrição e estado do grupo de pontos de distribuição
- Quantos pontos de distribuição são membros do grupo de pontos de distribuição
- Quantos pacotes foram atribuídos ao grupo
- A taxa de conformidade

Também visualiza as seguintes informações detalhadas sobre o estado:  

- Erros para o grupo de pontos de distribuição  
- Quantas distribuições estão em andamento
- Quantos foram distribuídos com sucesso  

### <a name="monitor-distribution-point-group-status"></a>Monitorizar o estado do grupo de pontos de distribuição  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de monitorização,** expanda o Estado de **Distribuição**e, em seguida, selecione o nó de Estado do Grupo de Ponto de **Distribuição.** Exibe os grupos de pontos de distribuição.  

2. Selecione o grupo de pontos de distribuição para o qual pretende informações detalhadas sobre o estado.  

3. No separador **Casa** da fita, selecione **'Ver Status**. Apresenta informações detalhadas sobre o estado do grupo de pontos de distribuição.  


## <a name="distribution-point-configuration-status"></a>Estado da configuração do ponto de distribuição

O nó **Estado da Configuração do Ponto de Distribuição** na área de trabalho **Monitorização** fornece informações acerca do ponto de distribuição. Pode rever quais os atributos que estão habilitados para o ponto de distribuição, como o PXE, multicast, validação de conteúdos. Consulte também o estado de distribuição do ponto de distribuição.

> [!WARNING]  
> O estado de configuração do ponto de distribuição é relativo às últimas 24 horas. Se o ponto de distribuição tiver um erro e recuperar, o estado de erro pode ser apresentado até 24 horas após a recuperação do ponto de distribuição.  

### <a name="monitor-distribution-point-configuration-status"></a>Monitorizar o estado de configuração do ponto de distribuição  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de monitorização,** expanda o Estado de **Distribuição**e, em seguida, selecione o nó de configuração do ponto de **distribuição.**  

2. Selecione um ponto de distribuição.  

3. No painel de resultados, mude para o separador **Detalhes.** Exibe informações sobre o estado para o ponto de distribuição.  


## <a name="client-data-sources-dashboard"></a>Painel de dados de dados do cliente

Utilize o dashboard **Fontes** de Dados do Cliente para entender melhor de onde os clientes obtêm conteúdo no seu ambiente. O dashboard começa a exibir dados depois de os clientes descarregarem conteúdo e reportarem essa informação de volta ao site. Este processo pode demorar até 24 horas.

> [!Note]  
> O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar a função **De Cache de Pares do Cliente** antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../manage/install-in-console-updates.md#bkmk_options).  

Na consola Do Gestor de Configuração, vá ao espaço de trabalho **de Monitorização,** expanda o Estado de **Distribuição**e selecione o nó de Fontes de Dados do **Cliente.** Selecione um período de tempo para aplicar ao painel de instrumentos. Em seguida, selecione o grupo de limites para o qual pretende visualizar informações. Pode pairar sobre os azulejos do rato para ver mais detalhes sobre os diferentes conteúdos ou fontes políticas.

Utilize também o relatório, **Fontes**de Dados do Cliente - Resumo , para visualizar um resumo das fontes de dados do cliente para cada grupo de fronteiras.

### <a name="dashboard-tiles"></a>Os mosaicos do dashboard

O painel inclui os seguintes azulejos:  

#### <a name="client-content-sources"></a>Fontes de Conteúdo do Cliente

Exibe as fontes a partir das quais os clientes obtiveram conteúdo:

- Ponto de distribuição
- [Ponto de distribuição em nuvem](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Peer Cache](../../../plan-design/hierarchy/client-peer-cache.md)
- [Otimização de Entrega](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (a partir da versão 1906)<sup>[Nota 1](#bkmk_note1)</sup>
- Microsoft Update: Os dispositivos reportam esta fonte quando o cliente do Gestor de Configuração descarrega atualizações de software a partir de serviços de nuvem da Microsoft. Estes serviços incluem microsoft update e Microsoft 365 Apps para empresa.

![Conteúdo do Cliente Fontes de azulejos no tablier](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> Começando na versão 1906<!--3555759-->, para incluir a Otimização de Entrega neste dashboard, faça as seguintes ações:
>
> - Configure a definição do cliente, Ative a **instalação de Atualizações Expressas em clientes** no grupo Deatualizações de Software
>
> - Implementar atualizações expressas do Windows 10
>
> Para mais informações, consulte os ficheiros de [instalação do Manage Express para atualizações do Windows 10](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Pontos de distribuição

Apresenta o número de pontos de distribuição que fazem parte do grupo de fronteira selecionado.

#### <a name="clients-that-used-a-distribution-point"></a>Clientes que usaram um ponto de distribuição

Do número de clientes que estão no grupo de fronteira selecionado, este azulejo mostra quantos usaram um ponto de distribuição para obter conteúdo.

#### <a name="peer-cache-sources"></a>Fontes de Cache peer

Para o grupo de fronteira selecionado, este azulejo mostra quantas fontes de cache de pares reportaram o histórico de descarregamento.

#### <a name="clients-that-used-a-peer"></a>Clientes que usaram um par

Do número de clientes que estão no grupo de fronteira selecionado, este azulejo mostra quantos usaram uma fonte de cache para obter conteúdo.

#### <a name="top-distributed-content"></a>Conteúdo distribuído de topo

Os pacotes mais distribuídos por tipo de origem
