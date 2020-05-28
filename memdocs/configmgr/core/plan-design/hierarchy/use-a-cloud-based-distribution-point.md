---
title: Ponto de distribuição em nuvem
titleSuffix: Configuration Manager
description: Planeie e design para distribuir conteúdo de software através do Microsoft Azure com pontos de distribuição em nuvem no Gestor de Configuração.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52c2b70d2b094d5a89d80aafa61f1db67a53816f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987707"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Use um ponto de distribuição em nuvem no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A implementação para partilha de conteúdos do Azure mudou. Utilize um portal de gestão de nuvem ativado por conteúdo, permitindo que a opção de permitir que a CMG funcione como um ponto de distribuição na **nuvem e sirva conteúdo a partir do armazenamento Azure**. Para mais informações, consulte [Modificar um CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> Não poderá criar um ponto tradicional de distribuição de nuvens no futuro. Para mais informações, consulte [funcionalidades removidas e depreciadas](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Um ponto de distribuição em nuvem é um ponto de distribuição do Gestor de Configuração que é hospedado como Plataforma-as-a-Service (PaaS) no Microsoft Azure. Este serviço suporta os seguintes cenários:  

- Fornecer conteúdo de software a clientes baseados na Internet sem infraestruturas adicionais no local  

- Ativar a nuvem do seu sistema de distribuição de conteúdos  

- Reduzir a necessidade de pontos de distribuição tradicionais  

Este artigo ajuda-o a aprender sobre o ponto de distribuição da nuvem, planeia a sua utilização e projeta a sua implementação. Inclui as seguintes secções:

