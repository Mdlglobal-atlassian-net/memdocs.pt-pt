---
title: Configuration Manager no Azure
titleSuffix: Configuration Manager
description: Informações sobre a utilização do Gestor de Configuração num ambiente Azure.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c12372325573c6795396ff0832ca60cba68b8c29
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078503"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Gestor de Configuração em Azure - Perguntas Frequentes

*Aplica-se a: Gestor de Configuração (ramo atual)*

As seguintes perguntas e respostas podem ajudá-lo a entender quando usar e como configurar o Configurmanager de Configuração no Microsoft Azure.

## <a name="general-questions"></a>Perguntas Gerais
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>A minha empresa está a tentar mover o maior número possível de servidores físicos para o Microsoft Azure, posso transferir servidores do Gestor de Configuração para o Azure?
Certamente, este é um cenário apoiado.  Consulte suporte para ambientes de [virtualização para gestor](../plan-design/configs/support-for-virtualization-environments.md)de configuração .

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Ótimo! O meu ambiente requer vários sítios. Todos os locais primários para crianças devem estar em Azure com o site da administração central ou no local? E os locais secundários?
As comunicações site-to-site (replicação baseada em ficheiros e base de dados) beneficiam da proximidade de estarem alojadas no Azure. No entanto, todo o tráfego relacionado com o cliente estaria afastado dos servidores do site e dos sistemas do site. Se utilizar uma ligação de rede rápida e fiável entre o Azure e a sua intranet com um plano de dados ilimitado, hospedar todas as suas infraestruturas em Azure é uma opção.

No entanto, se utilizar um plano de dados medido e a largura de banda ou o custo disponíveis é uma preocupação, ou a ligação de rede entre o Azure e a sua intranet não é rápida ou pode ser pouco fiável, então considere colocar sites específicos (e sistemas de sites) no local e, em seguida, use os controlos de largura de banda incorporados no Gestor de Configuração.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Ter O Gestor de Configuração em Azure um cenário SaaS (Software como serviço)?
Não, é um IaaS (Infraestrutura como serviço) porque hospeda os seus servidores de infraestrutura do Gestor de Configuração em máquinas virtuais Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>A que áreas devo prestar atenção ao considerar uma mudança da minha infraestrutura de Gestor de Configuração para OAzure?
Grande questão, aqui estão as áreas que são mais importantes na tomada desta decisão, cada um é explorado numa secção separada deste tópico:
1. Redes
2. Disponibilidade
3. Desempenho
4. Custo
5. Experiência do Utilizador

## <a name="networking"></a>Redes
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>E os requisitos de networking, devo usar o ExpressRoute ou um Azure VPN Gateway?
O networking é uma decisão muito importante. As velocidades de rede e a latência podem afetar a funcionalidade entre o servidor do site e os sistemas de site remoto e qualquer comunicação do cliente aos sistemas do site. A nossa recomendação é usar o ExpressRoute. Mas não existe uma limitação de Configuração Manager para o impedir de usar o Gateway Azure VPN. Deve rever cuidadosamente os seus requisitos (desempenho, patching, distribuição de software, implementação do sistema de operação) a partir desta infraestrutura e, em seguida, tomar a sua decisão. Algumas coisas a considerar para cada solução incluem:

- **Rota expresso** (recomendado)
  - Extensão natural ao seu datacenter (pode ligar vários datacenters)
  - Ligações privadas entre datacenters Azure e sua infraestrutura
  - Não passa pela internet pública.
  - Oferece fiabilidade, velocidades rápidas, latência mais baixa, alta segurança
  - Ofertas até 10gbps de velocidade e opções de plano de dados ilimitados
