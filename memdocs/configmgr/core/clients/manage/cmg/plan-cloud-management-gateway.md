---
title: Planear o gateway de gestão na cloud
titleSuffix: Configuration Manager
description: Planeie e desenhe o gateway de gestão de nuvem (CMG) para simplificar a gestão de clientes baseados na Internet.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 67b6fc51493dce4ee1718586cbf454da91883409
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254627"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Plano para o gateway de gestão de nuvem em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1101764-->
O portal de gestão de nuvem (CMG) fornece uma forma simples de gerir os clientes do Gestor de Configuração na internet. Ao implementar o CMG como um serviço de cloud no Microsoft Azure, você pode gerir clientes tradicionais que vagueiam pela internet sem infraestruturas adicionais no local. Também não precisa de expor a sua infraestrutura no local à internet.

> [!NOTE]
> O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Após a criação dos pré-requisitos, a criação do CMG consiste nos seguintes três passos na consola Do Gestor de Configuração:

1. Desloque o serviço de nuvem CMG para o Azure.
2. Adicione a função de ponto de ligação CMG.
3. Configure as funções do site e do site para o serviço.
Uma vez implementados e configurados, os clientes acedem perfeitamente às funções no local, independentemente de estarem na intranet ou na internet.

Este artigo fornece os conhecimentos fundamentais para aprender sobre o CMG, projetar como se encaixa no seu ambiente, e planear a implementação.

## <a name="scenarios"></a>Cenários

Existem vários cenários para os quais um CMG é benéfico. Os seguintes cenários são alguns dos mais comuns:  

- Gerencie os clientes tradicionais do Windows com identidade de domínio active- dispor. Estes clientes incluem o Windows 8.1 e o Windows 10. Utiliza certificados PKI para proteger o canal de comunicação. As atividades de gestão incluem:  

  - Atualizações de software e proteção de pontofinal
  - Inventário e estatuto de cliente
  - Definições de compatibilidade
  - Distribuição de software para o dispositivo
  - Sequência de tarefas de upgrade do Windows 10 no local

- Gerencie os clientes tradicionais do Windows 10 com identidade moderna, híbrido ou puro domínio em nuvem associada ao Azure Ative Directory (Azure AD). Os clientes usam a AD Azure para autenticar certificados PKI em vez de PKI. A utilização de AD Azure é mais simples de configurar, configurar e manter do que sistemas PKI mais complexos. As atividades de gestão são as mesmas que o primeiro cenário, bem como:  

  - Distribuição de software ao utilizador  

- Instale o cliente do Gestor de Configuração em dispositivos Windows 10 através da internet. A utilização da Azure AD permite que o dispositivo autentique à CMG para registo e atribuição de clientes. Pode instalar o cliente manualmente ou utilizar outro método de distribuição de software, como o Microsoft Intune.  

- Novo fornecimento de dispositivos com cogestão. Ao inscrever automaticamente clientes existentes, a CMG não é necessária para a cogestão. É necessário para novos dispositivos que envolvam Windows AutoPilot, Azure AD, Microsoft Intune e Configuration Manager. Para mais informações, consulte [Caminhos para a cogestão.](../../../../comanage/quickstart-paths.md)

### <a name="specific-use-cases"></a>Casos de utilização específica

Nestes cenários podem aplicar-se os seguintes casos específicos de utilização do dispositivo:

- Dispositivos de roaming, tais como portáteis  

- Dispositivos de escritório remoto/sucursal que são menos caros e mais eficientes para gerir através da internet do que através de um WAN ou através de uma VPN.  

- Fusões e aquisições, onde pode ser mais fácil juntar dispositivos à Azure AD e gerir através de uma CMG.  

- Clientes de grupo de trabalho. Estes dispositivos podem necessitar de configuração adicional, como certificados.<!-- SCCMDocs#1925 -->

    A partir da versão 2002, o Gestor de Configuração suporta a autenticação baseada em token, o que pode ajudar na gestão de clientes de grupos de trabalho remotos. Para mais informações, consulte [a autenticação baseada em Token para CMG](../../deploy/deploy-clients-cmg-token.md).

