---
title: Nova versão 1802
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1802 do Gestor de Configuração.
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e7bc30c4350d96654a0f6a6ae548d63c2928e791
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904661"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Novidades na versão 1802 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1802 para o atual ramo do Gestor de Configuração está disponível como uma atualização na consola. Aplique esta atualização em sites que executam a versão 1702, 1706 ou 1710. <!-- baseline only statement: -->Ao instalar um novo site, também está disponível como uma versão de base.

Além de novas funcionalidades, esta versão também inclui alterações adicionais, tais como correções de bugs. Para mais informações, consulte [resumo das alterações no atual ramo do Gestor de Configuração, versão 1802](https://support.microsoft.com/help/4101375).

As seguintes atualizações adicionais para esta versão também estão disponíveis:
- [Rollup de atualização para o ramo atual do Gestor de Configuração, versão 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de base do 'Gestor de Configuração'.  
>
> Saiba mais sobre:    
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)  
> - [Instalação de atualizações nos sites](../../servers/manage/updates.md)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)

As seguintes secções fornecem detalhes sobre as alterações e novas capacidades na versão 1802 do Gestor de Configuração.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do local

### <a name="reassign-distribution-point"></a>Ponto de distribuição de reatribuir
<!-- 1306937 -->
Muitos clientes têm grandes infraestruturas de Gestor de Configuração, e estão a reduzir os locais primários ou secundários para simplificar o seu ambiente. Ainda precisam de reter pontos de distribuição em sucursais para servir conteúdo a clientes geridos. Estes pontos de distribuição contêm frequentemente vários terabytes ou mais de conteúdo. Este conteúdo é dispendioso em termos de tempo e largura de banda da rede para distribuir a estes servidores remotos. Esta funcionalidade permite-lhe reatribuir um ponto de distribuição a outro site primário sem redistribuir o conteúdo. Esta ação atualiza a atribuição do sistema do site enquanto persiste todo o conteúdo no servidor. Para mais informações, consulte [Reassign um ponto](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign)de distribuição .

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configure a otimização da entrega do Windows para utilizar grupos de limites do Gestor de Configuração
<!-- 1324696 -->
Utiliza grupos de limites do Gestor de Configuração para definir e regular a distribuição de conteúdos através da sua rede corporativa e para escritórios remotos. A [Otimização](/windows/deployment/update/waas-delivery-optimization) de Entrega do Windows é uma tecnologia baseada em nuvem, peer-to-peer para partilhar conteúdos entre dispositivos Windows 10. A partir desta versão, configure a Otimização da Entrega para utilizar os seus grupos de fronteira ao partilhar conteúdo entre os pares. Uma nova definição de cliente aplica o identificador de grupo de limites como o identificador do grupo de otimização de entrega no cliente. Quando o cliente comunica com o serviço de nuvem de otimização de entrega, utiliza este identificador para localizar os pares com o conteúdo pretendido. Para mais informações, consulte [conceitos fundamentais para a gestão de conteúdos.](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)

### <a name="support-for-windows-10-arm64-devices"></a>Suporte para dispositivos ARM64 do Windows 10
<!-- 1353704 -->
A partir desta versão, o cliente do Gestor de Configuração é suportado nos dispositivos ARM64 do Windows 10. As funcionalidades de gestão de clientes existentes devem funcionar com estes novos dispositivos. Por exemplo, inventário de hardware e software, atualizações de software e gestão de aplicações. Atualmente, a implantação do sistema operativo não é suportada. 

### <a name="improved-support-for-cng-certificates"></a>Melhor apoio aos certificados de GNC
<!-- 1357314 -->
Configuração Manager (ramo atual) versão 1710 suporta [Cryptografia: Certificados de Próxima Geração (CNG).](../network/cng-certificates-overview.md) A versão 1710 limita o suporte aos certificados de cliente em vários cenários. 

A partir desta versão, utilize certificados CNG para as seguintes funções de servidor ativadas por HTTPS:
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software
- Ponto de Migração de Estado  