- **Gateway de VPN**
  - VPNs site-to-site/ponto-a-site
  - O tráfego passa pela internet pública
  - Utiliza a Segurança do Protocolo de Internet (IPsec) e a Troca de Chaves da Internet (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>O ExpressRoute tem muitas opções diferentes, como ilimitada vs. medido, diferentes opções de velocidade e complemento premium. Qual devo escolher?
As opções que selecionar dependem do cenário que está a implementar e da quantidade de dados que planeia distribuir. A transferência de dados do Gestor de Configuração pode ser controlada entre servidores do site e pontos de distribuição, mas a comunicação servidor-site-para-site não pode ser controlada.   Quando utiliza um plano de dados medido, colocar sites específicos (e sistemas de sites) no local e utilizar os controlos de largura de [banda incorporados do Diretor](../plan-design/hierarchy/fundamental-concepts-for-content-management.md) de Configuração pode ajudar a controlar o custo da utilização do Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>E os requisitos de instalação, como domínios de Diretório Ativo? Ainda preciso de me juntar aos servidores do site para um domínio de Diretório Ativo?
Sim. Quando se muda para o Azure, as [configurações suportadas](../plan-design/configs/supported-configurations.md) permanecem as mesmas, incluindo os requisitos de Diretório Ativo para a instalação do Gestor de Configuração.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Compreendo a necessidade de me juntar aos servidores do site para um domínio de Diretório Ativo, mas posso usar o Diretório Ativo Azure?
Não, o Azure Ative Directory não é apoiado neste momento. Os servidores do seu site ainda devem ser membros de um domínio do [Diretório Ativo do Windows](../plan-design/configs/support-for-active-directory-domains.md).



## <a name="availability"></a>Disponibilidade
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Uma das razões pelas quais estou a transferir infraestruturas para Otávio é a promessa de grande disponibilidade. Posso aproveitar opções de alta disponibilidade, como conjuntos de disponibilidade De VM Azure para VMs que vou usar para O Gestor de Configuração?
Sim! Os conjuntos de disponibilidade Azure VM podem ser usados para funções redundantes do sistema de sites, como pontos de distribuição ou pontos de gestão.

Também pode usá-los para os servidores do site do Gestor de Configuração. Por exemplo, os sites da administração central e os locais primários podem estar todos no mesmo conjunto de disponibilidade que pode ajudá-lo a garantir que não são reiniciados ao mesmo tempo.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Como posso disponibilizar a minha base de dados? Posso usar a Base de Dados Azure SQL? Ou tenho de usar o Microsoft SQL Server num VM?
Tem de utilizar o Microsoft SQL Server num VM. O Gestor de Configuração não suporta o Servidor Azure SQL neste momento. Mas pode utilizar funcionalidades como SempreOn Availability Groups para o seu servidor SQL. [Os Grupos de Disponibilidade AlwaysOn](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) são recomendados e são oficialmente suportados a partir da versão 1602 do Gestor de Configuração.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Posso usar os equilibradores de carga Azure com funções do sistema de site, como pontos de gestão ou pontos de atualização de software?
Embora o Gestor de Configuração não seja testado com os equilibradores de carga Azure, se a funcionalidade for transparente para a aplicação, não deverá ter quaisquer efeitos adversos nas operações normais.


## <a name="performance"></a>Desempenho
### <a name="what-factors-affect-performance-in-this-scenario"></a>Que fatores afetam o desempenho neste cenário?
[Tamanho e tipo Azure VM,](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs)discos Azure VM (armazenamento premium é recomendado, especialmente para O Servidor SQL), latência em rede e velocidade são as áreas mais importantes.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Então, conte-me mais sobre máquinas virtuais Azure; Que tamanho devo usar vMs?
Em geral, a sua potência computacional (CPU e Memória) precisa de satisfazer o [hardware recomendado para o Gestor](../plan-design/configs/recommended-hardware.md)de Configuração . Mas existem algumas diferenças entre hardware de computador regular e VMs Azure, especialmente quando se trata dos discos que estes VMs usam.  O tamanho dos VMs que utiliza depende do tamanho do seu ambiente, mas aqui ficam algumas recomendações:
- Para implantações de produção de qualquer tamanho significativo recomendamos "**S**" classe Azure VMs. Isto porque podem alavancar discos de Armazenamento Premium.  Os VMs da classe "S" não utilizam o armazenamento de bolhas e, em geral, não cumprirão os requisitos de desempenho necessários para uma experiência de produção aceitável.
- Vários discos de armazenamento Premium devem ser utilizados para uma escala mais elevada e listrados na consola de Gestão de Discos Windows para o máximo de IOPS.  
- Recomendamos a utilização de discos melhores ou múltiplos premium durante a implementação inicial do site (como P30 em vez de P20, e 2xP30 num volume listrado em vez de 1xP30). Em seguida, se o seu site mais tarde precisar de aumentar em tamanho VM devido a carga adicional, você pode aproveitar o CPU adicional e memória que um tamanho VM maior fornece. Também terá discos já em vigor que podem tirar partido da entrada adicional de IOPS que o tamanho vM maior permite.



As tabelas a seguir listam as contagens iniciais sugeridas do disco para utilizar em locais de administração primária e central para instalações de vários tamanhos:

Base de dados do **site co-localizado** - Site de administração primária ou central com a base de dados do site no servidor do site:

| Clientes desktop    |Tamanho VM recomendado|Discos Recomendados|
|--------------------|-------------------|-----------------|
|**Até 25k**       |   DS4_V2          |2xP30 (listrado)  |
|**25k a 50k**      |   DS13_V2         |2xP30 (listrado)  |
|**50k a 100k**     |   DS14_V2         |3xP30 (listrado)  |


**Base** de dados de site remoto - Site de administração primária ou central com a base de dados do site num servidor remoto:

| Clientes desktop    |Tamanho VM recomendado|Discos Recomendados |
|--------------------|-------------------|------------------|
|**Até 25k**       | Servidor do site: F4S </br>Servidor de base de dados: DS12_V2 | Servidor do site: 1xP30 </br>Servidor de base de dados: 2xP30 (listrado)  |
|**25k a 50k**      | Servidor do site: F4S </br>Servidor de base de dados: DS13_V2 | Servidor do site: 1xP30 </br>Servidor de base de dados: 2xP30 (listrado)   |
|**50k a 100k**     | Servidor do site: F8S </br>Servidor de base de dados: DS14_V2 | Servidor do site: 2xP30 (listrado)   </br>Servidor de base de dados: 3xP30 (listrado)   |

O seguinte mostra uma configuração de exemplo para clientes de 50 k a 100k em DS14_V2 com discos 3xP30 ![em volume listrado com volumes lógicos separados para o sistema de configuração e ficheiros de base de dados: VM)discos](media/vm_disks.png)  