> [!Important]
> Por padrão, todos os clientes recebem política para um CMG, e começam a usá-la quando se tornam baseadas na Internet. Dependendo do cenário e do caso de utilização que se aplique à sua organização, poderá ter de analisar o uso da CMG. Para mais informações, consulte os clientes Enable para utilizar um cenário de cliente de gateway de gestão de [nuvem.](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway)

## <a name="topology-design"></a>Design de topologia

### <a name="cmg-components"></a>Componentes CMG

A implantação e o funcionamento da CMG incluem os seguintes componentes:  

- O **serviço de nuvem CMG** em Azure autentica e reencaminha pedidos de clientes do Gestor de Configuração para o ponto de ligação CMG.  

- A função do sistema de pontode **ligação CMG** permite uma ligação consistente e de alto desempenho desde a rede no local até ao serviço CMG em Azure. Também publica definições para o CMG, incluindo informações de ligação e definições de segurança. O ponto de ligação CMG reme os pedidos do cliente da CMG para funções no local de acordo com mapeamentos de URL.

- A função do sistema de ponto de [**ligação**](../../../servers/deploy/configure/about-the-service-connection-point.md) de serviço executa a componente do gestor de serviço sinuoso, que trata de todas as tarefas de implementação da CMG. Além disso, monitoriza e reporta a saúde do serviço e regista informações a partir da AD Azure. Certifique-se de que o seu ponto de ligação de serviço está no [modo on-line](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).  

- O site de **gestão de pontos** de gestão presta pedidos de clientes por normal.  

- O software **update point** site role services client requests per normal.  

- **Os clientes baseados na Internet ligam-se** à CMG para aceder aos componentes do Gestor de Configuração no local.

- A CMG utiliza um serviço web **HTTPS baseado em certificados** para ajudar a garantir a comunicação de rede com os clientes.  

- Os clientes baseados na Internet utilizam **certificados PKI ou Azure AD** para identidade e autenticação.  

