---
title: Configure grupos de fronteira
titleSuffix: Configuration Manager
description: Ajudar os clientes a encontrar sistemas de site usando grupos de fronteira para logicamente organizar localizações de rede relacionadas chamadas limites
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce77c43f49556b3a60e36f05127f82d4d135762a
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643270"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Configure grupos de limites para gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize grupos de fronteira no Gestor de Configuração para organizar logicamente localizações de rede[relacionadas (limites)](boundaries.md)para facilitar a gestão da sua infraestrutura. Atribuir limites a grupos de fronteira antes de usar o grupo de fronteira.

Por padrão, o Gestor de Configuração cria um grupo de limites de site predefinido em cada site.

Para configurar grupos de fronteiras, associar limites (localizações de rede) e funções do sistema de site, como pontos de distribuição, para o grupo de fronteiras. Esta configuração ajuda clientes associados a servidores do sistema de sites, como pontos de distribuição que estão localizados perto dos clientes da rede.

Para aumentar a disponibilidade de servidores para uma gama mais ampla de localizações de rede, atribua o mesmo limite e o mesmo servidor a mais de um grupo de fronteiras.

Os clientes usam um grupo de limites para:  

- Atribuição automática de site  
- Para encontrar um servidor de sistema de site que possa fornecer um serviço, incluindo:

  - Pontos de distribuição para localização de conteúdos  
  - Pontos de atualização de software  
  - Pontos de migração do Estado  

    > [!NOTE]
    > O ponto de migração do Estado não usa relações de recuo. Para mais informações, consulte [Fallback.](#fallback)

  - Pontos de gestão preferenciais  

    > [!NOTE]  
    > Se utilizar pontos de gestão preferidos, ative esta opção para a hierarquia, não a partir da configuração do grupo de limites. Para mais informações, consulte [Permitir a utilização de pontos de gestão preferenciais](boundary-group-procedures.md#bkmk_proc-prefer).  

  - Gateway de gestão de nuvem (a partir da versão 1902)

## <a name="boundary-groups-and-relationships"></a>Grupos de fronteirae relações

Para cada grupo de fronteiras da sua hierarquia, pode atribuir:

- Um ou mais limites. O atual grupo **de** fronteiras de um cliente é uma localização de rede que é definida como um limite atribuído a um grupo de fronteiraespecífico. Um cliente pode ter mais do que um grupo de fronteiras atual.  

- Uma ou mais funções do sistema do site. Os clientes podem sempre utilizar funções associadas ao seu atual grupo de fronteiras. Dependendo de configurações adicionais, podem usar funções em grupos de fronteira adicionais.  

Para cada grupo de fronteira que cria, pode configurar uma ligação de ida para outro grupo de fronteiras. A ligação chama-se **relação.** Os grupos de fronteira a que se ligam são chamados grupos de fronteira **vizinhos.** Um grupo de fronteiras pode ter mais do que uma relação, cada um com um grupo específico de fronteira sinuoso.

Quando um cliente não encontra um sistema de site disponível no seu grupo de limites atual, a configuração de cada relação determina quando começa a procurar um grupo de fronteiras do vizinho. Esta busca de grupos adicionais chama-se **recuo.**

Para mais informações, consulte os seguintes procedimentos:  

- [Criar um grupo de fronteiras](boundary-group-procedures.md#bkmk_create)  
- [Configurar um grupo de fronteiras](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a>Mostrar grupos de fronteira para dispositivos

<!--6521835-->

A partir da versão 2002, para ajudá-lo a identificar melhor e resolver comportamentos de dispositivos com grupos de fronteira, pode ver os grupos de fronteira para dispositivos específicos. No nó dos **Dispositivos** ou quando mostrar os membros de uma Coleção de **Dispositivos,** adicione a nova coluna **do Grupo Limite** na vista da lista.

- Se um dispositivo estiver em mais de um grupo de fronteiras, o valor é uma lista separada de nomes de grupos de fronteiras.

- Os dados atualizam quando o cliente faz um pedido de localização para o site, ou no máximo a cada 24 horas.

- Se um cliente está a vaguear e não é membro de um grupo de fronteiras, o valor é em branco.

> [!NOTE]
> Esta informação é de dados do site e apenas disponível em sites primários. Não verá um valor para esta coluna quando ligar o Gestor de Configuração a um site de administração central.

## <a name="fallback"></a>Contingência

Para prevenir problemas quando os clientes não conseguem encontrar um sistema de site disponível no seu atual grupo de fronteira, defina a relação entre grupos de fronteira para comportamento de recuo. O Fallback permite que um cliente expanda a sua pesquisa para grupos de fronteira adicionais para encontrar um sistema de site disponível.

As relações são configuradas num separador de propriedades de grupo de **fronteira.** Quando configuras uma relação, defines uma ligação a um grupo de fronteiras do vizinho. Para cada tipo de função de sistema de site suportado, configure configurar configurações independentes para o recuo para o grupo de fronteira do vizinho. Para mais informações, consulte o comportamento de recuo da [Configuração.](boundary-group-procedures.md#bkmk_bg-fallback)

Por exemplo, quando configurar uma relação com um grupo de limites específico, desfaça o recuo para que os pontos de distribuição ocorram após 20 minutos. O padrão é de 120 minutos Para um exemplo mais extenso, consulte [Exemplo de utilização de grupos de fronteira](#example-of-using-boundary-groups).

Se um cliente não encontrar uma função de sistema de site disponível no seu atual grupo de limites, o cliente utiliza o tempo de recuo em minutos. Este tempo de recuo determina quando o cliente começa a procurar um sistema de site disponível associado ao grupo de fronteira do vizinho.  

Quando um cliente não consegue encontrar um sistema de site disponível, começa a pesquisar locais de grupos de fronteira vizinhos. Este comportamento aumenta o conjunto de sistemas de site disponíveis. A configuração de grupos de fronteiras e suas relações define o uso do cliente deste conjunto de sistemas de site disponíveis.

- Um grupo de fronteiras pode ter mais do que uma relação. Com esta configuração, pode configurar o recuo de cada tipo de sistema de site para diferentes vizinhos para ocorrer após diferentes períodos de tempo.  

- Os clientes só recuam para um grupo de fronteiras que é um vizinho direto do seu atual grupo de fronteiras.  

- Quando um cliente é membro de mais de um grupo de fronteiras, define o seu atual grupo de fronteiras como uma união de todos os seus grupos de fronteira. O cliente recai para os vizinhos de qualquer um desses grupos de fronteiras originais.  

> [!NOTE]
> O papel do ponto de migração do Estado não usa relações de recuo. Se adicionar tanto as funções de ponto de migração do Estado como o ponto de distribuição ao mesmo servidor do sistema do site, não configure o recuo no seu grupo de fronteira. Se precisar de utilizar o recuo do grupo de limites para o ponto de distribuição, adicione a função do ponto de migração do estado num servidor de sistema de site diferente.<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>O grupo de fronteira do site padrão

Pode criar os seus próprios grupos de fronteira, e cada site tem um grupo de limites de site padrão que o Gestor de Configuração cria. Este grupo é nomeado Código de site do **&lt;Grupo Padrão-Site-Boundary-Group>**. Por exemplo, o grupo do site ABC seria nomeado **Padrão-Site-Boundary-Group&lt;ABC>**.

Para cada grupo de limites que cria, o Gestor de Configuração cria automaticamente uma ligação implícita a cada grupo de limites do site predefinido na hierarquia.  

- O link implícito é uma opção de recuo padrão de um grupo de fronteira atual para o grupo de fronteira padrão do site. O tempo de recuo padrão é de 120 minutos.  

- Para clientes não num limite associado a qualquer grupo de limites: para identificar funções válidas do sistema do site, utilize o grupo de limites do site predefinido a partir do seu site designado.  

Para gerir o recuo para o grupo de fronteira do site padrão:  

- Abra as propriedades do grupo de limite padrão do site e altere os valores no separador **Comportamento Padrão.** As alterações que faz aqui aplicam-se a *todas as* ligações implícitas a este grupo de fronteira. Quando configurar uma ligação explícita a este grupo de limites do site predefinido a partir de outro grupo de fronteira, sobrepor-se a estas definições predefinidas.  

- Abra as propriedades de um grupo de fronteira personalizado. Altere os valores para o link explícito para um grupo de fronteira do site predefinido. Quando se define um novo tempo em minutos para recuos ou recuos, essa alteração afeta apenas o link que está a configurar. A configuração do link explícito sobrepõe as definições no separador **Comportamento Padrão** de um grupo de limites do site predefinido.  

## <a name="site-assignment"></a>Atribuição do site  

É possível configurar cada grupo de limites com um site atribuído para clientes.  

- Um cliente recém-instalado que utiliza a atribuição automática do site junta-se ao site atribuído de um grupo de fronteira que contém a localização atual da rede do cliente.  

- Depois de atribuir a um site, um cliente não altera a sua atribuição do site quando muda a sua localização de rede. Por exemplo, um cliente vagueia por uma nova localização da rede. Esta localização é um limite em um grupo de fronteira com uma atribuição de site diferente. O site designado pelo cliente não muda.  

- Quando o Ative Directory System Discovery descobre um novo recurso, o site avalia a informação da rede para o recurso contra os limites em grupos de fronteira. Este processo associa o novo recurso a um site atribuído que será utilizado pelo método de instalação push do cliente.  

- Quando um limite é membro de mais de um grupo de fronteiras que têm diferentes sites atribuídos, os clientes selecionam aleatoriamente um dos sites.  

- As alterações a um site de fronteiras atribuídos aplicam-se apenas a novas ações de atribuição do site. Os clientes que anteriormente atribuídos a um site não reavaliam a sua atribuição do site com base em alterações na configuração de um grupo de fronteira (ou na sua própria localização de rede).  

Para obter mais informações sobre a atribuição do site do cliente, consulte [A utilização automática da atribuição do site para computadores](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment).  

Para obter mais informações sobre como configurar a atribuição do site, consulte os seguintes procedimentos:

- [Configure a atribuição do site e selecione servidores de sistemas de site](boundary-group-procedures.md#bkmk_references)
- [Configure um site de recuo para atribuição automática do site](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>Pontos de distribuição

Quando um cliente solicita a localização de um ponto de distribuição, o Gestor de Configuração envia ao cliente uma lista de sistemas de site. Estes sistemas de site são do tipo apropriado associado a cada grupo de fronteira que inclui a localização atual da rede do cliente:

- **Durante a distribuição**do software, os clientes solicitam uma localização para conteúdos de implantação numa fonte de conteúdo válida. Esta localização pode ser um ponto de distribuição, ou uma fonte de cache de pares.  

- Durante a **implantação do OS,** os clientes solicitam um local para enviar ou receber as suas informações de migração do Estado.  

  - Os clientes adquirem conteúdo com base em comportamentos de grupo de limites. Para obter mais informações, consulte o suporte da [sequência de tarefas para grupos de fronteira](#bkmk_bgr-osd).  

Durante a implementação de conteúdos, se um cliente solicitar conteúdo que não esteja disponível a partir de uma fonte no seu atual grupo de limites, o cliente continua a solicitar esse conteúdo. O cliente tenta diferentes fontes de conteúdo no seu atual grupo de limites até atingir o período de recuo para um vizinho ou o grupo de limites do site padrão. Se o cliente ainda não encontrou conteúdo, então expande a sua procura por fontes de conteúdo para incluir os grupos de fronteira do vizinho.

Se configurar o conteúdo para distribuir a pedido, e não estiver disponível num ponto de distribuição quando um cliente o solicita, o site começa a transferir o conteúdo para esse ponto de distribuição. É possível que o cliente encontre esse servidor como uma fonte de conteúdo antes de recuar para usar um grupo de fronteiras do vizinho.

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a>Instalação do cliente

<!--1358840-->
Ao instalar o cliente do Gestor de Configuração, o processo ccmsetup contacta o ponto de gestão para localizar o conteúdo necessário. O ponto de gestão devolve pontos de distribuição com base na configuração do grupo de limites. Se definir relações no grupo de fronteira, o ponto de gestão devolve pontos de distribuição na seguinte ordem:

1. Grupo de fronteira atual  
2. Grupos de fronteira do vizinho  
3. O grupo de fronteira padrão do site  

> [!Note]  
> O processo de configuração do cliente não usa o tempo de recuo. Para localizar o conteúdo o mais rápido possível, ele imediatamente volta para o próximo grupo de fronteiras.
>
> Em versões anteriores do Gestor de Configuração, durante este processo o ponto de gestão apenas devolveu pontos de distribuição no atual grupo de fronteira do cliente. Se não houver conteúdo disponível, o processo de configuração recuou para descarregar conteúdo a partir do ponto de gestão. Não havia opção de voltar aos pontos de distribuição de outros grupos de fronteira que pudessem ter o conteúdo necessário.

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a>Suporte de sequência de tarefas para grupos de fronteira

<!--1359025-->
Quando um dispositivo executa uma sequência de tarefas e precisa de adquirir conteúdo, utiliza comportamentos de grupo de limites semelhantes ao cliente do Gestor de Configuração.

Configure este comportamento utilizando as seguintes definições na página **pontos** de distribuição da implementação da sequência de tarefas:

- Quando não houver nenhum ponto de **distribuição local disponível, utilize um ponto**de distribuição remoto : Para esta implementação, a sequência de tarefas pode voltar aos pontos de distribuição num grupo de fronteira sinuoso.  

- Permitir que os **clientes utilizem pontos de distribuição do grupo**de fronteira do site padrão : Para esta implementação, a sequência de tarefas pode voltar aos pontos de distribuição no grupo de fronteira do site predefinido.  

Para utilizar este novo comportamento, certifique-se de atualizar os clientes para a versão mais recente.

#### <a name="location-priority"></a>Prioridade de localização  

A sequência de tarefas tenta adquirir conteúdo na seguinte ordem:  

1. Fontes de cache de pares  

2. Pontos de distribuição no *atual* grupo de fronteiras  

3. Pontos de distribuição em um grupo de fronteira *vizinho*  

    > [!Important]  
    > Devido à natureza em tempo real do processamento da sequência de tarefas, não espera pelo tempo de falha num grupo de fronteira sinuoso. Usa os tempos de failover para dar prioridade aos grupos de fronteira vizinhos. Por exemplo, se a sequência de tarefas não conseguir adquirir conteúdo a partir de um ponto de distribuição no seu atual grupo de fronteira, tenta imediatamente um ponto de distribuição num grupo de fronteira sinuoso com o menor tempo de falha. Se esse processo falhar, falha até um ponto de distribuição num grupo de fronteira sinuoso com um tempo de falha maior.  

4. Pontos de distribuição no grupo de fronteira padrão do *site*  

O ficheiro de registo de sequência de **tarefas smsts.log** mostra a prioridade das fontes de localização que utiliza com base nas propriedades de implementação.

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Opções de grupo de limites para downloads de pares

<!--1356193, 1358749-->
Os grupos de fronteiras incluem as seguintes definições adicionais para lhe dar mais controlo sobre a distribuição de conteúdos no seu ambiente:  

- [Permitir downloads de pares neste grupo de fronteiras](#bkmk_bgoptions1)  

- [Durante os downloads de pares, utilize apenas pares dentro da mesma subnet](#bkmk_bgoptions2)  

- [Prefira pontos de distribuição em vez de pares com a mesma subnet](#bkmk_bgoptions3)  

- [Prefira pontos de distribuição em nuvem em vez de pontos de distribuição](#bkmk_bgoptions4)  

Para obter mais informações sobre como configurar estas definições, consulte [Configurar um grupo de limites](boundary-group-procedures.md#bkmk_config).

Se um dispositivo estiver em mais de um grupo de fronteiras, aplicam-se os seguintes comportamentos para estas definições:

- **Permitir o download de pares neste grupo de fronteiras**: Se for desativado em qualquer grupo de fronteira, o cliente não utilizará a otimização da entrega.
- Durante os **downloads de pares, utilize apenas pares com a mesma sub-rede**: Se estiver ativado em qualquer grupo de fronteira, esta definição entra em vigor.
- **Prefira pontos de distribuição em vez de pares dentro da mesma sub-rede**: Se estiver ativado em qualquer grupo de fronteira, esta definição entra em vigor.
- **Prefira fontes baseadas em nuvem sobre fontes no local**: Se estiver ativada em qualquer grupo de fronteira, esta definição entra em vigor.

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a>Permitir downloads de pares neste grupo de fronteiras

Esta definição está ativada por predefinição. O ponto de gestão fornece aos clientes uma lista de locais de conteúdo que inclui fontes de pares. Esta definição também afeta a aplicação de IDs do Grupo para [otimização de entrega](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).  

Existem dois cenários comuns em que deve considerar a desativação desta opção:  

- Se tiver um grupo de fronteiras que inclua limites de locais geograficamente dispersos, como uma VPN. Dois clientes podem estar no mesmo grupo de fronteiraporque estão ligados através da VPN, mas em locais muito diferentes que são inadequados para a partilha de conteúdos pelos pares.  

- Se utilizar um único grupo de limites para a atribuição do site que não referencia pontos de distribuição.  

> [!IMPORTANT]
> Se um dispositivo estiver em mais de um grupo de fronteiras, certifique-se de que ativa esta definição em todos os grupos de fronteira para o dispositivo. Caso contrário, o cliente não utilizará a otimização da entrega. Por exemplo, não define a chave de registo DOGroupID.

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a>Durante os downloads de pares, utilize apenas pares dentro da mesma subnet

Esta definição depende da opção anterior. Se ativar esta opção, o ponto de gestão apenas inclui na lista de dados de conteúdo fontes de pares que estão na mesma sub-rede que o cliente.

Cenários comuns para permitir esta opção:

- O design do seu grupo de fronteira para distribuição de conteúdos inclui um grande grupo de fronteiras que se sobrepõe a outros grupos de fronteira menores. Com esta nova configuração, a lista de fontes de conteúdo que o ponto de gestão fornece aos clientes apenas inclui fontes par imediadas da mesma subnet.

- Você tem um único grande grupo de fronteiras para todos os locais de escritório remoto. Ative esta opção e os clientes só partilham conteúdo dentro da sub-rede no local do escritório remoto, em vez de arriscarem partilhar conteúdo entre locais.

A partir da versão 2002, dependendo da configuração da sua rede, pode excluir determinadas subredes para correspondência. Por exemplo, você quer incluir um limite, mas excluir uma sub-rede VPN específica. Por predefinição, o Gestor de Configuração`2001:0000:%`exclui a subnet teredo predefinida ().<!--3555777-->

> [!NOTE]
> Na versão 2002, quando [se expande um site primário autónomo](../install/prerequisites-for-installing-sites.md#bkmk_expand) para adicionar um site de administração central (CAS), a lista de exclusão da sub-rede reverte para o padrão. Para contornar este problema, após a expansão do site, executar o script PowerShell para personalizar a lista de exclusão da sub-rede no CAS.<!-- 6309068 -->

Importe a sua lista de exclusão de sub-rede como uma cadeia de sub-rede separada pela vírcula. Use o sinal`%`por cento como um personagem wildcard. No servidor de site de alto nível, detete ou leia a propriedade incorporada **subnetExclusionList** para o componente **SMS_HIERARCHY_MANAGER** na classe **SMS_SCI_Component.** Para mais informações, consulte [SMS_SCI_Component classe WMI](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)do servidor .

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>Sample PowerShell script para atualizar a lista de exclusão da subnet

O seguinte guião é uma forma de alterar este valor. Anexar as suas subredes à `2001:0000:%,172.16.16.0`variável **PropertyValue** após . É uma corda separada de vírina. Execute este script no servidor de site de alto nível na sua hierarquia.

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> Por predefinição, o Gestor de Configuração inclui a sub-rede Teredo nesta lista. Quando mudar a lista, leia sempre o valor existente primeiro. Anexar subredes adicionais à lista e, em seguida, definir o novo valor.

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a>Prefira pontos de distribuição em vez de pares com a mesma subnet

Por padrão, o ponto de gestão prioriza as fontes de cache dos pares no topo da lista de locais de conteúdo. Esta definição inverte essa prioridade para os clientes que estão na mesma sub-rede que a fonte de cache dos pares.

> [!TIP]
> Este comportamento aplica-se ao cliente do Gestor de Configuração. Não se aplica quando a sequência de tarefas descarrega conteúdo. Quando a sequência de tarefas funciona, prefere fontes de cache de pares em vez de pontos de distribuição.<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a>Prefira pontos de distribuição em nuvem em vez de pontos de distribuição

Se tiver uma sucursal com uma ligação de internet mais rápida, agora pode priorizar o conteúdo em nuvem.  

Na versão 1902, este cenário é agora intitulado **Prefer cloud sources over-premise sources**. As fontes baseadas na nuvem incluem o seguinte:<!-- SCCMDocs#1529 -->

- Pontos de distribuição em nuvem
- Microsoft Update (adicionado na versão 1902)

## <a name="software-update-points"></a>Pontos de atualização de software

Os clientes usam grupos de fronteira para encontrar um novo ponto de atualização de software. Para controlar quais os servidores que um cliente pode encontrar, adicione pontos de atualização de software individuais a diferentes grupos de fronteira.

Se adicionar todos os pontos de atualização de software existentes ao grupo de limites do site padrão, o cliente seleciona um ponto de atualização de software a partir do conjunto de servidores disponíveis. Este comportamento é semelhante às versões anteriores do ramo atual do Gestor de Configuração. Para um comportamento controlado de seleção e recuo, adicione pontos de atualização de software individuais a diferentes grupos de fronteira.

Se instalar um novo site, os pontos de atualização de software não são adicionados ao grupo de limites do site padrão. Aatualização de software atribui pontos para um grupo de limites para que os clientes possam encontrá-los e usá-los.

### <a name="fallback-for-software-update-points"></a>Recuo para pontos de atualização de software

O recuo para pontos de atualização de software está configurado como outras funções do sistema do site, mas tem as seguintes ressalvas:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Novos clientes usam grupos de limites para selecionar pontos de atualização de software

Quando instala novos clientes, selecionam um ponto de atualização de software dos servidores associados aos grupos de limites que configura. Este comportamento substitui o comportamento anterior, onde os clientes selecionam um ponto de atualização de software aleatoriamente a partir de uma lista dos servidores que partilham a floresta do cliente.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Os clientes continuam a usar um último ponto de atualização de software conhecido até que eles recuem para encontrar um novo

Os clientes que já têm um ponto de atualização de software continuam a usá-lo até que não possa ser alcançado. Este comportamento inclui o uso contínuo de um ponto de atualização de software que não está associado ao atual grupo de fronteira do cliente.

Este comportamento é intencional. O cliente continua a usar um ponto de atualização de software existente, mesmo quando não está no atual grupo de limites do cliente. Quando o ponto de atualização do software muda, o cliente sincroniza os dados com o novo servidor, o que causa uma utilização significativa da rede. Se todos os clientes mudarem para um novo servidor ao mesmo tempo, o atraso na transição ajuda a evitar saturar a sua rede.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Um cliente tenta sempre alcançar o seu último ponto de atualização de software conhecido durante 120 minutos antes de iniciar o recuo

Após 120 minutos, se o cliente não estabeleceu contacto, então começa a recuar. Quando o recuo começa, o cliente recebe uma lista de todos os pontos de atualização de software no seu atual grupo de fronteira. Pontos adicionais de atualização de software em grupos de limites padrão vizinhos e do site estão disponíveis com base em configurações de backback.

### <a name="fallback-configurations-for-software-update-points"></a>Configurações de recuo para pontos de atualização de software

Pode configurar **os tempos de recuo (em minutos)** para que os pontos de atualização de software sejam inferiores a 120 minutos. No entanto, o cliente ainda tenta alcançar o seu ponto de atualização de software original durante 120 minutos. Em seguida, expande a sua pesquisa para servidores adicionais. Os tempos de recuo do grupo de fronteira começam quando o cliente não consegue chegar ao seu servidor original. Quando o cliente expande a sua pesquisa, o site fornece quaisquer grupos de limites configurados por menos de 120 minutos.

Para bloquear o recuo de uma atualização de software, indique um grupo de fronteiras do vizinho, configure a definição para **Never fallback**.

Depois de não ter atingido o seu servidor original durante duas horas, o cliente usa então um ciclo mais curto para estabelecer uma ligação a um novo ponto de atualização de software. Este comportamento permite ao cliente pesquisar rapidamente através da lista de potenciais pontos de atualização de software.

#### <a name="example"></a>Exemplo

Configura pontos de atualização de software no grupo *A* de fronteira para recuar após **10** minutos. Configura a mesma regulação para o grupo de limites *B* a **130** minutos. Um cliente do grupo *de fronteiraZ* não consegue alcançar o seu último ponto de atualização de software conhecido.

- Durante os próximos 120 minutos, o cliente tenta alcançar apenas o seu servidor original no grupo de fronteira Z. Após 10 minutos, o Gestor de Configuração adiciona os pontos de atualização de software do grupo de fronteira A para o conjunto de servidores disponíveis. No entanto, o cliente não tenta contactá-los ou qualquer outro servidor até que o período inicial de 120 minutos decorrido.  

- Depois de tentar contactar o ponto de atualização de software original durante 120 minutos, o cliente expande a sua pesquisa. Adiciona servidores ao conjunto disponível de pontos de atualização de software que estão na sua corrente e quaisquer grupos de fronteira vizinhos configurados por 120 minutos ou menos. Esta piscina inclui os servidores do grupo de fronteira A, que foram previamente adicionados ao conjunto de servidores disponíveis.  

- Após mais 10 minutos, o cliente expande a pesquisa para incluir pontos de atualização de software do grupo B de fronteira. Este período é de 130 minutos do tempo total após o cliente não ter atingido pela primeira vez o seu último ponto de atualização de software conhecido.  

### <a name="manually-switch-to-a-new-software-update-point"></a>Mude manualmente para um novo ponto de atualização de software

Juntamente com o recuo, utilize a notificação do cliente para forçar manualmente um dispositivo a mudar para um novo ponto de atualização de software.

Quando muda para um novo servidor, os dispositivos usam recuo para encontrar o novo servidor. Os clientes mudam para o novo ponto de atualização de software durante o seu próximo ciclo de atualizações de software.<!-- SCCMDocs#1537 -->

Reveja as configurações do seu grupo de limites. Antes de iniciar esta alteração, certifique-se de que os pontos de atualização do software estão nos grupos de limites corretos.

Para mais informações, consulte [Manualmente mudar os clientes para um novo ponto](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs)de atualização de software .

## <a name="management-points"></a>Pontos de gestão

<!-- 1324594 -->
Configure relações de recuo para pontos de gestão entre grupos de fronteira. Este comportamento proporciona um maior controlo para os pontos de gestão que os clientes usam. No separador **Relationships** das propriedades do grupo de fronteira, há uma coluna para ponto de gestão. Quando se adiciona um novo grupo de limites de recuo, o tempo de recuo para o ponto de gestão é atualmente sempre zero (0). Este comportamento é o mesmo para o **Comportamento Padrão** no grupo de limite padrão do site.

Anteriormente, um problema comum ocorreu quando se tinha um ponto de gestão protegido numa rede segura. Os clientes da rede principal receberam uma política que incluía este ponto de gestão protegido, mesmo que não pudessem comunicar com ele através de uma firewall. Para resolver este problema agora, use a opção **Nunca recuo** para garantir que os clientes apenas recaem para pontos de gestão com os quais podem comunicar.

> [!Note]  
> Se permitir que os pontos de distribuição do grupo de limite sinuoso do site caiam, e um ponto de gestão é colocalizado num ponto de distribuição, o site também adiciona esse ponto de gestão ao grupo de limite sinuoso do site.<!--VSO 2841292-->  

Se um cliente estiver num grupo de fronteiras que sem um ponto de gestão atribuído, o site dá ao cliente toda a lista de pontos de gestão. Este comportamento garante que um cliente recebe sempre uma lista de pontos de gestão.

O recuo do grupo de limites de pontode gestão não altera o comportamento durante a instalação do cliente (ccmsetup.exe). Se a linha de comando não especificar o ponto de gestão inicial utilizando o parâmetro/MP, o novo cliente recebe a lista completa dos pontos de gestão disponíveis. Para o seu processo inicial de bootstrap, o cliente usa o primeiro ponto de gestão a que pode aceder. Assim que o cliente se regista no site, recebe a lista de pontos de gestão devidamente classificada com este novo comportamento.

Para obter mais informações sobre o comportamento do cliente para adquirir conteúdo durante a instalação, consulte a [instalação do Cliente.](#bkmk_ccmsetup)

Durante a atualização do cliente, se não especificar o parâmetro da linha de comando/MP, o cliente consulta fontes como Ative Directory e WMI para qualquer ponto de gestão disponível. A atualização do cliente não honra a configuração do grupo de limites. <!--VSO 2841292-->  

Para que os clientes utilizem esta capacidade, ative a seguinte definição: **Os clientes preferem utilizar pontos de gestão especificados em grupos de fronteira** em **Definições de Hierarquia**.

> [!Note]  
> Os processos de implantação do OS não estão cientes de grupos de fronteira para pontos de gestão.  

### <a name="troubleshooting"></a>Resolução de problemas

Novas entradas aparecem no **LocationServices.log**. O atributo **da Localidade** identifica um dos seguintes estados:

- **0**: Desconhecido  

- **1**: O ponto de gestão especificado está apenas no grupo de limite sinuoso do site para recuo  

- **2**: O ponto de gestão especificado encontra-se num grupo de fronteira remoto ou vizinho. Quando o ponto de gestão está em ambos os grupos de fronteira padrão do vizinho e do site, a localidade é 2.  

- **3**: O ponto de gestão especificado encontra-se no grupo de fronteira local ou atual. Quando o ponto de gestão está no atual grupo de fronteira e um vizinho ou o grupo de fronteira padrão do site, a localidade é 3. Se não permitir a definição de pontos de gestão preferenciais em Definições de Hierarquia, a localidade é sempre 3 independentemente do grupo de fronteira em que o ponto de gestão se encontra.  

Os clientes usam os pontos de gestão local primeiro (localidade 3), segundo remoto (localidade 2), depois recuo (localidade 1).

Quando um cliente recebe cinco erros em 10 minutos e não consegue comunicar com um ponto de gestão no seu atual grupo de fronteira, tenta contactar um ponto de gestão num vizinho ou no grupo de fronteira padrão do site. Se o ponto de gestão do atual grupo de fronteiras voltar mais tarde, o cliente regressa ao ponto de gestão local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando o serviço de agente de configuração reinicia.

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a>Pontos de gestão preferenciais

> [!Note]
> O comportamento desta configuração de hierarquia, **os Clientes preferem usar pontos de gestão especificados em grupos de fronteira,** alterados na versão 1802. Quando ativa esta definição, o Gestor de Configuração utiliza a funcionalidade do grupo de limites para o ponto de gestão atribuído. Para mais informações, consulte [pontos de gestão.](#management-points)

Os pontos de gestão preferenciais permitem a um cliente identificar um ponto de gestão associado à sua localização atual de rede (limite).  

- Um cliente tenta utilizar um ponto de gestão preferido do seu site atribuído antes de utilizar um não configurado como preferido do seu site designado.  

- Para utilizar esta opção, ative os **Clientes preferirem utilizar pontos de gestão especificados em grupos de fronteira** em **Definições de Hierarquia**. Em seguida, configure grupos de fronteira em locais primários individuais. Inclua os pontos de gestão que devem ser associados aos limites associados desse grupo de fronteiras. Para mais informações, consulte [Permitir a utilização de pontos de gestão preferenciais](boundary-group-procedures.md#bkmk_proc-prefer).  

- Quando configura pontos de gestão preferenciais, e um cliente organiza a sua lista de pontos de gestão, o cliente coloca os pontos de gestão preferidos no topo da sua lista. Esta lista inclui todos os pontos de gestão do site designado pelo cliente.  

> [!NOTE]  
> Roaming de clientes significa que muda as suas localizações de rede. Por exemplo, quando um portátil viaja para um local remoto do escritório. Quando um cliente vagueia, pode usar um ponto de gestão do site local antes de tentar usar um servidor a partir do seu site designado. Esta lista de servidores do seu site atribuído inclui os pontos de gestão preferidos. Para mais informações, consulte [como os clientes encontram recursos e serviços](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)do site.  

## <a name="overlapping-boundaries"></a>Fronteiras sobrepostas  

O Gestor de Configuração suporta configurações de limites sobrepostas para a localização do conteúdo. Quando a localização da rede do cliente pertence a mais de um grupo de fronteiras:

- Quando um cliente solicita conteúdo, o Gestor de Configuração envia ao cliente uma lista de todos os pontos de distribuição que têm o conteúdo.  

- Quando um cliente solicita a um servidor para enviar ou receber as suas informações de migração do Estado, o Gestor de Configuração envia ao cliente uma lista de todos os pontos de migração do Estado associados a um grupo de fronteiras que inclui a localização atual da rede do cliente.  

Este comportamento permite que o cliente selecione o servidor mais próximo para transferir o conteúdo ou as informações de migração de estado.  

## <a name="example-of-using-boundary-groups"></a>Exemplo de utilização de grupos de fronteira

O exemplo seguinte utiliza um cliente que procura conteúdo a partir de um ponto de distribuição. Este exemplo pode ser aplicado a outras funções do sistema do site que utilizam grupos de fronteira.

Crie três grupos de fronteira que não partilhem limites ou servidores do sistema de site:  

- Grupo BG_A com pontos de distribuição DP_A1 e DP_A2  

- Grupo BG_B com pontos de distribuição DP_B1 e DP_B2  

- Grupo BG_C com pontos de distribuição DP_C1 e DP_C2  

Adicione as localizações de rede dos seus clientes como limites apenas ao grupo de fronteira BG_A. Em seguida, configurar as relações desse grupo de fronteira para os outros dois grupos de fronteira:  

- Configure os pontos de distribuição para o primeiro grupo *vizinho* (BG_B) a ser usado após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos estão bem ligados aos locais de fronteira do primeiro grupo.  

- Configure o segundo grupo *vizinho* (BG_C) para ser utilizado após 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos estão do outro lado de um WAN dos outros dois grupos de fronteira.  

- Adicione também ao grupo de limites do site padrão outro ponto de distribuição que está no servidor do site. Este servidor é a sua localização de origem de conteúdo menos preferencial, mas está centralmente localizado em todos os seus grupos de fronteira.

    Exemplo de grupos de fronteiras e tempos de recuo:

    ![Exemplo de grupos de fronteiras e tempos de recuo](media/BG_Fallback.png)  

Com esta configuração:  

- O cliente começa a procurar conteúdo a partir de pontos de distribuição no *seu* atual grupo de fronteira (BG_A). Procura cada ponto de distribuição durante dois minutos e, em seguida, muda para o próximo ponto de distribuição no grupo de fronteira. O conjunto de locais de origem de conteúdo válidos do cliente inclui DP_A1 e DP_A2.  

- Se o cliente não encontrar conteúdo do *seu* atual grupo de fronteira seleções após 10 minutos de pesquisa, adiciona os pontos de distribuição do grupo de fronteira BG_B à sua pesquisa. Em seguida, continua a procurar conteúdo a partir de um ponto de distribuição no seu conjunto combinado de servidores. Este pool agora inclui servidores dos grupos de fronteira BG_A e BG_B. O cliente continua a contactar cada ponto de distribuição durante dois minutos e, em seguida, muda para o próximo servidor na sua piscina. O conjunto de locais de origem de conteúdo válidos do cliente inclui DP_A1, DP_A2, DP_B1 e DP_B2.  

- Após mais 10 minutos (20 minutos no total), se o cliente ainda não tiver encontrado um ponto de distribuição com conteúdo, expande a sua piscina para incluir servidores disponíveis do segundo grupo *vizinho,* grupo de fronteira BG_C. O cliente tem agora seis pontos de distribuição para pesquisar: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2. Continua a mudar para um novo ponto de distribuição a cada dois minutos até encontrar conteúdo.  

- Se o cliente não tiver encontrado conteúdo após um total de 120 minutos, recua para incluir o grupo de fronteira do *site padrão* como parte da sua pesquisa contínua. Agora, a piscina inclui todos os pontos de distribuição dos três grupos de fronteira configurados, e o ponto de distribuição final localizado no servidor do site. O cliente continua então a sua pesquisa de conteúdo, alterando pontos de distribuição de dois em dois minutos até que o conteúdo seja encontrado.  

Ao configurar os diferentes grupos vizinhos para estarem disponíveis em diferentes momentos, controla-se quando são adicionados pontos de distribuição específicos como uma localização de fonte de conteúdo. O cliente usa o backback para o grupo de limites do site padrão como uma rede de segurança para conteúdo que não está disponível em qualquer outro local.

## <a name="changes-from-prior-versions"></a>Alterações a partir de versões anteriores

Seguem-se as principais alterações aos grupos de fronteira e a forma como os clientes encontram conteúdo na atual sucursal do Gestor de Configuração. Muitas destas mudanças e conceitos trabalham em conjunto.

### <a name="configurations-for-fast-or-slow-are-removed"></a>As configurações para fast ou slow são removidas

Já não configura pontos de distribuição individuais para ser rápido ou lento. Em vez disso, cada sistema de site associado a um grupo de fronteiras é tratado da mesma forma. Devido a esta alteração, o separador **Referências** das propriedades do grupo de fronteira já não suporta a configuração de Fast ou Slow.  

### <a name="new-default-boundary-group-at-each-site"></a>Novo grupo de limites padrão em cada site

Cada site primário tem um novo grupo de limites padrão chamado **&lt;Padrão-Site-Boundary-Group sitecode>**. Quando um cliente não está num local de rede atribuído a um grupo de limites, utiliza os sistemas de site associados ao grupo padrão a partir do seu site designado. Planeie usar este grupo de fronteiras como substituto do conceito de localização de conteúdo de recuo.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>**Permitir que as localizações de origem de recaída para o conteúdo** sejam removidas

Já não configura explicitamente um ponto de distribuição a ser utilizado para o recuo. As opções para configurar esta definição são removidas da consola.

Além disso, o resultado da definição Permitir que os **clientes utilizem uma localização de origem de recuo para conteúdo** num tipo de implementação para aplicações mudou. Esta definição num tipo de implementação permite agora que um cliente utilize o grupo de limites do site padrão como uma localização de fonte de conteúdo.

#### <a name="boundary-groups-relationships"></a>Relações de grupos de fronteira

Pode ligar cada grupo de fronteiraa a um ou mais grupos de fronteira adicionais. Estes links formam relações que configura no novo separador de propriedades do grupo de fronteira chamado **Relacionamentos:**  

- Cada grupo de fronteira saciado diretamente é chamado de grupo de fronteira **atual.**  

- Qualquer grupo de fronteira que um cliente possa usar devido a uma associação entre o atual grupo de *fronteiras* desse cliente e outro grupo é chamado de grupo de fronteira sinuoso. **neighbor**  

- No separador **Relationships,** adicione grupos de fronteira para usar como um grupo de fronteira *sinuoso.* Também configure um tempo em minutos para o recuo. Quando um cliente não encontra conteúdo a partir de um ponto de distribuição no grupo *atual,* desta vez é quando o cliente começa a pesquisar localizações de conteúdo de grupos de fronteira *vizinhos.*  

    Quando adiciona ou altera uma configuração de grupo de limites, pode bloquear o recuo para esse grupo de limites específico do grupo atual que está a configurar.  

Para utilizar a nova configuração, defina associações explícitas (links) de um grupo de fronteira para outro. Configure todos os pontos de distribuição desse grupo associado com o mesmo tempo em minutos. Quando um cliente não encontra uma fonte de conteúdo do *seu* atual grupo de limites, o tempo que configura determina quando começa a procurar fontes de conteúdo do seu grupo de fronteira sinuoso.

Além dos grupos de fronteira que configura explicitamente, cada grupo de fronteira tem uma ligação implícita ao grupo de fronteira do site predefinido. Esta ligação torna-se ativa após 120 minutos. Em seguida, o grupo de fronteira do site padrão torna-se um grupo de fronteira sinuoso vizinho. Este comportamento permite que os clientes utilizem como localização de fonte de conteúdo os pontos de distribuição associados a esse grupo de fronteira.

Este comportamento substitui o que anteriormente era referido como recuo para o conteúdo. Sobrepor-se a este comportamento padrão de 120 minutos associando explicitamente o grupo de fronteira do site padrão a um grupo *atual.* Detete um tempo específico em minutos ou bloqueie totalmente o recuo para evitar a sua utilização.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Os clientes tentam obter conteúdo de cada ponto de distribuição por até dois minutos

Quando um cliente procura uma localização de fonte de conteúdo, tenta aceder a cada ponto de distribuição durante dois minutos antes de tentar outro ponto de distribuição. Este comportamento é uma mudança em versões anteriores onde os clientes tentaram ligar-se a um ponto de distribuição por até duas horas.

- Os clientes selecionam aleatoriamente o primeiro ponto de distribuição do conjunto de servidores disponíveis no atual grupo de *fronteiras* do cliente (ou grupos).  

- Após dois minutos, se o cliente não tiver encontrado o conteúdo, muda para um novo ponto de distribuição e tenta obter conteúdo desse servidor. Este processo repete-se de dois em dois minutos até que o cliente encontre o conteúdo ou chegue ao último servidor na sua piscina.  

- Se um cliente não conseguir encontrar uma localização de origem de conteúdo válida a partir do seu pool *atual* antes de atingir o período de recuo para *um* grupo de fronteira vizinho, o cliente adiciona então os pontos de distribuição desse grupo *vizinho* ao final da sua lista atual. Em seguida, procura o grupo expandido de localizações de origem que inclui os pontos de distribuição de ambos os grupos de fronteira.  

    > [!TIP]  
    > Quando cria uma ligação explícita do grupo de fronteira atual para o grupo de fronteira do site padrão, e define um tempo de recuo que é inferior ao tempo de recuo para uma ligação a um grupo de fronteiras vizinho, os clientes começam a procurar localizações de origem do grupo de fronteira do site padrão antes de incluir o grupo vizinho.  

- Quando o cliente não obtém conteúdo do último servidor da piscina, inicia novamente o processo.  

## <a name="see-also"></a>Consulte também

- [Procedimentos para os grupos de limites](boundary-group-procedures.md)  

- [Sobre limites](boundaries.md)  

- [Conceitos fundamentais da gestão de conteúdos](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  
