---
title: Novidades na versão 1906
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1906 do ramo atual do Gestor de Configuração.
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2db1a719aaf1cb79973f1af8e2de3c1bbb91d605
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879094"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Novidades na versão 1906 do diretor de configuração da filial atual

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1906 para o atual ramo do Gestor de Configuração está disponível como uma atualização na consola. Aplique esta atualização em sites que executam a versão 1802 ou posterior. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Este artigo resume as mudanças e novas funcionalidades no Gestor de Configuração, versão 1906.  

Reveja sempre a mais recente lista de verificação para instalar esta atualização. Para mais informações, consulte a Lista de [Verificação para instalar a atualização 1906](../../servers/manage/checklist-for-installing-update-1906.md). Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).

Para tirar o máximo partido das novas funcionalidades do Gestor de Configuração, depois de atualizar o site, também atualize os clientes para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

> [!Tip]  
> Para ser notificado quando esta página for atualizada, copie e cole o seguinte URL no seu leitor de feed RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>Alterações de requisitos

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>Cliente da versão 1906 requer suporte de assinatura de código SHA-2

<!--SCCMDocs-pr#3404-->
Devido a fraquezas no algoritmo SHA-1 e a alinhar-se com os padrões da indústria, a Microsoft agora apenas assina binários de Gestor de Configuração usando o algoritmo SHA-2 mais seguro. As seguintes versões do Windows OS requerem uma atualização para o suporte de assinatura de código SHA-2:

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

Para mais informações, consulte [os pré-requisitos para os clientes windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2).


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Infraestrutura do local

### <a name="site-server-maintenance-task-improvements"></a>Melhorias na tarefa de manutenção do servidor do site

<!--3555894-->
As tarefas de manutenção do servidor do site podem agora ser visualizadas e editadas a partir do seu próprio separador na visão de detalhes de um servidor de site. O novo separador **Tarefas de Manutenção** dá-lhe informações como:

- Se a tarefa estiver ativada
- O calendário de tarefas
- Última hora de início
- Última hora de conclusão
- Se a tarefa concluída com sucesso

![Novo separador para tarefas de manutenção na visão detalhada de um servidor de site](./media/3555894-maintenance-tasks.png)

Para mais informações, consulte [as tarefas de manutenção.](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906)

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Monitorização da atualização da base de dados do Gestor de Configuração

<!--4200581-->
Ao aplicar uma atualização do Gestor de Configuração, pode agora ver o estado da tarefa de base de **dados De upgrade ConfigMgr** na janela de estado de instalação.

- Se a atualização da base de dados estiver bloqueada, receberão o aviso, **em curso, que necessitará de atenção.**
   - O cmupdate.log registará o nome do programa e o sessionid da SQL que está bloqueando a atualização da base de dados.
- Quando a atualização da base de dados já não estiver bloqueada, o estado será reiniciado em **curso** ou **Concluído**.
   - Quando a atualização da base de dados está bloqueada, uma verificação é feita a cada 5 minutos para ver se ainda está bloqueada.

   ![Monitorização da atualização da base de dados durante a instalação](./media/4200581-database-upgrade-monitoring.png)

Para mais informações, consulte [Instalar atualizações na consola](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install).

### <a name="management-insights-rule-for-ntlm-fallback"></a>Regra dos insights de gestão para o recuo da NTLM

<!--4572953-->
Os conhecimentos de gestão incluem uma nova regra que deteta se ativou o método de recuo de autenticação NTLM menos seguro para o site: o recuo da **NTLM está ativado**.

