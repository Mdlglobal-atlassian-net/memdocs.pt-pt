---
title: Espião de Política
titleSuffix: Configuration Manager
description: Use Policy Spy para visualizar e resolver problemas o sistema de política nos clientes do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6038a3332c63a58d1f3c423491b1aa17aa28b080
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723181"
---
# <a name="policy-spy"></a>Espião de Política

*Aplica-se a: Gestor de Configuração (ramo atual)*

Policy Spy é uma das ferramentas do Gestor de [Configuração.](tools.md) É uma ferramenta para visualizar e resolver problemas o sistema de política nos clientes do Gestor de Configuração. Executar **PolicySpy.exe** para abrir a interface do utilizador. Para obter mais informações sobre o uso da linha de comando, consulte [a sintaxe](#bkmk_policyspy-syntax)da linha de comando .

> [!Important]  
> Executar Policy Spy como administrador. Se não **correr como administrador,** vê o seguinte erro na Informação do Cliente:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="command-line-syntax"></a><a name="bkmk_policyspy-syntax"></a>Sintaxe de linha de comando

O Policy Spy destina-se principalmente a ser utilizado através da sua interface de utilizador. Fornece opções limitadas de linha de comando para apoiar a automatização e o processamento de lotes.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Opção:`/export`
Esta opção exporta silenciosamente a política do computador local ou remoto. `<ExportFilename>`é o nome de ficheiro para o qual a ferramenta salva a política de exportação XML. Se especificar `<computername>` a opção, o Policy Spy exporta a política desse computador em vez do computador local.

> [!Note]  
> Esta opção de linha de comando não fornece uma forma de especificar as credenciais do utilizador. Para utilizar credenciais alternativas para aceder a um computador remoto, utilize o comando **runas** para abrir um novo pedido de comando com as credenciais de segurança necessárias.  


## <a name="usage"></a>Utilização

### <a name="tools-menu"></a>Menu de ferramentas

As seguintes ações estão disponíveis no menu **Ferramentas:**  

- **Open Remote**: Liga-se à política do cliente do Gestor de Configuração num computador remoto. Utilize a caixa de diálogo Connect para recuperar o nome do computador remoto e credenciais de utilizador opcionais. Se a ligação falhar, exibe informações de erro no painel Informação do Cliente. Se a ligação falhar novamente, tente ligar selecionando **Refresh** no menu **Editar** ou premindo F5.  

- **Open File**: Abre um ficheiro de exportação de políticas (XML) criado pela opção **Política de Exportação.** A ferramenta exibe a política exportada exatamente igual à de uma política ao vivo. Desativa algumas funcionalidades que só se aplicam quando se conecta a um cliente real.  

- Atribuição de **máquinas de pedido**: Desencadeia um pedido de atribuição de políticas de máquinas no computador-alvo. Esta funcionalidade é desativada ao visualizar a política exportada.  

- **Avaliar a Política**da Máquina : Desencadeia uma avaliação da política da máquina no computador-alvo. Esta funcionalidade é desativada ao visualizar uma política exportada.  

- **Solicitar atribuições ao utilizador**: Desencadeia um pedido de atribuição de políticas de utilizador para o utilizador atualmente inscrito. Esta funcionalidade só está disponível quando se vê uma política no computador local.  

- **Avaliar a Política do Utilizador**: Aciona uma avaliação da política do utilizador para o utilizador atualmente inscrito. Esta funcionalidade só está disponível quando se vê uma política no computador local.  

- **Política de Reset**: Remove todas as políticas não predefinidas e redefine os cookies de política para o site. Em seguida, desencadeia um pedido de atribuição de políticas de máquinas. Esta funcionalidade é desativada ao visualizar uma política exportada.  

- **Política de Exportação**: Exporta a política do computador-alvo para um ficheiro XML. Veja este ficheiro em qualquer computador com Policy Spy. Para abrir o ficheiro de exportação, selecione **Open File** no menu **Ferramentas.** Esta funcionalidade é desativada ao visualizar uma política exportada.  


### <a name="edit-menu"></a>Editar menu

As seguintes ações estão disponíveis no menu **Editar:**  

- **Eliminar**: Elimina a instância selecionada no painel resultados. Esta ação só é apoiada em casos políticos. Se tentar eliminar outra coisa que não as instâncias de política, a ferramenta apresenta uma mensagem de erro. Esta funcionalidade é desativada ao visualizar uma política exportada.  

- **Atualização**: Atualiza todos os resultados para ver as últimas informações. Todos os nós de árvores que são expandidos antes de refrescar são automaticamente expandidos depois. Se o Policy Spy não se ligou com sucesso à política do computador-alvo, tenta ligar-se novamente. Esta funcionalidade é desativada ao visualizar uma política exportada.  

- **Eventos Claros**: Limpa todos os itens do separador Eventos.  



## <a name="results-pane"></a>Painel de resultados

O painel de resultados apresenta diferentes visões do sistema de política no computador-alvo. Aceda a estas vistas clicando num dos quatro separadores seguintes: 
- [Atual](#bkmk_policyspy-actual)
- [Pedido](#bkmk_policyspy-requested)
- [Padrão](#bkmk_policyspy-default)
- [Eventos](#bkmk_policyspy-events)


### <a name="actual"></a><a name="bkmk_policyspy-actual"></a>Real

Este separador exibe a política atual do cliente. A política atual determina o comportamento de um cliente e o comportamento dos seus agentes clientes, tais como distribuição de software e inventário. O separador apresenta resultados num formato de árvore com um nó de raiz para o espaço de nome do computador e cada espaço de nome específico do utilizador. Expanda um nó de espaço de nome para apresentar uma lista de aulas. Expanda uma classe para apresentar uma lista dos seus casos. A lista de turmas inclui apenas turmas que têm instâncias.


### <a name="requested"></a><a name="bkmk_policyspy-requested"></a>Solicitado

Este separador exibe as atribuições políticas que o cliente recuperou do seu site designado. O separador apresenta resultados em formato de árvore com um nó de raiz para o espaço de nome da máquina e cada espaço de nome específico do utilizador. Expandir um nó de espaço de nome exibe os seguintes nódosos:  

- **Configuração**: Apresenta uma lista de classes de configuração derivadas de CCM_Policy_Config, que inclui objeto seletiva, atribuições e outros.  

- **Definições**: Apresenta todas as definições ativas geradas por políticas. As definições são apresentadas sob o nó de Configuração. 

> [!Note]   
> Várias instâncias podem existir com o mesmo nome porque o cliente não fundiu estas definições num conjunto final de resultados. Policy Spy exibe instâncias sob este nó usando as propriedades RealKey em vez das suas verdadeiras chaves políticas. Correlacionar estas instâncias com o conjunto resultante exibido no separador Atual.  


### <a name="default"></a><a name="bkmk_policyspy-default"></a>Padrão

Este separador apresenta as mesmas informações que o separador **Solicitado.** Também inclui conteúdo dos espaços de nome DefaultMachine e DefaultUser.


### <a name="events"></a><a name="bkmk_policyspy-events"></a>Eventos

Este separador exibe eventos de agentes políticos à medida que acontecem. A vista cria uma subscrição de evento WMI para todos os eventos derivados de CCM_PolicyAgent_Event. A vista mostra um máximo de 200 eventos. Remove os eventos mais antigos do topo da lista, se necessário. Se selecionar o último item da lista, a lista desloca-se automaticamente para baixo à medida que adiciona novos eventos. Caso contrário, a vista mantém a sua posição atual, e deve deslocar-se para baixo ou premir a tecla Fim para ver novos eventos. Esta visão é sempre vazia quando se vê uma política exportada.



## <a name="client-info-pane"></a>Painel de Informações do Cliente
O painel Client Info apresenta uma lista de propriedades para o computador-alvo. Exibe as seguintes propriedades, se disponível:  
- Nome
- ID
- Versão
- Site
- MP atribuído
- DEPUTADO residente
- Proxy MP
- Estado proxy



## <a name="details-pane"></a>Painel de detalhes
O painel de detalhes apresenta informações detalhadas sobre a seleção atual. Se nenhuma seleção estiver ativa, exibe informações sobre o Próprio Policy Spy, incluindo a versão. Caso contrário, apresenta uma representação do formato de objeto de gestão (MOF) do item selecionado.

Policy Spy usa a sua própria rotina de geração MOF para criar um ecrã HTML mais fácil de usar do que o MOF de texto simples gerado pela WMI. Este comportamento permite que o Policy Spy adicione as seguintes funcionalidades para tornar o MOF mais legível:  

- Destaque da sintaxe  

- Objetos e matrizes redentados  

- As propriedades são organizadas em sistema, herdadas e grupos locais. Por padrão, colapsa o sistema e herdou grupos. Você pode ver imediatamente quais propriedades que a instância realmente usa.  

- Copie mof ou copie mof de texto simples para a área de prancheta. Esta funcionalidade é útil para colar o MOF em outras aplicações, ligando diretamente para a ferramenta MofComp.  

Por exemplo si, objetos de Política derivados de CCM_Policy_Policy, o painel de detalhes exibe o corpo político abaixo do MOF que exibe. Se o cliente não descarregou o órgão de política, o Policy Spy exibe uma hiperligação. Clique no link para descarregar o órgão de política diretamente do ponto de gestão do cliente. Se a ferramenta descarregar com sucesso o corpo de política, substitui a hiperligação com o conteúdo da resposta. Caso contrário, o Policy Spy atualiza o visor indicando que o pedido falhou.

