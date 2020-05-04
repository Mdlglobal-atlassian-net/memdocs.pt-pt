---
title: Tamanho e escala
titleSuffix: Configuration Manager
description: Determine o número de funções e sites do sistema do site que necessitará para suportar os dispositivos no seu ambiente.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0861bb73769beb6c7595b896afc8d0e156eef94d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709643"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Dimensionamento e números da escala do Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

Cada implementação do Gestor de Configuração tem um número máximo de sites, funções do sistema do site e dispositivos que pode suportar. Estes números variam consoante a sua estrutura hierárquica, que tipos e números de sites utiliza, e as funções do sistema do site que implementa. As informações neste artigo podem ajudá-lo a determinar o número de funções e sites do sistema do site que precisa para suportar os dispositivos que espera gerir.

Para obter mais informações, veja os artigos seguintes:

- [Hardware recomendado](recommended-hardware.md)
- [Sistemas operativos suportados para servidores do sistema de sites](supported-operating-systems-for-site-system-servers.md)  
- [Sistemas operativos suportados por clientes e dispositivos](supported-operating-systems-for-clients-and-devices.md)
- [Pré-requisitos do site e sistema de sites](site-and-site-system-prerequisites.md)

Estes números de suporte baseiam-se na utilização do hardware recomendado para o Gestor de Configuração. Baseiam-se também nas definições predefinidas para todas as funcionalidades disponíveis do Gestor de Configuração. Quando não utiliza o hardware recomendado ou utiliza configurações personalizadas mais agressivas, o desempenho dos sistemas do site pode degradar-se. Os sistemas do site podem não satisfazer os níveis de suporte indicados. (Um exemplo de configurações mais agressivas do cliente é executar hardware ou inventário de software com mais frequência do que os incumprimentos de uma vez a cada sete dias.)

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a>Tipos de site  

### <a name="central-administration-site"></a>Site de administração central  

- Um site da administração central suporta até 25 locais primários infantis.  

### <a name="primary-site"></a>Site primário  

- Cada local primário suporta até 250 locais secundários.  

