---
title: Novidades na versão 1806
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1806 do ramo atual do Gestor de Configuração.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 295940337f191b791d8c7a86de4003466213df6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719317"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Novidades na versão 1806 do gerente de configuração atual

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1806 para o atual ramo do Gestor de Configuração está disponível como uma atualização na consola. Aplique esta atualização em sites que executam a versão 1706, 1710 ou 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Reveja sempre a mais recente lista de verificação para instalar esta atualização. Para mais informações, consulte a Lista de [Verificação para instalar a atualização 1806](../../servers/manage/checklist-for-installing-update-1806.md). Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

As seguintes secções fornecem detalhes sobre as alterações e novas funcionalidades na versão 1806 do ramo atual do Gestor de Configuração.  



## <a name="deprecated-features-and-operating-systems"></a>Funcionalidades e sistemas operativos degradados

Saiba mais sobre as alterações de suporte antes de serem implementadas em [itens removidos e depreciados](deprecated/removed-and-deprecated.md).

A partir de 14 de agosto de 2018, a funcionalidade de gestão de dispositivos móveis híbridos é depreciada. Para mais informações, veja [o que aconteceu ao MDM híbrido.](../../../mdm/understand/what-happened-to-hybrid.md)<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Infraestrutura do local

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
O Gestor de Configuração sempre forneceu uma grande loja centralizada de dados do dispositivo, que os clientes usam para fins de reporte. O site normalmente recolhe estes dados semanalmente. A CMPivot é um novo utilitário na consola que agora fornece acesso ao estado real dos dispositivos no seu ambiente. Executa imediatamente uma consulta em todos os dispositivos atualmente conectados na recolha do alvo e devolve os resultados. Em seguida, pode filtrar e agrupar estes dados na ferramenta. Ao fornecer dados em tempo real de clientes online, pode responder mais rapidamente a questões de negócios, resolver problemas e responder a incidentes de segurança. 

Para mais informações, consulte [CMPivot](../../servers/manage/cmpivot.md).  


### <a name="site-server-high-availability"></a>Elevada disponibilidade do servidor do site
<!--1128774-->
Uma elevada disponibilidade para uma função de servidor de site primário autónomo é uma solução baseada em Configuração Manager para instalar um servidor de site adicional em modo passivo. O servidor do site em modo passivo é além do servidor do site existente que está em modo ativo. Um servidor de site em modo passivo está disponível para uso imediato, quando necessário. 

