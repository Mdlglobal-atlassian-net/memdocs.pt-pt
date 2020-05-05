---
title: Novidades na versão 1810
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1810 do ramo atual do Gestor de Configuração.
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6a9770dca209669659abf6e4fc9c23d5e6972981
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073556"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Novidades na versão 1810 do ramo atual do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1810 para o atual ramo do Gestor de Configuração está disponível como uma atualização na consola. Aplique esta atualização em sites que executam a versão 1710, 1802 ou 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> Este artigo resume as alterações e novas funcionalidades no Gestor de Configuração, versão 1810.  

Reveja sempre a mais recente lista de verificação para instalar esta atualização. Para mais informações, consulte a Lista de [Verificação para instalar a atualização 1810](../../servers/manage/checklist-for-installing-update-1810.md). Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).

Para aproveitar as novas funcionalidades do Gestor de Configuração, os clientes da primeira atualização para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> Para ser notificado quando esta página for atualizada, copie e cole o seguinte URL no seu leitor de feed RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a>Funcionalidades e sistemas operativos degradados

Saiba mais sobre as alterações de suporte antes de serem implementadas em [itens removidos e depreciados](deprecated/removed-and-deprecated.md).

A partir de 14 de agosto de 2018, a funcionalidade de gestão de dispositivos móveis híbridos é depreciada. Para mais informações, veja [o que aconteceu ao MDM híbrido.](../../../mdm/understand/what-happened-to-hybrid.md)<!--Intune feature 2683117-->  