- Um ponto de [**distribuição na nuvem**](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) fornece conteúdo a clientes baseados na Internet, conforme necessário.  

  - Uma CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados e o custo exigidos dos VMs Azure. Para mais informações, consulte [Modificar um CMG](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
Crie o CMG utilizando uma implementação do Gestor de **Recursos Azure.** [O Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma entidade única, chamada grupo de [recursos.](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) Ao implantar a CMG com o Azure Resource Manager, o site utiliza o Azure Ative Directory (Azure AD) para autenticar e criar os recursos em nuvem necessários. Esta implantação modernizada não requer o clássico certificado de gestão Azure.  

> [!NOTE]
> Esta capacidade não permite suporte para fornecedores de serviços de nuvem Azure (CSP). A implantação da CMG com o Azure Resource Manager continua a utilizar o clássico serviço de cloud, que o CSP não suporta. Para mais informações, consulte [os serviços azure disponíveis no Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).

Começando na versão 1902 do Gestor de Configuração, o Gestor de Recursos do Azure é o único mecanismo de implementação para novos casos do gateway de gestão de nuvem. As missões existentes continuam a funcionar.<!-- 3605704 -->

Na versão 1810 e anterior do Gestor de Configuração, o assistente CMG ainda oferece a opção para uma **implementação de serviço clássico** utilizando um certificado de gestão Azure. Para simplificar a implantação e gestão de recursos, o modelo de implantação do Gestor de Recursos Azure é recomendado para todas as novas instâncias cmg. Se possível, reimplante as instâncias CMG existentes através do Gestor de Recursos. Para mais informações, consulte [Modificar um CMG](setup-cloud-management-gateway.md#modify-a-cmg).

> [!IMPORTANT]
> A implantação clássica do serviço em Azure é depreciada para utilização no Gestor de Configuração. A versão 1810 é a última a apoiar a criação destas implantações Azure. Esta funcionalidade será removida numa futura versão do 'Gestor de Configuração'.<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>Design hierárquio

Crie o CMG no local de topo da sua hierarquia. Se isso é um site de administração central, então crie pontos de ligação CMG em locais primários infantis. A componente do gestor de serviços na nuvem está no ponto de ligação ao serviço, que também está no site da administração central. Este design pode partilhar o serviço em diferentes locais primários, se necessário.

Pode criar vários serviços CMG em Azure, e pode criar vários pontos de ligação CMG. Vários pontos de ligação CMG proporcionam o equilíbrio de carga do tráfego do cliente desde a CMG até às funções no local.

A partir da versão 1902, pode associar um CMG a um grupo de limites. Esta configuração permite que os clientes faltem ou recuem para a CMG para comunicação do cliente de acordo com [as relações de grupo de fronteira](../../../servers/deploy/configure/boundary-groups.md). Este comportamento é especialmente útil em cenários de sucursais e VPN. Pode direcionar o tráfego de clientes para longe de ligações WAN caras e lentas para, em vez disso, utilizar serviços mais rápidos no Microsoft Azure.<!--3640932-->

> [!NOTE]
> Os clientes baseados na Internet não caem em nenhum grupo de fronteiras.
>
> Na versão 1810 e anterior do Gestor de Configuração, o CMG não cai em nenhum grupo de fronteiras.

Outros fatores, como o número de clientes a gerir, também têm impacto no design da CMG. Para mais informações, consulte [Performance e escala.](#performance-and-scale)

#### <a name="example-1-standalone-primary-site"></a>Exemplo 1: local primário autónomo

Contoso tem um local primário autónomo num centro de dados no local, na sua sede em Nova Iorque.

- Criam um CMG na região de East US Azure para reduzir a latência da rede.
- Criam dois pontos de ligação CMG, ambos ligados ao único serviço CMG.  

À medida que os clientes vagueiam pela internet, comunicam com a CMG na região de East US Azure. A CMG encaminha esta comunicação através de ambos os pontos de ligação CMG.

#### <a name="example-2-hierarchy"></a>Exemplo 2: hierarquia

O Quarto Café tem um site de administração central num centro de dados no local, na sua sede em Seattle. Um local primário está no mesmo centro de dados, e o outro local primário está no seu principal escritório europeu em Paris.

- No site da administração central, criam um serviço CMG na região oeste dos EUA Azure. Escalam o número de VMs para a carga esperada de clientes de roaming em toda a hierarquia.
- No local primário sediado em Seattle, criam um ponto de ligação CMG ligado ao CMG único.
- No local primário sediado em Paris, criam um ponto de ligação CMG ligado ao CMG único.

À medida que os clientes vagueiam pela internet, comunicam com a CMG na região oeste dos EUA Azure. A CMG encaminha esta comunicação para o ponto de ligação CMG no local primário designado pelo cliente.

> [!TIP]
> Não é preciso implementar mais do que uma porta de entrada de gestão de nuvens para fins de geolocalização. O cliente do Gestor de Configuração não é afetado principalmente pela ligeira latência que pode ocorrer com o serviço de nuvem, mesmo quando geograficamente distante.

## <a name="requirements"></a>Requisitos

- Uma **assinatura Azure** para acolher o CMG.

- A sua conta de utilizador tem de ser um **administrador completo** ou administrador de **infraestrutura** no Gestor de Configuração.<!-- SCCMDocs#2146 -->

- Um **administrador azure** precisa de participar na criação inicial de determinados componentes, dependendo do seu design. Esta persona pode ser a mesma que o administrador do Gestor de Configuração, ou separada. Se separado, não requer permissões no Gestor de Configuração.

  - Para implementar o CMG, precisa de um Administrador de **Subscrição**
  - Para integrar o site com a Azure AD para a implementação do CMG utilizando o Gestor de Recursos Azure, você precisa de um **Administrador Global**

- Pelo menos um servidor windows no local para alojar o ponto de **ligação CMG**. Pode desempenhar esta função com outras funções do sistema do Site Do Gestor de Configuração.  

- O **ponto de ligação** de serviço deve estar no [modo on-line](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).  

- Integração com a **Azure AD** para a implementação do serviço com o Gestor de Recursos Azure. Para mais informações, consulte os [serviços do Configure Azure.](../../../servers/deploy/configure/azure-services-wizard.md)  

- Um certificado de [**autenticação**](certificates-for-cloud-management-gateway.md#bkmk_serverauth) do servidor para o CMG.  

- Podem ser **necessários outros certificados,** dependendo da versão osso do cliente e do modelo de autenticação. Para mais informações, consulte [os certificados CMG](certificates-for-cloud-management-gateway.md).  

    Quando utiliza a opção do site para **utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP,** o ponto de gestão pode ser HTTP. Para mais informações, consulte [O HTTP Melhorado](../../../plan-design/hierarchy/enhanced-http.md).

- Na versão 1810 ou mais anterior do Gestor de Configuração, se utilizar o método de implantação clássico do Azure, deve utilizar um certificado de [**gestão Azure**](certificates-for-cloud-management-gateway.md#bkmk_azuremgmt).  

    > [!TIP]  
    > Utilize o modelo de implementação do Gestor de **Recursos Azure.** Não requer este certificado de gestão.
    >
    > O método de implantação clássico é depreciado a partir da versão 1810.  

- Os clientes devem usar **o IPv4**.  

## <a name="specifications"></a>Especificações

- Todas as versões do Windows listadas em [sistemas operativos suportados para clientes e dispositivos](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) são suportadas para A CMG.  

- A CMG apenas suporta as funções de ponto de gestão e ponto de atualização de software.  

- A CMG não suporta clientes que apenas comunicam com endereços IPv6.<!--495606-->  

- Os pontos de atualização de software utilizando um balanceador de carga de rede não funcionam com a CMG. <!--505311-->  

- As implementações cmg utilizando o Modelo de Recursos Azure não permitem suporte para fornecedores de serviços de nuvem azure (CSP). A implantação da CMG com o Azure Resource Manager continua a utilizar o clássico serviço de cloud, que o CSP não suporta. Para mais informações, consulte [os serviços azure disponíveis no Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services)  

### <a name="support-for-configuration-manager-features"></a>Suporte para funcionalidades de Gestor de Configuração

A tabela que se segue lista o suporte CMG para as funcionalidades do Gestor de Configuração:

|Funcionalidade  |Suporte  |
|---------|---------|
| Atualizações de software     | ![Suportado](media/green_check.png) |
| Endpoint protection     | ![](media/green_check.png) <sup>[Nota](#bkmk_note1)</sup> apoiada 1 |
| Inventário de hardware e software     | ![Suportado](media/green_check.png) |
| Estado do cliente e notificações     | ![Suportado](media/green_check.png) |
| Executar scripts     | ![Suportado](media/green_check.png) |
| Definições de compatibilidade     | ![Suportado](media/green_check.png) |
| Instalação de cliente<br>(com integração da AD Azure)     | ![Suportado](media/green_check.png) |
| Distribuição de software (alvo de dispositivos)     | ![Suportado](media/green_check.png) |
| Distribuição de software (direcionado para o utilizador, necessário)<br>(com integração da AD Azure)     | ![Suportado](media/green_check.png) |
| Distribuição de software (direcionado para o utilizador, disponível)<br>(todos[os requisitos)](../../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices) | ![Suportado](media/green_check.png) |
| Sequência de tarefas de upgrade do Windows 10 no local      | ![Suportado](media/green_check.png) |
| Sequências de tarefas que não estão a usar imagens de arranque e são implementadas com uma opção: **Descarregue todos os conteúdos localmente antes** de iniciar a sequência de tarefas      | ![Suportado](media/green_check.png) |
| Sequências de tarefas que não estão a usar imagens de arranque  | ![Suportado](media/green_check.png) (1910)|
| CMPivot     | ![Suportado](media/green_check.png) |
| Qualquer outro cenário de sequência de tarefas     | ![Não suportado](media/Red_X.png) |
| Impulso do cliente     | ![Não suportado](media/Red_X.png) |
| Atribuição automática de site     | ![Não suportado](media/Red_X.png) |
| Pedidos de aprovação de software     | ![Não suportado](media/Red_X.png) |
| Consola do Configuration Manager     | ![Não suportado](media/Red_X.png) |
| Ferramentas remotas     | ![Não suportado](media/Red_X.png) |
| Site de reporte     | ![Não suportado](media/Red_X.png) |
| Reativação por LAN     | ![Não suportado](media/Red_X.png) |
| Clientes Mac, Linux e UNIX     | ![Não suportado](media/Red_X.png) |
| Cache de pares     | ![Não suportado](media/Red_X.png) |
| On-premises MDM (MDM no local)     | ![Não suportado](media/Red_X.png) |
| Gestão BitLocker     | ![Não suportado](media/Red_X.png) |

|Chave|
|--|
|![Suportado](media/green_check.png) = Esta funcionalidade é suportada com CMG por todas as versões suportadas do Gestor de Configuração  |
|![Suportado](media/green_check.png) *(YYMM*) = Esta funcionalidade é suportada com CMG a partir da versão *YYMM* do Gestor de Configuração  |
|![Não suportado](media/Red_X.png) = Esta funcionalidade não é suportada com CMG |

#### <a name="note-1-support-for-endpoint-protection"></a><a name="bkmk_note1"></a>Nota 1: Suporte para proteção de pontos finais
<!-- 4350561 -->
Para que os dispositivos unidos pelo domínio apliquem a política de proteção de pontos finais, exigem o acesso ao domínio. Os dispositivos com acesso pouco frequente à rede interna podem sofrer atrasos na aplicação da política de proteção de pontos finais. Se necessitar que os dispositivos apliquem imediatamente a política de proteção do ponto final depois de a receberem, considere uma das seguintes opções:

- Utilize a cogestão e mude a carga de trabalho de [Proteção de Pontofinal](../../../../comanage/workloads.md#endpoint-protection) para Intune e gerencie o [Antivírus](https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#microsoft-defender-antivirus) Microsoft Defender a partir da nuvem.

- Utilize itens de [configuração](../../../../compliance/deploy-use/create-configuration-items.md) em vez da funcionalidade antimalware nativa [antimalware para](../../../../protect/deploy-use/endpoint-antimalware-policies.md) aplicar a política de proteção de pontos finais.

## <a name="cost"></a>Custo

> [!IMPORTANT]  
> A seguinte informação sobre os custos destina-se apenas a estimativas. O seu ambiente pode ter outras variáveis que afetam o custo global da utilização da CMG.

A CMG utiliza os seguintes componentes Azure, que incorrem em encargos para a conta de subscrição do Azure:

### <a name="virtual-machine"></a>Máquina virtual

- A CMG utiliza o Azure Cloud Services como plataforma como serviço (PaaS). Este serviço utiliza máquinas virtuais (VMs) que incorrem em custos de computação.  

- A CMG utiliza um VM Standard A2 V2.  

- Selecione quantas instâncias vm suportam o CMG. Um é o padrão, e 16 é o máximo. Este número é definido na criação do CMG, e pode ser alterado posteriormente para escalar o serviço conforme necessário.

- Para obter mais informações sobre quantos VMs precisa para apoiar os seus clientes, consulte [Performance e escala](#performance-and-scale).

- Consulte a calculadora de [preços Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os custos potenciais.

    > [!NOTE]  
    > Os custos das máquinas virtuais variam por região.

### <a name="outbound-data-transfer"></a>Transferência de dados de saída

- Os encargos baseiam-se em dados que fluem do Azure (saída ou download). Quaisquer fluxos de dados para o Azure são gratuitos (ingressou ou upload). Os fluxos de dados da CMG do Azure incluem política para o cliente, notificações de clientes e respostas de clientes reencaminhados pela CMG para o site. Estas respostas incluem relatórios de inventário, mensagens de estado e estado de conformidade.  

- Mesmo sem que nenhum cliente se comunicasse com uma CMG, alguma comunicação de fundo causa tráfego de rede entre a CMG e o site no local.  

- Ver a transferência de **dados de Saída (GB)** na consola do Gestor de Configuração. Para mais informações, consulte [os clientes do Monitor na CMG](monitor-clients-cloud-management-gateway.md).  

- Consulte os detalhes de preços da [largura de banda Azure](https://azure.microsoft.com/pricing/details/bandwidth/) para ajudar a determinar os custos potenciais. Os preços para a transferência de dados são nilutos. Quanto mais usas, menos pagas por gigabyte.  

- *Apenas para fins estimados,* espere aproximadamente 100-300 MB por cliente por mês para clientes baseados na Internet. A estimativa mais baixa é para uma configuração padrão do cliente. A estimativa superior é para uma configuração mais agressiva do cliente. O seu uso real pode variar dependendo da forma como configura as definições do cliente.  

    > [!NOTE]  
    > A realização de outras ações, tais como a implementação de atualizações de software ou aplicações, aumenta a quantidade de transferência de dados de saída do Azure.

- Os clientes baseados na Internet obtêm conteúdo de atualização de software da Microsoft a partir do Windows Update sem custos. Não distribua pacotes de atualização com conteúdos de atualização da Microsoft para um ponto de distribuição na nuvem, caso contrário poderá incorrer em custos de armazenamento e de esgress de dados.  

- A configuração errada da opção CMG para Verificar a **revogação** do certificado de cliente pode causar tráfego adicional dos clientes à CMG. Este tráfego adicional pode aumentar os dados de saída do Azure, o que pode aumentar os seus custos Azure.<!-- SCCMDocs#1434 --> Para mais informações, consulte [Publicar a lista de revogação do certificado](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

### <a name="content-storage"></a>Armazenamento de conteúdo

- Os clientes baseados na Internet obtêm conteúdo de atualização de software da Microsoft a partir do Windows Update sem custos. Não distribua pacotes de atualização com conteúdos de atualização da Microsoft para um ponto de distribuição na nuvem, caso contrário poderá incorrer em custos de armazenamento e de esgress de dados.  

- Para qualquer outro conteúdo necessário, como aplicações ou atualizações de software de terceiros, deve distribuir para um ponto de distribuição na nuvem. Atualmente, a CMG suporta apenas o ponto de distribuição na nuvem para o envio de conteúdo para os clientes.
   - Ao utilizar um CMG para armazenamento de conteúdo, o conteúdo para atualizações de terceiros não será descarregado para os clientes se o conteúdo delta de Download quando a [definição](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) de cliente **disponível** estiver ativada. <!--6598587--> 

- Para mais informações, consulte o custo da utilização de [pontos](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost)de distribuição na nuvem .  

- Um CMG também pode ser um ponto de distribuição na nuvem para servir conteúdo aos clientes. Esta funcionalidade reduz os certificados e o custo exigidos dos VMs Azure. Para mais informações, consulte [Modificar um CMG](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

- A CMG utiliza armazenamento localmente redundante (LRS) do Azure. Para mais informações, consulte [o armazenamento localmente redundante.](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs)  

### <a name="other-costs"></a>Outros custos

- Cada serviço na nuvem tem um endereço IP dinâmico. Cada CMG distinto usa um novo endereço IP dinâmico. Adicionar VMs adicionais por CMG não aumenta estes endereços.  

## <a name="performance-and-scale"></a>Desempenho e dimensionamento

Para obter mais informações sobre a escala CMG, consulte [tamanho e números de escala](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg).

As seguintes recomendações podem ajudá-lo a melhorar o desempenho da CMG:

- A ligação entre o cliente do Gestor de Configuração e a CMG não é consciente da região. A comunicação do cliente não é afetada em grande parte pela latência/separação geográfica. Não é necessário implementar vários CMG para fins de geoproximidade. Coloque o CMG no local de alto nível da sua hierarquia e adicione instâncias para aumentar a escala.

- Para uma elevada disponibilidade do serviço, crie um CMG com pelo menos duas instâncias CMG e dois pontos de ligação CMG por site.  

- Dimensione a CMG para apoiar mais clientes adicionando mais casos de VM. O equilibrador de carga Azure controla as ligações do cliente ao serviço.  

- Crie mais pontos de ligação CMG para distribuir a carga entre eles. A CMG distribui o tráfego pelos seus pontos de ligação CMG de ligação de forma redonda.  

- Quando a CMG está sob alta carga com mais do que o número suportado de clientes, ainda lida com pedidos, mas pode haver atraso.  

> [!NOTE]
> Embora o Gestor de Configuração não tenha limites rígidos no número de clientes para um ponto de ligação CMG, o Windows Server tem uma gama de porta dinâmica TCP máxima padrão de 16.384. Se um site do Gestor de Configuração gerir mais de 16.384 clientes com um único ponto de ligação CMG, deve aumentar o limite do Servidor do Windows. Todos os clientes mantêm um canal para notificações de clientes, que mantém uma porta aberta no ponto de ligação CMG. Para obter mais informações sobre como usar o comando netsh para aumentar este limite, consulte o [artigo 929851](https://support.microsoft.com/help/929851)do Microsoft Support .

## <a name="ports-and-data-flow"></a>Portos e fluxo de dados

Não precisa abrir nenhum porto de entrada para a sua rede no local. O ponto de ligação de serviço e o ponto de ligação CMG iniciam todas as comunicações com o Azure e a CMG. Estas duas funções do sistema de site precisam de criar ligações de saída à nuvem da Microsoft. O ponto de ligação de serviço implanta e monitoriza o serviço em Azure, pelo que deve ser o modo online. O ponto de ligação CMG liga-se à CMG para gerir a comunicação entre as funções do sistema de instalação CMG e no local.

O diagrama a seguir é um fluxo de dados básico e conceptual para o CMG:

[![Fluxo de dados cmg](media/cmg-data-flow.png)](media/cmg-data-flow.png#lightbox)

1. O ponto de ligação de serviço liga-se ao Azure sobre a porta HTTPS 443. Autentica-se utilizando a Azure AD ou o certificado de gestão Azure. O ponto de ligação de serviço implanta o CMG em Azure. O CMG cria o serviço de nuvem HTTPS utilizando o certificado de autenticação do servidor.  

2. O ponto de ligação CMG liga-se ao CMG em Azure sobre TCP-TLS ou HTTPS. Mantém a ligação aberta e constrói o canal para futura comunicação bidirecional.  

3. O cliente liga-se ao CMG sobre a porta HTTPS 443. Autentica-se utilizando a Azure AD ou o certificado de autenticação do cliente.  

4. A CMG repara a comunicação do cliente sobre a ligação existente ao ponto de ligação CMG no local. Não precisas de abrir nenhuma porta de firewall de entrada.  

5. O ponto de ligação CMG reme a comunicação do cliente para o ponto de gestão no local e ponto de atualização de software.  

Para obter mais informações quando hospedar conteúdo em Azure, consulte [Use um ponto de distribuição baseado na nuvem](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="required-ports"></a>Portas necessárias

Esta tabela lista as portas e protocolos de rede exigidos. O *Cliente* é o dispositivo que inicia a ligação, exigindo uma porta de saída. O *Servidor* é o dispositivo que aceita a ligação, exigindo uma porta de entrada.

| Cliente | Protocolo | Porta | Servidor | Descrição |
|--------|----------|------|--------|-------------|
| Ponto de ligação de serviço | HTTPS | 443 | Azure | Implantação cmg |
| Ponto de ligação CMG | TCP-TLS | 10140-10155 | Serviço CMG | Protocolo preferido para construir canal CMG <sup> [Nota 1](#bkmk_port-note1)</sup> |
| Ponto de ligação CMG | HTTPS | 443 | Serviço CMG | Protocolo de recuo para construir canal CMG para apenas uma instância VM <sup> [Nota 2](#bkmk_port-note2)</sup> |
| Ponto de ligação CMG | HTTPS | 10124-10139 | Serviço CMG | Protocolo de recuo para construir canal CMG para dois ou mais casos vM <sup> [Nota 3](#bkmk_port-note3)</sup> |
| Cliente | HTTPS | 443 | CMG | Comunicação geral do cliente |
| Ponto de ligação CMG | HTTPS ou HTTP | 443 ou 80 | Ponto de gestão | Tráfego no local, porto depende da configuração do ponto de gestão |
| Ponto de ligação CMG | HTTPS ou HTTP | 443 ou 80 | Ponto de atualização de software | Tráfego no local, porta depende da configuração do ponto de atualização de software |

#### <a name="note-1-cmg-connection-point-tcp-tls-ports"></a><a name="bkmk_port-note1"></a>Nota 1: Portas tCP-TLS ponto de ligação CMG

O ponto de ligação CMG tenta primeiro estabelecer uma ligação TCP-TLS de longa duração a cada instância cmg VM. Liga-se à primeira instância VM na porta 10140. A segunda instância VM utiliza o porto 10141, até ao dia 16 no porto 10155. Uma ligação TCP-TLS tem o melhor desempenho, mas não suporta procuração de internet. Se o ponto de ligação CMG não conseguir ligar via TCP-TLS, então volta a cair para HTTPS<sup>[Nota 2](#bkmk_port-note2)</sup>.

#### <a name="note-2-cmg-connection-point-https-ports-for-one-vm"></a><a name="bkmk_port-note2"></a>Nota 2: Ponto de ligação CMG ponto de ligação PORTAS HTTPS para um VM

Se o ponto de ligação CMG não conseguir ligar-se ao CMG através da<sup>[Nota 1](#bkmk_port-note1)</sup>da TCP-TLS, liga-se ao equilibrista de carga da rede Azure sobre HTTPS 443 apenas para uma instância VM.  

#### <a name="note-3-cmg-connection-point-https-ports-for-two-or-more-vms"></a><a name="bkmk_port-note3"></a>Nota 3: Ponto de ligação CMG ponto de ligação PORTAS HTTPS para dois ou mais VMs

Se houver duas ou mais instâncias vM, o ponto de ligação CMG utiliza HTTPS 10124 para a primeira instância VM, e não HTTPS 443. Liga-se à segunda instância VM em HTTPS 10125, até à 16ª posição na porta HTTPS 10139.

### <a name="internet-access-requirements"></a>Requisitos de acesso à Internet

Se a sua organização restringir a comunicação de rede com a internet utilizando um firewall ou dispositivo proxy, tem de permitir que o ponto de ligação CMG e o ponto de ligação ao serviço acedam a pontos finais da Internet.

Para mais informações, consulte os requisitos de [acesso à Internet.](../../../plan-design/network/internet-endpoints.md#bkmk_cloud)

## <a name="next-steps"></a>Passos seguintes

- [Certificados para o gateway de gestão na cloud](certificates-for-cloud-management-gateway.md)
- [Segurança e privacidade para o gateway de gestão na cloud ](security-and-privacy-for-cloud-management-gateway.md)
- [Tamanho do gateway de gestão da nuvem e números de escala](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
- [Perguntas frequentes sobre o gateway de gestão de nuvens](cloud-management-gateway-faq.md)
- [Configurar o gateway de gestão na cloud](setup-cloud-management-gateway.md)