- [Características e benefícios](#bkmk_features)
- [Design de topologia](#bkmk_topology)
- [Requisitos](#bkmk_requirements)
- [Especificações](#bkmk_spec)
- [Custo](#bkmk_cost)
- [Desempenho e dimensionamento](#bkmk_perf)
- [Portos e fluxo de dados](#bkmk_dataflow)
- [Certificados](#bkmk_certs)
- [Perguntas Mais Frequentes (FAQ)](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a>Características e benefícios

### <a name="features"></a>Funcionalidades

O ponto de distribuição na nuvem suporta várias funcionalidades que também são oferecidas por pontos de distribuição no local:  

- Gerir pontos de distribuição de nuvem individualmente ou como membros de grupos de pontos de distribuição  

- Use um ponto de distribuição de nuvem como uma localização de conteúdo de recuo  

- Suporta clientes intranet e baseados na Internet  

### <a name="benefits"></a>Benefícios

O ponto de distribuição da nuvem proporciona os seguintes benefícios adicionais:  

- O site encripta o conteúdo antes de enviá-lo para o ponto de distribuição da nuvem em Azure.  

- Para atender às exigências em mudança de pedidos de conteúdo por parte dos clientes, escala manualmente o serviço de nuvem em Azure. Esta ação não requer que instale e disponibilize pontos de distribuição adicionais no Gestor de Configuração.  

- Suporta o download de conteúdos de clientes configurados para outras tecnologias de conteúdo, como o Windows BranchCache e fornecedores de conteúdos alternativos.  

- A partir da versão 1806, utilize pontos de distribuição na nuvem como locais de origem para pontos de distribuição de puxar.  


## <a name="topology-design"></a><a name="bkmk_topology"></a>Design de topologia

A implantação e o funcionamento do ponto de distribuição da nuvem inclui os seguintes componentes:  

- Um **serviço de nuvem** em Azure. O site distribui conteúdo para este serviço, que o armazena no armazenamento em nuvem Azure. O ponto de gestão fornece aos clientes esta localização de conteúdo na lista de fontes disponíveis, conforme apropriado.  

- Um site de **gestão** de serviços de serviços de cliente de cliente por normal.  

    - Os clientes no local normalmente usam um ponto de gestão no local.  

    - Os clientes baseados na Internet ou usam um portal de [gestão](../../clients/manage/cmg/plan-cloud-management-gateway.md)de nuvem, ou um [ponto de gestão baseado na Internet.](../../clients/manage/plan-internet-based-client-management.md)  

- O ponto de distribuição na nuvem utiliza um serviço web **HTTPS baseado em certificados** para ajudar a garantir a comunicação de rede com os clientes. Os clientes devem confiar neste certificado.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
A partir da versão 1806, crie um ponto de distribuição em nuvem utilizando uma implementação do Gestor de **Recursos Azure.** [O Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma entidade única, chamada grupo de [recursos.](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) Ao implantar um ponto de distribuição em nuvem com o Azure Resource Manager, o site utiliza o Azure Ative Directory (Azure AD) para autenticar e criar os recursos em nuvem necessários. Esta implantação modernizada não requer o clássico certificado de gestão Azure.  

> [!Note]  
> Esta funcionalidade não permite suporte para fornecedores de serviços de nuvem Azure (CSP). A implantação do ponto de distribuição em nuvem com o Azure Resource Manager continua a utilizar o serviço clássico de cloud, que o CSP não suporta. Para mais informações, consulte [os serviços azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

Começando na versão 1902 do Gestor de Configuração, o Gestor de Recursos do Azure é o único mecanismo de implementação para novos casos do ponto de distribuição da nuvem. As missões existentes continuam a funcionar.<!-- 3605704 -->

Na versão 1810 e anterior do Gestor de Configuração, o assistente de ponto de distribuição em nuvem ainda fornece a opção para uma **implementação de serviço clássico** usando um certificado de gestão Azure. Para simplificar a implantação e gestão de recursos, utilize o modelo de implantação do Gestor de Recursos Azure para todos os novos pontos de distribuição na nuvem. Se possível, reimplante os pontos de distribuição de nuvem existentes através do Gestor de Recursos.

> [!Important]  
> A partir da versão 1810, a implantação clássica de serviço sintetizada em Azure é depreciada para utilização no Gestor de Configuração. Esta versão é a última a apoiar a criação destas implementações azure. Esta funcionalidade será removida numa futura versão do 'Gestor de Configuração'.<!--SCCMDocs-pr issue #2993-->  

O Gestor de Configuração não migra os pontos clássicos de distribuição de nuvem existentes para o modelo de implementação do Gestor de Recursos Azure. Crie novos pontos de distribuição em nuvem utilizando implementações do Gestor de Recursos Azure e, em seguida, remova os pontos clássicos de distribuição da nuvem.

### <a name="hierarchy-design"></a>Design hierárquio

Quando criar o ponto de distribuição da nuvem depende de qual os clientes precisam de aceder ao conteúdo. A partir da versão 1806, existem três tipos de pontos de distribuição em nuvem:  

- Implantação do Gestor de Recursos Azure: Crie este tipo num local primário ou no site da administração central.  

- Implantação clássica do serviço: Crie este tipo apenas num local primário.  

- O gateway de gestão de nuvem também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados e o custo exigidos dos VMs Azure. Para mais informações, consulte [Plan for cloud management gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!--1358651-->  

Para determinar se deve incluir pontos de distribuição em nuvem em grupos de fronteira, considere os seguintes comportamentos:  

- Os clientes baseados na Internet não dependem de grupos de fronteira. Só utilizam pontos de distribuição virados para a Internet ou pontos de distribuição na nuvem. Se está a usar apenas pontos de distribuição em nuvem para servir este tipo de clientes, então não precisa incluí-los em grupos de fronteira.  

- Se quer que os clientes da sua rede interna utilizem um ponto de distribuição em nuvem, então tem de estar no mesmo grupo de fronteira que os clientes. Os clientes priorizam os pontos de distribuição na nuvem no último da sua lista de fontes de conteúdo, porque há um custo associado ao download de conteúdos do Azure. Assim, um ponto de distribuição em nuvem é normalmente usado como uma fonte de recuo para clientes baseados em intranet. Se você quer um design em nuvem primeiro, então desenhe seus grupos de fronteira para satisfazer este requisito de negócio. Para mais informações, consulte [os grupos de fronteira configure](../../servers/deploy/configure/boundary-groups.md).  

Apesar de instalar pontos de distribuição em nuvem em regiões específicas do Azure, os clientes não estão cientes das regiões de Azure. Eles escolhem aleatoriamente um ponto de distribuição de nuvem. Se instalar pontos de distribuição em nuvem em várias regiões, e um cliente receber mais de um na lista de localização de conteúdos, o cliente pode não utilizar um ponto de distribuição na nuvem da mesma região do Azure.  

### <a name="backup-and-recovery"></a>Cópia de segurança e recuperação  

Quando utilizar um ponto de distribuição em nuvem na sua hierarquia, use as seguintes informações para o ajudar a planear a cópia de segurança e a recuperação:  

- Quando utiliza a tarefa de manutenção do Servidor do Servidor do Servidor do **Site de Backup,** o Gestor de Configuração inclui automaticamente as configurações para o ponto de distribuição da nuvem.  

- Volte e guarde uma cópia do certificado de autenticação do servidor. Se utilizar a implantação clássica do serviço em Azure, também faça o back up e guarde uma cópia do certificado de gestão Azure. Quando restaurar o site primário do Gestor de Configuração para um servidor diferente, tem de reimportar os certificados.  


## <a name="requirements"></a><a name="bkmk_requirements"></a>Requisitos

- Precisa de uma **subscrição Azure** para acolher o serviço.  

    - Um **administrador azure** precisa de participar na criação inicial de determinados componentes, dependendo do seu design. Esta persona não requer permissões no Diretor de Configuração.  

- O servidor do site requer **acesso à Internet** para implementar e gerir o serviço de nuvem.  

- Ao utilizar o método de implementação do Gestor de **Recursos Azure,** integre o Gestor de Configuração com [o Azure AD](../../servers/deploy/configure/azure-services-wizard.md) para gestão de **nuvem.** A descoberta do *utilizador* da AD Azure não é necessária.  

- Um certificado de **autenticação do servidor.** Para mais informações, consulte a secção [de Certificados](#bkmk_certs) abaixo.  

    - Para reduzir a complexidade, utilize um fornecedor de certificados públicos para o certificado de autenticação do servidor. Ao fazê-lo, também precisa de um **pseudónimo DNS CNAME** para os clientes resolverem o nome do serviço na nuvem.  

- Na versão 1810 ou mais anterior do Gestor de Configuração, se utilizar o método de implantação clássico do Azure, precisa de um certificado de **gestão Azure**. Para mais informações, consulte a secção [de Certificados](#bkmk_certs) abaixo.  

    > [!TIP]  
    > Começando pela versão 1806 do Gestor de Configuração, utilize o modelo de implementação do Gestor de **Recursos Azure.** Não requer este certificado de gestão.  
    >
    > O método de implantação clássico é depreciado a partir da versão 1810.  

- Defina a definição do cliente, **permita o acesso aos pontos**de distribuição na nuvem, ao **Sim** no grupo **Cloud Services.** Por predefinição, este valor está definido como **Não**.  

- Os dispositivos clientes requerem **conectividade de internet**, e devem usar o **IPv4**.  


## <a name="specifications"></a><a name="bkmk_spec"></a>Especificações

- O ponto de distribuição em nuvem suporta todas as versões do Windows listadas em [sistemas operativos suportados para clientes e dispositivos.](../configs/supported-operating-systems-for-clients-and-devices.md)  

- Um administrador distribui os seguintes tipos de conteúdos de software suportados:  
  - Aplicações
  - Pacote
  - Pacotes de upgrade de OS
  - Atualizações de software de terceiros  

    > [!Important]  
    > - Embora a consola Do Gestor de Configuração não bloqueie a distribuição de atualizações de software da Microsoft para um ponto de distribuição na nuvem, está a pagar custos do Azure para armazenar conteúdo que os clientes não usam. Os clientes baseados na Internet recebem sempre conteúdos de atualização de software da Microsoft a partir do serviço cloud microsoft Update. Não distribua as atualizações de software da Microsoft para um ponto de distribuição na nuvem.
    > - Ao utilizar um CMG para armazenamento de conteúdo, o conteúdo para atualizações de terceiros não será descarregado para os clientes se o conteúdo delta de Download quando a [definição](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) de cliente **disponível** estiver ativada. <!--6598587--> 

- A partir da versão 1806, configure um ponto de distribuição de puxar para usar um ponto de distribuição em nuvem como fonte. Para mais informações, consulte [sobre os pontos](use-a-pull-distribution-point.md#about-source-distribution-points)de distribuição de origem .<!--1321554-->  

### <a name="deployment-settings"></a>Definições da implementação

- **Descarregue os conteúdos localmente quando necessário pela sequência de tarefas em execução**. A partir da versão 1910, o motor de sequência de tarefas pode descarregar pacotes a pedido a partir de um CMG ativado por conteúdo ou um ponto de distribuição em nuvem. Esta alteração proporciona flexibilidade adicional com as implementações de upgrade do Windows 10 para dispositivos baseados na Internet.

- **Descarregue todos os conteúdos localmente antes**de iniciar a sequência de tarefas . Na versão 1906 e anterior do Configurmanager, outras opções, como **o descarregamento de conteúdos localmente quando necessários pela sequência** de tarefas de execução, não funcionam neste cenário. O motor de sequência de tarefas não pode descarregar conteúdo de uma fonte de nuvem. O cliente do Gestor de Configuração deve descarregar o conteúdo a partir da fonte cloud antes de iniciar a sequência de tarefas. Ainda pode utilizar esta opção na versão 1910, se necessário para satisfazer os seus requisitos.

- Um ponto de distribuição em nuvem não suporta implementações de pacotes com a opção de executar o programa a **partir do ponto de distribuição**. Utilize a opção de implementação para **descarregar conteúdo a partir do ponto de distribuição e executar localmente**.  

### <a name="limitations"></a>Limitações  

- Não é possível utilizar um ponto de distribuição em nuvem para pXE ou implementações multicastactivadas.  

- Um ponto de distribuição em nuvem não suporta aplicações de streaming App-V.  

- Não se pode [pré-encenar conteúdo](manage-network-bandwidth.md#BKMK_PrestagingContent) num ponto de distribuição em nuvem. O gestor de distribuição do site primário que gere o ponto de distribuição em nuvem transfere todos os conteúdos.  

- Não se pode configurar um ponto de distribuição em nuvem como um ponto de distribuição de puxar.  


## <a name="cost"></a><a name="bkmk_cost"></a>Custo

<!--501018-->
> [!IMPORTANT]  
> A seguinte informação sobre os custos destina-se apenas a estimativas. O seu ambiente pode ter outras variáveis que afetam o custo global da utilização de um ponto de distribuição em nuvem.  

O Gestor de Configuração inclui as seguintes opções para ajudar a controlar os custos e monitorizar o acesso aos dados:  

- Controle e monitorize a quantidade de conteúdo que armazena num serviço de nuvem. Para mais informações, consulte [monitor pontos](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor)de distribuição em nuvem .  

- Configure O Gestor de Configuração para alertá-lo quando os limiares para transferências de clientes cumprem ou excedem os limites mensais. Para mais informações, consulte [os alertas de limiar](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts)de transferência de dados .

- Para ajudar a reduzir o número de transferências de dados de pontos de distribuição na nuvem pelos clientes, utilize uma das seguintes tecnologias de cache peer:  
  - Cache de pares do Gestor de Configuração
  - Windows BranchCache
  - Otimização de Entrega do Windows 10  

    Para mais informações, consulte [conceitos fundamentais para a gestão de conteúdos.](fundamental-concepts-for-content-management.md)  

### <a name="components"></a>Componentes

Um ponto de distribuição em nuvem utiliza os seguintes componentes Azure, que incorrem em encargos para a conta de subscrição do Azure:  

> [!Tip]  
> A partir da versão 1806, o portal de gestão de nuvem também pode servir conteúdo aos clientes. Esta funcionalidade reduz o custo consolidando os VMs Azure. Para mais informações, consulte Custo para gateway de [gestão](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost)de nuvem .  

#### <a name="virtual-machine"></a>Máquina virtual

- O ponto de distribuição em nuvem utiliza o Azure Cloud Services como plataforma como serviço (PaaS). Este serviço utiliza máquinas virtuais (VMs) que incorrem em custos de computação.  

- Cada serviço de ponto de distribuição em nuvem utiliza dois VMs Standard A0.  

- Consulte a calculadora de [preços Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os custos potenciais.

    > [!NOTE]  
    > Os custos das máquinas virtuais variam por região.

#### <a name="outbound-data-transfer"></a>Transferência de dados de saída

- Quaisquer fluxos de dados para o Azure são gratuitos (ingressou ou upload). A distribuição de conteúdos do site para o ponto de distribuição da nuvem está a ser enviada para o Azure.  

- Os encargos baseiam-se em dados que fluem do Azure (saída ou download). Os fluxos de dados do ponto de distribuição em nuvem do Azure consistem no conteúdo do software que os clientes descarregam.  

- Para mais informações, consulte [monitor pontos](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor)de distribuição em nuvem .  

- Consulte os detalhes de preços da [largura de banda Azure](https://azure.microsoft.com/pricing/details/bandwidth/) para ajudar a determinar os custos potenciais. Os preços para a transferência de dados são nilutos. Quanto mais usas, menos pagas por gigabyte.  

#### <a name="content-storage"></a>Armazenamento de conteúdo

- Os clientes baseados na Internet obtêm conteúdo de atualização de software da Microsoft a partir do serviço de cloud Microsoft Update sem custos. Não distribua pacotes de implementação de atualizações de software com atualizações de software da Microsoft para um ponto de distribuição na nuvem. Caso contrário, incorrerá em custos de armazenamento de dados para conteúdos que os clientes nunca usam.  

- Os pontos de distribuição em nuvem utilizam o seguinte armazenamento padrão de blob dependendo do modelo de implementação:  

    - Uma implantação do Gestor de Recursos Azure utiliza armazenamento localmente redundante do Azure (LRS). Esta alteração reduz o custo da conta de armazenamento. A implantação clássica não estava a usar as características adicionais do GRS. Para mais informações, consulte [o armazenamento localmente redundante.](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs)  

    - Uma implantação clássica com a versão 1810 do Gestor de Configuração ou anterior utiliza o armazenamento georedundant do Azure (GRS). Para mais informações, consulte [o armazenamento geo-redundante.](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs)  

#### <a name="other-costs"></a>Outros custos

- Cada serviço na nuvem tem um endereço IP dinâmico. Cada ponto de distribuição de nuvem distinto usa um novo endereço IP dinâmico. Adicionar VMs adicionais por serviço de nuvem não aumenta estes endereços.  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a>Portos e fluxo de dados

Existem dois fluxos de dados primários para o ponto de distribuição da nuvem:  

- O servidor do site conecta-se ao Azure para configurar o serviço de pontode distribuição em nuvem  

- Um cliente conecta-se ao ponto de distribuição na nuvem para descarregar conteúdo  

### <a name="site-server-to-azure"></a>Servidor do site para Azure

Não precisa abrir nenhum porto de entrada para a sua rede no local. O servidor do site inicia toda a comunicação com o Azure e o ponto de distribuição da nuvem para implementar, atualizar e gerir o serviço de cloud. O servidor do site precisa de criar ligações de saída para a nuvem da Microsoft. Esta ação equivale a instalar a função de sistema de sites de ponto de distribuição num site específico.  

### <a name="client-to-cloud-distribution-point"></a>Ponto de distribuição de cliente para nuvem

Não precisa abrir nenhum porto de entrada para a sua rede no local. Os clientes baseados na Internet comunicam diretamente com o serviço Azure. Os clientes da sua rede interna que utilizam um ponto de distribuição em nuvem precisam de se ligar à nuvem da Microsoft.

Para obter mais informações sobre a prioridade de localização do conteúdo e quando os clientes baseados em intranet usam um ponto de distribuição na nuvem, consulte a [prioridade da fonte de conteúdo](fundamental-concepts-for-content-management.md#content-source-priority).

Quando um cliente usa um ponto de distribuição na nuvem como localização de conteúdo:  

1. O ponto de gestão dá ao cliente um sinal de acesso, juntamente com a lista de fontes de conteúdo. Este token é válido por 24 horas, e dá ao cliente acesso ao ponto de distribuição da nuvem.  

2. O ponto de gestão responde ao pedido de localização do cliente com o **Serviço FQDN** do ponto de distribuição da nuvem. Esta propriedade é o mesmo que o nome comum do certificado de autenticação do servidor.  

    Se estiver a usar o seu nome de domínio, por exemplo, WallaceFalls.contoso.com, então o cliente primeiro tenta resolver este FQDN. Você precisa de um pseudónimo CNAME no DNS virado para a Internet do seu domínio para os clientes resolverem o nome do serviço Azure, por exemplo: WallaceFalls.cloudapp.net.  

3. O cliente em seguida resolve o nome do serviço Azure, por exemplo, WallaceFalls.cloudapp.net, para um endereço IP válido. Esta resposta deve ser tratada pelo DNS do Azure.  

4. O cliente liga-se ao ponto de distribuição da nuvem. A carga azure equilibra a ligação a uma das instâncias VM. O cliente autentica-se usando o sinal de acesso.  

5. O ponto de distribuição em nuvem autentica o sinal de acesso do cliente e, em seguida, dá ao cliente a localização exata do conteúdo no armazenamento Azure.  

6. Se o cliente confiar no certificado de autenticação do servidor do ponto de distribuição da nuvem, ele liga-se ao armazenamento Azure para descarregar o conteúdo.


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a>Desempenho e escala

<!--494872-->

Como em qualquer design de ponto de distribuição, considere os seguintes fatores:  

- Número de ligações simultâneas ao cliente
- O tamanho do conteúdo que os clientes descarregam
- O tempo permitido para satisfazer os seus requisitos de negócio

Dependendo do seu design de [topologia,](#bkmk_topology)se os clientes tiverem a opção de mais de um ponto de distribuição na nuvem para qualquer conteúdo, então eles naturalmente aleatoriamente através desses serviços de nuvem. Se distribuir apenas uma determinada peça de conteúdo para um único ponto de distribuição na nuvem, e um grande número de clientes tentar descarregar este conteúdo ao mesmo tempo, esta atividade coloca uma maior carga nesse único ponto de distribuição em nuvem. A adição de um ponto adicional de distribuição em nuvem também inclui um serviço de armazenamento Azure separado. Para obter mais informações sobre como o cliente comunica com os componentes do ponto de distribuição na nuvem e descarrega conteúdo, consulte [Portos e fluxo](#bkmk_dataflow)de dados .  

O ponto de distribuição da nuvem utiliza dois VMs Azure como a extremidade frontal do armazenamento Azure. Esta implementação padrão satisfaz a maioria das necessidades do cliente. Em algumas circunstâncias extremas, com um grande número de ligações de clientes simultâneos (por exemplo, 150.000 clientes), a capacidade de processamento dos VMs Azure não consegue acompanhar os pedidos dos clientes. Não é possível redimensionar os VMs Azure usados para o ponto de distribuição de nuvens. Embora não possa configurar o número de instâncias vM para o ponto de distribuição em nuvem no Gestor de Configuração, se necessário, reconfigurar o serviço de nuvem no portal Azure. Adicione manualmente mais instâncias vM, ou configure o serviço para escalar automaticamente.

> [!Important]  
> Quando atualiza o Gestor de Configuração, o site reimplementa o serviço de nuvem. Se reconfigurar manualmente o serviço de nuvem no portal Azure, o número de instâncias reinicia-se ao padrão de dois.  

O serviço de armazenamento Azure suporta 500 pedidos por segundo para um único ficheiro. Os testes de desempenho de um único ponto de distribuição em nuvem suportaram a distribuição de um único ficheiro de 100 MB a 50.000 clientes em 24 horas.<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a>Certificados  

Dependendo do design do ponto de distribuição em nuvem, precisa de um ou mais certificados digitais.  

### <a name="general-information"></a>Informações gerais

<!--SCCMDocs issue #779-->
Os certificados para pontos de distribuição na nuvem suportam as seguintes configurações:  

- Comprimento da chave de 4096 bits

- Certificados de versão 3. Para mais informações, consulte a visão geral dos [certificados de CNG](../network/cng-certificates-overview.md).  

- A partir da versão 1802, quando configurar o Windows com a seguinte política: **Criptografia do sistema: Utilize algoritmos compatíveis com FIPS para encriptação, hashing e assinatura**  

- A partir da versão 1802, suporte para TLS 1.2. Para mais informações, consulte [cryptographic controls de referência técnica](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities).  

### <a name="server-authentication-certificate"></a>Certificado de autenticação de servidor

*Este certificado é necessário para todas as implementações de pontos de distribuição em nuvem.*

Para mais informações, consulte o certificado de [autenticação do servidor CMG,](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth)e as seguintes subsecções, conforme necessário:  

- Certificado de raiz fidedigno da CMG aos clientes
- Certificado de autenticação do servidor emitido por fornecedor público
- Certificado de autenticação do servidor emitido da empresa PKI

O ponto de distribuição da nuvem utiliza este tipo de certificado da mesma forma que o gateway de gestão da nuvem. Os clientes também precisam confiar neste certificado. Para reduzir a complexidade, a Microsoft recomenda a utilização de um certificado emitido por um fornecedor público.

A menos que use um certificado wildcard, não reutilize o mesmo certificado. Cada instância do ponto de distribuição da nuvem e gateway de gestão de nuvem requer um certificado de autenticação exclusivo do servidor.

Para obter mais informações sobre a criação deste certificado a partir de um PKI, consulte [A implantação do certificado](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)de serviço para pontos de distribuição na nuvem .  

### <a name="azure-management-certificate"></a>Certificado de gestão Azure

*Este certificado é necessário para implementações clássicas de serviço. Não é necessário para implementações do Gestor de Recursos Azure.*

> [!Important]  
> Começando pela versão 1806 do Gestor de Configuração, utilize o modelo de implementação do Gestor de **Recursos Azure.** Não requer este certificado de gestão.  
>
> O método de implantação clássico é depreciado a partir da versão 1810.  
>
> Começando na versão 1902 do Gestor de Configuração, o Gestor de Recursos do Azure é o único mecanismo de implementação para novos casos do ponto de distribuição da nuvem. Este certificado não é exigido na versão 1902 do Gestor de Configuração.<!-- 3605704 -->

Se utilizar o método de implantação clássico do Azure com a versão 1810 ou mais anterior do Gestor de Configuração, precisa de um certificado de **gestão Azure**. Para mais informações, consulte a secção de certificados de [gestão Azure](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt) do artigo de certificados de gateway de gestão de nuvem. O servidor do site Do Gestor de Configuração utiliza este certificado para autenticar com o Azure para criar e gerir a implementação clássica.  

Para reduzir a complexidade, utilize o mesmo certificado de gestão Azure para todas as implementações clássicas de pontos de distribuição em nuvem e gateways de gestão de nuvem, em todas as subscrições do Azure e em todos os sites do Gestor de Configuração.


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a>Perguntas frequentes (FAQ)

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Um cliente precisa de um certificado para descarregar conteúdo de um ponto de distribuição na nuvem?

Não é necessário um certificado de autenticação de clientes. O cliente precisa confiar no certificado de autenticação do servidor utilizado pelo ponto de distribuição da nuvem. Se este certificado for emitido por um fornecedor de certificados públicos, a maioria dos dispositivos Windows já inclui certificados de raiz fidedignos para estes fornecedores. Se emitiu um certificado de autenticação do servidor do PKI da sua organização, então os seus clientes precisam confiar nos certificados emissores em toda a cadeia. Esta cadeia inclui a autoridade do certificado de raiz e quaisquer autoridades de certificados intermédios. Dependendo do seu design PKI, este certificado pode introduzir complexidade adicional na implantação do ponto de distribuição da nuvem. Para evitar esta complexidade, a Microsoft recomenda a utilização de um fornecedor de certificados públicos em que os seus clientes já confiem.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Os meus clientes no local podem usar um ponto de distribuição em nuvem?

Sim. Se quer que os clientes da sua rede interna utilizem um ponto de distribuição em nuvem, então tem de estar no mesmo grupo de fronteira que os clientes. Os clientes priorizam os pontos de distribuição na nuvem no último da sua lista de fontes de conteúdo, porque há um custo associado ao download de conteúdos do Azure. Assim, um ponto de distribuição em nuvem é normalmente usado como uma fonte de recuo para clientes baseados em intranet. Se você quer um design em nuvem primeiro, então desenhe os seus grupos de fronteira em conformidade. Para mais informações, consulte [os grupos de fronteira configure](../../servers/deploy/configure/boundary-groups.md).  

### <a name="do-i-need-azure-expressroute"></a>Preciso da Azure ExpressRoute?

[O Azure ExpressRoute](/azure/expressroute/expressroute-introduction) permite-lhe estender a sua rede no local para a nuvem da Microsoft. ExpressRoute, ou outras ligações de rede virtuais não são necessárias para o ponto de distribuição em nuvem do Gestor de Configuração.  

Se a sua organização utilizar o ExpressRoute, isole a subscrição Azure para o ponto de distribuição em nuvem a partir da subscrição que utiliza o ExpressRoute. Esta configuração garante que o ponto de distribuição da nuvem não está acidentalmente ligado desta forma.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Preciso manter as máquinas virtuais Azure?

Não é necessária manutenção. O design do ponto de distribuição em nuvem utiliza a plataforma Azure como serviço (PaaS). Utilizando a subscrição que fornece, o Gestor de Configuração cria os VMs necessários, armazenamento e networking. O Azure protege e atualiza as máquinas virtuais. Estes VMs não fazem parte do seu ambiente no local, como é o caso da infraestrutura como serviço (IaaS). O ponto de distribuição da nuvem é um PaaS que estende o ambiente do Seu Gestor de Configuração para a nuvem. Para mais informações, consulte [as vantagens de segurança de um modelo de serviço em nuvem PaaS](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>O ponto de distribuição da nuvem utiliza o Azure CDN?

A Rede de Entrega de Conteúdos Azure (CDN) é uma solução global para fornecer rapidamente conteúdo de alta largura de banda, apertando o conteúdo em nós físicos estrategicamente colocados em todo o mundo. Para mais informações, consulte [o que é Azure CDN?](https://docs.microsoft.com/azure/cdn/cdn-overview)

O ponto de distribuição de nuvem do Gestor de Configuração não suporta atualmente o Azure CDN.


## <a name="next-steps"></a>Próximos passos

[Instale pontos de distribuição em nuvem](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