### <a name="boundary-group-fallback-for-management-points"></a>Recuo do grupo de fronteirapara pontos de gestão
<!-- 1324594 -->
Configure relações de recuo para pontos de gestão entre [grupos de fronteiras](../../servers/deploy/configure/boundary-groups.md). Este comportamento proporciona um maior controlo para os pontos de gestão que os clientes usam. Para mais informações, consulte [os grupos de fronteira configure](../../servers/deploy/configure/boundary-groups.md#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Afinidade do site de ponto de distribuição de nuvem
<!--503719-->
Esta funcionalidade beneficia os clientes com uma hierarquia multi-site, geograficamente dispersa, utilizando pontos de distribuição em nuvem. Quando um cliente baseado na Internet procura conteúdo, anteriormente não havia ordem para a lista de pontos de distribuição na nuvem recebidos pelo cliente. Este comportamento pode resultar em clientes baseados na Internet que recebem conteúdo de pontos de distribuição geograficamente distantes da nuvem. O descarregamento de conteúdo de um servidor tão distante é tipicamente mais lento do que um servidor mais próximo.
 
Com a finidade do site de ponto de distribuição na nuvem, um cliente baseado na Internet recebe uma lista ordenada. Esta lista prioriza os pontos de distribuição em nuvem do site designado pelo cliente. Este comportamento permite ao administrador preservar a sua intenção de design para transferências de conteúdos a partir de recursos do site.
 

## <a name="management-insights"></a>Informações de gestão
<!-- 1353967 -->
Os conhecimentos de gestão no Gestor de Configuração fornecem informações sobre o estado atual do seu ambiente. A informação baseia-se na análise de dados da base de dados do site. As ideias ajudam-no a entender melhor o seu ambiente e a tomar medidas com base na perceção. Para mais detalhes consulte, [Management Insights](../../servers/manage/management-insights.md)

No Gestor de Configuração 1802, estão disponíveis as seguintes informações:
- Aplicações:
    - Aplicações sem implementações
- Serviços de Nuvem: <!--1356412-->
    - Avaliar a prontidão de cogestão 
    - Ative os seus dispositivos com direção ativa híbrida Azure
    - Modernizar a sua identidade e infraestrutura de acesso
    -  Atualize os seus clientes para o Windows 10, versão 1709 ou superior 
- Coleções:
    - Coleções Vazias
- Gestão Simplificada:  <!--1355148-->
    - Versões de clientes desatualizadas  
- Centro de Software: 
    - Utilizadores diretos para o Centro de Software em vez de Catálogo de Aplicações  
    - Use a nova versão do Software Center 
- Windows 10: <!--1357421-->
    - Configure a chave de telemetria do Windows e a chave de id comercial 
    - Conecte o Gestor de Configuração à Prontidão de Upgrade 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Gestão de clientes

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Suporte de gateway de gestão de nuvem para Gestor de Recursos Azure
<!-- 1324735 -->
Ao criar uma instância do gateway de [gestão](../../clients/manage/cmg/plan-cloud-management-gateway.md) da nuvem (CMG), o assistente oferece agora a opção de criar uma implementação do Gestor de **Recursos Azure**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma entidade única, chamada grupo de [recursos.](/azure/azure-resource-manager/resource-group-overview#resource-groups) Ao implantar a CMG com o Azure Resource Manager, o site utiliza o Azure Ative Directory (Azure AD) para autenticar e criar os recursos em nuvem necessários. Esta implantação modernizada não requer o clássico certificado de gestão Azure. Para mais informações, consulte o [design de topologia CMG.](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)

> [!IMPORTANT]
> Esta capacidade não permite suporte para fornecedores de serviços de nuvem Azure (CSP). A implantação da CMG com o Azure Resource Manager continua a utilizar o clássico serviço de cloud, que o CSP não suporta. Para mais informações, consulte [os serviços Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Melhorias na porta de entrada de gestão de nuvem  

- A partir desta versão, o portal de **gestão** da nuvem já não é uma funcionalidade de pré-lançamento.  

- A documentação da funcionalidade é revista e melhorada. Para obter mais informações, veja os seguintes artigos:
    - [Plano para o gateway de gestão de nuvem](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [Tamanho do gateway de gestão da nuvem e números de escala](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [Segurança e privacidade para o gateway de gestão na cloud](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [Perguntas frequentes sobre o gateway de gestão de nuvens](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [Certificados para o gateway de gestão na cloud](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [Configurar o gateway de gestão na cloud](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Configure o inventário de hardware para recolher cordas maiores que 255 caracteres
<!-- 1357389 -->
Pode configurar o comprimento das cordas para ser superior a 255 caracteres para propriedades de inventário de hardware. Esta alteração aplica-se apenas a classes recém-adicionadas e a propriedades de inventário de hardware que não são chaves. Para mais detalhes, consulte o artigo de inventário de [hardware Extend.](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255) 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Anúncio de depreciação para apoio ao cliente Linux e Unix
 <!--510139-->
A Microsoft pretende deprecer o suporte ao cliente Linux e UNIX no Gestor de Configuração daqui a cerca de um ano, de modo a que os clientes não sejam incluídos na versão 1902 no início do calendário de 2019. O lançamento do Gestor de Configuração 1810, no final do calendário de 2018, será o último lançamento a incluir os clientes Linux e UNIX, e serão suportados para o ciclo de vida completo do Gestor de Configuração 1810. Após o Gestor de Configuração 1810, os clientes devem considerar a Microsoft Azure Management para gerir os servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

### <a name="surface-device-dashboard"></a>Dashboard de dispositivos Surface
<!--1355788-->
O dashboard do dispositivo Surface fornece informações sobre os dispositivos Surface encontrados no seu ambiente. Na consola, vá a Dispositivos de Superfície **de Monitorização**  >  **Surface Devices**. Pode ver os itens:
- Por cento das superfícies
- Por cento dos modelos Surface
- As cinco melhores versões de firmware

Para mais detalhes, consulte o artigo do [Painel de Superfície.](../../clients/manage/surface-device-dashboard.md)

### <a name="change-in-the-configuration-manager-client-install"></a>Alterar a instalação do cliente do Gestor de Configuração
<!--1356195-->
A partir desta versão, a Silverlight já não está instalada nos dispositivos do cliente automaticamente. Para mais informações, consulte [pré-requisitos para a implementação](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies) de clientes para computadores Windows

## <a name="co-management"></a>Cogestão

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Carga de trabalho de proteção de pontofinal de transição para Intune usando cogestão
<!-- 1357365 -->
 A carga de trabalho de proteção de pontofinal pode ser transitada para Intune após permitir a cogestão. Para fazer a transição da carga de trabalho de proteção de pontofinal, vá para a página de propriedades de cogestão e mova a barra de slider de Configuração Manager para **Pilot** ou **All**. Para mais detalhes sobre as cargas de trabalho, consulte a [cogestão de cargas de trabalho.](../../../comanage/workloads.md) Para obter mais informações sobre cogestão, consulte [co-management para dispositivos Windows 10](../../../comanage/overview.md).
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Painel de cogestão em Gestor de Configuração
<!--1356648-->
A partir deste lançamento, pode ver um dashboard com informações sobre cogestão. O painel ajuda-o a rever máquinas cogeridas no seu ambiente. Os gráficos podem ajudar a identificar dispositivos que possam precisar de atenção. Para mais detalhes, consulte o artigo do [painel de cogestão.](../../../comanage/how-to-monitor.md#co-management-dashboard) 


## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="microsoft-edge-browser-policies"></a>Políticas de navegador Microsoft Edge
<!-- 1357310 -->
Para os clientes que utilizam o navegador Web [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) nos clientes do Windows 10, crie uma política de definições de conformidade do Gestor de Configuração para configurar várias definições do Microsoft Edge. Para mais informações, consulte [Create Microsoft Edge perfil de navegador](../../../compliance/deploy-use/browser-profiles.md). 



## <a name="application-management"></a>Gestão de Aplicações

### <a name="allow-user-interaction-when-installing-an-application"></a>Permitir a interação do utilizador ao instalar uma aplicação
<!-- 1356976 -->
Permitir que um utilizador final interaja com uma instalação de aplicação durante o funcionamento da sequência de tarefas. Por exemplo, executar um processo de configuração que indique o utilizador final para várias opções. Alguns instaladores de aplicações não podem silenciar as solicitações do utilizador, ou o processo de instalação pode exigir valores de configuração específicos apenas conhecidos do utilizador. Esta funcionalidade permite-lhe lidar com estes cenários de instalação. Para mais informações, consulte [Especifique as opções](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux)de experiência do utilizador para o tipo de implementação .

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Não atualize automaticamente aplicações supersed
<!-- 1351266 -->
Configure uma implementação de aplicação para não atualizar automaticamente qualquer versão supersed. Agora, ao criar a implementação, na página de Definições de **Implementação** do **Assistente de Software de Implementação,** para a instalação **disponível,** pode ativar ou desativar a opção de **atualizar automaticamente quaisquer versões supersed desta aplicação.** Para mais informações, consulte as definições de [implementação .](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)

### <a name="approve-application-requests-for-users-per-device"></a>Aprovar pedidos de pedido para utilizadores por dispositivo
<!-- 1357015 -->
A partir desta versão, quando um utilizador solicita uma aplicação que requer aprovação, o nome do dispositivo específico é agora uma parte do pedido. Se o administrador aprovar o pedido, o utilizador só poderá instalar a aplicação nesse dispositivo. O utilizador deve submeter outro pedido para instalar a aplicação noutro dispositivo. Para mais informações, consulte as definições de [implementação .](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)

 > [!Note]  
 > Esta é uma característica opcional. Para mais informações, consulte [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).  


### <a name="run-scripts-improvements"></a>Executar melhorias nos scripts 
<!-- 1236459 -->
 A partir deste lançamento, **o Run Scripts** já não é uma funcionalidade de pré-lançamento. A saída do script volta agora usando a formatação JSON. Para mais informações, consulte [Criar e executar scripts PowerShell a partir da consola Do Gestor de Configuração](../../../apps/deploy-use/create-deploy-scripts.md).


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequência de tarefas de upgrade do Windows 10 no local através do gateway de gestão de nuvem
<!-- 1357149 -->
A sequência [de tarefas de upgrade do](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) Windows 10 no local suporta agora a implementação de clientes baseados na Internet geridos através do portal de [gestão](../../clients/manage/cmg/plan-cloud-management-gateway.md)de nuvem . Esta capacidade permite que os utilizadores remotos atualizem mais facilmente para o Windows 10 sem precisarem de se conectar à rede corporativa. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](../../../osd/deploy-use/deploy-a-task-sequence.md).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhorias na sequência de tarefas de upgrade do Windows 10
<!-- 1357425 -->
O modelo de sequência de tarefas padrão para a atualização do Windows 10 inclui agora grupos adicionais com ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que estão a atualizar com sucesso dispositivos para o Windows 10. Para mais informações, consulte [criar uma sequência de tarefas para atualizar um OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Melhorias na implementação do sistema operativo
Esta versão inclui as seguintes melhorias na implementação do sistema operativo:
- No Windows PE, ao lançar cmtrace.exe, já não é solicitado a escolher se faz deste programa o visualizador predefinido para ficheiros de registo. <!-- SMS 500897 -->
- Adicione imagens de boot ao passo de sequência de tarefas do [pacote de transferência.](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent)
- Melhorias na etapa da sequência de tarefas de [execução:](../../../osd/understand/task-sequence-steps.md#child-task-sequence) <!-- 1261338 -->   
  - Suporte para todos os cenários de implementação do sistema operativo a partir do Software Center, PXE e meios de comunicação.
  - Melhorias nas ações de consola, tais como cópia, importação, exportação e aviso durante a eliminação do objeto.
  - Suporte para o assistente de ficheiro de [conteúdo pré-encenado.](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)
  - Integração com verificação de implantação. Para obter mais informações, consulte [as implementações da sequência de tarefas de alto risco](../../../osd/deploy-use/deploy-a-task-sequence.md). 
  - O passo da sequência de tarefas de execução pode agora ser usado em vários níveis de sequências de tarefas, e não apenas numa única relação pai-filho. As relações a vários níveis aumentam a complexidade, por isso, use com cuidado. Estas relações ainda são verificadas para referências circulares.

### <a name="deployment-templates-for-task-sequences"></a>Modelos de implementação para sequências de tarefas
<!-- 1357391 -->
O [assistente de implementação para sequências](../../../osd/deploy-use/deploy-a-task-sequence.md) de tarefas pode agora criar um modelo de implementação. O modelo de implementação pode ser guardado e aplicado a uma sequência de tarefas existente ou nova para criar uma implementação. 

### <a name="phased-deployments-for-task-sequences"></a>Implementações faseadas para sequências de tarefas
<!--1356837-->
 As implementações faseadas são uma [função de pré-lançamento](../../servers/manage/pre-release-features.md). As implementações faseadas automatizam um lançamento coordenado e sequenciado de uma sequência de tarefas em várias coleções. Pode [criar implementações faseadas](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) com o padrão de duas fases ou configurar manualmente várias fases. A implantação faseada das sequências de tarefas não suporta a instalação de PXE ou de suporte.




## <a name="software-center"></a>Centro de Software

### <a name="install-multiple-applications-in-software-center"></a>Instalar várias aplicações no Centro de Software
<!-- 1357126 -->
Se um utilizador final ou técnico de desktop precisar de instalar várias aplicações num dispositivo, o Software Center suporta agora a instalação de várias aplicações selecionadas. Este comportamento permite ao utilizador ser mais eficiente enquanto não espera que uma instalação termine antes de iniciar a seguinte. Para mais informações, consulte [Instalar várias aplicações](../../understand/software-center.md#install-multiple-applications) no novo guia de utilizadores do Centro de Software.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Utilize o Centro de Software para navegar e instalar aplicações disponíveis pelo utilizador em dispositivos ligados ao Azure AD
<!-- 1322613 -->
Se implementar aplicações como disponível para os utilizadores, elas podem agora navegar e instalá-las através do Software Center nos dispositivos Azure Ative Directory (Azure AD). Para mais informações, consulte [implementar aplicações disponíveis pelo utilizador em dispositivos ligados ao Azure AD](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Ocultar aplicações instaladas no Centro de Software
<!--1357592-->
As aplicações instaladas podem agora ser ocultadas no Centro de Software. As aplicações que já estão instaladas deixarão de aparecer no separador Aplicações quando esta opção estiver ativada nas definições do cliente. Esta opção é definida como predefinição quando instala ou atualiza para O Gestor de Configuração 1802.  As aplicações instaladas ainda estão disponíveis para revisão sob o separador de estado de instalação. [Ocultar as aplicações instaladas no Software Center](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled) tem detalhes adicionais.   

### <a name="hide-unapproved-applications-in-software-center"></a>Ocultar aplicações não aprovadas no Centro de Software
 <!--1355146-->
Quando esta opção de definição de cliente está ativada, as aplicações disponíveis do utilizador que requerem aprovação estão escondidas no Software Center.  [Ocultar aplicações não aprovadas no Software Center](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved) tem detalhes adicionais.  

### <a name="software-center-shows-user-additional-compliance-information"></a>O Centro de Software mostra informações adicionais sobre conformidade do utilizador
<!-- 1235616 -->
 Ao utilizar o estatuto de Attestation de Saúde do Dispositivo como regra de conformidade para o acesso condicional aos recursos da empresa, o Software Center mostra agora ao utilizador a definição de Atestado de Saúde do Dispositivo que não está em conformidade.


 ## <a name="software-updates"></a>Atualizações de software 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Agende a avaliação automática da regra de implantação para ser compensada a partir de um dia base. 
<!--1357133-->
As regras de implantação automática podem ser programadas para avaliar a compensação de um dia base. Ou seja, se o patch terça-feira realmente cair na quarta-feira para você, o calendário de avaliação pode ser definido para a segunda terça-feira do mês compensado por um dia. Para mais detalhes, consulte [A implementação automática](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule)de atualizações de software . 



## <a name="reporting"></a>Relatórios

### <a name="report-for-default-browser-counts"></a>Relatório para contagem de navegador padrão
<!-- 1357830 -->
Agora há um novo relatório para mostrar a contagem de clientes com um navegador web específico como o padrão do Windows. Consulte o relatório de contagem de **navegador predefinido** no grupo de relatórios **Software - Empresas e Produtos.** Para mais informações, consulte a [Lista de Relatórios](../../servers/manage/list-of-reports.md#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Relatório sobre informações do dispositivo Do Mépiloto Windows
<!-- 1351442 -->
O Windows Autopilot é uma solução para o embarque e configuração de novos dispositivos Windows 10 de uma forma moderna. Para mais informações, consulte uma [visão geral do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Um dos métodos de registo de dispositivos existentes com o Windows Autopilot é fazer o upload de informações do dispositivo para a Microsoft Store para negócios e educação. Estas informações incluem o número de série do dispositivo, identificador de produto Windows e um identificador de hardware. Utilize o Gestor de Configuração para recolher e reportar as informações deste dispositivo com o novo relatório, **Windows Autopilot Device Information**, no nó de **Hardware - Relatórios Gerais.** Para mais informações, consulte [Como preparar dispositivos baseados na Internet para cogestão](../../../comanage/how-to-prepare-Win10.md#windows-autopilot) na preparação para a cogestão.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Relatório sobre detalhes de manutenção do Windows 10 para uma coleção específica
<!--1357653-->
Os detalhes de **manutenção do Windows 10 para um** relatório de recolha específico mostram informações gerais sobre a manutenção do Windows 10 para uma recolha específica. Este relatório mostra o Id de Recursos, o nome NetBIOS, o nome OS, o nome de lançamento do OS, a construção, a sucursal de OS e o estado de manutenção dos dispositivos Windows 10. Para mais informações, consulte a [Lista de Relatórios](../../servers/manage/list-of-reports.md#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Proteger dispositivos

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Melhorias nas políticas do Gestor de Configuração para o Windows Defender Exploit Guard
<!-- 1356220 -->
Foram adicionadas definições de política adicionais para os componentes de acesso à [pasta Attack Surface](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR) Reduction e [Controlled](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA) foram adicionadas no Gestor de Configuração para o Windows Defender [Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Novas definições de interação do anfitrião para o Windows Defender Application Guard
<!-- 1356256 -->
Para a versão 1709 do Windows 10 e dispositivos posteriores, existem duas novas definições de interação para o [Windows Defender Application Guard:](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS) 
- Os websites podem ter acesso ao processador de gráficos virtuais do anfitrião. 
- Os ficheiros descarregados no interior do contentor podem ser persistidos no hospedeiro. 




## <a name="configuration-manager-console"></a>Consola do Configuration Manager

### <a name="improvements-to-the-configuration-manager-console"></a>Melhorias na consola do Gestor de Configuração 
Esta versão inclui as seguintes melhorias na consola Do Gestor de Configuração.
- As listas de dispositivos em Ativos e Compliance, Dispositivos, apresentam agora o utilizador principal por defeito. Esta coluna apenas aparece no nó dos Dispositivos. A última sessão registada no utilizador também pode ser adicionada como uma coluna opcional.<!-- 1357280 --> Ative as definições do cliente de [afinidade](../../clients/deploy/about-client-settings.md#user-and-device-affinity) do utilizador e do dispositivo para o site associar um utilizador primário a um dispositivo.
- Se uma coleção é membro de outra coleção e é renomeada, então o novo nome é atualizado de acordo com as regras de adesão.<!--1357282--> 
- Ao utilizar o controlo remoto de um cliente com vários monitores em diferentes escalas de DPI, o cursor de rato agora mapeia corretamente entre eles. <!--433170-->
- O painel de instrumentos de Gestão de [Clientes do Office 365](../../../sum/deploy-use/office-365-dashboard.md) apresenta uma lista de dispositivos relevantes quando são selecionadas secções de gráficos. <!--1357281 --> 



## <a name="next-steps"></a>Passos Seguintes
Quando estiver pronto para instalar esta versão, consulte [Atualizações para 'Gestor](../../servers/manage/updates.md)de Configuração'.