Para mais informações, consulte [a Management insights](../../servers/manage/management-insights.md#security).

### <a name="improvements-to-support-for-sql-always-on"></a>Melhorias no suporte para SQL Always On

- Adicione uma nova réplica sincronizada da configuração<!--3127336-->: Pode agora adicionar um novo nó de réplica secundária a um grupo de disponibilidade SQL Always On existente. Em vez de um processo manual, utilize a configuração do 'Gestor de Configuração' para fazer esta alteração. Para mais informações, consulte [Configure SQL Server Always On grupos de disponibilidade](../../servers/deploy/configure/configure-aoag.md#bkmk_sync).

- Falha de rede multi-subnet<!-- SCCMDocs-pr#3734 -->: Agora pode ativar a palavra-chave de cadeia de [ligação MultiSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) no Servidor SQL. Também precisa de configurar manualmente o servidor do site. Para obter mais informações, consulte o pré-requisito de falha da [multi-sub-rede.](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover)

- Apoio a pontos de vista distribuídos<!-- SCCMDocs-pr#3792 -->: A base de dados do site pode ser hospedada num grupo de disponibilidade do SQL Server Always On, e pode ativar as ligações de replicação da base de dados para utilizar [visualizações distribuídas](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep).

    > [!Note]  
    > Esta alteração não se aplica aos clusters do Servidor SQL.

- A recuperação do site pode recriar a base de dados num grupo SQL Always On. Este processo funciona com sementeção manual e automática.<!-- SCCMDocs-pr#3846 -->

- Novos controlos pré-requisitode configuração:<!-- SCCMDocs-pr#3899 -->  

    - As réplicas do grupo de disponibilidade SQL devem ter o mesmo modo de sementeira
    - Réplicas do grupo de disponibilidade SQL devem ser saudáveis

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>Gestão ligada à nuvem

### <a name="azure-active-directory-user-group-discovery"></a>Descoberta do grupo de utilizadores do Diretório Ativo Azure

<!--3611956-->

Agora pode descobrir grupos de utilizadores e membros desses grupos do Azure Ative Directory (Azure AD). Os utilizadores encontrados em grupos de Anúncios Azure que o site não descobriu anteriormente são adicionados como recursos de utilizador no Gestor de Configuração. É criado um registo de recursos do grupo de utilizadores quando o grupo é um grupo de segurança. Esta funcionalidade é uma [funcionalidade de pré-lançamento](../../servers/manage/pre-release-features.md) e precisa de ser ativada.

Para mais informações, consulte os métodos de [descoberta do Configure.](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>Sincronizar os resultados da adesão à coleção aos grupos de Diretórios Ativos da Azure

<!--3607475-->

Agora pode permitir a sincronização de membros da coleção a um grupo de Diretórios Ativos Azure (Azure AD). Esta sincronização é uma característica de pré-lançamento. Para o ativar, consulte [as funcionalidades de pré-lançamento](../../servers/manage/pre-release-features.md).

A sincronização permite-lhe utilizar as suas regras de agrupamento no local existentes na nuvem, criando membros do grupo Azure AD com base nos resultados da adesão à coleção. Apenas os dispositivos com um registo de Diretório Ativo Azure refletem-se no Grupo Azure AD. Os dispositivos de adesão da Hybrid Azure AD e azure Ative Directory são suportados.

Para mais informações, consulte [Criar coleções.](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)


## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Desktop Analytics

### <a name="readiness-insights-for-desktop-apps"></a>Insights de prontidão para aplicativos de desktop

<!-- 4021225 -->

Agora pode obter informações mais detalhadas para as suas aplicações de desktop, incluindo aplicações de linha de negócio. O ex-kit de ferramentas App Health Analyzer está agora integrado com o cliente do Gestor de Configuração. Esta integração simplifica a implementação e a gestão de insights de prontidão de aplicações no portal Desktop Analytics.

Para mais informações, consulte a [avaliação](../../../desktop-analytics/compat-assessment.md#advanced-insights)da compatibilidade no Desktop Analytics .


### <a name="dalogscollector-tool"></a>Ferramenta DALogsCollector

<!--4622989-->
Utilize a ferramenta DesktopAnalyticsLogsCollector.ps1 do Diretor de Configuração instalar o diretório para ajudar a resolver problemas no Desktop Analytics. Executa alguns passos básicos de resolução de problemas e recolhe os registos relevantes num único diretório de trabalho.

Para mais informações, consulte o colecionador de [Registos.](../../../desktop-analytics/log-collector.md)


## <a name="real-time-management"></a><a name="bkmk_real"></a>Gestão em tempo real

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>Adicione juntas, operadores adicionais e agregadores na CMPivot

<!--4054074-->

Para a CMPivot, tem agora operadores aritméticos adicionais, agregadores e a capacidade de adicionar consultas, como a utilização de Registo e Arquivo em conjunto.

Para mais informações, consulte [CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot1906).

### <a name="cmpivot-standalone"></a>CMPivot autónomo

<!--3555890, 4619340, 4692885 -->

Agora pode usar a CMPivot como uma aplicação autónoma. A CMPivot autónoma é uma **funcionalidade de pré-lançamento** e só está disponível em inglês. Execute a CMPivot fora da consola do Gestor de Configuração para ver o estado real dos dispositivos no seu ambiente. Esta alteração permite-lhe utilizar o CMPivot num dispositivo sem antes instalar a consola.

Pode partilhar o poder da CMPivot com outras personalidades, tais como helpdesk ou administradores de segurança, que não têm a consola instalada no seu computador. Estas outras personalidades podem usar cmPivot para consultar o Gestor de Configuração ao lado das outras ferramentas que tradicionalmente utilizam. Ao partilhar estes dados de gestão ricos, pode trabalhar em conjunto para resolver proativamente problemas de negócio que cruzam funções.

Para mais informações, consulte as funcionalidades [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) e [Pré-lançamento](../../servers/manage/pre-release-features.md#bkmk_table).

### <a name="added-permissions-to-the-security-administrator-role"></a>Permissões adicionais ao papel de Administrador de Segurança

<!--4683130-->

As seguintes permissões foram adicionadas ao papel de Administrador de [**Segurança**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) incorporado do Gestor de Configuração:

- Ler no Script SMS
- Executar CMPivot na coleção
- Ler no Relatório de Inventário

Para mais informações, consulte [CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot_secadmin1906).


## <a name="content-management"></a><a name="bkmk_content"></a>Gestão de conteúdos

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>Dados de descarregamento de otimização de entrega no painel de dados de dados dos clientes

<!--3555759-->
O painel de dados do cliente inclui agora dados de Otimização de [Entrega.](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) Este dashboard ajuda-o a entender de onde os clientes estão a obter conteúdo no seu ambiente.

Para mais informações, consulte o dashboard Source De [Dados do Cliente](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>Use o seu ponto de distribuição como um servidor de cache em rede para otimização de entrega

<!--3555764-->
Agora pode instalar o servidor de Cache de Otimização de Entrega nos seus pontos de distribuição. Ao gravar este conteúdo no local, os seus clientes podem beneficiar da funcionalidade de Otimização de Entrega, mas pode ajudar a proteger os links WAN.

Este servidor de cache funciona como uma cache transparente a pedido para conteúdos descarregados pela Otimização da Entrega. Utilize as definições do cliente para se certificar de que este servidor é oferecido apenas aos membros do grupo de limites do Gestor de Configuração local.

Para mais informações, consulte a [Otimização de Otimização da Rede de Depósito sintetizá-lo no Gestor de Configuração](../hierarchy/microsoft-connected-cache.md).


## <a name="client-management"></a><a name="bkmk_client"></a>Gestão de clientes

### <a name="support-for-windows-virtual-desktop"></a>Suporte para Windows Virtual Desktop

<!--3556025-->
[O Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) é uma funcionalidade de pré-visualização do Microsoft Azure e do Microsoft 365. Agora pode utilizar o Gestor de Configuração para gerir estes dispositivos virtuais que executam o Windows em Azure.

Semelhante a um servidor de terminal, estes dispositivos virtuais permitem múltiplas sessões de utilizador ativas simultâneas. Para ajudar no desempenho do cliente, o Gestor de Configuração desativa agora as políticas do utilizador em qualquer dispositivo que permita estas múltiplas sessões de utilizador. Mesmo que ative as políticas do utilizador, o cliente desativa-as por padrão nestes dispositivos, que incluem o Windows Virtual Desktop e servidores de terminais.

Para mais informações, consulte [versões De SO suportadas para clientes e dispositivos.](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers)

### <a name="support-center-onetrace-preview"></a>OneTrace do Centro de Suporte (Pré-visualização)

<!--3555962-->
OneTrace é um novo espectador de log com Centro de Suporte. Funciona da mesma forma com a CMTrace, com as seguintes melhorias:

- Uma vista atabáuada
- Janelas dockable
- Capacidades de pesquisa melhoradas
- Capacidade de ativar filtros sem sair da vista de registo
- Scrollbar sugere identificar rapidamente aglomerados de erros
- Abertura de registo rápido para ficheiros grandes

![Screenshot do espectador de registo OneTrace](./media/3555962-onetrace.png)

Para mais informações, consulte [o Suporte Center OneTrace](../../support/support-center-onetrace.md).

### <a name="configure-client-cache-minimum-retention-period"></a>Configure o período mínimo de retenção do cache do cliente

<!--4485509-->
Pode agora especificar o tempo mínimo para o cliente do Gestor de Configuração manter o conteúdo em cache. Esta definição do cliente define a quantidade mínima de tempo que o agente do Gestor de Configuração deve esperar antes de poder remover o conteúdo da cache no caso de ser necessário mais espaço. No grupo de definições de **cache do Cliente,** configure a seguinte definição: A duração mínima antes de **conteúdo em cache pode ser removida (minutos)**.

> [!Note]  
> No mesmo grupo de definição de cliente, a definição existente para ativar o cliente do Gestor de **Configuração em pleno SISTEMA para partilhar conteúdo** é agora renomeado para Enable como fonte de cache de **pares**. O comportamento da configuração não muda.  

Para mais informações, consulte [as definições de cache do Cliente](../../clients/deploy/about-client-settings.md#client-cache-settings).


## <a name="co-management"></a><a name="bkmk_comgmt"></a>Cogestão

### <a name="improvements-to-co-management-auto-enrollment"></a>Melhorias na cogestão da inscrição automática

- Um novo dispositivo cogerido inscreveu-se automaticamente no serviço Microsoft Intune com base no seu *token* de dispositivo Azure Ative Directory (Azure AD). Não é preciso esperar que um utilizador inicie o contrato para a inscrição automática. Esta alteração ajuda a reduzir o número de dispositivos com o estado de [inscrição](../../../comanage/how-to-monitor.md#co-management-enrollment-status) Pendente de *registo do utilizador*.<!-- 4454491 -->

- Para os clientes que já têm dispositivos matriculados na cogestão, os novos dispositivos matriculam-se imediatamente assim que cumprem os pré-requisitos. Por exemplo, uma vez que o dispositivo é unido ao Azure AD e o cliente do Gestor de Configuração é instalado.<!--4321130-->

Para mais informações, consulte [Enable co-management](../../../comanage/how-to-enable.md).

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>Múltiplos grupos piloto para trabalhos de cogestão

<!--3555750-->
Agora pode configurar diferentes coleções-piloto para cada uma das cargas de trabalho de cogestão. A utilização de diferentes coleções piloto permite-lhe ter uma abordagem mais granular ao deslocar cargas de trabalho.

- No separador **Habilitação,** pode agora especificar uma coleção **de inscrição automática intune.**
    - A coleção **Intune Auto Registration** deve conter todos os clientes que pretende embarcar em cogestão. É essencialmente um superconjunto de todas as outras coleções de encenação.

- No separador **Encenação,** em vez de utilizar uma coleção piloto para todas as cargas de trabalho, pode agora escolher uma coleção individual para cada carga de trabalho.

    ![Co-management O separador Staging permite-lhe escolher uma coleção para cada carga de trabalho](./media/3555750-co-management-staging-tab.png)

Estas opções também estão disponíveis quando permite a cogestão.

Para mais informações, consulte [Enable co-management](../../../comanage/how-to-enable.md).

### <a name="co-management-support-for-government-cloud"></a>Apoio de cogestão para a nuvem do governo

<!--4075452-->
Os clientes do governo dos EUA podem agora usar a cogestão com a Nuvem governamental azure (portal.azure.us). Para mais informações, consulte [Enable co-management](../../../comanage/how-to-enable.md).


## <a name="application-management"></a><a name="bkmk_app"></a>Gestão de aplicações

### <a name="filter-applications-deployed-to-devices"></a>Aplicações de filtro implantadas em dispositivos

<!--4451056-->
As categorias de utilizadores para implementações de aplicações direcionadas para dispositivos mostram agora como filtros no Centro de Software. Especifique uma categoria de **utilizador** para uma aplicação na página do Centro de **Software** das suas propriedades. Em seguida, abra a aplicação no Software Center e veja os filtros disponíveis.

Para mais informações, consulte [Manualmente a informação sobre a aplicação.](../../../apps/deploy-use/create-applications.md#bkmk_manual-app)

### <a name="application-groups"></a>Grupos de candidatura

<!--3555907-->
Crie um conjunto de aplicações que pode enviar para um utilizador ou recolha de dispositivos como uma única implementação. Os metadados que especifica sobre o grupo de aplicações são vistos no Software Center como uma única entidade. Pode encomendar as aplicações no grupo para que o cliente as instale numa encomenda específica.

Esta funcionalidade é pré-lançamento. Para o ativar, consulte [as funcionalidades de pré-lançamento](../../servers/manage/pre-release-features.md).

Para mais informações, consulte [Criar grupos](../../../apps/deploy-use/create-app-groups.md)de aplicação .

### <a name="retry-the-install-of-pre-approved-applications"></a>Voltar a instalar aplicações pré-aprovadas

<!--4336307-->
Agora pode voltar a tentar a instalação de uma aplicação que aprovou anteriormente para um utilizador ou dispositivo. A opção de aprovação é apenas para implementações disponíveis. Se o utilizador desinstalar a aplicação, ou se o processo de instalação inicial falhar, o 'Gestor de Configuração' não reavalia o seu estado e reinstala-a. Esta funcionalidade permite que um técnico de suporte retente rapidamente a instalação da aplicação para um utilizador que pede ajuda.

Para mais informações, consulte [Aprovar aplicações.](../../../apps/deploy-use/app-approval.md)

### <a name="install-an-application-for-a-device"></a>Instalar uma aplicação para um dispositivo

<!--4402180-->
A partir da consola 'Gestor de Configuração', já pode instalar aplicações num dispositivo em tempo real. Esta funcionalidade pode ajudar a reduzir a necessidade de coleções separadas para cada aplicação.

Para mais informações, consulte [Instalar aplicações para um dispositivo](../../../apps/deploy-use/install-app-for-device.md).

### <a name="improvements-to-app-approvals"></a>Melhorias nas aprovações de apps

<!--4224910-->
Esta versão inclui as seguintes melhorias nas aprovações das aplicações:

- Se aprovar um pedido de aplicação na consola e negá-lo, pode agora aprová-lo novamente. A aplicação é reinstalada no cliente depois de a aprovar.  

- Na consola de Gestor de Configuração, espaço de trabalho da Biblioteca de **Software,** sob gestão de **aplicações,** o nó de Pedidos de **Aprovação** é renomeado Pedidos de **Aplicação**.<!-- SCCMDocs-pr#4028 -->

- Há um novo método WMI, **DeleteInstance** para remover um pedido de aprovação de aplicações. Esta ação não desinstala a aplicação no dispositivo. Se ainda não estiver instalada, o utilizador não pode instalar a aplicação a partir do Software Center.

- Ligue para a **API CreateApprovedRequest** para criar um pedido pré-aprovado para uma aplicação num dispositivo. Para evitar a instalação automática da aplicação no cliente, defina o parâmetro **de instalação automática** para `FALSE` . O utilizador vê a aplicação no Centro de Software, mas não está instalada automaticamente.

Para mais informações, consulte [Aprovar aplicações.](../../../apps/deploy-use/app-approval.md)


## <a name="os-deployment"></a><a name="bkmk_osd"></a>Implantação de Os

### <a name="task-sequence-debugger"></a>Debugger de sequência de tarefas

<!--3612274-->
O debugger da sequência de tarefas é uma nova ferramenta de resolução de problemas. Implementa uma sequência de tarefas em modo dedepura para uma coleção de um dispositivo. Permite-lhe passar pela sequência de tarefas de forma controlada para ajudar na resolução de problemas e na investigação.

![Screenshot do debugger da sequência de tarefas](./media/3612274-tsdebug.png)

Esta funcionalidade é pré-lançamento. Para o ativar, consulte [as funcionalidades de pré-lançamento](../../servers/manage/pre-release-features.md).

Para mais informações, consulte [Debug uma sequência](../../../osd/deploy-use/debug-task-sequence.md)de tarefas .

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>Limpar conteúdo de aplicativo a partir da cache do cliente durante a sequência de tarefas

<!--4485675-->
No passo de sequência de **tarefas de instalação da aplicação,** pode agora eliminar o conteúdo da aplicação da cache do cliente após o passo.

Para mais informações, consulte [sobre os passos](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication)da sequência de tarefas .

> [!Important]  
> Atualize o cliente-alvo para a versão mais recente para suportar esta nova funcionalidade.

### <a name="reclaim-sedo-lock-for-task-sequences"></a>Recuperar o bloqueio SEDO para sequências de tarefas

<!--3699337-->
Se a consola do Gestor de Configuração deixar de responder, pode ser bloqueado para não fazer mais alterações numa sequência de tarefas. Agora, quando tentar aceder a uma sequência de tarefas bloqueada, pode agora **descartar alterações**e continuar a editar o objeto.

Para mais informações, consulte [Utilize o editor da sequência de tarefas](../../../osd/understand/task-sequence-editor.md#bkmk_sedo).

### <a name="pre-cache-driver-packages-and-os-images"></a>Pacotes de motorista pré-cache e imagens de SO

<!--4224642-->
A pré-cache da sequência de tarefas inclui agora tipos de conteúdo adicionais. O conteúdo pré-cache anteriormente aplicado apenas a pacotes de upgrade de SO. Agora pode usar pré-cache para reduzir o consumo de largura de banda de:

- Imagens do SO
- Pacotes de controladores
- Pacote

Para mais informações, consulte o [conteúdo pré-cache da Configure](../../../osd/deploy-use/configure-precache-content.md).

### <a name="improvements-to-os-deployment"></a>Melhorias na implantação do OS

Esta versão inclui as seguintes melhorias na implementação do OS:

- Utilize os seguintes dois cmdlets PowerShell para criar e editar o passo de sequência de [tarefas](../../../osd/understand/task-sequence-steps.md#child-task-sequence) executar:<!--2839943-->

    - **Nova CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- Agora é mais fácil editar variáveis quando se executa uma sequência de tarefas. Depois de selecionar uma sequência de tarefas na janela do Assistente da Sequência de Tarefas, a página para editar variáveis de sequência de tarefas inclui um botão **Editar.**<!-- 4668846 --> Para mais informações, consulte [Como utilizar variáveis de sequência de tarefas](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz).

- O passo da sequência **de tarefas Desativação BitLocker** tem um novo contador de reinício. Utilize esta opção para especificar o número de reinícios para manter o BitLocker desativado. Esta alteração ajuda-o a simplificar a sua sequência de tarefas. Pode usar um único passo, em vez de adicionar várias instâncias deste passo. <!--4512937--> Para mais informações, consulte [Disable BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker).

- Utilize a nova variável de sequência de **tarefaS SMSTSRebootDelayNext** com a variável [SMSTSRebootDelayDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) existente. Se quiser que mais tarde ocorram reboots com um tempo limite diferente do primeiro, detete esta nova variável para um valor diferente em segundos. <!--4447680--> Para mais informações, consulte [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext).

- A sequência de tarefas define uma nova variável apenas de leitura **_SMSTSLastContentDownloadLocation**. Esta variável contém o último local onde a sequência de tarefas foi descarregada ou tentou descarregar conteúdo. Inspecione esta variável em vez de analisar os registos do cliente.<!-- 2840337 -->

- Quando cria meios de sequência de tarefas, o Gestor de Configuração não adiciona um ficheiro autorun.inf. Este ficheiro é geralmente bloqueado por produtos antimalware. Ainda pode incluir o ficheiro se necessário para o seu cenário.<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>Melhorias no PXE

A opção 82 durante o aperto de mão PXE DHCP é agora suportada com o resposta PXE sem WDS. A opção 82 não é suportada com a WDS.


## <a name="software-center"></a><a name="bkmk_userxp"></a>Centro de Software

### <a name="improvements-to-software-center-tab-customizations"></a>Melhorias nas personalizações do separador do Software Center

<!--4063773-->
Agora pode adicionar cinco separadores personalizados no Software Center. Também pode editar a ordem em que estes separadores aparecem no Centro de Software.

Para mais informações, consulte [as definições do cliente do Software Center](../../clients/deploy/about-client-settings.md#software-center).

### <a name="software-center-infrastructure-improvements"></a>Melhorias na infraestrutura do Software Center

<!--3555950-->

Este lançamento inclui as seguintes melhorias de infraestrutura para o Centro de Software:

- O Software Center comunica agora com um ponto de gestão para aplicações direcionadas aos utilizadores conforme disponível. Já não usa o catálogo de aplicações. Esta alteração facilita a sua remoção do catálogo de aplicações do site.

- Anteriormente, o Software Center escolheu o primeiro ponto de gestão da lista de servidores disponíveis. A partir deste lançamento, utiliza o mesmo ponto de gestão que o cliente utiliza. Esta alteração permite ao Software Center utilizar o mesmo ponto de gestão do site primário atribuído que o cliente.

> [!Important]  
> Estas melhorias iterativas para o Software Center e o ponto de gestão são para reformar as funções de catálogo de aplicações.
>
> - A experiência do utilizador Silverlight não é suportada a partir da versão atual do ramo 1806.
> - A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações.
> - O suporte termina para as funções de catálogo de aplicações com a versão 1910.  

Para mais informações, consulte [Remova o catálogo de aplicações](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat) e [planeie o Centro](../../../apps/plan-design/plan-for-software-center.md)de Software .

### <a name="redesigned-notification-for-newly-available-software"></a>Notificação redesenhada para software recém-disponível

<!--3555904-->
A notificação **do Novo Software está disponível** só será mostrada uma vez para um utilizador para uma determinada aplicação e revisão. O utilizador deixará de ver a notificação sempre que iniciar sessão. Só verão outra notificação para um pedido se tiver mudado ou sido redistribuído.

Para mais informações, consulte [Criar e implementar uma aplicação](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience).

### <a name="more-frequent-countdown-notifications-for-restarts"></a>Notificações de contagem regressiva mais frequentes para reinícios

<!--3976435-->

Os utilizadores finais serão agora recordados com mais frequência de um reinício pendente com notificações de contagem regressiva intermitentes. Pode definir o intervalo para as notificações intermitentes nas **Definições** do Cliente na página De reiniciar o **computador.** Altere o valor para **Especificar a duração do soneto para as notificações de contagem regressiva do computador (minutos)** para configurar a frequência com que um utilizador é lembrado sobre um reinício pendente até que a notificação final de contagem regressiva ocorra.

Além disso, o valor máximo para **exibir uma notificação temporária ao utilizador que indique o intervalo antes de o utilizador ser desligado ou o computador reiniciar (minutos)** aumentou de 1440 minutos (24 horas) para 20160 minutos (duas semanas).

Para mais informações, consulte notificações de [reinício do Dispositivo](../../clients/deploy/device-restart-notifications.md) e sobre as [definições do cliente](../../clients/deploy/about-client-settings.md#computer-restart).

### <a name="direct-link-to-custom-tabs-in-software-center"></a>Link direto para separadores personalizados no Centro de Software

<!--4655176-->

Agora pode fornecer aos utilizadores um link direto para um [separador personalizado](../../clients/deploy/about-client-settings.md#software-center-tab-visibility) no Software Center.

Utilize o seguinte formato URL para abrir o Centro de Software para um separador específico:

`softwarecenter:page=CustomTab1`

A corda `CustomTab1` é o primeiro separador personalizado em ordem.

Por exemplo, digite este URL na janela Windows **Run.**

Também pode usar esta sintaxe para abrir separadores predefinidos no Centro de Software:

|Linha de comandos  |Tecla de Tabulação  |
|---------|---------|
|`AvailableSoftware`|Aplicações|
|`Updates`|Atualizações|
|`OSD`|Sistemas Operativos|
|`InstallationStatus`|Estado de instalação|
|`Compliance`|Conformidade do dispositivo|
|`Options`|Opções|

Para mais informações, consulte [a visibilidade do separador Do Software Center](../../clients/deploy/about-client-settings.md#software-center-tab-visibility).

## <a name="software-updates"></a><a name="bkmk_sum"></a>Atualizações de software

### <a name="additional-options-for-wsus-maintenance"></a>Opções adicionais para manutenção wSUS

<!--4110109-->
Tem agora tarefas adicionais de manutenção da WSUS que o Gestor de Configuração pode executar para manter pontos de atualização de software saudáveis. A manutenção wSUS ocorre após cada sincronização. Além de declinar atualizações expiradas no WSUS, o Gestor de Configuração pode agora:

- Remova atualizações obsoletas da base de dados wSUS.
- Adicione índices não agrupados à base de dados wSUS para melhorar o desempenho da limpeza wSUS.

Para mais informações, consulte a [manutenção de atualizações](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906)de Software.

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>Configure o tempo máximo de execução padrão para atualizações de software

<!--3734426-->

Pode agora especificar o tempo máximo que uma instalação de atualização de software tem de ser concluída. Pode especificar os seguintes itens no separador Tempo máximo de **execução** no Ponto de Atualização de Software:

- **O tempo máximo de execução para as atualizações de funcionalidades do Windows (minutos)**
- **O tempo máximo de execução para as atualizações do Office 365 e as atualizações sem recurso para windows (minutos)**

Para mais informações, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime)de software .

### <a name="configure-dynamic-update-during-feature-updates"></a>Configure a atualização dinâmica durante as atualizações de funcionalidades

<!--4062619-->

Utilize uma nova definição de cliente para configurar a [Atualização Dinâmica](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) durante as instalações da atualização da funcionalidade Windows 10. A Dynamic Update instala pacotes de idiomas, funcionalidades a pedido, controladores e atualizações cumulativas durante a configuração do Windows, direcionando o cliente para o download destas atualizações a partir da internet.

Para mais informações, consulte as definições do cliente de [atualização de Software](../../clients/deploy/about-client-settings.md#software-updates) e [gerencie o Windows como um serviço](../../../osd/deploy-use/manage-windows-as-a-service.md).

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Novo Windows 10, versão 1903 e mais tarde categoria de produto

<!--4682946-->

**O Windows 10, a versão 1903 e mais tarde** foi adicionado ao Microsoft Update como seu próprio produto, em vez de fazer parte do produto **do Windows 10** como versões anteriores. Esta alteração fez com que fizesse uma série de passos manuais para garantir que os seus clientes vêem estas atualizações. Ajudamos a reduzir o número de passos manuais que tem de tomar para o novo produto.

Quando atualiza para a versão 1906 do Gestor de Configuração e tem o produto **Windows 10** selecionado para sincronização, as seguintes ações ocorrem automaticamente:

- O **Windows 10, a versão 1903 e o** produto posterior são adicionados para sincronização.
- As Regras de Implementação Automática que contêm o produto **Windows 10** serão atualizadas para incluir o **Windows 10, a versão 1903 e mais tarde.**
- Os planos de manutenção são atualizados para incluir o **Windows 10, a versão 1903 e o** produto posterior.

Para mais informações, consulte [classificações e produtos de Configuração para sincronizar,](../../../sum/get-started/configure-classifications-and-products.md) [planos de manutenção](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)e [regras de implementação automáticas.](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)

### <a name="drill-through-required-updates"></a>Perfurar através de atualizações necessárias

<!--4224414-->
Agora pode perfurar as estatísticas de conformidade para ver quais os dispositivos que requerem uma atualização específica do software. Para ver a lista do dispositivo, é necessário permissão para visualizar atualizações e as coleções a que os dispositivos pertencem. Para aprofundar a lista do dispositivo, selecione a hiperligação necessária para **ver** ao lado da tabela de tartes no separador **Resumo** para uma atualização. Clicar na hiperligação leva-o a um nó temporário em **Dispositivos** onde pode ver os dispositivos que necessitam da atualização.

A hiperligação **requerida de visualização** está disponível nos seguintes locais:

   - **Biblioteca de**  >  Software **Atualizações de**  >  software **Todas as atualizações de software**
   - **Biblioteca de**  >  Software Serviço do **Windows 10**  >  **Todas as atualizações do Windows 10**
   - **Biblioteca de**  >  Software **Escritório 365 Gestão de**  >  Clientes **Atualizações do Office 365**

Para mais informações, consulte [as atualizações](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates)de software do Monitor , [Gerencie o Windows como um serviço](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates)e [gerencie as atualizações do Office 365 ProPlus.](../../../sum/deploy-use/manage-office-365-proplus-updates.md#drill-through-required-office-365-updates)


## <a name="office-management"></a><a name="bkmk_o365"></a>Gestão de escritórios

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Painel de prontidão de upgrade do Office 365 ProPlus

<!--4021125-->

Para o ajudar a determinar quais os dispositivos que estão prontos para fazer o upgrade para o Office 365 ProPlus, há um novo painel de instrumentos de prontidão. Inclui o azulejo de prontidão de **atualização do Office 365 ProPlus** que foi lançado na versão atual do Office Manager de Configuração 1902. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software,** expanda o **Office 365 Client Management,** e selecione o nó de prontidão de **atualização do Office 365 ProPlus.**

Para obter mais informações sobre o dashboard, pré-requisitos e utilizando estes dados, consulte a integração para a [prontidão do Office 365 ProPlus](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).


## <a name="protection"></a><a name="bkmk_protect"></a>Proteção

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Critérios de confiança de arquivo de ficheiros do Windows Defender Application Guard

<!--3555858-->

Existe uma nova definição de política que permite aos utilizadores confiar em ficheiros que normalmente se abrem no Windows Defender Application Guard (WDAG). Após a conclusão com sucesso, os ficheiros serão abertos no dispositivo de acolhimento em vez de no WDAG.

Para mais informações, consulte Criar e implementar a política de Guarda de [Aplicações do Windows Defender](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Consola de Gestor de Configuração

### <a name="role-based-access-for-folders"></a>Acesso baseado em papéis para pastas

<!--3600867-->

Agora pode definir os âmbitos de segurança nas pastas. Se tiver acesso a um objeto na pasta ou não tiver acesso à pasta, não poderá ver o objeto. Da mesma forma, se tiver acesso a uma pasta, mas não a um objeto dentro dela, não verá esse objeto. Clique na direita numa pasta, escolha **Definir Âmbitos**de Segurança e, em seguida, escolha os âmbitos de segurança que pretende aplicar.

Para mais informações, consulte [A utilização da consola do Gestor de Configuração](../../servers/manage/admin-console.md#tips) e configurar a [administração baseada em funções.](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder)

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Adicione a coluna SMBIOS GUID aos nódosos de recolha de dispositivos e dispositivos

<!--4526580-->
Tanto nos nós de **Recolha de Dispositivos** como **de Dispositivos,** pode agora adicionar uma nova coluna para **smbios GUID**. Este valor é o mesmo que a propriedade **BIOS GUID** da classe Recursos do Sistema. É um identificador único para o hardware do dispositivo.

### <a name="administration-service-support-for-security-nodes"></a>Apoio ao serviço de administração para os nódosos de segurança

<!--4223683-->
Agora pode permitir que alguns nódosos da consola Do Gestor de Configuração utilizem o serviço de administração. Esta alteração permite que a consola comunique com o Fornecedor SMS em HTTPS em vez de via WMI.

Para mais informações, consulte [o serviço de Administração.](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)

> [!Note]
> A partir da versão 1906, o separador de **comunicação** de computador cliente nas propriedades do site é agora chamado de Segurança da **Comunicação**.<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>Separador de coleções no nó dos dispositivos

<!--4616810-->
No espaço de trabalho **de Ativos e Compliance,** vá ao nó dos **Dispositivos** e selecione um dispositivo. No painel de detalhes, mude para o novo separador **Coleções.** Este separador lista as coleções que incluem este dispositivo.

> [!Note]  
> - Este separador não está atualmente disponível a partir de um subnódoo de dispositivos sob o nó de **Recolha de Dispositivos.** Por exemplo, quando seleciona a opção de **mostrar aos membros** numa coleção.
> - Este separador pode não povoar como esperado para alguns utilizadores. Para ver a lista completa de coleções a que pertence um dispositivo, deve ter a função de segurança **do Administrador Completo.** Trata-se de um problema conhecido. <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>Separador de sequências de tarefas no nó de aplicações

<!--4616810-->
No espaço de trabalho da Biblioteca de **Software,** expandir gestão de **aplicações,** ir ao nó de **Aplicações** e selecionar uma aplicação. No painel de detalhes, mude para o novo separador de **sequências de tarefas.** Este separador lista as sequências de tarefas que referem esta aplicação.

### <a name="show-collection-name-for-scripts"></a>Mostrar nome de coleção para scripts

<!--4616810-->
No espaço de trabalho **de monitorização,** selecione o nó do Estado do **Script.** Agora lista o **Nome de Recolha** para além do ID.

### <a name="real-time-actions-from-device-lists"></a>Ações em tempo real a partir de listas de dispositivos

<!--4616810-->
Existem várias formas de apresentar uma lista de dispositivos sob o nó de **Dispositivos** no espaço de trabalho **De Ativos e Compliance.**

- No espaço de trabalho **De Ativos e Compliance,** selecione o nó de **Recolha de Dispositivos.** Selecione uma coleção de dispositivos e escolha a ação para **mostrar aos membros**. Esta ação abre um subnódoo do nó dos **Dispositivos** com uma lista de dispositivos para essa recolha.  

  - Ao selecionar o subnódoo da coleção, pode agora iniciar a **CMPivot** do grupo Coleção da fita.  

- No espaço de trabalho **de monitorização,** selecione o nó de **Implantação.** Selecione uma implementação e escolha a ação **'Ver Status'** na fita. No painel de estado de implantação, clique duas vezes no total dos ativos para perfurar uma lista de dispositivos.  

  - Quando selecionar um dispositivo nesta lista, pode agora iniciar **cmPivot** e **executar scripts** do grupo dispositivo da fita.  

### <a name="order-by-program-name-in-task-sequence"></a>Ordem por nome de programa na sequência de tarefas

<!--4616810-->
No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.** Editar uma sequência de tarefas e selecionar ou adicionar o passo ['Pacote instalação'.](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) Se um pacote tem mais de um programa, a lista de abandono supor agora os programas alfabeticamente.

### <a name="correct-names-for-client-operations"></a>Nomes corretos para operações de clientes

<!--4616810-->
No espaço de trabalho **de Monitorização,** selecione **Operações de Cliente.** A operação para mudar para o próximo Ponto de **Atualização** de Software está agora devidamente nomeada.


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a>Funcionalidades e sistemas operativos degradados

Saiba mais sobre as alterações de suporte antes de serem implementadas em [itens removidos e depreciados](deprecated/removed-and-deprecated.md).

A versão 1906 deixa cair o suporte para as seguintes funcionalidades:  

- Não é possível instalar novas funções de catálogo de aplicações. Os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Para mais informações, consulte [Plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).

A versão 1906 deprecia o suporte aos seguintes produtos:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>Outras atualizações

A partir desta versão, as seguintes funcionalidades deixaram de ser pré-lançamento:

- [Serviço de administração do SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Gestão do Controlo de Aplicações do Windows Defender](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Além de novas funcionalidades, esta versão também inclui alterações adicionais, tais como correções de bugs. Para mais informações, consulte [resumo das alterações no atual ramo do Gestor de Configuração, versão 1906](https://support.microsoft.com/help/4514258).

Para obter mais informações sobre as alterações nas cmdlets do Windows PowerShell para O Gestor de Configuração, consulte [as notas de lançamento da versão PowerShell de 1906](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps).

O rollup de atualização seguinte (4517869) está disponível na consola a partir de 1 de outubro de 2019: Rollup de atualização para o ramo atual do Gestor de [Configuração, versão 1906](https://support.microsoft.com/help/4517869).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Próximos passos

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
A partir de 16 de agosto de 2019, a versão 1906 está globalmente disponível para todos os clientes instalarem.

Quando estiver pronto para instalar esta versão, consulte [a instalação de atualizações para O Gestor](../../servers/manage/updates.md) de Configuração e lista de [verificação para instalar a atualização 1906](../../servers/manage/checklist-for-installing-update-1906.md).

> [!TIP]  
> Para instalar um novo site, utilize uma versão de base do Gestor de Configuração.  
>
> Saiba mais sobre:
>
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)  

Para questões conhecidas e significativas, consulte as notas de [lançamento.](../../servers/deploy/install/release-notes.md)

Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).