- O número de sites secundários por local primário baseia-se em ligações de rede de área ampla (WAN) continuamente ligadas e fiáveis. Para locais com menos de 500 clientes, considere um ponto de distribuição em vez de um site secundário.  

  Para obter informações sobre o número de clientes e dispositivos que um site primário pode suportar, consulte [os números do Cliente para sites e hierarquias.](#bkmk_clientnumbers)  

### <a name="secondary-site"></a>Site Secundário  

- Sites secundários não suportam sites infantis.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Funções do sistema do site

### <a name="application-catalog-web-service-point"></a>Ponto de serviço web de catálogo de aplicações  

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- Pode instalar várias instâncias do ponto de serviço web do Catálogo de Aplicações em sites primários.  

### <a name="application-catalog-website-point"></a>Ponto de site do catálogo de aplicações  

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- Pode instalar várias instâncias do ponto do site do Catálogo de Aplicações em sites primários.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a>Gateway de gestão de nuvem

- Pode instalar várias instâncias do gateway de gestão de nuvem (CMG) em locais primários, ou no site da administração central.  

    > [!Tip]  
    > Numa hierarquia, crie a CMG no site da administração central.  

  - Um CMG suporta uma a 16 instâncias de máquina virtual (VM) no serviço de nuvem Azure.  

  - Cada instância CMG VM suporta 6.000 ligações de clientes simultâneas. Quando a CMG está sob alta carga devido a mais do que o número suportado de clientes, ainda lida com pedidos, mas pode haver atraso.  

Para mais informações, consulte desempenho [e escala](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) cmg

### <a name="cloud-management-gateway-connection-point"></a>Ponto de ligação de gateway de gestão de nuvem

- Pode instalar várias instâncias do ponto de ligação CMG nos locais primários.  

- Um ponto de ligação CMG pode suportar um CMG com até quatro instâncias VM. Se o CMG tiver mais de quatro instâncias VM, adicione um segundo ponto de ligação CMG para equilibrar a carga. Uma CMG com 16 instâncias VM deve estar ligada a quatro pontos de ligação CMG.

Para mais informações, consulte desempenho [e escala](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) cmg

> [!NOTE]
> Ao considerar os requisitos de hardware para o ponto de ligação CMG, consulte [o hardware recomendado para servidores](recommended-hardware.md#bkmk_RemoteSiteSystem)de sistema de site remoto .<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Ponto de distribuição  

- Pontos de distribuição por site:  

  - Cada site primário e secundário suporta até 250 pontos de distribuição.  

  - Cada site primário e secundário suporta até 2000 pontos de distribuição adicionais que são configurados como pontos de distribuição de puxar. **Por exemplo,** um único site primário suporta 2250 pontos de distribuição quando 2000 desses pontos de distribuição são configurados como pontos de distribuição de puxar.  

  - Cada ponto de distribuição suporta ligações de até 4.000 clientes.  

  - Um ponto de distribuição de puxar age como um cliente quando acede ao conteúdo a partir de um ponto de distribuição de fonte.  

- Cada local primário suporta um total combinado de até 5.000 pontos de distribuição. Este total inclui todos os pontos de distribuição no local primário e todos os pontos de distribuição que pertencem aos locais secundários para crianças do local primário.  

- Cada ponto de distribuição suporta um total combinado de até 10.000 pacotes e aplicações.  

> [!WARNING]  
> O número real de clientes que um ponto de distribuição pode suportar depende da velocidade da rede e da configuração do hardware do servidor.  
>
> O número de pontos de distribuição de puxar que um ponto de distribuição de origem pode suportar depende da velocidade da rede e da configuração do hardware do ponto de distribuição de fonte. Mas este número também é afetado pela quantidade de conteúdo que implementou. Este efeito deve-se ao facto de, ao contrário dos clientes que normalmente acedem ao conteúdo em diferentes momentos durante uma implementação, todos os pontos de distribuição de pull-distribution solicitam conteúdo ao mesmo tempo. Os pontos de distribuição de pull podem solicitar todos os conteúdos disponíveis, e não apenas o conteúdo que lhes é aplicável. Quando coloca uma carga de processamento elevada num ponto de distribuição de fonte, pode haver atrasos inesperados na distribuição do conteúdo para os pontos de distribuição do alvo.  

### <a name="fallback-status-point"></a>Ponto de estado de contingência  

- Cada ponto de situação de recuo pode suportar até 100.000 clientes.  

### <a name="management-point"></a>Ponto de gestão  

- Cada site primário suporta até 15 pontos de gestão.  

    > [!TIP]  
    > Não instale pontos de gestão em servidores que se encontram num link lento a partir do servidor principal do site ou do servidor de base de dados do site.  

- Cada site secundário suporta um único ponto de gestão que deve ser instalado no servidor do site secundário.  

Para obter informações sobre o número de clientes e dispositivos que um ponto de gestão pode suportar, consulte a secção pontos de [Gestão.](#bkmk_mp)  

### <a name="software-update-point"></a>Ponto de atualização de software  

Utilize as seguintes recomendações como base. Esta linha de base ajuda-o a determinar a informação para o planeamento de capacidade de atualizações de software que é apropriado para a sua organização. Os requisitos reais de capacidade podem variar das recomendações enumeradas neste artigo, dependendo dos seguintes critérios:

- O seu ambiente específico de networking
- O hardware que usa para alojar o sistema de pontos de atualização de software
- O número de clientes geridos
- As outras funções do sistema do site instaladas no servidor  

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Planeamento da capacidade para o ponto de atualização de software  

O número de clientes suportados depende da versão dos Serviços de Atualização do Servidor do Windows (WSUS) que funciona no ponto de atualização de software. Também depende se o papel do sistema de pontode atualização de software coexiste com outra função do sistema do site:  

- O ponto de atualização de software pode suportar até 25.000 clientes quando a WSUS executa o servidor de pontode atualização de software, e o ponto de atualização de software coexiste com outra função do sistema do site.  

- O ponto de atualização do software pode suportar até 150.000 clientes quando um servidor remoto cumpre os requisitos do WSUS, o WSUS é usado com o Gestor de Configuração, e configura as seguintes definições:

  Piscinas de aplicações IIS:

  - Aumentar o Comprimento da Fila WsusPool para 2000
  - Aumente o limite de memória privada WsusPool x4 vezes, ou definido para 0 (ilimitado). Por exemplo, se o limite de predefinição for de 1.843.200 KB, aumente-o para 7.372.800. Para mais informações, consulte este blog de suporte do Gestor de [Configuração.](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/)  

    Para obter mais informações sobre os requisitos de hardware para o ponto de atualização de software, consulte [o hardware recomendado para os sistemas do site](recommended-hardware.md#bkmk_ScaleSieSystems).  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a>Planeamento de capacidade para atualizações de software objetos  

Utilize as seguintes informações de capacidade para planear objetos de atualizações de software:  

- **Limite de 1000 atualizações** de software numa implementação -Limite o número de atualizações de software para 1000 para cada implementação de atualização de software. Quando criar uma regra de implementação automática (ADR), especifique critérios que limitam o número de atualizações de software. O ADR falha quando os critérios especificados devolvem mais de 1000 atualizações de software. Verifique o estado do ADR a partir do nó de Regras de **Implementação Automática** na consola Do Gestor de Configuração. Quando implementar manualmente atualizações de software, não selecione mais de 1000 atualizações para implementar.  

  Também limite o número de atualizações de software para 1000 numa linha de base de configuração. Para mais informações, consulte Criar linhas de base de [configuração](../../../compliance/deploy-use/create-configuration-baselines.md).

- **Limite de 580 âmbitos de segurança para regras de implantação automática** -<!--ado 4962928-->
Limite o número de âmbitos de segurança das regras de implantação automática (ADRs) para menos de 580. Quando se cria um ADR, os âmbitos de segurança que têm acesso ao mesmo são automaticamente adicionados. Se existirem mais de 580 âmbitos de segurança definidos, o ADR não funcionará e um erro é registado em ruleengine.log.

### <a name="sms-provider"></a>Fornecedor de SMS

<!-- SCCMDocs#1958 -->

Cada instância do Fornecedor SMS suporta ligações simultâneas a partir de múltiplos pedidos. As únicas limitações nestas ligações são o número de ligações do servidor que estão disponíveis para o Windows, e os recursos disponíveis no servidor para atender os pedidos de ligação.

Para mais informações, consulte [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md).

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a>Números de clientes para sites e hierarquias

Utilize as seguintes informações para determinar quantos clientes e quais os tipos de clientes que pode suportar num site ou numa hierarquia.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a>Hierarquia com um site de administração central

Um site de administração central suporta um número total de dispositivos que inclui até o número de dispositivos listados para os três grupos seguintes:  

- 700.000 ambientes de trabalho do Windows. Consulte também o suporte para [dispositivos incorporados](#embedded).

- 25.000 dispositivos que executam Mac e Windows CE 7.0  

- 100.000 dispositivos que gere utilizando a gestão de dispositivos móveis no local (MDM)

Por exemplo, numa hierarquia pode suportar 700.000 desktops, até 25.000 dispositivos Mac e Windows CE 7.0 e até 100.000 dispositivos geridos pelo MDM no local. Esta hierarquia suporta um total de 825.000 dispositivos.

> [!IMPORTANT]  
> Numa hierarquia onde o site da administração central utiliza uma edição Standard do SQL Server, a hierarquia suporta um máximo de 50.000 desktops e dispositivos. Para suportar mais de 50.000 desktops e dispositivos, deve utilizar uma edição enterprise do SQL Server. Este requisito aplica-se apenas a um site de administração central. Não se aplica a um local primário autónomo ou a um local primário para crianças. A edição do SQL Server que utiliza para um site primário não limita a sua capacidade de suportar o número declarado de clientes.

A edição do SQL Server que está a ser utilizada num site primário autónomo não limita a capacidade desse site de suportar até ao número declarado de clientes.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a>Local primário infantil

Cada local primário infantil numa hierarquia com um site de administração central suporta o seguinte número de clientes:  

- 150.000 clientes e dispositivos totais que não se limitam a um grupo ou tipo específico, desde que o suporte não exceda o número que é suportado para a hierarquia. Consulte também, suporte para [dispositivos incorporados](#embedded).

Por exemplo, um site primário suporta 25.000 dispositivos Mac e Windows CE 7.0. Este número é o limite para uma hierarquia. Este site primário pode então suportar mais 125.000 computadores de secretária. O número total de dispositivos suportados para o local primário da criança é o limite máximo suportado de 150.000.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a>Local primário autónomo

Um local primário autónomo suporta o seguinte número de dispositivos:  

- 175.000 clientes e dispositivos totais, para não exceder:  

  - 150.000 desktops (computadores que executam Windows, Linux e UNIX). Consulte também, suporte para [dispositivos incorporados](#embedded).

  - 25.000 dispositivos que executam Mac e Windows CE 7.0

  - 50.000 dispositivos que gere utilizando MDM no local  

Por exemplo, um site primário autónomo que suporta 150.000 desktops e 10.000 Macs só pode suportar mais 15.000 dispositivos móveis geridos pelo MDM no local.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a>Sites primários e dispositivos Incorporados ao Windows

Os sites primários suportam dispositivos Incorporados do Windows que têm filtros de escrita baseados em ficheiros (FBWF) ativados. Quando os dispositivos incorporados não têm filtros de escrita ativados, um site primário pode suportar uma série de dispositivos incorporados até ao número permitido de dispositivos para esse site. Quando os dispositivos incorporados têm filtros de escrita FBWF ou Unificados (UWF), um site primário pode suportar um máximo de 10.000 dispositivos incorporados no Windows. Estes dispositivos devem ser configurados com as exceções enumeradas na nota importante encontrada no Planeamento para implementação do [cliente em dispositivos Incorporados](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)pelo Windows . Um site primário suporta apenas 3.000 dispositivos Windows Embedded que têm EWF ativado e que não estão configurados para as exceções.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a>Sítios secundários

Os sites secundários suportam o seguinte número de dispositivos:  

- 15.000 desktops (computadores que executam Windows, Linux e UNIX)  

### <a name="management-points"></a><a name="bkmk_mp"></a>Pontos de gestão

Cada ponto de gestão pode suportar o seguinte número de dispositivos:  

- 25.000 clientes e dispositivos totais, para não exceder:  

  - 25.000 desktops (computadores que executam Windows, Linux e UNIX)  

  - Um dos seguintes (não ambos):  

    - 10.000 dispositivos que são geridos através do USO de MDM no local  

    - 10.000 dispositivos que executam clientes Mac e Windows CE 7.0
