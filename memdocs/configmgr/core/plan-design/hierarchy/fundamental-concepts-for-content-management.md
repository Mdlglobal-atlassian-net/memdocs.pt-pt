---
title: Noções básicas de gestão de conteúdo
titleSuffix: Configuration Manager
description: Utilize ferramentas e opções no Gestor de Configuração para gerir o conteúdo que implementa.
ms.date: 12/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cb91e62c4ffce37068b2de5e125865e28ff8c53b
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878957"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Conceitos fundamentais para gestão de conteúdos em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração suporta um sistema robusto de ferramentas e opções para gerir conteúdos de software. Implementações de software tais como aplicações, pacotes, atualizações de software e implementações de SO todos precisam de conteúdo. O Gestor de Configuração armazena o conteúdo em ambos os servidores do site e pontos de distribuição. Este conteúdo requer uma grande quantidade de largura de banda da rede quando está a ser transferido entre locais. Para planear e utilizar eficazmente a infraestrutura de gestão de conteúdos, primeiro compreenda as opções e configurações disponíveis. Em seguida, considere como usá-los para melhor se adaptar ao seu ambiente de networking e necessidades de implementação de conteúdos.  

> [!TIP]  
> Para obter mais informações sobre o processo de distribuição de conteúdos e encontrar ajuda no diagnóstico e resolução de problemas gerais de distribuição de conteúdos, consulte [a Compreensão e a resolução de conteúdos no Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

As seguintes secções são conceitos-chave para a gestão de conteúdos. Quando um conceito precisar de informações complexas ou adicionais, são fornecidas hiperligações para direcioná-lo para esses detalhes.


## <a name="accounts-used-for-content-management"></a>Contas utilizadas para a gestão de conteúdos

As contas que se seguem podem ser utilizadas com a gestão de conteúdos:  

### <a name="network-access-account"></a>Conta de acesso à rede

Usado pelos clientes para se conectar a um ponto de distribuição e aceder a conteúdos. Por padrão, a conta de computador é experimentada primeiro.  

Esta conta também é usada por pontos de distribuição de puxar para descarregar conteúdo de um ponto de distribuição de origem numa floresta remota.  

A partir da versão 1806, alguns cenários já não requerem uma conta de acesso à rede. Pode permitir que o site utilize http melhorado com autenticação de Diretório Ativo Azure.<!--1358228-->

Para mais informações, consulte [a conta](accounts.md#network-access-account)de acesso à Rede .

### <a name="package-access-account"></a>Conta de acesso ao pacote

Por predefinição, o Gestor de Configuração dá acesso aos conteúdos num ponto de distribuição para as contas genéricas de acesso Utilizadores e Administradores. No entanto, pode configurar permissões adicionais para restringir o acesso.

Para mais informações, consulte a conta de acesso ao [pacote](accounts.md#package-access-account).


## <a name="bandwidth-throttling-and-scheduling"></a>Limitação de largura de banda e agendamento

Tanto a limitação como o agendamento são opções que o ajudam a controlar quando o conteúdo é distribuído de um servidor do site para pontos de distribuição. Estas capacidades são semelhantes, mas não diretamente relacionadas com controlos de largura de banda para replicação baseada em ficheiros site-to-site.  

Para mais informações, consulte Gerir a [largura de banda da rede](manage-network-bandwidth.md).


## <a name="binary-differential-replication"></a>Replicação diferencial binária

O Gestor de Configuração utiliza replicação diferencial binária (BDR) para atualizar o conteúdo que distribuiu anteriormente para outros sites ou para pontos de distribuição remotos. Para suportar a redução da utilização da largura de banda da BDR, instale a função de **Compressão Diferencial Remota** nos pontos de distribuição. Para mais informações, consulte os [pré-requisitos](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq)do ponto de distribuição .

O BDR minimiza a largura de banda da rede utilizada para enviar atualizações para conteúdos distribuídos. Reenvia apenas o conteúdo novo ou alterado em vez de enviar todo o conjunto de ficheiros de origem de conteúdo cada vez que altera esses ficheiros.  

Quando o BDR é utilizado, o Gestor de Configuração identifica as alterações que ocorrem aos ficheiros de origem para cada conjunto de conteúdo que distribuiu anteriormente.  

- Quando os ficheiros no conteúdo de origem mudam, o site cria uma nova versão incremental do conteúdo. Em seguida, replica apenas os ficheiros alterados para sites de destino e pontos de distribuição. Um ficheiro é considerado alterado se o renomear ou mover, ou se alterar o conteúdo do ficheiro. Por exemplo, se substituir um único ficheiro de condutor por um pacote de controlador que distribuiu anteriormente em vários sites, apenas o ficheiro de condutor alterado é replicado.  

- O Gestor de Configuração suporta até cinco versões incrementais de um conjunto de conteúdos antes de reenviar todo o conjunto de conteúdos. Após a quinta atualização, a próxima alteração ao conjunto de conteúdos faz com que o site crie uma nova versão do conjunto de conteúdos. O Gestor de Configuração distribui então a nova versão do conjunto de conteúdos para substituir o conjunto anterior e qualquer uma das suas versões incrementais. Após a distribuição do novo conjunto de conteúdos, as alterações incrementais posteriores aos ficheiros de origem são novamente replicadas pelo BDR.  

A BDR é suportada entre cada site principal e site subordinado numa hierarquia. O BDR é suportado dentro de um site entre o servidor do site e os seus pontos de distribuição regulares. No entanto, pontos de distribuição de puxar e pontos de distribuição na nuvem não suportam o BDR para transferir conteúdo. Os pontos de distribuição suportam deltas de nível de ficheiro, transferindo novos ficheiros, mas não blocos dentro de um ficheiro.

As aplicações utilizam sempre a replicação diferencial de binários. O BDR é opcional para pacotes e não está ativado por padrão. Para utilizar o BDR para pacotes, ative esta funcionalidade para cada embalagem. Selecione a opção Ativar a **replicação diferencial binária** quando criar ou editar um pacote.


### <a name="bdr-or-delta-replication"></a>Réplica de BDR ou delta

<!-- SCCMDocs#1209 -->
As listas seguintes resumem as diferenças entre a *replicação diferencial binária* (BDR) e a *replicação delta*.

#### <a name="summary-of-binary-differential-replication"></a>Resumo da replicação diferencial binária

- Termo do Gestor de Configuração para **compressão diferencial remota** do Windows
- *Diferenças*de nível de bloco
- Sempre habilitado para apps
- Opcional em pacotes legados
- Se um ficheiro já existir no ponto de distribuição, e houver uma alteração, o site usa o BDR para replicar a alteração do nível de bloco em vez de todo o ficheiro.

#### <a name="summary-of-delta-replication"></a>Resumo da replicação delta

- *Diferenças*de nível de ficheiro
- Por defeito, não configurável
- Quando um pacote muda, o site verifica as alterações aos ficheiros individuais em vez de todo o pacote.
    - Se um ficheiro mudar, utilize o BDR para fazer o trabalho
    - Se houver um novo ficheiro, copie o novo ficheiro


## <a name="peer-caching-technologies"></a>Tecnologias de cache de pares

<!-- SCCMDocs#1044 -->

O Gestor de Configuração suporta várias opções para gerir conteúdos entre dispositivos pares na mesma rede:

- [BranchCache](#branchcache)
- [Otimização de Entrega](#delivery-optimization)
- [Cache de pares do Gestor de Configuração](#peer-cache)

Utilize a tabela seguinte para comparar as principais características destas tecnologias:

| Funcionalidade  | Cache de pares &nbsp;  | &nbsp;Otimização de Entrega  | BranchCache  |
|---------|---------|---------|---------|
| Através de subredes | Sim | Sim | Não |
| Limitar largura de banda | Sim (BITS) | Sim (nativo) | Sim (BITS) |
| Conteúdo parcial | Sim | Sim | Sim |
| Tamanho da cache de controlo no disco | Sim | Sim | Sim |
| Descoberta de fonte de pares | Manual (definição de cliente) | Automático | Automático |
| Descoberta de pares | Através de ponto de gestão usando grupos de fronteira | Serviço de nuvem DO | Difusão |
| Relatórios | Painel de dados do cliente | Painel de dados do cliente | Painel de dados do cliente |
| Controlo de utilização wan | Grupos de limites | DO GroupID | Subnet apenas |
| Conteúdo suportado | Todos os conteúdos da ConfigMgr | Atualizações do Windows, controladores, aplicações de loja | Todos os conteúdos da ConfigMgr |
| Controlo de políticas | Definições do agente cliente | Definições do agente cliente (parcial) | Definições do agente cliente |

### <a name="recommendations"></a>Recomendações

- Gestão moderna: Se já está a usar ferramentas modernas como intune, implemente a Otimização de Entrega

- Gestor de Configuração e cogestão: Utilize uma combinação de cache de pares e otimização de entrega. Utilize cache de pares com pontos de distribuição no local e utilize a Otimização de Entrega para cenários de nuvem.

- BranchCache existente implementado: Use as três tecnologias paralelamente. Utilize cache de pares e otimização de entrega para cenários que não são suportados pela BranchCache.


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) é uma tecnologia Windows. Os clientes que suportam a BranchCache, e descarregaram uma implementação que configura para a BranchCache, e depois servem como fonte de conteúdo para outros clientes ativados pela BranchCache.  

Por exemplo, tem um ponto de distribuição que executa o Windows Server 2012 ou mais tarde, e está configurado como um servidor BranchCache. Quando o primeiro cliente ativado pela BranchCache solicita conteúdo a partir deste servidor, o cliente descarrega esse conteúdo e cache-lo.  

- Esse cliente disponibiliza então o conteúdo para clientes adicionais ativados pela BranchCache na mesma subnet que também cache o conteúdo.  
- Outros clientes na mesma subnet não têm de descarregar conteúdo a partir do ponto de distribuição.  
- O conteúdo é distribuído por vários clientes para futuras transferências.  

Para mais informações, consulte [Suporte para Windows BranchCache](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache).

## <a name="delivery-optimization"></a>Otimização de Entrega

<!-- 1324696 -->
Utiliza grupos de limites do Gestor de Configuração para definir e regular a distribuição de conteúdos através da sua rede corporativa e para escritórios remotos. A [Otimização](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) de Entrega do Windows é uma tecnologia baseada em nuvem, peer-to-peer para partilhar conteúdos entre dispositivos Windows 10. Configure a Otimização da Entrega para utilizar os seus grupos de fronteira ao partilhar conteúdo entre pares. As definições do cliente aplicam o identificador de grupo de limites como o identificador do grupo de otimização de entrega no cliente. Quando o cliente comunica com o serviço de nuvem de otimização de entrega, utiliza este identificador para localizar os pares com o conteúdo. Para mais informações, consulte as definições do cliente de otimização de [entrega.](../../clients/deploy/about-client-settings.md#delivery-optimization)

A Otimização da Entrega é a tecnologia recomendada para otimizar a entrega de ficheiros de instalação expresso do Windows 10 para atualizações de qualidade do Windows 10. A partir da versão 1910 do Gestor de Configuração, o acesso da DeliveryInternet ao serviço de nuvem de otimização de entregas é um requisito para utilizar a sua funcionalidade peer-to-peer. Para obter informações sobre os pontos finais da Internet necessários, consulte [frequentemente perguntas para otimização de entregas.](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions) A otimização pode ser usada para todas as atualizações do Windows. Para mais informações, consulte otimizar a [entrega da atualização do Windows 10.](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)


## <a name="microsoft-connected-cache"></a>Cache Ligada da Microsoft

<!--3555764-->
A partir da versão 1906, pode instalar um servidor Microsoft Connected Cache nos seus pontos de distribuição. Ao gravar este conteúdo no local, os seus clientes podem beneficiar da funcionalidade de Otimização de Entrega, mas pode ajudar a proteger os links WAN.

> [!NOTE]
> A partir da versão 1910, esta funcionalidade chama-se **Microsoft Connected Cache**. Anteriormente era conhecido como Delivery Optimization In-Network Cache.

Este servidor de cache funciona como uma cache transparente a pedido para conteúdos descarregados pela Otimização da Entrega. Utilize as definições do cliente para se certificar de que este servidor é oferecido apenas aos membros do grupo de limites do Gestor de Configuração local.

Esta cache é separada do conteúdo do ponto de distribuição do Gestor de Configuração. Se escolher a mesma unidade que a função do ponto de distribuição, armazena conteúdo separadamente.

Para mais informações, consulte o [Microsoft Connected Cache no 'Configuração Manager'.](microsoft-connected-cache.md)


## <a name="peer-cache"></a>Cache de pares

A cache de pares de clientes ajuda-o a gerir a implementação de conteúdos para clientes em locais remotos. A cache peer é uma solução de Gestor de Configuração incorporada que permite aos clientes partilhar conteúdo com outros clientes diretamente a partir da sua cache local.

Primeiro implemente as definições do cliente que permitem a cache dos pares para uma coleção. Em seguida, os membros dessa coleção podem atuar como uma fonte de conteúdo de pares para outros clientes no mesmo grupo de fronteira.

A partir da versão 1806, as fontes de cache dos pares dos clientes podem dividir o conteúdo em partes. Estas peças minimizam a transferência de rede para reduzir a utilização de WAN. O ponto de gestão fornece um rastreio mais detalhado das partes de conteúdo. Tenta eliminar mais do que um download do mesmo conteúdo por grupo de fronteiras.<!--1357346-->

Para mais informações, consulte [o cache peer para clientes do Gestor de Configuração](client-peer-cache.md).


## <a name="windows-pe-peer-cache"></a>Cache ponto a ponto do Windows PE

Quando implementa um novo SISTEMA com 'Gestor de Configuração', os computadores que executam a sequência de tarefas podem utilizar a cache de pares do Windows PE. Descarregam conteúdo a partir de uma fonte de cache de pares em vez de de um ponto de distribuição. Este comportamento ajuda a minimizar o tráfego de WAN em cenários de sucursais onde não há ponto de distribuição local.

Para mais informações, consulte a [cache dos pares do Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="windows-ledbat"></a>Windows LEDBAT

<!--1358112-->
O Windows Low Delay Background Transport (LEDBAT) é uma funcionalidade de controlo de congestionamento de rede do Windows Server para ajudar a gerir as transferências de rede de fundo. Para os pontos de distribuição em versões suportadas do Windows Server, permita uma opção para ajudar a ajustar o tráfego de rede. Em seguida, os clientes só usam largura de banda da rede quando estão disponíveis.

Para obter mais informações sobre o Windows LEDBAT em geral, consulte o post de blog [new transport advancements.](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726)

Para obter mais informações sobre como utilizar o Windows LEDBAT com pontos de distribuição do Gestor de Configuração, consulte a definição para ajustar a velocidade de **descarregamento para utilizar a largura de banda da rede não utilizada (Windows LEDBAT)** quando [configurar as definições gerais de um ponto de distribuição](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).


## <a name="client-locations"></a>Localizações de clientes

Seguem-se as localizações a partir das quais os clientes acedem a conteúdo:  

- **Intranet** (no local):  

    - Os pontos de distribuição podem utilizar HTTP ou HTTPs.  

    - Utilize apenas um ponto de distribuição em nuvem para recuo quando não estiverem disponíveis pontos de distribuição no local.  

- **Internet**:  

    - Requer pontos de distribuição virados para a Internet para aceitar HTTPS.  

    - Pode usar um ponto de distribuição em nuvem ou gateway de gestão de nuvem (CMG).  

        A partir da versão 1806, um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados e o custo exigidos dos VMs Azure. Para mais informações, consulte [Modificar um CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md).

- **Grupo de trabalho:**  

    - Requer pontos de distribuição para aceitar HTTPS.  

    - Pode usar um ponto de distribuição em nuvem ou CMG.  


## <a name="content-source-priority"></a>Prioridade de fonte de conteúdo

Quando um cliente precisa de conteúdo, faz um pedido de localização de conteúdo para o ponto de gestão. O ponto de gestão devolve uma lista de localizações de origem válidas para o conteúdo solicitado. Esta lista varia consoante o cenário específico, tecnologias em uso, design do site, grupos de fronteira e configurações de implementação. A lista seguinte contém todos os possíveis locais de origem de conteúdo que um cliente pode utilizar, na ordem em que os prioriza:  

1. O ponto de distribuição no mesmo computador que o cliente
2. Uma fonte de pares na mesma rede subnet
3. Um ponto de distribuição na mesma subnet de rede
4. Uma fonte de pares no mesmo grupo de fronteiras
5. Um ponto de distribuição no atual grupo de fronteiras
6. Um ponto de distribuição em um grupo de fronteira vizinho configurado para recuo
7. Um ponto de distribuição no grupo de fronteira do site padrão
8. O serviço de nuvem Windows Update
9. Um ponto de distribuição virado para a Internet
10. Um ponto de distribuição de nuvem em Azure

> [!Note]  
> <!-- SCCMDocs#1607 -->Otimização de Entrega não é aplicável a esta priorização de origem. Esta lista é como o cliente do Gestor de Configuração encontra conteúdo. O Windows Update Agent descarrega conteúdo para otimização de entrega. Se o Windows Update Agent não conseguir encontrar o conteúdo, então o cliente do Gestor de Configuração utiliza esta lista para o procurar.

## <a name="content-library"></a>Biblioteca de conteúdos

A biblioteca de conteúdos é a loja de conteúdo de uma instância única no Gestor de Configuração. Esta biblioteca reduz o tamanho total do conteúdo que distribui.  

- Saiba mais sobre a biblioteca de [conteúdos.](the-content-library.md)
- Utilize a ferramenta de limpeza da biblioteca de [conteúdos](content-library-cleanup-tool.md) para remover conteúdos que já não estão associados a uma aplicação.  


## <a name="distribution-points"></a>Pontos de distribuição

O Gestor de Configuração utiliza pontos de distribuição para armazenar ficheiros que são necessários para que o software seja executado em computadores clientes. Os clientes devem ter acesso a pelo menos um ponto de distribuição a partir do qual podem descarregar os ficheiros para conteúdos que você implementa.  

O ponto de distribuição básico (não especializado) é geralmente referido como um ponto de distribuição padrão. Existem duas variações no ponto de distribuição padrão que recebem especial atenção:  

- **Ponto de distribuição**de puxar : Uma variação de um ponto de distribuição onde o ponto de distribuição obtém conteúdo de outro ponto de distribuição (um ponto de distribuição de origem). Este processo é semelhante à forma como os clientes descarregam conteúdo a partir de pontos de distribuição. Os pontos de distribuição de puxar podem ajudá-lo a evitar estrangulamentos de largura de banda da rede que ocorrem quando o servidor do site deve distribuir diretamente o conteúdo para cada ponto de distribuição. [Utilize um ponto de distribuição de puxar](use-a-pull-distribution-point.md).

- **Ponto de distribuição**em nuvem : Uma variação de um ponto de distribuição instalado no Microsoft Azure. [Aprenda a usar um ponto](use-a-cloud-based-distribution-point.md)de distribuição em nuvem .  

Os pontos de distribuição padrão suportam uma gama de configurações e funcionalidades:  

- Utilize controlos como **horários** ou estrangulamento de largura de **banda** para ajudar a controlar esta transferência.  

- Utilize outras opções, incluindo **conteúdo pré-encenado,** e **pontos de distribuição de puxar** para minimizar e controlar o consumo da rede.  

- **BranchCache,** **cache de pares**e **Otimização** de Entrega são tecnologias peer-to-peer para reduzir a largura de banda da rede que é usada quando implementa conteúdo.  

- Existem diferentes configurações para implementações de OS, tais como **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** e **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**  

- Opções para **dispositivos móveis**  
  
Cloud e pull pontos de distribuição suportam muitas destas mesmas configurações, mas têm limitações específicas para cada variação de ponto de distribuição.  


## <a name="distribution-point-groups"></a>Grupos de pontos de distribuição

Os grupos de pontos de distribuição são agrupamentos lógicos de pontos de distribuição que podem simplificar a distribuição de conteúdos.  

Para mais informações, consulte [Gerir grupos](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)de pontos de distribuição .


## <a name="distribution-point-priority"></a>Prioridade de pontos de distribuição

O valor de prioridade do ponto de distribuição baseia-se na quantidade de tempo necessária para transferir implementações anteriores para esse ponto de distribuição.  

- Este valor é auto-afinação. Está definido em cada ponto de distribuição para ajudar o Gestor de Configuração a transferir mais rapidamente conteúdo para mais pontos de distribuição.  

- Quando distribui conteúdo para vários pontos de distribuição ao mesmo tempo, ou para um grupo de pontos de distribuição, o site envia primeiro o conteúdo para o servidor com a maior prioridade. Em seguida, envia esse mesmo conteúdo para um ponto de distribuição com uma prioridade menor.  

- A prioridade do ponto de distribuição não substitui a prioridade de distribuição dos pacotes. A prioridade do pacote continua a ser o fator decisivo de quando o site envia conteúdos diferentes.  

Por exemplo, tem um pacote que tem uma alta prioridade de pacote. Distribui-se para um servidor com uma prioridade de baixo ponto de distribuição. Este pacote de alta prioridade transfere-se sempre antes de um pacote que tem uma prioridade menor. A prioridade do pacote aplica-se mesmo que o site distribua pacotes prioritários mais baixos para servidores com prioridades de ponto de distribuição mais elevadas.

A alta prioridade do pacote garante que o Gestor de Configuração distribui esse conteúdo para pontos de distribuição antes de enviar quaisquer pacotes com uma prioridade menor.  

> [!NOTE]  
> Os pontos de distribuição de extração também utilizam um conceito de prioridade para ordenar a sequência dos respetivos pontos de distribuição de origem.  
>
> - A prioridade do ponto de distribuição para transferências de conteúdos para o servidor é distinta da prioridade que os pontos de distribuição de puxar usam. Os pontos de distribuição de puxar usam a sua prioridade quando procuram conteúdo a partir de um ponto de distribuição de fonte.  
> - Para mais informações, consulte [Utilize um ponto de distribuição de puxar](use-a-pull-distribution-point.md).  


## <a name="fallback"></a>Contingência

Várias coisas mudaram com a filial atual do Gestor de Configuração na forma como os clientes encontram um ponto de distribuição que tem conteúdo, incluindo recuo.

Os clientes que não conseguem encontrar conteúdo a partir de um ponto de distribuição associado ao seu grupo de fronteira atual recuam para usar localizações de fonte de conteúdo associadas a grupos de fronteira vizinhos. Para ser usado para o recuo, um grupo de fronteira sinuoso deve ter uma relação definida com o atual grupo de fronteiras do cliente. Esta relação inclui um tempo configurado que deve passar perante um cliente que não consegue encontrar conteúdo localmente inclui fontes de conteúdo do grupo de fronteira do vizinho como parte da sua pesquisa.

Os conceitos de pontos de distribuição preferidos deixaram de ser utilizados e as definições para **permitir localizações** de origem de recuo para conteúdos já não estão disponíveis ou executadas.

Para mais informações, consulte [os grupos de fronteira](../../servers/deploy/configure/boundary-groups.md).


## <a name="network-bandwidth"></a>Largura de banda de rede

Para ajudar a gerir a quantidade de largura de banda da rede que é usada quando distribui conteúdo, pode utilizar as seguintes opções:  

- **Conteúdo pré-encenado**: Transferir conteúdo para um ponto de distribuição sem distribuir o conteúdo pela rede.  

- **Agendamento e estrangulamento**: Configurações que o ajudam a controlar quando e como o conteúdo é distribuído em pontos de distribuição.  

Para mais informações, consulte Gerir a [largura de banda da rede](manage-network-bandwidth.md).


## <a name="network-connection-speed-to-content-source"></a>Velocidade da ligação de rede à origem de conteúdo

Várias coisas mudaram com a filial atual do Gestor de Configuração na forma como os clientes encontram um ponto de distribuição que tem conteúdo. Estas alterações incluem a velocidade da rede para uma fonte de conteúdo.

As velocidades de ligação à rede que definem um ponto de distribuição como **Fast** ou **Slow** já não são utilizadas. Em vez disso, cada sistema de site que está associado a um grupo de fronteiras é tratado da mesma forma.

Para mais informações, consulte [os grupos de fronteira](../../servers/deploy/configure/boundary-groups.md).


## <a name="on-demand-content-distribution"></a>Distribuição de conteúdo a pedido

A distribuição de conteúdos a pedido é uma opção para aplicações individuais e implementações de pacotes. Esta opção permite a distribuição de conteúdo sonoro para servidores preferidos.  

- Para permitir esta definição para uma implementação, ative: **Distribua o conteúdo deste pacote para pontos**de distribuição preferidos .  

- Quando permite esta opção para uma implementação, e um cliente solicita esse conteúdo, mas o conteúdo não está disponível em nenhum dos pontos de distribuição preferidos do cliente, o Gestor de Configuração distribui automaticamente esse conteúdo para os pontos de distribuição preferidos do cliente.  

- Embora isto desencadeie o Gestor de Configuração para distribuir automaticamente o conteúdo para os pontos de distribuição preferidos desse cliente, o cliente poderá obter esse conteúdo a partir de outros pontos de distribuição antes que os pontos de distribuição preferidos para o cliente recebam a implementação. Quando este comportamento ocorrer, o conteúdo estará então presente nesse ponto de distribuição para ser usado pelo próximo cliente que procura essa implementação.  

Para mais informações, consulte [os grupos de fronteira](../../servers/deploy/configure/boundary-groups.md).


## <a name="package-transfer-manager"></a>Gestor de transferência de pacotes

O gestor de transferência de pacotes é o componente do servidor do site que transfere conteúdo para pontos de distribuição em outros computadores.  

Para mais informações, consulte o [gestor de transferências de pacotes.](package-transfer-manager.md)  


## <a name="prestage-content"></a>Pré-configurar conteúdo

A predefinição do conteúdo é um processo de transferência de conteúdo para um ponto de distribuição sem distribuir o conteúdo pela rede.  

Para mais informações, consulte Gerir a [largura de banda da rede](manage-network-bandwidth.md).