## <a name="user-experience"></a>Experiência do Utilizador
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Menciona que a experiência do utilizador é uma das principais áreas de importância, porque é que isso?
As decisões que tomar para networking, disponibilidade, desempenho e onde coloca os servidores do site do Gestor de Configuração podem afetar diretamente os seus utilizadores. Acreditamos que uma mudança para o Azure deve ser transparente para os seus utilizadores para que não experimentem uma mudança nas suas interações diárias com o Gestor de Configuração.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>Está bem, já percebi. Planeio instalar um único local primário autónomo numa máquina virtual Azure e quero ter a certeza que os meus custos são baixos. Devo colocar sistemas de site (remotos) (como pontos de gestão, pontos de distribuição e pontos de atualização de software) também em máquinas virtuais Azure ou no local?
Com exceção da comunicação do servidor do site para um ponto de distribuição, estas comunicações servidor-servidor num site podem ocorrer a qualquer momento e não utilizam mecanismos para controlar a utilização da largura de banda da rede. Uma vez que não é possível controlar a comunicação entre os sistemas do site, devem ser considerados quaisquer custos associados a estas comunicações.

As velocidades de rede e a latência são outros fatores a ter em conta também. Redes lentas ou pouco fiáveis podem ter impacto na funcionalidade entre o servidor do site e os sistemas de site remoto, bem como qualquer comunicação do cliente aos sistemas do site. O número de clientes geridos que utilizam um determinado sistema de site, bem como as funcionalidades que utiliza ativamente, também devem ser considerados.
Em geral, pode aproveitar a orientação normal, uma vez que se relaciona com ligações WAN e sistemas de site como ponto de partida. Idealmente, a entrada de rede que seleciona e recebe entre o Azure e a sua intranet será consistente com um WAN que está bem relacionado com uma rede rápida.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>E a distribuição de conteúdos e a gestão de conteúdos? Os pontos de distribuição padrão devem estar em Azure ou no local, e devo utilizar a BranchCache ou os pontos de distribuição no local? Ou devo fazer uso exclusivo de Pontos de Distribuição de Nuvem?
A abordagem para a gestão de conteúdos é praticamente a mesma que para servidores de sites e sistemas de site.
- Se utilizar uma ligação de rede rápida e fiável entre o Azure e a sua intranet com um plano de dados ilimitado, hospedar pontos de distribuição padrão no Azure pode ser uma opção.
- Se utilizar um plano de dados medido e o custo da largura de banda é uma preocupação ou a ligação de rede entre o Azure e a sua intranet não é rápida ou pode não ser fiável, então poderá considerar outras abordagens. Estes incluem a localização de pontos de distribuição padrão ou de puxar no local, bem como a utilização da BranchCache. A utilização de pontos de distribuição baseados na nuvem também é uma opção, mas existem alguns limites para os tipos de conteúdo suportados (por exemplo, nenhum suporte para pacotes de atualizações de software).