Suporte para System Center Endpoint Protection (SCEP) para Mac e Linux (todas as versões) termina em 31 de dezembro de 2018. A disponibilidade de novas definições de vírus para SCEP para Mac e SCEP para Linux pode ser descontinuada após o fim do suporte. Para mais informações, consulte [End of support blog post](https://go.microsoft.com/fwlink/?linkid=870182).

As implementações clássicas de serviço em Azure estão agora depreciadas no Gestor de Configuração. Comece a utilizar as implementações do Gestor de Recursos Azure para o gateway de gestão de nuvem e o ponto de distribuição da nuvem. Para mais informações, consulte [Plano para CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Infraestrutura do local

### <a name="support-for-windows-server-2019"></a>Suporte para Windows Server 2019

<!--1359195-->
O Gestor de Configuração suporta agora o Windows Server 2019 e o Windows Server, versão 1809, como sistemas de site.

Para obter mais informações, consulte [sistemas operativos suportados para servidores](../configs/supported-operating-systems-for-site-system-servers.md)do sistema do site .


### <a name="hierarchy-support-for-site-server-high-availability"></a>Suporte hierárquica para alta disponibilidade do servidor do site

<!--3607755, fka 1358224-->
Os sites da administração central e os sites primários infantis podem agora ter um servidor adicional do site em modo passivo.

Para mais informações, consulte a elevada disponibilidade do [servidor do Site](../../servers/deploy/configure/site-server-high-availability.md).


### <a name="improvements-to-setup-prerequisites"></a>Melhorias nos pré-requisitos de configuração

Quando instala ou atualiza para a versão 1810, a configuração do Gestor de Configuração inclui ou melhora as seguintes verificações prévias:

- **Reinício do sistema pendente**: Esta verificação pré-requisito é agora mais resistente. Verifica as chaves de registo adicionais para as funcionalidades do Windows. Para mais informações, consulte [O reinício do sistema pendente](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **SQL alterar limpeza de rastreio**de alterações : Uma nova verificação se a base de dados do site tem um atraso de dados de rastreio de alterações SQL. Para obter mais informações, incluindo um procedimento para verificar e limpar este atraso, consulte a limpeza de rastreio de [alterações SQL](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **Versão SQL Native Client**: Esta verificação pré-requisito é atualizada para versões do SQL Native Client que suportam TLS 1.2. A versão mínima é [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Para mais informações, consulte a [versão SQL Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Sistema**de site no nó de cluster windows : O processo de configuração do Gestor de Configuração já não bloqueia a instalação da função do servidor do site num computador com a função Windows para o Clusterfailover. O SQL Always On requer esta função, pelo que anteriormente não conseguiu colocar a base de dados do site no servidor do site. Com esta alteração, pode criar um site altamente disponível com menos servidores utilizando o SQL Always On e um servidor de site em modo passivo. Para mais informações, consulte [o Cluster Failover do Windows](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster). <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>Nova permissão para ações de notificação de clientes

<!--SCCMDocs-pr issue #2972-->
As ações de notificação do cliente exigem agora a permissão de **Recursos notificados** na classe SMS_Collection. As seguintes funções incorporadas têm esta permissão por defeito:

- Administrador Total  
- Administrador de Infraestrutura  

Adicione esta permissão a quaisquer funções personalizadas que precisem de usar ações de notificação do cliente.

Para mais informações, consulte [notificações do Cliente](../../clients/manage/client-notification.md).



## <a name="content-management"></a><a name="bkmk_content"></a>Gestão de conteúdos

### <a name="new-boundary-group-options"></a>Novas opções de grupo de fronteiras

<!--1358749-->
Os grupos de fronteira seguem agora as seguintes definições adicionais para lhe dar mais controlo sobre a distribuição de conteúdos no seu ambiente:

- **Prefira pontos de distribuição em vez de pares com a mesma sub-rede**: Por padrão, o ponto de gestão prioriza as fontes de cache dos pares no topo da lista de locais de conteúdo. Esta definição inverte essa prioridade para os clientes que estão na mesma sub-rede que a fonte de cache dos pares.  

- **Prefira pontos**de distribuição em nuvem em vez de pontos de distribuição : Se tiver uma sucursal com uma ligação de internet mais rápida, pode agora priorizar o conteúdo em nuvem.  

Para mais informações, consulte as opções do [grupo Boundary para downloads de pares](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Regra de insights de gestão para versão cliente fonte de cache peer

<!-- 1358008 -->
O nó **Management Insights** tem uma nova regra para identificar clientes que servem como fonte de cache de pares, mas não atualizaram a partir de uma versão de cliente pré-1806. A nova regra é atualizar as fontes de **cache dos pares para a versão mais recente do cliente do Gestor de Configuração,** e faz parte do novo grupo de regras de **manutenção proactiva.** Os clientes pré-1806 não podem ser usados como fonte de cache para clientes que executam a versão 1806 ou mais tarde. Selecione **Tomar medidas** para abrir uma vista de dispositivo que exibe a lista de clientes.

Para mais informações, consulte [a Management insights](../../servers/manage/management-insights.md).



## <a name="client-management"></a><a name="bkmk_client"></a>Gestão de clientes

### <a name="new-client-notification-action-to-wake-up-device"></a>Nova ação de notificação do cliente para despertar dispositivo

<!--1317364-->
Agora pode acordar os clientes da consola Do Gestor de Configuração, mesmo que o cliente não esteja na mesma sub-rede que o servidor do site. Se precisar de fazer dispositivos de manutenção ou consulta, não se limita a clientes remotos que estão a dormir. O servidor do site usa o canal de notificação do cliente para identificar outro cliente que está acordado na mesma subnet remota. O cliente acordado envia então um velório a pedido da LAN (pacote mágico).

Para mais informações, consulte [Configure Wake on LAN](../../clients/deploy/configure-wake-on-lan.md) e [Como acordar os clientes](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Nova opção para realizar notificação do cliente a partir do nó dos dispositivos

<!--1317364-->
Até 1810, a opção **notificação** do cliente só estava disponível a partir do nó de Recolha de Dispositivos ou quando viu a adesão a uma Coleção de Dispositivos. Agora é possível realizar uma **Notificação** do Cliente a partir do nó de **Dispositivos** diretamente. Não há mais um requisito para estar dentro de uma vista de membros da coleção.

Para mais informações, consulte [notificações do Cliente](../../clients/manage/client-notification.md).


### <a name="improvements-to-collection-evaluation"></a>Melhorias na avaliação da recolha

<!--3607726, fka 1358981-->
As seguintes alterações no comportamento de avaliação da recolha podem melhorar o desempenho do local:  

- Anteriormente, quando configurava uma programação numa coleção baseada em consultas, o site continuaria a avaliar a consulta se permitia ou não a definição de recolha para **agendar uma atualização completa desta coleção.** Para desativar totalmente o horário, teve de alterar o horário para **Nenhum.** Agora o site limpa o horário quando desativa este cenário. Para especificar um calendário para avaliação de recolha, ative a opção de **agendar uma atualização completa sobre esta coleção.**  

- Não é possível desativar a avaliação de coleções incorporadas como **a All Systems,** mas agora pode configurar o horário. Este comportamento permite personalizar esta ação num momento que satisfaz os seus requisitos de negócio.

Para mais informações, consulte [Como criar coleções.](../../clients/manage/collections/create-collections.md#bkmk_create)


### <a name="improvement-to-client-installation"></a>Melhoria da instalação do cliente

<!--1358840-->
Ao instalar o cliente do Gestor de Configuração, o processo ccmsetup contacta o ponto de gestão para localizar o conteúdo necessário. Anteriormente, neste processo, o ponto de gestão apenas devolve pontos de distribuição no atual grupo de fronteira do cliente. Se não houver conteúdo disponível, o processo de configuração recua para descarregar conteúdo a partir do ponto de gestão. Não há opção de voltar aos pontos de distribuição em outros grupos de fronteira que possam ter o conteúdo necessário. Agora, o ponto de gestão devolve pontos de distribuição com base na configuração do grupo de limites.

Para mais informações, consulte [os grupos de fronteira configure](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup).



## <a name="co-management"></a><a name="bkmk_comgmt"></a>Cogestão

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Política de conformidade de aplicações exigida para dispositivos cogeridos

<!--1358196-->
Defina as regras de política de conformidade no Gestor de Configuração para aplicações necessárias. Esta avaliação da aplicação faz parte do estado de conformidade global enviado à Microsoft Intune para dispositivos cogeridos.

Para obter mais informações, consulte a [cogestão de cargas de trabalho.](../../../comanage/workloads.md)


### <a name="improvement-to-co-management-dashboard"></a>Melhoria do painel de cogestão

<!--1358980-->
O painel de cogestão é melhorado com as seguintes informações mais detalhadas:  

- O azulejo do estado de inscrição de **cogestão** inclui estados adicionais

- Um novo **azulejo de cogestão** com um gráfico de funil mostra estados do processo de inscrição

- Um novo azulejo com contagem de erros de **inscrição**

![Imagem de painel de cogestão mostrando os quatro primeiros azulejos](media/1358980-comgmt-dashboard.png)

Para mais informações, consulte [o painel de cogestão](../../../comanage/how-to-monitor.md#co-management-dashboard).


### <a name="improvements-to-internet-based-client-setup"></a>Melhorias na configuração de clientes baseados na Internet

<!--3607731, fka 1359181-->
Esta versão simplifica ainda o processo de configuração do cliente do Gestor de Configuração para os clientes na internet. O site publica informações adicionais do Azure Ative Directory (Azure AD) para o gateway de gestão de nuvem (CMG). Um cliente azure-joined ad obtém esta informação da CMG durante o processo ccmsetup, usando o mesmo inquilino ao qual se juntou. Este comportamento simplifica ainda mais os dispositivos de inscrição para a cogestão num ambiente com mais de um inquilino da AD Azure. Agora, as duas únicas propriedades ccmsetup necessárias são **CCMHOSTNAME** e **SMSSiteCode**.

Para mais informações, consulte [Como preparar dispositivos baseados na Internet para cogestão](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).



## <a name="application-management"></a><a name="bkmk_app"></a>Gestão de aplicações

### <a name="convert-applications-to-msix"></a>Converter aplicações para MSIX

<!--3607729, fka 1359029-->
A partir da versão 1806, o Gestor de Configuração suporta a implementação do novo pacote de aplicações do Windows 10 (.msix). Agora pode converter as aplicações existentes do Instalador do Windows (.msi) para o formato MSIX.

Para mais informações, consulte [Create Windows aplicações](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).  


### <a name="repair-applications"></a>Aplicações de reparação

<!--1357866-->
Especifique uma linha de comando de reparação para os tipos de instalação do Instalador do Windows e do Instalador de Scripts. Em seguida, se ativar a opção na implementação, um novo botão está disponível no Centro de Software para **reparar** a aplicação. Quando configurar uma aplicação com um programa de reparação, os utilizadores podem iniciar o comando a partir do Centro de Software.

Para mais informações, consulte [Criar aplicações](../../../apps/deploy-use/create-applications.md#bkmk_dt-content) e [implementar aplicações.](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)


### <a name="approve-application-requests-via-email"></a>Aprovar pedidos de pedido por e-mail

<!--1321550-->
Configure notificações de e-mail para pedidos de aprovação de pedidos de aplicação. Quando um utilizador solicita uma aplicação, recebe um e-mail. Clique em links no e-mail para aprovar ou negar o pedido, sem necessitar da consola 'Gestor de Configuração'.

Para mais informações, consulte [Aprovar aplicações.](../../../apps/deploy-use/app-approval.md)


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Os métodos de deteção não carregam perfis do Windows PowerShell

<!--3607762, fka 1359239-->
Pode utilizar scripts Windows PowerShell para métodos de deteção em aplicações e configurações em itens de configuração. Quando estes scripts funcionam em clientes, o cliente do `-NoProfile` Gestor de Configuração chama agora powerShell com o parâmetro. Esta opção inicia a PowerShell sem perfis.

Um perfil PowerShell é um script que corre quando o PowerShell começa. Pode criar um perfil PowerShell para personalizar o seu ambiente e adicionar elementos específicos da sessão a todas as sessões da PowerShell que iniciar.

> [!Note]  
> Esta mudança de comportamento não se aplica a [Scripts](../../../apps/deploy-use/create-deploy-scripts.md) ou [CMPivot](../../servers/manage/cmpivot.md). Ambas as funcionalidades já utilizam este parâmetro PowerShell.  

Para mais informações, consulte [Criar aplicações](../../../apps/deploy-use/create-applications.md) e criar itens de [configuração personalizados.](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)



## <a name="os-deployment"></a><a name="bkmk_osd"></a>Implantação de Os

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Suporte de sequência de tarefas do Windows Autopilot para dispositivos existentes

<!--3607717, fka 1358333-->
[O Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) já se encontra disponível com o Windows 10, versão 1809 ou posterior. Esta nova funcionalidade permite-lhe reimagem e fornecer um dispositivo Windows 7 para o [modo de utilização do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) utilizando uma única sequência de tarefas nativa do Gestor de Configuração.

Para obter mais informações, veja [Windows Autopilot for existing devices](../../../osd/deploy-use/windows-autopilot-for-existing-devices.md) (Windows Autopilot para dispositivos existentes).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Especifique a unidade para manutenção de imagem offline do OS

<!--1358924-->
Agora especifique a unidade que o Gestor de Configuração utiliza ao adicionar atualizações de software às imagens do OS e aos pacotes de atualização do OS. Este processo pode consumir uma grande quantidade de espaço em disco com ficheiros temporários, pelo que esta opção lhe dá flexibilidade para selecionar a unidade a utilizar.

Para mais informações, consulte [Gerir as imagens do OS](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive) ou gerir [pacotes](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive)de upgrade do OS .


### <a name="task-sequence-support-for-boundary-groups"></a>Suporte de sequência de tarefas para grupos de fronteira

<!--1359025-->
Quando um dispositivo executa uma sequência de tarefas e precisa de adquirir conteúdo, agora utiliza comportamentos de grupo de limites semelhantes ao cliente do Gestor de Configuração.

Para mais informações, consulte [os grupos de fronteira](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Melhorias na manutenção do condutor

<!--3607716, fka 1358270-->
Os pacotes de condutores têm agora campos de metadados adicionais para **o Fabricante** e **o Modelo**. Utilize estes campos para etiquetar pacotes de condutores com informações para ajudar na limpeza geral, ou para identificar condutores antigos e duplicados que possa eliminar.

Para mais informações, consulte [Gerir os condutores](../../../osd/get-started/manage-drivers.md).

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Melhorias nos filtros do plano de manutenção do Windows 10

<!--3098809, 3113836, 3204570 -->
Foram adicionados filtros adicionais aos planos de manutenção do Windows 10. Agora pode filtrar por **Arquitetura,** **Categoria de Produto,** e se a atualização for **superseded**.

Para mais informações, consulte o plano de [manutenção do Windows 10.](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan)

### <a name="new-task-sequence-variable-for-last-action-name"></a>Nova variável de sequência de tarefas para o último nome de ação

<!--SCCMDocs-pr issue #2964-->
Juntamente com a variável de sequência de tarefas _SMSTSLastActionRetCode, a sequência de tarefas também define uma nova variável **_SMSTSLastActionName**. Também regista este valor no ficheiro smsts.log. Esta nova variável é benéfica quando se resoluuma sequência de tarefas. Quando um passo falha, um script personalizado pode incluir o nome do passo juntamente com o código de retorno.

Para obter mais informações, consulte variáveis de sequência de [tarefas](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName).



## <a name="software-updates"></a><a name="bkmk_sum"></a>Atualizações de software

### <a name="phased-deployment-of-software-updates"></a>Implementação faseada de atualizações de software

<!--1358146-->
Criar implementações faseadas para atualizações de software. As implementações faseadas permitem-lhe orquestrar um lançamento coordenado e sequenciado de software com base em critérios e grupos personalizáveis.

Para mais informações, consulte [Criar implementações faseadas](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Melhoria das janelas de manutenção para atualizações de software

<!--vso2839307-->
A seguinte definição de cliente está no grupo **Software Updates** para controlar o comportamento de instalação de atualizações de software nas janelas de manutenção: Ativar a **instalação de atualizações na janela de manutenção "Todas as implementações" quando a janela de manutenção "Software update" estiver disponível**

Por padrão, esta opção é **Não** para manter consistente com o comportamento existente. Mude-o para **Sim** para permitir que os clientes utilizem outras janelas de manutenção disponíveis para instalar atualizações de software.

Para mais informações, consulte as definições do [cliente de Software.](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint)


### <a name="improvement-to-software-updates-maintenance"></a>Melhoria da manutenção de atualizações de software

<!--2839349-->
As tarefas de limpeza da WSUS são agora executadas em sites secundários. A limpeza do WSUS para atualizações expiradas é executada e as atualizações supersed são recusadas no WSUS para sites secundários.

Para mais informações, consulte o comportamento de [limpeza wSUS a partir da versão 1810](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)

### <a name="improvement-to-software-update-supersedence-rules"></a>Melhoria das regras de supersedência da atualização de software

<!--3098809, 2977644-->
Agora pode especificar as regras de supersedência para atualizações de funcionalidades separadamente de atualizações não-funcionalidades. Isto significa que as suas atualizações não serão removidas do Gestor de Configuração antes de ter concluído a manutenção dos seus clientes windows 10.

Para mais informações, consulte [Supersedence rules](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules).

## <a name="reporting"></a><a name="bkmk_report"></a>Reportagem

### <a name="improvement-to-lifecycle-dashboard"></a>Melhoria do painel de instrumentos de ciclo de vida

<!--1358702-->
O painel de instrumentos de ciclo de vida do produto inclui agora informações para **o System Center 2012 Configuration Manager e mais tarde**.

Há também um novo relatório, **Lifecycle 05A - Painel de instrumentos**de ciclo de vida do produto. Inclui informações semelhantes às do painel de instrumentos da consola.

Para obter mais informações sobre este dashboard, consulte [Utilize o painel de instrumentos](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)do ciclo de vida do produto .


### <a name="improvement-to-data-warehouse"></a>Melhoria do armazém de dados

<!--1358870-->
Agora pode sincronizar mais tabelas da base de dados do site para o armazém de dados. Esta alteração permite-lhe criar mais relatórios com base nos seus requisitos de negócio.

Para mais informações, consulte [data warehouse](../../servers/manage/data-warehouse.md).



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Consola de Gestor de Configuração

### <a name="configuration-manager-administrator-authentication"></a>Autenticação do administrador do Gestor de Configuração

<!--1357013-->
Pode agora especificar o nível mínimo de autenticação para os administradores acederem aos sites do Gestor de Configuração. Esta funcionalidade impõe aos administradores que assinem no Windows com o nível exigido. Para configurar esta definição, encontre o separador **autenticação** nas **definições da hierarquia**.

Para mais informações, consulte [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth).


### <a name="support-center"></a>Centro de Suporte

<!--1357489-->
Utilize o Centro de Suporte para resolução de problemas do cliente, visualização de registoem em tempo real ou capturando o estado de um computador cliente do Gestor de Configuração para posterior análise. O Centro de Suporte é uma única ferramenta para combinar muitas ferramentas de resolução de problemas do administrador. Encontre o instalador do Centro de Suporte no servidor do site na pasta **cd.latest\SMSSETUP\Tools\SupportCenter.**

Para mais informações, consulte Centro de [Suporte](../../support/support-center.md).


### <a name="management-insights-dashboard"></a>Painel de insights de gestão

<!--1357979-->
O nó De Insights de **Gestão** agora inclui um painel gráfico. Este painel apresenta uma visão geral dos estados de regra, o que facilita a sua demonstração do seu progresso. O painel inclui os seguintes azulejos:

- **Índice de insights**de gestão : Acompanha o progresso global das regras de insights de gestão. O índice é uma média ponderada. As regras críticas são as que valem mais. Este índice dá o menor peso às regras opcionais.  

- **Grupos de insights**de gestão : Mostra por cento das regras em cada grupo.  

- Prioridade dos insights de **gestão**: Mostra por cento das regras por prioridade.  

- **Todos os insights**: Uma tabela de insights, incluindo prioridade e estado.  

![Screenshot do painel de insights de gestão](media/1357979-management-insights-dashboard.png)

Para mais informações, consulte [a Management insights](../../servers/manage/management-insights.md).


### <a name="improvements-to-cmpivot"></a>Melhorias à CMPivot

<!--1359068-->
A CMPivot inclui as seguintes melhorias:

- Guardar consultas **favoritas**  

- No separador Resumo de Consulta, selecione a contagem de dispositivos Failed ou Offline e, em seguida, selecione a opção de **Criar Recolha**.

Para obter mais informações sobre desempenho adicional e melhorias na resolução de problemas para a CMPivot, consulte [Melhorias nos scripts](#bkmk_scripts).

Para mais informações sobre a CMPivot, consulte [CMPivot](../../servers/manage/cmpivot.md).


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a>Melhorias nos scripts

<!--1358239-->
Agora pode ver a saída detalhada do script em formato JSON cru ou estruturado. Esta formatação facilita a leitura e análise da saída.

As seguintes melhorias de desempenho e resolução de problemas aplicam-se tanto à CMPivot como aos scripts:

- Os clientes atualizados devolvem a saída a menos de 80 KB ao site num canal de comunicação rápida. Esta alteração aumenta o desempenho da visualização do script ou da saída de consulta.  

- Registos adicionais para resolução de problemas  

Para obter mais informações, veja os artigos seguintes:  

- [Criar e executar scripts PowerShell a partir da consola De Configuração Manager](../../../apps/deploy-use/create-deploy-scripts.md)  

- [Resolução de Problemas do CMPivot](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>SMS Provider API

<!--3607711, fka 1321523-->
O Provedor SMS agora fornece acesso de interoperabilidade apenas a API a apenas de leitura ao WMI em HTTPS, chamado serviço de **administração**. Esta API REST pode ser usada no lugar de um serviço web personalizado para aceder a informações a partir do site.

O Provedor de **SMS** aparece como um papel com uma opção para permitir a comunicação sobre o gateway de gestão de nuvem. A utilização atual para esta definição é ativar as aprovações de aplicações por e-mail a partir de um dispositivo remoto.

Para mais informações, consulte [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a>NO LOCAL MDM

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Uma ligação Intune já não é necessária para novas implantações de MDM no local

<!--1359124-->
O MDM no local pré-requisito para configurar uma subscrição Microsoft Intune já não é necessário para novas implementações. A sua organização ainda requer licenças Intune para usar esta funcionalidade. Não é possível remover atualmente a ligação Intune das implementações de MDM existentes no local. Para mais informações, consulte o post do [blog de suporte Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Outras atualizações

Além de novas funcionalidades, esta versão também inclui alterações adicionais, tais como correções de bugs. Para mais informações, consulte [resumo das alterações no atual ramo do Gestor de Configuração, versão 1810](https://support.microsoft.com/help/4482169).

Para obter mais informações sobre as alterações nas cmdlets do Windows PowerShell para O Gestor de Configuração, consulte [as notas de lançamento da versão PowerShell 1810](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps).

O rollup de atualização seguinte (4488598) está disponível na consola a partir de 25 de março de 2019: [Atualização de rollup 2 para configuração de gestão atual, versão 1810](https://support.microsoft.com/help/4488598). Isto substitui o rollup da atualização anterior, KB 4486457.


### <a name="hotfixes"></a>Correções

Estão disponíveis os seguintes hotfixes adicionais para abordar questões específicas:

| ID | Título | Date | Na consola |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Certificado de conector Microsoft Intune não renova no Gestor de Configuração | 18 janeiro 2019 | Sim |
| [4490434](https://support.microsoft.com/help/4490434) | As colunas duplicadas de descoberta de utilizadores são criadas no Gestor de Configuração | 22 fevereiro 2019 | Sim |
| [4490575](https://support.microsoft.com/help/4490575) | As instalações de atualização deixam de responder ou nunca mostram a conclusão no Diretor de Configuração, versão 1810 | 22 fevereiro 2019 | Sim |


## <a name="next-steps"></a>Passos seguintes

Quando estiver pronto para instalar esta versão, consulte [a instalação de atualizações para O Gestor](../../servers/manage/updates.md) de Configuração e lista de [verificação para instalar a atualização 1810](../../servers/manage/checklist-for-installing-update-1810.md).

> [!TIP]  
> Para instalar um novo site, utilize uma versão de base do Gestor de Configuração.  
>
> Saiba mais sobre:
>
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)  

Para questões conhecidas e significativas, consulte as notas de [lançamento.](../../servers/deploy/install/release-notes.md)

Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).