Para obter mais informações, veja os artigos seguintes: 
- [Elevada disponibilidade do servidor do site](../../servers/deploy/configure/site-server-high-availability.md) 
- [Flowchart - Configurar um servidor de site em modo passivo](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [Fluxograma – Promover o servidor do site (planeado)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [Fluxograma – Promover o servidor do site (não planeado)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### <a name="improvements-to-management-insights"></a>Melhorias nos conhecimentos de gestão
Esta versão inclui as seguintes melhorias aos conhecimentos de gestão:  

- Alguns conhecimentos de gestão têm agora a opção de tomar uma ação. Esta ação está a navegar para o nó associado na consola, ou a mostrar uma visão filtrada e baseada em consultas.<!--1357930-->  

- Um novo grupo de Manutenção Proativa está disponível com seis novas regras, que ajudam a destacar potenciais problemas de configuração para evitar através da manutenção regular.<!--1352184-->  

Para mais informações, consulte [a Management insights](../../servers/manage/management-insights.md).


### <a name="configuration-manager-tools"></a>Ferramentas do Configuration Manager
<!--1357145-->
O servidor do Gestor de Configuração e as ferramentas do cliente estão agora incluídos no servidor. Encontre-os `CD.Latest\SMSSETUP\Tools` na pasta no servidor do site. Não é necessária mais nenhuma instalação. 

Para mais informações, consulte [as ferramentas do Gestor de Configuração.](../../support/tools.md)


### <a name="exclude-active-directory-containers-from-discovery"></a>Excluir recipientes de Diretório Ativo da descoberta
<!--1358143-->
Para reduzir o número de objetos descobertos, exclua recipientes específicos da descoberta do sistema De Diretório. 

Para mais informações, consulte [Configure Ative Directory System Discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd).



## <a name="content-management"></a>Gestão de conteúdos

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Configure uma biblioteca de conteúdos remotos para o servidor do site
<!--1357525-->
Para configurar a elevada disponibilidade do servidor do site ou para libertar o espaço de disco rígido na sua administração central ou servidores de site primários, realoque a biblioteca de conteúdos para outro local de armazenamento. Mova a biblioteca de conteúdos para outra unidade no servidor do site, um servidor separado ou discos tolerantes a falhas numa rede de área de armazenamento (SAN). 

Para obter mais informações, veja os artigos seguintes: 
- [A biblioteca de conteúdos](../hierarchy/the-content-library.md)
- [Fluxograma – Gerir a biblioteca de conteúdos](../hierarchy/manage-content-library-flowchart.md)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Suporte de ponto de distribuição em nuvem para Gestor de Recursos Azure
<!--1322209-->
Ao criar um ponto de distribuição em nuvem, o assistente oferece agora a opção de criar uma implementação do Gestor de **Recursos Azure**. O Azure Resource Manager é uma plataforma moderna para gerir todos os recursos de solução como uma entidade única, chamada grupo de recursos. Ao implantar um ponto de distribuição em nuvem com o Azure Resource Manager, o site utiliza o Diretório Ativo Azure para autenticar e criar os recursos em nuvem necessários. Esta implantação modernizada não requer o clássico certificado de gestão Azure. 

A documentação da funcionalidade para o ponto de distribuição da nuvem também é revista e melhorada. Para obter mais informações, veja os artigos seguintes:
- [Use um ponto de distribuição de nuvem](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [Instale um ponto de distribuição em nuvem](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Pontos de distribuição suportam pontos de distribuição em nuvem como fonte  
<!--1321554-->
Muitos clientes usam pontos de distribuição de puxar em agências remotas ou sucursais, que descarregam conteúdo de um ponto de distribuição de fonte através do WAN. Se os seus escritórios remotos tiverem uma melhor ligação à internet ou para reduzir a carga nas suas ligações WAN, pode agora utilizar um ponto de distribuição em nuvem no Microsoft Azure como fonte. Quando adiciona uma fonte no separador **Pull Distribution Point** das propriedades do ponto de distribuição, qualquer ponto de distribuição em nuvem no site está agora listado como um ponto de distribuição disponível. O comportamento de ambas as funções do sistema do site continua a ser o mesmo de outra forma. 

Para mais informações, consulte [Utilize pontos de distribuição de puxar](../hierarchy/use-a-pull-distribution-point.md).


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Ativar pontos de distribuição para usar o controlo de congestionamento da rede
<!--1358112-->
O Windows Low Delay Background Transport (LEDBAT) é uma funcionalidade do Windows Server para ajudar a gerir as transferências de rede de fundo. Para os pontos de distribuição em versões suportadas do Windows Server, permita uma opção para ajudar a ajustar o tráfego de rede. Os clientes só usam largura de banda da rede quando estão disponíveis. 

Para mais informações, consulte [o Windows LEDBAT](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Suporte parcial de descarregamento na cache de pares de clientes para reduzir a utilização de WAN
<!--1357346-->
As fontes de cache dos clientes podem agora dividir o conteúdo em partes. Estas peças minimizam a transferência de rede para reduzir a utilização de WAN. O ponto de gestão fornece um rastreio mais detalhado das partes de conteúdo. Tenta eliminar mais do que um download do mesmo conteúdo por grupo de fronteiras. 

Para mais informações, consulte [suporte para download parcial](../hierarchy/client-peer-cache.md#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Opções de grupo de limites para downloads de pares
<!--1356193-->
Os grupos de fronteira saem agora de definições adicionais para lhe dar mais controlo sobre a distribuição de conteúdos no seu ambiente. Esta versão adiciona as seguintes opções:  

- **Permitir downloads de pares neste grupo de fronteiras**: O ponto de gestão fornece aos clientes uma lista de locais de conteúdo que inclui fontes de pares. Esta definição também afeta a aplicação de IDs do Grupo para otimização de entrega.  

- Durante os **downloads de pares, utilize apenas pares dentro da mesma sub-rede**: O ponto de gestão inclui apenas na lista de dados de conteúdo fontes de pares que se encontram na mesma sub-rede que o cliente.  

Para mais informações, consulte as opções do [grupo Boundary para downloads de pares](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="improvement-to-peer-cache-source-location-status"></a>Melhoria do estado de localização da fonte de cache peer
<!--SCCMDocs issue 850-->
O Gestor de Configuração é mais eficiente para determinar se uma fonte de cache de pares percorreu outro local. Este comportamento garante que o ponto de gestão o oferece como fonte de conteúdo para os clientes na nova localização e não na localização antiga. Se estiver a utilizar a funcionalidade de cache de pares com fontes de cache de pares de roaming, depois de atualizar o site para a versão 1806, também atualize todas as fontes de cache de pares para a versão mais recente do cliente. O ponto de gestão não inclui estas fontes de cache de pares na lista de locais de conteúdo até que sejam atualizados para pelo menos a versão 1806.

Para mais informações, consulte [Requisitos para cache de pares](../hierarchy/client-peer-cache.md#requirements).



<!-- ## Migration  -->



## <a name="client-management"></a>Gestão de clientes

### <a name="improvement-to-client-push-security"></a>Melhoria da segurança do impulso do cliente
<!--1358204-->
Ao utilizar o método de pressão do cliente para instalar o cliente Do Gestor de Configuração, o site pode agora exigir a autenticação mútua kerberos. Esta melhoria ajuda a garantir a comunicação entre o servidor e o cliente. 

Para mais informações, consulte [Como instalar clientes com pressão](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)do cliente .


### <a name="enhanced-http-site-system"></a><a name="bkmk_ehttp"></a>Sistema de site HTTP melhorado
<!--1356889,1358228-->
A utilização da comunicação HTTPS é recomendada para todos os caminhos de comunicação do Gestor de Configuração, mas pode ser um desafio para alguns clientes devido à sobrecarga de gestão de certificados PKI.

Esta versão inclui melhorias na forma como os clientes comunicam com os sistemas do site. Nas propriedades do site, separador de comunicação de **computador cliente,** selecione a opção para **HTTPS ou HTTP,** e, em seguida, ativar a nova opção de **utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP**. Esta funcionalidade é uma [funcionalidade de pré-lançamento.](../../servers/manage/pre-release-features.md)

Para mais informações, consulte [O HTTP Melhorado](../hierarchy/enhanced-http.md).


### <a name="azure-ad-device-identity"></a>Identidade do dispositivo Azure AD 
<!--1358460-->
Um dispositivo Azure [Azure AD filiado](/azure/active-directory/devices/concept-azure-ad-join) ou [híbrido azure](/azure/active-directory/devices/concept-azure-ad-join-hybrid) sem um utilizador Azure AD assinado pode comunicar com segurança com o seu site atribuído. A identidade do dispositivo baseado na nuvem é agora suficiente para autenticar com o CMG e o ponto de gestão.  

Para mais informações, consulte [O HTTP Melhorado](../hierarchy/enhanced-http.md).


### <a name="cmtrace-installed-with-client"></a>CMTrace instalado com cliente
<!--1357971-->
A ferramenta de visualização de log CMTrace é agora instalada automaticamente juntamente com o cliente do Gestor de Configuração. É adicionado ao diretório de instalação do `%WinDir%\ccm\cmtrace.exe`cliente, que por padrão é . 

Para mais informações, consulte [CMTrace](../../support/cmtrace.md).


### <a name="cloud-management-dashboard"></a>Painel de gestão de nuvem
<!--1358461-->
O novo painel de gestão de nuvem proporciona uma visão centralizada para o uso de gateway de gestão de nuvem (CMG). Quando o site está a bordo com a AD Azure, também exibe dados sobre utilizadores e dispositivos da nuvem.   

Esta funcionalidade também inclui o analisador de **ligação CMG** para verificação em tempo real para ajudar na resolução de problemas. O utilitário na consola verifica o estado atual do serviço e o canal de comunicação através do ponto de ligação CMG a quaisquer pontos de gestão que permitam o tráfego cmg. 

Para mais informações, consulte as seguintes secções do artigo da CMG do [Monitor:](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md)  
- [Painel de gestão de nuvem](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [Analisador de ligação](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>Melhorias na porta de entrada de gestão de nuvem

A versão 1806 inclui as seguintes melhorias ao gateway de gestão da nuvem (CMG):

#### <a name="simplified-client-bootstrap-command-line"></a>Linha de comando de botas de cliente simplificada
<!--1358215-->
Ao instalar o cliente Do Gestor de Configuração na internet através de um CMG, a linha de comando agora requer menos propriedades. Esta melhoria reduz o tamanho da linha de comando utilizada no Microsoft Intune quando se prepara para a cogestão. 

Para mais informações, consulte [Como preparar dispositivos baseados na Internet para cogestão](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

#### <a name="download-content-from-a-cmg"></a>Descarregue conteúdo de um CMG
<!--1358651-->
Anteriormente, tinha de implantar um ponto de distribuição em nuvem e CMG como funções separadas. Uma CMG pode agora também servir conteúdo aos clientes. Esta funcionalidade reduz os certificados e o custo exigidos dos VMs Azure. 

Para mais informações, consulte [Modificar um CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Certificado de raiz fidedigno não é necessário com Azure AD
<!--503899-->
Quando cria um CMG, já não é necessário fornecer um [certificado de raiz fidedigno](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) na página Definições. Este certificado não é necessário quando se utiliza o Azure Ative Directory (Azure AD) para autenticação do cliente, mas costumava ser exigido no assistente. Se estiver a utilizar certificados de autenticação de clientes PKI, então ainda deve adicionar um certificado de raiz fidedigno à CMG.



## <a name="co-management"></a>Cogestão

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Sync MDM política da Microsoft Intune para um dispositivo cogerido
<!--1357377-->
Quando muda uma carga de trabalho de cogestão, os dispositivos cogeridos sincronizam automaticamente a política de MDM da Microsoft Intune. Esta sincronização também acontece quando inicia a ação de Política de Computador de **Descarregamento** a partir de Notificações de Cliente na consola 'Gestor de Configuração'. 

Para mais informações, consulte Como mudar as cargas de [trabalho do Gestor de Configuração para Intune](../../../comanage/how-to-switch-workloads.md).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Transição de novas cargas de trabalho para Intune usando cogestão
As seguintes cargas de trabalho podem agora transitar de Configuração Manager para Intune após permitir a cogestão:  

- **Configuração do dispositivo**<!--1357903-->: Esta carga de trabalho permite-lhe utilizar o Intune para implementar as políticas de MDM, ao mesmo tempo que continua a utilizar o Gestor de Configuração para a implementação de aplicações.  

- **Office 365**<!--1357841-->: Os dispositivos não instalam as implementações do Office 365 do Diretor de Configuração.  

- **Aplicações móveis**<!--1357892-->: Quaisquer aplicações disponíveis implantadas a partir de Intune estão disponíveis no Portal da Empresa. As aplicações que implementa no 'Gestor de Configuração' estão disponíveis no Software Center. Esta funcionalidade é uma [funcionalidade de pré-lançamento.](../../servers/manage/pre-release-features.md)  

Para fazer a transição destas cargas de trabalho, vá à página de propriedades de cogestão e mova a barra de slider de carga de trabalho de Configuração Manager para **Pilot** ou **All**. 

Para mais informações, consulte [co-management para dispositivos Windows 10](../../../comanage/overview.md).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Apoio a várias hierarquias a um inquilino intune
<!--1357944-->
Alguns clientes têm várias hierarquias do Gestor de Configuração e querem consolidar-se no futuro com um único inquilino para o Azure Ative Directory e microsoft Intune. A cogestão agora suporta a ligação de mais de um ambiente de Gerente de Configuração ao mesmo inquilino Intune.

Para obter mais informações, consulte os [pré-requisitos de cogestão.](../../../comanage/overview.md#prerequisites)
 


## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configure as definições do SmartScreen do Windows Defender para o Microsoft Edge
<!--1353701-->
A política de definições de conformidade do navegador Microsoft Edge adiciona as seguintes três definições para o Windows Defender SmartScreen: 
- Permitir o SmartScreen
- Os utilizadores podem anular o pedido do SmartScreen para sites
- Os utilizadores podem anular o pedido do SmartScreen para ficheiros

Para mais informações, consulte [as definições](../../../compliance/deploy-use/browser-profiles.md)do Microsoft Edge .


### <a name="scap-extensions"></a>Extensões scap
<!--1357552-->
Converta o conteúdo do Protocolo de Automação de Conteúdo de Segurança (SCAP) para as linhas de base de definições de conformidade e gere relatórios SCAP utilizando uma extensão de consola. Esta funcionalidade também inclui um novo dashboard para visualizar a conformidade do cliente, bem como a conformidade da regra XCCDF. 





## <a name="application-management"></a>Gestão de aplicações

### <a name="phased-deployment-of-applications"></a>Implantação faseada de aplicações
<!--1358147-->
Criar uma implementação faseada para uma aplicação. As implementações faseadas permitem-lhe orquestrar um lançamento coordenado e sequenciado de software com base em critérios e grupos personalizáveis. Por exemplo, implemente a aplicação para uma coleção piloto e, em seguida, continue automaticamente o lançamento com base em critérios de sucesso. 

Para obter mais informações, veja os artigos seguintes:  

- [Criar uma implementação faseada](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gerir e monitorizar as implementações faseadas](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Disponibilize pacotes de aplicativos Windows para todos os utilizadores num dispositivo
<!--1358310-->
Disponibilize uma aplicação com um pacote de aplicações Windows para todos os utilizadores do dispositivo. Um exemplo comum deste cenário é fornecer uma aplicação da Microsoft Store for Business and Education, como Minecraft: Education Edition, a todos os dispositivos utilizados pelos alunos de uma escola. Anteriormente, o Gestor de Configuração apenas suportava a instalação destas aplicações por utilizador. Depois de iniciar sessão num novo dispositivo, um aluno teria de esperar para aceder a uma aplicação. Agora, quando a aplicação é aprovisionada para o dispositivo para todos os utilizadores, podem ser produtivas mais rapidamente. 

Para mais informações, consulte [Create Windows aplicações](../../../apps/get-started/creating-windows-applications.md#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integração de ferramentas de personalização de escritório com o Instalador office 365
<!--1358149-->
A Ferramenta de Personalização do Office está agora integrada com o Instalador office 365 na consola Do Gestor de Configuração. Ao criar uma implantação para o Office 365, configure dinamicamente as mais recentes definições de gestão do Office. A Microsoft atualiza a Ferramenta de Personalização do Office quando lançar novas construções do Office 365. Esta integração permite-lhe tirar partido de novas definições de gestão no Office 365 assim que estiverem disponíveis. 

Para mais informações, consulte o [Deploy Office 365 apps](../../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).


### <a name="support-for-new-windows-app-package-formats"></a>Suporte para novos formatos de pacotes de aplicativos Windows
<!--1357427-->
O Gestor de Configuração suporta agora a implementação de novos formatos de pacote de aplicações Do Windows 10 (.msix) e pacote de aplicações (.msixbundle). 

Para mais informações, consulte [Create Windows aplicações](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).


### <a name="uninstall-application-on-approval-revocation"></a>Desinstalar aplicação na revogação da aprovação
<!--1357891-->
O comportamento mudou quando revoga a aprovação de uma candidatura. Agora, quando nega o pedido para a aplicação, o cliente desinstala a aplicação a partir do dispositivo do utilizador. Este comportamento requer que ative a [funcionalidade opcional](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_options) Aprovar pedidos de **aplicação para utilizadores por dispositivo**. 

Para mais informações, consulte [aplicações de implementação](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).


### <a name="package-conversion-manager"></a>Gestor de Conversão de Pacotes 
<!--1357861-->
O Gestor de Conversão de Pacotes é agora uma ferramenta integrada que lhe permite converter pacotes legados em aplicações atuais do Gestor de Configuração. Depois pode utilizar funcionalidades de aplicações como dependências, regras de exigência e afinidade do dispositivo de utilização.

Para mais informações, consulte O Gestor de Conversão de [Pacotes](../../../apps/pcm/package-conversion-manager.md).



## <a name="os-deployment"></a>Implementação de SO

### <a name="improvements-to-phased-deployments"></a>Melhorias nas implementações faseadas

Esta versão inclui as seguintes melhorias nas implementações faseadas:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Criar uma implantação faseada com fases configuradas manualmente
<!--1358148-->
Para uma sequência de tarefas, configure manualmente as fases quando criar uma implementação faseada. Adicione até 10 fases adicionais a partir do separador **Fases** do assistente de implantação faseada. Ainda pode criar automaticamente uma implementação de duas fases padrão. 

Para mais informações, consulte [Criar uma implementação faseada com fases configuradas manualmente](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual).

#### <a name="phased-deployment-status"></a>Estado de implantação faseada
<!--1358577-->
As implementações faseadas têm agora uma experiência de monitorização nativa. A partir do nó de **implantação** no espaço de trabalho **de monitorização,** selecione uma implantação faseada e, em seguida, clique no Estado de **Implantação Faseada** na fita. 

Para obter mais informações, consulte [Gerir e monitorizar as implementações faseadas](../../../osd/deploy-use/manage-monitor-phased-deployments.md).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Lançamento gradual durante implantações faseadas
<!--1358578-->
Durante uma implantação faseada, o lançamento em cada fase pode agora acontecer gradualmente. Este comportamento ajuda a mitigar o risco de problemas de implementação, e diminui a carga na rede causada pela distribuição de conteúdos aos clientes. O site pode gradualmente disponibilizar o software dependendo da configuração para cada fase. Cada cliente numa fase tem um prazo em relação ao tempo que o software é disponibilizado. O intervalo de tempo entre o tempo disponível e o prazo é o mesmo para todos os clientes numa fase. 

Para mais informações, consulte [as definições de fase](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhorias na sequência de tarefas de upgrade do Windows 10
<!--1358500-->
O modelo de sequência de tarefas padrão para a atualização do Windows 10 inclui agora outro novo grupo com ações recomendadas para adicionar caso o processo de atualização falhe. Estas ações facilitam a resolução de problemas. Uma dessas ferramentas é o Windows [SetupDiag.](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) É uma ferramenta de diagnóstico autónoma para obter detalhes sobre o porquê de uma atualização do Windows 10 não ter sido bem sucedida. 

Para mais informações, consulte Criar uma sequência de [tarefas para atualizar um OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias nos pontos de distribuição ativados pelo PXE
<!--1357580-->
No separador **PXE** das propriedades do ponto de distribuição, verifique **Ativar um serviço de resposta PXE sem o Serviço**de Implementação do Windows . Esta nova opção permite um resposta PXE no ponto de distribuição, o que não requer Serviços de Implementação do Windows (WDS). Como o WDS não é necessário, o ponto de distribuição ativado pelo PXE pode ser um cliente ou servidor OS, incluindo o Windows Server Core. Este novo serviço de resposta PXE suporta o IPv6, e também aumenta a flexibilidade dos pontos de distribuição ativados pelo PXE em escritórios remotos. 

Para mais informações, consulte [o Ative PXE no ponto de distribuição](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Conta de acesso à rede não é necessária para alguns cenários
<!--1358278,1358279-->
A funcionalidade do sistema de [site Enhanced HTTP](#bkmk_ehttp) também remove algumas dependências da conta de acesso à rede. Quando permite que a nova opção de utilização de certificados gerados pelo Gestor de Configuração utilize os certificados gerados pelo Gestor de **Configuração para sistemas de site HTTP,** os seguintes cenários não requerem uma conta de acesso à rede para descarregar conteúdo a partir de um ponto de distribuição:  

- Sequências de tarefas que saem dos meios de arranque ou PXE
- Sequências de tarefas que correm do Centro de Software  

Estas sequências de tarefapodem ser para implementação de OS ou personalizadas. Também é suportado para computadores de grupo de trabalho.

Para obter mais informações, consulte as [sequências de tarefas e a conta de acesso à rede](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).


### <a name="other-improvements-to-os-deployment"></a>Outras melhorias na implantação do OS

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Máscara dados sensíveis armazenados em variáveis de sequência de tarefas
 <!--1358330-->
 Na etapa variável de sequência de **tarefas definida,** selecione a nova opção para **não exibir este valor**. 

 Para mais informações, consulte [definir variável de sequência](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)de tarefas . 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Nome do programa de máscara durante passo de comando executar de uma sequência de tarefa
 <!--1358493-->
 Para evitar que os dados potencialmente sensíveis sejam exibidos ou registados, configure a variável de sequência de tarefas **OSDDoNotLogCommand .**  

 Para obter mais informações, consulte variáveis de sequência de [tarefas](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand). 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Variável de sequência de tarefas para parâmetros DISM ao instalar condutores
 <!--516679/2840016-->
 Para especificar parâmetros adicionais da linha de comando para o DISM, utilize a nova variável de sequência de tarefas **OSDInstallDriversAdditionalOptions**. 

 Para obter mais informações, consulte variáveis de sequência de [tarefas](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions). 

#### <a name="option-to-use-full-disk-encryption"></a>Opção de usar encriptação completa do disco
 <!--SCCMDocs-pr issue 2671-->
 Tanto os passos **Enable BitLocker** como **os bitLocker de pré-disposição** incluem agora uma opção para utilizar a **encriptação completa do disco**. Por defeito, estes passos encriptam o espaço usado na unidade. Este comportamento padrão é recomendado, uma vez que é mais rápido e eficiente. 

 Para mais informações consulte [Enable BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker) e [BitLocker pré-provision .](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker) 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>O modo de provisionamento do cliente não está ativado com a compatibilidade de atualização do Windows 10
 <!--SCCMDocs-pr issue 2812-->
 Agora, quando ativa a opção de realizar a compatibilidade do **Windows Configuração sem iniciar a atualização,** o passo de sequência de tarefas do **Sistema Operativo** de Upgrade não coloca o cliente do Gestor de Configuração no modo de provisionamento.

 Para mais informações, consulte [Sistema Operativo de Upgrade](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).

#### <a name="revised-documentation-for-task-sequence-variables"></a>Documentação revista para variáveis de sequência de tarefas
Dois novos artigos estão agora disponíveis para compreender variáveis de sequência de tarefas:  

- [Como utilizar variáveis](../../../osd/understand/using-task-sequence-variables.md) de sequência de tarefas é um novo artigo que descreve os diferentes tipos de variáveis, métodos para definir as variáveis e como acessá-las.  

- [Variáveis](../../../osd/understand/task-sequence-variables.md) de sequência de tarefas é uma referência para todas as variáveis de sequência de tarefas disponíveis. Este artigo combina os artigos anteriores, que separavam variáveis incorporadas das variáveis de ação. 



## <a name="software-center"></a>Centro de Software

> [!Important]  
> Para aproveitar as novas funcionalidades do Gestor de Configuração, os clientes da primeira atualização para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.


### <a name="software-center-infrastructure-improvements"></a>Melhorias na infraestrutura do Software Center
<!--1358309-->
As funções de catálogo de aplicações já não são necessárias para exibir aplicações disponíveis pelo utilizador no Software Center. Esta alteração ajuda-o a reduzir a infraestrutura de servidores necessária para entregar aplicações aos utilizadores. O Software Center conta agora com o ponto de gestão para obter esta informação, o que ajuda a maiores ambientes a escalar melhor, atribuindo-os a [grupos de fronteira.](../../servers/deploy/configure/boundary-groups.md#management-points)

Para mais informações, consulte [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)  

> [!Note]  
> As funções de ponto de catálogo de catálogo de aplicações e ponto de serviço web já não são *necessárias* em 1806, mas ainda desempenham funções *suportadas.* 
> 
> A experiência do **utilizador Silverlight** para o ponto de site do catálogo de aplicações já não é suportada. Para mais informações, consulte [funcionalidades removidas e depreciadas](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especifique a visibilidade do link do site do catálogo de aplicações no Software Center
<!--1358214-->
Utilize as definições do cliente para controlar se o link para Abrir o site do Catálogo de **Aplicações** aparece no nó de estado de **instalação** do Software Center.  

Para mais informações, consulte [as definições do cliente do Software Center](../../clients/deploy/about-client-settings.md#software-center).

> [!Note]  
> A experiência do **utilizador Silverlight** para o ponto de site do catálogo de aplicações já não é suportada. Para mais informações, consulte [funcionalidades removidas e depreciadas](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Separador personalizado para página web no Centro de Software
<!--1358132-->
Utilize as definições do cliente para criar um separador personalizado para abrir uma página web no Software Center. Esta funcionalidade permite-lhe mostrar conteúdo aos seus utilizadores finais de forma consistente e fiável. A lista seguinte inclui alguns exemplos:  

- Contacte it: informações sobre como contactar o departamento de TI da sua organização  

- It Support Center: Ações de self-service de TI, tais como pesquisar uma base de conhecimento ou abrir um bilhete de apoio.  

- Documentação do utilizador final: artigos para utilizadores da sua organização sobre vários tópicos de TI, tais como a utilização de aplicações ou a atualização para o Windows 10.  

Para mais informações, consulte [as definições](../../clients/deploy/about-client-settings.md#software-center) do cliente do Software Center e o guia de utilizador do [Centro de Software](../../understand/software-center.md).


### <a name="maintenance-windows-in-software-center"></a>Janelas de manutenção no Centro de Software
<!--1358131-->
O Software Center apresenta agora a próxima janela de manutenção programada. No separador Estado de Instalação, altere a vista de All para Upcoming. Apresenta o intervalo de tempo e a lista de implementações que estão programadas. Se não houver futuras janelas de manutenção, a lista está em branco. 

Para mais informações, consulte [Como utilizar as janelas de manutenção](../../clients/manage/collections/use-maintenance-windows.md) e o guia de utilizador do Centro de [Software](../../understand/software-center.md).



## <a name="software-updates"></a>Atualizações de software

### <a name="third-party-software-updates"></a>Atualizações de software de terceiros
<!--1357605, 1352101, 1358714-->
As atualizações de software de terceiros permitem subscrever catálogos de parceiros na consola Do Gestor de Configuração e publicar as atualizações para a WSUS. Em seguida, pode implementar estas atualizações utilizando o processo de gestão de atualizações de software existente. 

Para mais informações, consulte [Permitir atualizações de terceiros](../../../sum/deploy-use/third-party-software-updates.md).


### <a name="deploy-software-updates-without-content"></a>Implementar atualizações de software sem conteúdo
<!--1357933-->
Implemente atualizações de software para dispositivos sem primeiro descarregar e distribuir conteúdo para pontos de distribuição. Esta funcionalidade é benéfica quando se lida com conteúdos de atualização extremamente grandes, ou quando sempre deseja que os clientes obtenha conteúdo do serviço cloud microsoft Update. Os clientes neste cenário também podem descarregar conteúdos de pares que já tenham os conteúdos necessários. O cliente do Gestor de Configuração continua a gerir o download de conteúdos, podendo assim utilizar a funcionalidade de cache de pares do Gestor de Configuração, ou outras tecnologias, como a Otimização de Entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Gestor de Configuração, incluindo atualizações do Windows e do Office. 

Para mais informações, consulte a opção **no pacote de implementação quando** implementar [manualmente atualizações](../../../sum/deploy-use/manually-deploy-software-updates.md) de software ou [implementar automaticamente atualizações](../../../sum/deploy-use/automatically-deploy-software-updates.md)de software .


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrar regras de implementação automática pela arquitetura de atualização de software
 <!--1322266-->
Agora pode filtrar regras de implantação automática (ADR) para excluir arquiteturas como Itanium e ARM64. Na página de **Atualizações** de Software do Assistente de Regra de Implementação Automática Create, o filtro de propriedade **da Arquitetura** já está disponível. 

Para mais informações, consulte [a implementação automática](../../../sum/deploy-use/automatically-deploy-software-updates.md)de atualizações de software .


### <a name="improved-wsus-maintenance"></a>Melhor manutenção da WSUS 
<!--1357898-->
O assistente de limpeza WSUS agora recusa atualizações que são expiradas de acordo com as regras de supersedência definidas nas propriedades do componente de ponto de atualização de software. 

Para mais informações, consulte a [manutenção de atualizações](../../../sum/deploy-use/software-updates-maintenance.md)de Software.



## <a name="reporting"></a>Relatórios

### <a name="new-software-updates-compliance-report"></a>Novo relatório de conformidade atualiza atualizações de software
<!--1357775-->
Ver relatórios para atualizações de software a conformidade tradicionalmente inclui dados de clientes que não contactaram recentemente o site. Um novo relatório, **Compliance 9 - Saúde e conformidade em geral,** permite filtrar os resultados de conformidade de um grupo específico de atualização de software por clientes "saudáveis". Este relatório mostra o estado de conformidade mais realista dos clientes ativos no seu ambiente. 

Para mais informações, consulte relatórios de [atualizações](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports)de Software .



## <a name="inventory"></a>Inventário

### <a name="improvement-to-hardware-inventory-for-large-integer-values"></a><a name="bkmk_bigint"></a>Melhoria do inventário de hardware para grandes valores inteiros
<!--1357880-->
O inventário de hardware previamente tinha um limite para os inteiros superiores a 4.294.967.296 (2^32). Este limite poderia ser atingido para atributos como tamanhos de disco rígido em bytes. O ponto de gestão não processou valores inteiros acima deste limite, pelo que nenhum valor foi armazenado na base de dados. Agora, nesta versão, o limite é aumentado para 18.446.744.073.709.551.616 (2^64). 

Para mais informações, consulte [a utilização de grandes valores inteiros.](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint)


### <a name="hardware-inventory-default-unit-revision"></a>Revisão da unidade padrão de inventário de hardware
<!--514442-->
Na [versão 1710](whats-new-in-version-1710.md#site-infrastructure)do Gestor de Configuração, a unidade padrão utilizada em muitas visualizações de reporte passou de megabytes (MB) para gigabytes (GB). Devido a melhorias no inventário de [hardware para grandes valores inteiros](#bkmk_bigint), e com base no feedback do cliente, esta unidade padrão é agora MB novamente.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Consola do Configuration Manager

### <a name="product-lifecycle-dashboard"></a>Painel de instrumentos de ciclo de vida do produto
<!--1319632-->
O painel de instrumentos de ciclo de vida do produto mostra o estado da Política de Ciclo de Vida da Microsoft para os produtos microsoft instalados em dispositivos geridos com o Gestor de Configuração. Também lhe fornece informações sobre produtos da Microsoft no seu ambiente, estado de suporte e datas finais de suporte. Utilize o painel de instrumentos para compreender a disponibilidade de suporte para cada produto. Esta informação ajuda-o a planear quando atualizar os produtos da Microsoft que utiliza antes de ser atingido o seu suporte atual.   

Para mais informações, consulte o painel de instrumentos de vida do [produto.](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)


### <a name="copy-asset-details-from-monitoring-views"></a>Copiar detalhes do ativo a partir de visualizações de monitorização
<!--1357856-->
As seguintes áreas do espaço de trabalho **de monitorização** suportam agora texto de cópia:  

- No nó **de Implantações,** selecione uma implementação e clique no **'Ver Status**. No painel de detalhes do **ativo** da vista Estado de Implementação, selecione um ou mais dispositivos.  

- Expandir o nó **do Estado** de Distribuição e selecionar o Estado **do Conteúdo**. Selecione uma peça de software e clique em **'Ver Status**'. No painel de detalhes do **ativo** da vista Estado do Conteúdo, selecione um ou mais pontos de distribuição. 

Clique no ativo e selecione **Copiar**. Esta ação copia os ativos selecionados como uma lista delimitada de vírina que inclui todos os detalhes. O atalho de teclado **CTRL** + **C** também funciona nestas vistas. 

Para mais informações, consulte [as melhorias da Consola na versão 1806](../../servers/manage/admin-console.md#copy-details-in-monitoring-views).


### <a name="improvements-to-the-surface-dashboard"></a>Melhorias no painel surface
<!--1358654-->
Esta versão inclui as seguintes melhorias no painel surface:  

- O painel de instrumentos Surface apresenta agora uma lista de dispositivos relevantes quando seleciona secções específicas de gráficos:  

   - Clicar no azulejo **Por cento dos dispositivos de superfície** abre uma lista de dispositivos Surface.  

   - Clicar numa barra no azulejo **top 5 firmware versions** abre uma lista de dispositivos Surface com essa versão específica do firmware.  

- Ao visualizar estas listas de dispositivos a partir do painel de instrumentos Surface, clique num dispositivo para executar ações comuns.  

Para mais informações, consulte o [painel de instrumentos surface](../../clients/manage/surface-device-dashboard.md).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Veja o utilizador atualmente assinado para um dispositivo
<!--1358202-->
Agora, por padrão, o nó de **Dispositivos** do espaço de trabalho **Ativos e Compliance** apresenta uma coluna para o **atualmente registado no utilizador**. Também apresenta para qualquer lista de dispositivos específicos de recolha. Este valor é tão atual como o estatuto do [cliente.](../../clients/manage/monitor-clients.md#bkmk_indStatus) Quando o utilizador assina, o cliente limpa este valor. Se nenhum utilizador for assinado, o valor é em branco. 

Para mais informações, consulte [as melhorias da Consola na versão 1806](../../servers/manage/admin-console.md#view-users-for-a-device).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Enviar feedback da consola 'Gestor de Configuração'  
<!--1357542-->

Mande um sorriso! Já pode contar diretamente à equipa do Gestor de Configuração as suas experiências. Enviar feedback é fácil a partir da consola 'Gestor de Configuração'. Queremos ouvir todo o seu feedback: louvor, problemas e sugestões. Na consola 'Gestor de Configuração', clique no botão de sorriso no canto superior direito acima da fita. Este feedback vai diretamente para a equipa de produtos da Microsoft para O Gestor de Configuração. Enquanto a utilização do Hub de Feedback do Windows 10 ainda é suportada, é sucudedo a utilização do mecanismo de feedback na consola.  

Para mais informações, consulte [as melhorias da Consola na versão 1806](../../servers/manage/admin-console.md#send-feedback) e no feedback do [Produto.](../../understand/find-help.md#BKMK_1806Feedback)



## <a name="other-updates"></a>Outras atualizações

Além de novas funcionalidades, esta versão também inclui alterações adicionais, tais como correções de bugs. Para mais informações, consulte [resumo das alterações no atual ramo do Gestor de Configuração, versão 1806](https://support.microsoft.com/help/4459701).

Para obter mais informações sobre as alterações nas cmdlets do Windows PowerShell para O Gestor de Configuração, consulte [powerShell 1806 Notas](https://docs.microsoft.com/powershell/sccm/1806_release_notes?view=sccm-ps)de lançamento .

O rollup de atualização seguinte (4462978) está disponível na consola a partir de 24 de outubro de 2018: Rollup de atualização para o ramo atual do Gestor de [Configuração, versão 1806](https://support.microsoft.com/help/4462978).


### <a name="hotfixes"></a>Correções

Estão disponíveis os seguintes hotfixes adicionais para abordar questões específicas:

| ID | Título | Date | Na consola |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Atualização para configuração manager versão 1806, primeira onda | 31 agosto 2018 | Sim |
| [4465865](https://support.microsoft.com/help/4465865) | As atualizações de software não descarregam no ambiente do Gestor de Configuração se o WSUS estiver desligado<br><br>Esta atualização também está no rollup da atualização (4462978) | 01 outubro 2018 | Sim |
| [4471892](https://support.microsoft.com/help/4471892) | PXE Responder não trabalha em subnets no Diretor de Configuração 1806 | 23 de novembro de 2018 | Não |
| [4487960](https://support.microsoft.com/help/4487960) | Certificado de conector Microsoft Intune não renova no Gestor de Configuração | 18 janeiro 2019 | Sim |


## <a name="next-steps"></a>Passos seguintes

Quando estiver pronto para instalar esta versão, consulte [a instalação de atualizações para O Gestor](../../servers/manage/updates.md) de Configuração e lista de [verificação para instalar a atualização 1806](../../servers/manage/checklist-for-installing-update-1806.md).

> [!TIP]  
> Para instalar um novo site, utilize uma versão de base do Gestor de Configuração.  
>
> Saiba mais sobre:    
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)

Para questões conhecidas e significativas, consulte as notas de [lançamento.](../../servers/deploy/install/release-notes.md)

Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).