> [!NOTE]
>  Se for necessário suporte pXE ou multicast, deve utilizar pontos de distribuição no local (standard ou pull) para responder aos pedidos de arranque.


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Embora esteja bem com as limitações dos pontos de distribuição baseados na nuvem, não quero colocar o meu ponto de gestão num DMZ, mesmo que isso seja necessário para apoiar os meus clientes baseados na Internet. Tenho outrao opção?
Sim! Com a versão 1610 do Gestor de Configuração, introduzimos o [Cloud Management Gateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) como uma funcionalidade de pré-lançamento. (Esta funcionalidade apareceu pela primeira vez na versão de pré-visualização técnica 1606 como serviço de procuração de [nuvem).](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)

O **Cloud Management Gateway** fornece uma forma simples de gerir os clientes do Gestor de Configuração na internet. O serviço, que é implantado no Microsoft Azure e requer uma subscrição do Azure, conecta-se à sua infraestrutura de Configuração no local utilizando uma nova função chamada ponto de conector de gateway de gestão de nuvem. Depois de implementado e configurado, os clientes podem aceder às funções do sistema de configuração do Gestor de Configuração no local, independentemente de estarem ligados à rede privada interna ou à internet.

Você pode começar a usar o gateway de gestão de nuvem no seu ambiente e dar-nos feedback para melhorar isso. Para obter informações sobre as funcionalidades de pré-lançamento, consulte [utilize as funcionalidades de pré-lançamento a partir de atualizações](../servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Também ouvi dizer que tens outra nova funcionalidade chamada Peer Cache introduzida como uma funcionalidade de pré-lançamento na versão 1610. É diferente de BranchCache? Qual devo escolher?
Sim, totalmente diferente. [Peer Cache](../plan-design/hierarchy/client-peer-cache.md) é uma tecnologia 100% nativa do Gestor de Configuração onde branchCache é uma característica do Windows. Ambos podem ser úteis para si; BranchCache utiliza uma transmissão para encontrar o conteúdo necessário, enquanto peer Cache utiliza o fluxo regular de fluxo de distribuição dos Gestores de Configuração e as definições de grupo de limites.

Pode configurar qualquer cliente para ser uma fonte de Peer Cache. Em seguida, quando os pontos de gestão fornecem aos clientes informações sobre as localizações de fonte de conteúdo, eles fornecem detalhes sobre os pontos de distribuição e quaisquer fontes de Peer Cache que tenham o conteúdo que o cliente necessita.


## <a name="cost"></a>Custo
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>Fale-me um pouco sobre o custo. Será esta uma solução rentável para mim?
É difícil dizer, já que cada ambiente é diferente. A melhor coisa a fazer é custar o seu ambiente usando a calculadora de preços do Microsoft Azure:https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Recursos Adicionais
**Fundamentos:**https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Tipos de máquinas VM Azure:**
- Tamanhos da máquina azure:https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
- Preços VM:https://azure.microsoft.com/pricing/details/virtual-machines/  
- Preços de armazenamento:https://azure.microsoft.com/pricing/details/storage/

**Considerações de desempenho do disco:**    
- Introdução premium do disco:https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Informação mais profunda do Disco Premium:https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- Recolha útil de gráficos para tamanhos max e alvos Perf para armazenamento:https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- Outra Introdução + alguns dados legais uber-geek sobre como o Armazenamento Premium funciona atrás das capas:https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Disponibilidade:**
- Azure IaaS Uptime SLA's:https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- Conjuntos de disponibilidade explicados:https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Conectividade:**
- Rota expressa vs. Azure VPN:https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- Preços da rota expressa:https://azure.microsoft.com/pricing/details/expressroute/
- Mais sobre a Rota expresso:https://azure.microsoft.com/documentation/articles/expressroute-introduction/
