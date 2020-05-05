---
title: Referência dos ficheiros de registo
titleSuffix: Configuration Manager
description: Uma referência de todos os ficheiros de registo para clientes, servidor e componentes dependentes do Gestor de Configuração.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36ab89f1e9988adc167bf69ff7d9f53b02bbe10f
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166545"
---
# <a name="log-file-reference"></a>Referência dos ficheiros de registo

*Aplica-se a: Gestor de Configuração (ramo atual)*

No Gestor de Configuração, os componentes do cliente e do servidor do site registam informações sobre o processo em ficheiros de registo individuais. Pode utilizar a informação nestes ficheiros de registo para o ajudar a resolver problemas que possam ocorrer. Por predefinição, o Gestor de Configuração permite o registo de componentes de clientes e servidores.

Para obter informações mais gerais sobre ficheiros de registo no 'Gestor de Configuração', consulte [sobre ficheiros de registo](about-log-files.md). Este artigo inclui informações sobre as ferramentas a utilizar, como configurar os registos e onde encontrá-los.

As seguintes secções fornecem detalhes sobre os diferentes ficheiros de registo disponíveis para si. Monitorize os registos do cliente e do servidor do Gestor de Configuração para obter detalhes de operação e veja informações de erro para resolver problemas.  

- [Ficheiros de registo do cliente](#BKMK_ClientLogs)  

  - [Operações de clientes](#BKMK_ClientOpLogs)  

  - [Instalação do cliente](#BKMK_ClientInstallLog)  

  - [Cliente para Linux e UNIX](#BKMK_LogFilesforLnU)  

  - [Cliente para computadores Mac](#BKMK_LogfilesforMac)  

- [Ficheiros de registo do servidor](#BKMK_ServerLogs)  

  - [Servidor do site e sistemas de sites](#BKMK_SiteSiteServerLog)  

  - [Instalação do servidor do site](#BKMK_SiteInstallLog)

  - [Ponto de serviço de armazém de dados](#BKMK_DataWarehouse)

  - [Ponto de estado de contingência](#BKMK_FSPLog)  

  - [Ponto de gestão](#BKMK_MPLog)  

  - [Ponto de ligação de serviço](#BKMK_WITLog)  

  - [Ponto de atualização de software](#BKMK_SUPLog)  

- [Registar ficheiros por funcionalidade](#BKMK_FunctionLogs)  

  - [Gestão de aplicações](#BKMK_AppManageLog)  

  - [Asset Intelligence](#BKMK_AILog)  

  - [Cópia de segurança e recuperação](#BKMK_BnRLog)  

  - [Inscrição de certificado](#BKMK_CertificateEnrollment)

  - [Notificação do cliente](#BKMK_BGB)

  - [Gateway de gestão da cloud](#cloud-management-gateway)

  - [Definições de conformidade e acesso a recursos da empresa](#BKMK_CompSettingsLog)  

  - [Consola do Configuration Manager](#BKMK_ConsoleLog)  

  - [Gestão de conteúdos](#BKMK_ContentLog)  

  - [Análise de Computadores](#desktop-analytics)

  - [Descoberta](#BKMK_DiscoveryLog)  

  - [Endpoint Protection](#BKMK_EPLog)  

  - [Extensões](#BKMK_Extensions)  

  - [Inventário](#BKMK_InventoryLog)  

  - [Migração](#BKMK_MigrationLog)  

  - [Dispositivos móveis](#BKMK_MDMLog)  

  - [Implementação de SO](#BKMK_OSDLog)  

  - [Gestão de energia](#BKMK_PowerMgmtLog)  

  - [Controlo remoto](#BKMK_RCLog)  

  - [Relatórios](#BKMK_ReportLog)  

  - [Administração baseada em funções](#BKMK_RBALog)  

  - [Medição de software](#BKMK_MeteringLog)  

  - [Atualizações de software](#BKMK_SU_NAPLog)  

  - [Acordar na LAN](#BKMK_WOLLog)  

  - [Serviço do Windows 10](#BKMK_WindowsServicingLog)

  - [Windows Update Agent](#BKMK_WULog)  

  - [Servidor WSUS](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a>Ficheiros de registo do cliente

As seguintes secções listam os ficheiros de registo relacionados com operações de cliente e instalação do cliente.  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a>Operações de clientes

A tabela seguinte lista os ficheiros de registo localizados no cliente do Gestor de Configuração.  

|Nome do registo|Descrição|  
|--------------|-----------------|  
|ADALOperationProvider.log|Informações sobre pedidos simbólicos de autenticação de clientes com a Biblioteca de Autenticação (Azure AD) do Diretório Ativo (ADAL).|
|BitLockerManagementHandler.log|Regista informações sobre as políticas de gestão do BitLocker.|
|CAS.log|O serviço de Acesso ao Conteúdo. Mantém a cache do pacote local no cliente.|  
|Ccm32BitLauncher.log|Regista ações para iniciar aplicações no cliente *marcadas como 32 bits*.|  
|CcmEval.log|Regista atividades de avaliação do estado do cliente do Gestor de Configuração e detalhes para componentes que são exigidos pelo cliente do Gestor de Configuração.|  
|CcmEvalTask.log|Regista as atividades de avaliação do estado do cliente do Gestor de Configuração que são iniciadas pela tarefa agendada de avaliação.|  
|CcmExec.log|Regista atividades do cliente e do serviço Anfitrião de Agente do SMS. Este ficheiro de registo também inclui informações sobre como ativar e desativar o proxy de reativação.|  
|CcmMessaging.log|Regista atividades relacionadas com a comunicação entre o cliente e os pontos de gestão.|  
|CCMNotificationAgent.log|Regista atividades relacionadas com as operações de notificação de cliente.|  
|Ccmperf.log|Regista atividades relacionadas com a manutenção e a captura de dados relacionados com os contadores de desempenho do cliente.|  
|CcmRestart.log|Regista a atividade de reinício do serviço de cliente.|  
|CCMSDKProvider.log|Regista atividades das interfaces SDK do cliente.|  
|ccmsqlce.log|Grava atividades para a SQL Compact Edition que o cliente utiliza. Este registo é normalmente utilizado apenas quando ativa o abate de depuração, ou há um problema com o componente. A tarefa de saúde do cliente (ccmeval) normalmente corrige os problemas com esta componente.|
|CertificateMaintenance.log|Mantém certificados para os Serviços de Domínio do Active Directory e os pontos de gestão.|  
|CIDownloader.log|Regista detalhes sobre transferências de definições de itens de configuração.|  
|CITaskMgr.log|Registre tarefas para cada aplicação e tipo de implementação, tais como descarregamento de conteúdo e instalação ou desinstalação de ações.|  
|ClientAuth.log|Registos de assinatura e autenticação para o cliente.|  
|ClientIDManagerStartup.log|Cria e mantém o cliente GUID e identifica tarefas durante o registo e atribuição do cliente.|  
|ClientLocation.log|Regista tarefas relacionadas com a atribuição do site do cliente.|  
|CMHttpsReadiness.log|Regista os resultados da execução da Ferramenta de Avaliação de Prontidão HTTPS do Gestor de Configuração. Esta ferramenta verifica se os computadores têm um certificado de autenticação de cliente de infraestrutura de chave pública (PKI) que pode ser usado com O Gestor de Configuração.|  
|CmRcService.log|Regista informações para o serviço de controlo remoto.|  
|CoManagementHandler.log|Use para resolver problemas de cogestão no cliente.|
|ContentTransferManager.log|Agenda o Serviço de Transferência Inteligente de Fundo (BITS) ou bloco de mensagens de servidor (SMB) para descarregar ou aceder a pacotes.|  
|DataTransferService.log|Regista todas as comunicações BITS para acesso a políticas ou pacotes.|  
|DeltaDownload.log|Regista informações sobre o download de atualizações expressas e atualizações descarregadas através da Otimização de Entrega.|  
|Diagnóstico.log|Regista o estado das ações de diagnóstico do cliente.|
|EndpointProtectionAgent|Regista informações sobre a instalação do cliente de Proteção endpoint do System Center e a aplicação da política antimalware a esse cliente.|  
|execmgr.log|Regista detalhes dos pacotes e sequências de tarefas que são executados no cliente.|  
|ExpressionSolver.log|Regista detalhes sobre métodos de deteção melhorados que são usados quando a exploração verbosa ou depurada é ativada.|  
|ExternalEventAgent.log|Regista o histórico de deteção de malware do Endpoint Protection e eventos relacionados com o estado do cliente.|  
|FileBITS.log|Regista todas as tarefas de acesso do pacote SMB.|  
|FileSystemFile.log|Regista a atividade do fornecedor do Windows Management Instrumentation (WMI) para recolha de ficheiros e inventário de software.|  
|FSPStateMessage.log|Regista a atividade de mensagens de estado que são enviadas pelo cliente para o ponto de estado de contingência.|  
|InternetProxy.log|Regista a configuração de procuração de rede e utiliza a atividade para o cliente.|  
|InventoryAgent.log|Regista atividades de inventário de hardware, inventário de software e ações de deteção de heartbeat no cliente.|  
|LocationCache.log|Regista a atividade de utilização e manutenção de cache de localização para o cliente.|  
|LocationServices.log|Regista a atividade do cliente para localizar pontos de gestão, pontos de atualização de software e pontos de distribuição.|  
|M365AHandler.log|Informações sobre a política de definições de Desktop Analytics|
|MaintenanceCoordinator.log|Regista a atividade para tarefas gerais de manutenção para o cliente.|  
|Mifprovider.log|Regista a atividade do fornecedor wMI para ficheiros de formato de informação de gestão (MIF).|  
|mtrmgr.log|Monitoriza todos os processos de medição de software.|  
|PolicyAgent.log|Regista pedidos de políticas efetuadas através do Serviço de Transferência de Dados.|  
|PolicyAgentProvider.log|Regista alterações de política.|  
|PolicyEvaluator.log|Regista detalhes sobre a avaliação das políticas em computadores cliente, incluindo políticas de atualizações de software.|  
|PolicyPlatformClient.log|Regista o processo de reparação e conformidade de todos os fornecedores localizados na \Program Files\Microsoft Policy Platform, exceto o fornecedor de ficheiros.|  
|PolicySdk.log|Regista atividades das interfaces SDK do sistema de políticas.|  
|Pwrmgmt.log|Regista informações sobre a ativação ou desativação e a configuração de definições de cliente do proxy de reativação.|  
|PwrProvider.log|Regista as atividades do fornecedor de gestão de energia (PWRInvProvider) hospedados no serviço WMI. Em todas as versões suportadas do Windows, o fornecedor enumera as definições atuais nos computadores durante o inventário de hardware e aplica as definições do plano de energia.|  
|SCClient_&lt;*nome*de\>utilizador de*domínio*\>@&lt;_1.log|Regista a atividade no Centro de Software para o utilizador especificado no computador cliente.|  
|SCClient_&lt;*nome*de\>utilizador de*domínio*\>@&lt;_2.log|Regista a atividade do histórico no Centro de Software para o utilizador especificado no computador cliente.|  
|Scheduler.log|Regista atividades de tarefas agendadas para todas as operações de cliente.|  
|SCNotify_&lt;*nome*de\>utilizador de*domínio*\>@&lt;_1.log|Regista a atividade para notificar os utilizadores sobre software para o utilizador especificado.|  
|SCNotify_&lt;*domain*\>@&lt;nome de\>&lt;*utilizador*de domínio _1-*date_time*>.log|Regista a informação do histórico para notificar os utilizadores sobre software para o utilizador especificado.|  
|setuppolicyevaluator.log|Regista a configuração e a criação da política de inventário no WMI.|  
|&lt;*domínio* SleepAgent_\>@SYSTEM_0.log|O ficheiro principal de registo para procuração de despertar.|  
|smscliui.log|Utilização de registos do cliente do Gestor de Configuração no Painel de Controlo.|  
|SrcUpdateMgr.log|Regista a atividade das aplicações do Windows Installer instaladas que são atualizadas com as localizações de origem do ponto de distribuição atual.|  
|StatusAgent.log|Regista mensagens de estado que são criadas pelos componentes de cliente.|  
|SWMTRReportGen.log|Gera um relatório de dados de uso que é recolhido pelo agente de medição. Estes dados são registados no ficheiro Mtrmgr.log.|  
|UserAffinity.log|Regista detalhes sobre a afinidade de dispositivo do utilizador.|  
|VirtualApp.log|Regista informações específicas para a avaliação dos tipos de implementação de implementação de aplicações virtualização (App-V).|  
|Wedmtrace.log|Regista operações relacionadas com filtros de escrita nos clientes do Windows Embedded.|  
|wakeprxy-install.log|Registre informações de instalação quando os clientes recebem a opção de definição do cliente para ativar o proxy de despertar.|  
|wakeprxy-uninstall.log|Regista informações sobre a desinstalação de procuração de despertar quando os clientes recebem a opção de definição de cliente para desligar o proxy de despertar, se o procuramento de despertar foi previamente ligado.|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a>Instalação do cliente

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a instalação do cliente do Gestor de Configuração.  

|Nome do registo|Descrição|  
|--------------|-----------------|  
|ccmsetup.log|Regista tarefas ccmsetup.exe para configuração do cliente, atualização do cliente e remoção do cliente. Pode ser utilizado para resolver problemas de instalação de cliente.|  
|ccmsetup-ccmeval.log|Regista tarefas ccmsetup.exe para o estado do cliente e reparação.|  
|CcmRepair.log|Regista as atividades de reparação do agente de cliente.|  
|Client.msi.log|Gravações de configuração tarefas feitas por cliente.msi. Pode ser utilizado para resolver problemas de instalação ou remoção de clientes.|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a>Cliente da Linux e da UNIX

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX.
>
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

O cliente do Gestor de Configuração do Linux e da UNIX regista informações nos seguintes ficheiros de registo:  

> [!TIP]
> Utilize o CMTrace para visualizar os ficheiros de registo do cliente para linux e UNIX.

|Nome do registo|Detalhes|
|-------------------|-----------------------------------------------------------------|
|Scxcm.log| O ficheiro de registo do serviço principal do cliente do Gestor de Configuração para o Linux e o UNIX (ccmexec.bin). Este ficheiro de registo contém informações sobre a instalação e as operações do ccmexec.bin. em curso Por predefinição, este ficheiro de registo está localizado em **/var/opt/microsoft/scxcm.log**. Para alterar a localização do ficheiro de registo, edite **/opt/microsoft/configmgr/etc/scxcm.conf** e altere o campo **PATH**. Não precisa de reiniciar o computador ou serviço do cliente para que a mudança faça efeito. Pode definir o nível de registo para uma de quatro configurações diferentes. |
| Scxcmprovider.log |O ficheiro de registo do serviço CIM do cliente do Gestor de Configuração para o Linux e o UNIX (omiserver.bin). Este ficheiro de registo contém informações sobre as operações do nwserver.bin em curso. Este tronco está `/var/opt/microsoft/configmgr/scxcmprovider.log`localizado a . Para alterar a localização do ficheiro de registo, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** e altere o campo **PATH**. Não precisa de reiniciar o computador ou serviço do cliente para que a mudança faça efeito. Pode definir o nível de registo para uma de três definições.|

Ambos os ficheiros de registo suportam vários níveis de registo:  

- **scxcm.log**. Para alterar o nível de registo, **edite/opt/microsoft/configmgr/etc/scxcm.conf** e altere cada instância da etiqueta **MÓDULO** para o nível de registo que deseja:  

  - ERRO: Indica problemas que requerem atenção  

  - AVISO: Indica possíveis problemas para operações de clientes  

  - INFORMAÇÃO: Registo saqueado mais detalhado que indica o estado de vários eventos no cliente  

  - TRACE: Madeireiro verboso que normalmente é usado para diagnosticar problemas  

- **scxcmprovider.log**. Para alterar o nível de registo, **edite/opt/microsoft/omi/etc/scxcmprovider.conf** e altere cada instância da etiqueta **MÓDULO** para o nível de registo que deseja:  

  - ERRO: Indica problemas que requerem atenção  

  - AVISO: Indica possíveis problemas para operações de clientes

  - INFORMAÇÃO: Registo saqueado mais detalhado que indica o estado de vários eventos no cliente  

Em condições normais de funcionamento, utilize o nível de registo ERROR. Este nível de registo cria o menor ficheiro de registo. À medida que o nível de registo é aumentado de ERROR para WARNING, para INFO, e depois para TRACE, um ficheiro de registo maior é criado à medida que mais dados são escritos para o ficheiro.  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a>Gerir ficheiros de registo para o cliente Linux e UNIX

O cliente da Linux e da UNIX não limita o tamanho máximo dos ficheiros de registo do cliente. Também não copia automaticamente o conteúdo dos seus ficheiros .log para outro ficheiro, como um ficheiro .lo_. Se pretender controlar o tamanho máximo dos ficheiros de registo, implemente um processo para gerir os ficheiros de registo independentes do cliente do Gestor de Configuração para o Linux e uniX.  

Por exemplo, pode utilizar o **logrotate** de comando padrão Linux e UNIX para gerir o tamanho e rotação dos ficheiros de registo do cliente. O cliente do Gestor de Configuração do Linux e da UNIX tem uma interface que permite o **logrotate** sinalizar o cliente quando a rotação de registo saca, para que o cliente possa retomar a sessão de log ingime no ficheiro de registo.  

Para obter informações sobre o comando **logrotate**, veja a documentação das distribuições de Linux e UNIX que utiliza.  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a>Cliente para computadores Mac

O cliente do Gestor de Configuração para computadores Mac regista informações nos seguintes ficheiros de registo no computador Mac:  

|Nome do registo|Detalhes|Localização|
|--------------|-------------|-------------|
|CCMClient-&lt;*date_time*>.log|Regista atividades relacionadas com as operações do cliente Mac, incluindo gestão de aplicações, inventário e registo de erros.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent-date_time&lt;*date_time*>.log|Regista informações relacionadas com operações de clientes, incluindo o utilizador iniciar sessão e iniciar operações, e atividade informática Mac.| `~/Library/Logs`|  
|CCMNotifications-&lt;*date_time*>.log|Regista atividades relacionadas com notificações do Gestor de Configuração exibidas no computador Mac.| `~/Library/Logs`|  
|CCMPrefPane-&lt;*date_time*>.log|Regista atividades relacionadas com as preferências do Gestor de Configuração no computador Mac, que inclui o estado geral e o registo de erros.| `~/Library/Logs`|  

O ficheiro de registo **SMS_DM.log** no servidor do sistema do site também regista a comunicação entre os computadores Mac e o ponto de gestão que é configurado para dispositivos móveis e computadores Mac.  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a>Ficheiros de registo do servidor

As seguintes secções listam ficheiros de registo que estão no servidor do site ou que estão relacionados com funções específicas do sistema do site.  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a>Sistemas de servidores e sites do site

A tabela seguinte lista os ficheiros de registo que estão no servidor do servidor do Site do Gestor de Configuração e nos servidores do sistema do site.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Regista a atividade de processamento de registo.|Servidor do site|  
|ADForestDisc.log|Regista ações da Deteção de Florestas do Active Directory.|Servidor do site|  
|adminservice.log|Regista ações para o serviço de administração do SMS Provider REST API|Computador com o Fornecedor de SMS|
|ADService.log|Regista detalhes sobre grupos de segurança e a criação de contas no Active Directory.|Servidor do site|  
|adsgdis.log|Regista ações da Deteção de Grupos do Active Directory.|Servidor do site|  
|adsysdis.log|Regista ações da Deteção de Sistemas do Active Directory.|Servidor do site|  
|adusrdis.log|Regista ações da Deteção de Utilizadores do Active Directory.|Servidor do site|  
|BusinessAppProcessWorker.log|Processamento de registos para aplicações microsoft Store para empresas.|Servidor do site|
|ccm.log|Registre atividades para instalação de push do cliente.|Servidor do site|  
|CertMgr.log|Regista atividades de certificados para comunicação intralocal.|Servidor do sistema de sites|  
|chmgr.log|Regista atividades do gestor de estado de funcionamento de cliente.|Servidor do site|  
|Cidm.log|Regista alterações das definições de cliente efetuadas pelo CIDM (Client Install Data Manager).|Servidor do site|  
|CollectionAADGroupSyncWorker.log | A partir da versão 2002, registro arquivo para sincronização dos resultados da associação de recolha para o Diretório Ativo Azure. Na versão 1910 e anterior, o registo para esta funcionalidade foi combinado em SMS_AZUREAD_DISCOVERY_AGENT.log. | Servidor do site|
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do site|  
|compmon.log|Regista o estado de threads de componentes monitorizados para o servidor do site.|Servidor do sistema de sites|  
|compsumm.log|Regista tarefas do Summarizer de Estado do Componente.|Servidor do site|  
|ComRegSetup.log|Regista a instalação inicial de resultados de registo COM para um servidor do site.|Servidor do sistema de sites|  
|dataldr.log|Regista informações sobre o processamento de ficheiros MIF e inventário de hardware na base de dados do Gestor de Configuração.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|despool.log|Regista transferências de comunicação site a site recebidas.|Servidor do site|  
|distmgr.log|Regista detalhes sobre a criação de pacotes, compressão, replicação de diferenças e atualizações de informações. Também pode incluir outras atividades da componente do gestor de distribuição. Por exemplo, instalar um ponto de distribuição, tentativas de ligação e instalar componentes. Para obter mais informações sobre outras funcionalidades que utilizam este registo, consulte o ponto de [ligação](#BKMK_WITLog) do serviço e [a implementação do OS](#BKMK_OSDLog).|Servidor do site|  
|EPCtrlMgr.log|Regista informações sobre a sincronização de informações de ameaça de malware do servidor de funções do site Endpoint Protection com a base de dados do Gestor de Configuração.|Servidor do site|  
|EPMgr.log|Regista o estado da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EPSetup.log|Fornece informações sobre a instalação da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EnrollSrv.log|Regista atividades do processo do serviço de registo.|Servidor do sistema de sites|  
|EnrollWeb.log|Regista atividades do processo do Web site de registo.|Servidor do sistema de sites|  
|fspmgr.log|Regista atividades da função de sistema de sites do ponto de estado de contingência.|Servidor do sistema de sites|  
|hman.log|Regista informações sobre alterações na configuração do site e sobre a publicação de informações do site em Serviços de Domínio de Diretório Ativo.|Servidor do site|  
|Inboxast.log|Regista os ficheiros que são movidos do ponto de gestão para a pasta A RECEBER correspondente no servidor do site.|Servidor do site|  
|inboxmgr.log|Regista atividades de transferência de ficheiros entre pastas A Receber.|Servidor do site|  
|inboxmon.log|Regista o processamento de ficheiros a receber e atualizações de contadores de desempenho.|Servidor do site|  
|invproc.log|Regista o reencaminhamento de ficheiros MIF de um site secundário para o seu site principal.|Servidor do site|  
|migmctrl.log|Regista informações sobre ações de migração que envolvam empregos migratórios, pontos de distribuição partilhados e atualizações de pontos de distribuição.|Site de alto nível na hierarquia do Gestor de Configuração, e cada local primário infantil. Numa hierarquia multiprimária do site, utilize o ficheiro de registo que é criado no site da administração central.|  
|mpcontrol.log|Regista o registo do ponto de gestão com o Windows Internet Name Service (WINS). Regista a disponibilidade do ponto de gestão a cada 10 minutos.|Servidor do sistema de sites|  
|mpfdm.log|Regista as ações do componente do ponto de gestão que move ficheiros de cliente para a pasta A RECEBER correspondente no servidor do site.|Servidor do sistema de sites|  
|mpMSI.log|Regista detalhes sobre a instalação do ponto de gestão.|Servidor do site|  
|MPSetup.log|Regista o processo do wrapper de instalação do ponto de gestão.|Servidor do site|  
|netdisc.log|Regista ações da Deteção de Rede.|Servidor do site|  
|NotiCtrl.log|Notificações de pedido de pedido de pedido.|Servidor do site|  
|ntsvrdis.log|Regista a atividade de deteção de servidores de sistema de sites.|Servidor do site|  
|Objreplmgr|Regista o processamento de notificações de alteração de objetos para replicação.|Servidor do site|  
|offermgr.log|Regista atualizações de anúncios.|Servidor do site|  
|offersum.log|Regista o resumo das mensagens de estado de implementação.|Servidor do site|  
|OfflineServicingMgr.log|Regista as atividades de aplicação de atualizações a ficheiros de imagem de sistema operativo.|Servidor do site|  
|outboxmon.log|Regista o processamento de ficheiros a enviar e atualizações de contadores de desempenho.|Servidor do site|  
|PerfSetup.log|Regista os resultados da instalação de contadores de desempenho.|Servidor do sistema de sites|  
|PkgXferMgr.log|Regista as ações do componente SMS_Executive que é responsável pelo envio de conteúdo de um site primário para um ponto de distribuição remoto.|Servidor do site|  
|policypv.log|Regista as atualizações das políticas de cliente para refletir as alterações das implementações ou definições de cliente.|Servidor do site principal|  
|rcmctrl.log|Regista as atividades de replicação de base de dados entre sites na hierarquia.|Servidor do site|  
|replmgr.log|Regista a replicação de ficheiros entre os componentes do servidor do site e o componente do Programador.|Servidor do site|  
|ResourceExplorer.log|Regista erros, avisos e informações sobre executar o Resource Explorer.|Computador que executa a consola De Configuração Manager|  
|RESTPROVIDERSetup.log|Instalação do serviço de administração sms provider REST API|Computador com o Fornecedor de SMS|
|ruleengine.log|Regista detalhes sobre regras de implementação automática para a identificação, transferência de conteúdo e criação de implementação e de grupos de atualização de software.|Servidor do site|  
|Schedule.log|Regista detalhes sobre replicação de ficheiros e tarefas site a site.|Servidor do site|  
|Sender.log|Regista os ficheiros que são transferidos entre sites através de replicação baseada em ficheiros.|Servidor do site|  
|sinvproc.log|Regista informações sobre o processamento de dados de inventário de software para a base de dados do site.|Servidor do site|  
|sitecomp.log|Regista detalhes sobre a manutenção dos componentes instalados do site em todos os servidores de sistema de sites do site.|Servidor do site|  
|sitectrl.log|Regista as alterações de definições do site efetuadas nos objetos de controlo do site na base de dados.|Servidor do site|  
|sitestat.log|Regista a disponibilidade e o processo de monitorização do espaço em disco de todos os sistemas.|Servidor do site|
|SMS_AZUREAD_DISCOVERY_AGENT.log| Ficheiro de log para azure Ative Directory (Azure AD) utilizador e descoberta do grupo de utilizadores. Na versão 1910 e anterior, também incluiu sincronização dos resultados da adesão à Azure AD.| Servidor do site|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|Ficheiro de registo para componente que sincroniza aplicações da Microsoft Store for Business.|Servidor do site|
|SMS_ISVUPDATES_SYNCAGENT.log| Ficheiro de registo para sincronização de atualizações de software de terceiros.| Ponto de atualização de software de alto nível na hierarquia do Gestor de Configuração.|
|SMS_OrchestrationGroup.log| Arquivo de registo para grupos de orquestração|Servidor do site|
|SMS_PhasedDeployment.log| Ficheiro de registo para implementações faseadas|Site de alto nível na hierarquia do Gestor de Configuração|
|SMS_REST_PROVIDER.log|Estado de saúde de serviço para o serviço de administração do Prestador SMS REST API, incluindo informações sobre certificados|Computador com o Fornecedor de SMS|
|SmsAdminUI.log|Atividade da consola Do Gestor de Configuração de Registos.|Computador que executa a consola De Configuração Manager|  
|SMSAWEBSVCSetup.log|Regista as atividades de instalação do serviço Web do Catálogo de Aplicações.|Servidor do sistema de sites|  
|smsbkup.log|Regista a saída do processo de cópia de segurança do site.|Servidor do site|  
|smsdbmon.log|Regista alterações de bases de dados.|Servidor do site|  
|SMSENROLLSRVSetup.log|Regista as atividades de instalação do serviço Web de registo.|Servidor do sistema de sites|  
|SMSENROLLWEBSetup.log|Regista as atividades de instalação do Web site de registo.|Servidor do sistema de sites|  
|smsexec.log|Regista o processamento de todos os threads de componentes de servidor do site.|Servidor do site ou servidor de sistema de sites|  
|SMSFSPSetup.log|Regista mensagens geradas pela instalação de um ponto de estado de contingência.|Servidor do sistema de sites|  
|SMSPORTALWEBSetup.log|Regista as atividades de instalação do Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|SMSProv.log|Regista o acesso do fornecedor WMI à base de dados do site.|Computador com o Fornecedor de SMS|  
|srsrpMSI.log|Regista resultados detalhados do processo de instalação do ponto de relatório a partir da saída MSI.|Servidor do sistema de sites|  
|srsrpsetup.log|Regista resultados do processo de instalação do ponto de relatório.|Servidor do sistema de sites|  
|statesys.log|Regista o processamento de mensagens de sistema de estado.|Servidor do site|  
|statmgr.log|Regista a escrita de todas as mensagens de estado na base de dados.|Servidor do site|  
|swmproc.log|Regista o processamento de ficheiros e definições de medição.|Servidor do site|  

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a>Instalação do servidor do site

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a instalação do site.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Regista atividades pré-requisitos de avaliação e instalação de componentes.|Servidor do site|  
|ConfigMgrSetup.log|Regista uma saída detalhada da configuração do servidor do site.|Servidor do Site|  
|ConfigMgrSetupWizard.log|Regista informações relacionadas com a atividade no Assistente de Configuração.|Servidor do Site|  
|SMS_BOOTSTRAP.log|Regista informações sobre o progresso do início do processo de instalação do site secundário. Os detalhes do processo de configuração estão contidos no ficheiro ConfigMgrSetup.log.|Servidor do Site|  
|smstsvc.log|Regista informações sobre a instalação, utilização e remoção de um serviço Windows. O Windows utiliza este serviço para testar a conectividade da rede e as permissões entre servidores. Utiliza a conta de computador do servidor que cria a ligação.|Servidor do site e servidor do sistema do site|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a>Ponto de serviço de armazém de dados

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de serviço do armazém de dados.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|DWSSMSI.log|Regista mensagens geradas pela instalação de um ponto de serviço de armazém de dados.|Servidor do sistema de sites|  
|DWSSSetup.log|Regista mensagens geradas pela instalação de um ponto de serviço de armazém de dados.|Servidor do sistema de sites|  
|Microsoft.ConfigMgrDataWarehouse.log|Regista informações sobre a sincronização de dados entre a base de dados do site e a base de dados do armazém de dados.|Servidor do sistema de sites|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a>Ponto de estado de recuo

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de estado de contingência.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Regista detalhes sobre comunicações com o ponto de estado de contingência a partir de clientes legados de dispositivos móveis e de computadores cliente.|Servidor do sistema de sites|  
|fspMSI.log|Regista mensagens geradas pela instalação de um ponto de estado de contingência.|Servidor do sistema de sites|  
|fspmgr.log|Regista atividades da função de sistema de sites do ponto de estado de contingência.|Servidor do sistema de sites|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a>Ponto de gestão

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de gestão.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Regista atividades de mensagens de cliente no ponto final.|Servidor do sistema de sites|  
|MP_CliReg.log|Regista a atividade de registo de cliente processada pelo ponto de gestão.|Servidor do sistema de sites|  
|MP_Ddr.log|Grava a conversão de registos XML.ddr de clientes e, em seguida, copia-os para o servidor do site.|Servidor do sistema de sites|  
|MP_Framework.log|Regista as atividades do ponto de gestão central e dos componentes da estrutura de cliente.|Servidor do sistema de sites|  
|MP_GetAuth.log|Regista a atividade de autorização de cliente.|Servidor do sistema de sites|  
|MP_GetPolicy.log|Regista a atividade de pedidos de política de computadores cliente.|Servidor do sistema de sites|  
|MP_Hinv.log|Regista detalhes sobre a conversão de registos de inventário de hardware XML a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|  
|MP_Location.log|Regista a atividade de pedido e resposta de localização a partir de clientes.|Servidor do sistema de sites|  
|MP_OOBMgr.log|Regista as atividades do ponto de gestão relacionadas com a receção de um OTP de um cliente.|Servidor do sistema de sites|  
|MP_Policy.log|Regista a comunicação de políticas.|Servidor do sistema de sites|  
|MP_Relay.log|Regista a transferência de ficheiros que são recolhidos do cliente.|Servidor do sistema de sites|  
|MP_Retry.log|Grava processos de repetição de inventário de hardware.|Servidor do sistema de sites|  
|MP_Sinv.log|Regista detalhes sobre a conversão de registos de inventário de software XML a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|  
|MP_SinvCollFile.log|Regista detalhes sobre a recolha de ficheiros.|Servidor do sistema de sites|  
|MP_Status.log|Regista detalhes sobre a conversão de ficheiros de mensagens de estado XML.svf a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|
|mpcontrol.log|Regista o registo do ponto de gestão com o WINS. Regista a disponibilidade do ponto de gestão a cada 10 minutos.|Servidor do site|  
|mpfdm.log|Regista as ações do componente do ponto de gestão que move ficheiros de cliente para a pasta A RECEBER correspondente no servidor do site.|Servidor do sistema de sites|  
|mpMSI.log|Regista detalhes sobre a instalação do ponto de gestão.|Servidor do site|  
|MPSetup.log|Regista o processo do wrapper de instalação do ponto de gestão.|Servidor do site|  
|UserService.log|Regista os pedidos dos utilizadores do Software Center, recuperando/instalando aplicações disponíveis pelo utilizador a partir do servidor.|Servidor do sistema de sites|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a>Ponto de ligação de serviço

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de ligação de serviço.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Regista informações de certificados e de contas proxy.|Servidor do site|  
|CollEval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Site primário e site de administração central|  
|Cloudusersync.log|Regista a ativação de licenças para os utilizadores.|Computador com o ponto de ligação de serviço|  
|Dataldr.log|Regista informações sobre o processamento de ficheiros MIF.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|Distmgr.log|Regista detalhes sobre pedidos de distribuição de conteúdo.|Servidor de site de nível superior|  
|Dmpdownloader.log|Regista detalhes sobre downloads da Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|Dmpuploader.log|Regista detalhes relacionados com o upload de alterações na base de dados para o Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|hman.log|Regista informações sobre o reencaminhamento de mensagens.|Servidor do site|  
|MSfBSyncWorker.log|Regista informações sobre a comunicação com a Microsoft Store for Business.|Computador com o ponto de ligação de serviço|
|objreplmgr.log|Regista o processamento de política e de atribuição.|Servidor do site principal|  
|PolicyPV.log|Regista a criação de política de todas as políticas.|Servidor do site|  
|outgoingcontentmanager.log|Regista o conteúdo enviado para o Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|Sitecomp.log|Regista os detalhes da instalação do ponto de ligação de serviço.|Servidor do site|  
|SmsAdminUI.log|Atividade da consola Do Gestor de Configuração de Registos.|Computador que executa a consola De Configuração Manager|  
|SMS_CLOUDCONNECTION.log|Regista informações sobre serviços na nuvem.|Computador com o ponto de ligação de serviço|
|Smsprov.log|Regista atividades do Fornecedor sms. As atividades da consola do Gestor de Configuração utilizam o Fornecedor SMS.|Computador com o Fornecedor de SMS|  
|SrvBoot.log|Regista os detalhes sobre o serviço do instalador do ponto de ligação de serviço.|Computador com o ponto de ligação de serviço|  
|Statesys.log|Regista o processamento de mensagens de gestão de dispositivos móveis.|Site primário e site de administração central|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a>Ponto de atualização de software

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de atualização do software.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Regista detalhes sobre a replicação de ficheiros de notificação de atualizações de software de um site-mãe para sites infantis.|Servidor do site|  
|PatchDownloader.log|Regista detalhes sobre o processo de transferência de atualizações de software da origem da atualização para o destino da transferência no servidor do site.|Quando descarrega manualmente as atualizações, `%temp%` este ficheiro encontra-se no seu diretório no computador onde utiliza a consola. Para regras de implementação automáticas, se o cliente do Gestor de Configuração estiver instalado no servidor do site, este ficheiro encontra-se no servidor do site em `%windir%\CCM\Logs`.|  
|ruleengine.log|Regista detalhes sobre regras de implementação automática para a identificação, transferência de conteúdo e criação de implementação e de grupos de atualização de software.|Servidor do site|
|SMS_ISVUPDATES_SYNCAGENT.log| Ficheiro de registo para sincronização de atualizações de software de terceiros.| Ponto de atualização de software de alto nível na hierarquia do Gestor de Configuração.|
|SUPSetup.log|Regista detalhes sobre a instalação do ponto de atualização de software. Quando a instalação de ponto de atualização de software estiver concluída, é escrito **Instalação bem-sucedida** neste ficheiro de registo.|Servidor do sistema de sites|  
|WCM.log|Regista detalhes sobre a configuração do ponto de atualização de software e ligações ao servidor WSUS para categorias de atualizações subscritas, classificações e idiomas.|Servidor do site que se conecta ao servidor WSUS|  
|WSUSCtrl.log|Regista detalhes sobre a configuração, a conectividade de base de dados e o estado de funcionamento do servidor WSUS do site.|Servidor do sistema de sites|  
|wsyncmgr.log|Regista detalhes sobre o processo de sincronização de atualizações de software.|Servidor do sistema de sites|  
|WUSSyncXML.log|Regista detalhes sobre a Ferramenta de Inventário para o processo de sincronização da Microsoft Updates.|Computador cliente configurado como o anfitrião de sincronização para a Ferramenta de Inventário para atualizações da Microsoft|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a>Registar ficheiros por funcionalidade

As seguintes secções listam ficheiros de registo relacionados com funções de Gestor de Configuração.  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a>Gestão de aplicações

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão da aplicação.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Regista os detalhes sobre o estado atual e previsto das aplicações, a sua aplicabilidade, se os requisitos foram satisfeitos, os tipos de implementação e as dependências.|Cliente|  
|AppDiscovery.log|Regista os detalhes sobre a descoberta ou deteção de aplicações em computadores cliente.|Cliente|  
|AppEnforce.log|Regista os detalhes sobre medidas de imposição (instalar e desinstalar) tomadas para aplicações do cliente.|Cliente|  
|AppGroupHandler.log|A partir da versão 1906, informações de deteção e execução para grupos de aplicações|Cliente|
|awebsctl.log|Regista atividades de monitorização para a função do site de site de ponto de serviço do Catálogo de Aplicações.|Servidor do sistema de sites|  
|awebsvcMSI.log|Regista informações detalhadas de instalação da função do sistema de sites do ponto de serviço Web do Catálogo de Aplicações.|Servidor do sistema de sites|  
|BusinessAppProcessWorker.log|Processamento de registos para aplicações microsoft Store para empresas.|Servidor do site|
|Ccmsdkprovider.log|Regista as atividades do SDK de gestão de aplicações.|Cliente|  
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do sistema de sites|  
|ConfigMgrSoftwareCatalog.log|Regista a atividade do Catálogo de Aplicações, que inclui a sua utilização do Silverlight.|Cliente|  
|MSfBSyncWorker.log|Regista informações sobre a comunicação com a Microsoft Store for Business.|Computador com o ponto de ligação de serviço|
|NotiCtrl.log|Notificações de pedido de pedido de pedido.|Servidor do site|  
|portlctl.log|Regista as atividades de monitorização da função do sistema de sites do ponto do Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|portlwebMSI.log|Regista a atividade de instalação do MSI para a função de Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|PrestageContent.log|Regista detalhes sobre a utilização da ferramenta ExtractContent.exe num ponto de distribuição remoto e pré-encenado. Esta ferramenta extrai o conteúdo exportado para um ficheiro.|Servidor do sistema de sites|  
|ServicePortalWebService.log|Regista a atividade do serviço Web do Catálogo de Aplicações.|Servidor do sistema de sites|  
|ServicePortalWebSite.log|Regista a atividade do Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|DefiniçõesAgente.log|Execução de aplicações específicas, orquestração de registos de avaliação de grupo de aplicações e detalhes das políticas de cogestão.|Cliente|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|Ficheiro de registo para componente que sincroniza aplicações da Microsoft Store for Business.|Servidor do site|
|SMS_CLOUDCONNECTION.log|Regista informações sobre serviços na nuvem.|Computador com o ponto de ligação de serviço|
|SMSdpmon.log|Regista os detalhes sobre a tarefa agendada de monitorização do estado de funcionamento do ponto de distribuição configurada num ponto de distribuição.|Servidor do site|  
|SoftwareCatalogUpdateEndpoint.log|Regista atividades para gerir o URL para o Catálogo de Aplicações mostrado no Centro de Software.|Cliente|  
|SoftwareCenterSystemTasks.log|Regista atividades relacionadas com a validação prévia de componentes do Software Center.|Cliente|  

#### <a name="packages-and-programs"></a>Pacotes e programas

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a implementação de pacotes e programas.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do site|  
|execmgr.log|Regista os detalhes sobre pacotes e sequências de tarefas que são executados.|Cliente|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a>Inteligência de Ativos

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Asset Intelligence.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Regista as atividades das ações de inventário do Asset Intelligence.|Cliente|  
|aikbmgr.log|Regista os detalhes sobre o processamento de ficheiros XML a partir da caixa de entrada para atualização do catálogo do Asset Intelligence.|Servidor do site|  
|AIUpdateSvc.log|Regista a interação do ponto de sincronização da Inteligência de Ativos com o serviço de nuvem.|Servidor do sistema de sites|  
|AIUSMSI.log|Regista detalhes sobre a instalação da função do sistema de site de pontode sincronização de Inteligência de Ativos.|Servidor do sistema de sites|  
|AIUSSetup.log|Regista detalhes sobre a instalação da função do sistema de site de pontode sincronização de Inteligência de Ativos.|Servidor do sistema de sites|  
|ManagedProvider.log|Regista os detalhes sobre a deteção de software com uma etiqueta de identificação de software associada. Também regista atividades relacionadas com o inventário de hardware.|Servidor do sistema de sites|  
|MVLSImport.log|Regista os detalhes sobre o processamento de ficheiros de licenciamento importados.|Servidor do sistema de sites|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a>Backup e recuperação

A tabela seguinte lista ficheiros de registo que contêm informações relacionadas com ações de backup e recuperação, incluindo resets do site, e alterações ao Fornecedor SMS.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Regista informações sobre tarefas de configuração e recuperação quando o Gestor de Configuração recupera um site de cópia de segurança.|Servidor do site|  
|Smsbkup.log|Regista os detalhes sobre a atividade de cópia de segurança do site.|Servidor do site|  
|smssqlbkup.log|Regista a saída do processo de backup da base de dados do site quando o SQL Server é instalado num servidor que não é o servidor do site.|Servidor da base de dados do site|  
|Smswriter.log|Regista informações sobre o estado do escritor VSS do Gestor de Configuração que é usado pelo processo de backup.|Servidor do site|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a>Inscrição de certificado

A tabela seguinte lista os ficheiros de registo do Gestor de Configuração que contêm informações relacionadas com a inscrição do certificado. A inscrição do certificado utiliza o ponto de registo do certificado e o Módulo de Política do Gestor de Configuração no servidor que está a executar o Serviço de Inscrição de Dispositivos de Rede (NDES).  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|Crp.log|Grava atividades de inscrição.|Ponto de registo de certificados|  
|Crpctrl.log|Regista o estado de funcionamento operacional do ponto de registo de certificados.|Ponto de registo de certificados|  
|Crpsetup.log|Regista os detalhes sobre a instalação e a configuração do ponto de registo de certificados.|Ponto de registo de certificados|  
|Crpmsi.log|Regista os detalhes sobre a instalação e a configuração do ponto de registo de certificados.|Ponto de registo de certificados|  
|NDESPlugin.log|Os registos contestam as atividades de verificação e inscrição de certificados.|Módulo de Política de Gestor de Configuração e o Serviço de Inscrição de Dispositivos de Rede|  

Juntamente com os ficheiros de registo do Gestor de Configuração, reveja os registos da Aplicação do Windows no Observador de Eventos no servidor que executa o Serviço de Inscrição de Dispositivos de Rede e o servidor que acolhe o ponto de registo do certificado. Por exemplo, procure mensagens da origem **NetworkDeviceEnrollmentService**.

Também pode utilizar os seguintes ficheiros de registo:  

- Ficheiros de registo IIS para serviço de inscrição de dispositivos de rede: **%SYSTEMDRIVE%inetpub\logs\LogFiles\W3SVC1**  

- Ficheiros de registo IIS para o ponto de registo do certificado: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- Ficheiro de registo da Política de Inscrição de Dispositivos de Rede: **mscep.log**  

    > [!NOTE]  
    > Este ficheiro está localizado na pasta para o perfil da conta NDES, por exemplo, em C:\Users\SCEPSvc. Para obter mais informações sobre como ativar o registo de NDES, consulte a secção [Enable Logging](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) do wiki NDES.  

### <a name="client-notification"></a><a name="BKMK_BGB"></a>Notificação do cliente

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a notificação do cliente.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Regista detalhes sobre as atividades do servidor do site relacionadas com tarefas de notificação do cliente e processamento de ficheiros de estado online e de tarefa.|Servidor do site|  
|BGBServer.log|Regista as atividades do servidor de notificação, como a comunicação cliente-servidor e a tarefas de empurrar para os clientes. Também regista informações sobre a geração de ficheiros de estado online e de tarefa saem para o servidor do site.|Ponto de gestão|  
|BgbSetup.log|Regista as atividades do processo de instalação do servidor de notificação durante a instalação e desinstalação.|Ponto de gestão|  
|bgbisapiMSI.log|Regista detalhes sobre a instalação e deinstalação do servidor de notificação.|Ponto de gestão|  
|BgbHttpProxy.log|Regista as atividades do proxy de HTTP de notificação enquanto reencaminha as mensagens de clientes utilizando o HTTP de e para o servidor de notificação.|Cliente|  
|CcmNotificationAgent.log|Regista as atividades do agente de notificação, tais como comunicação cliente-servidor e informações sobre tarefas recebidas e enviadas para outros agentes clientes.|Cliente|  

### <a name="cloud-management-gateway"></a>Gateway de gestão da cloud

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o gateway de gestão da nuvem.

|Nome do registo|Descrição|Computador com o ficheiro de registo|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Regista detalhes sobre a implementação do serviço de gateway de gestão de nuvem, estado de serviço em curso e utilização de dados associados ao serviço. Para configurar o nível de registo, edite o valor **do nível de registo** na seguinte chave de registo:`HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|A pasta *installdir* no servidor principal do site ou CAS.|
|CMGSetup.log <sup> [Nota 1](#bkmk_note1)</sup>|Regista detalhes sobre a segunda fase da implementação do gateway de gestão da nuvem (implantação local em Azure). Para configurar o nível de registo, utilize o **nível** de definição De rastreio **(Informação** (Predefinido), **Verbose,** **Erro**) no separador de configuração dos **serviços do portal Azure\Cloud.**|Os **logs %approot%\no** seu servidor Azure, ou a pasta SMS/Logs no servidor do sistema do site|
|CMGService.log <sup> [Nota 1](#bkmk_note1)</sup>|Regista detalhes sobre o componente do núcleo de gateway de gestão de nuvem em Azure. Para configurar o nível de registo, utilize o **nível** de definição De rastreio **(Informação** (Predefinido), **Verbose,** **Erro**) no separador de configuração dos **serviços do portal Azure\Cloud.**|Os **logs %approot%\no** seu servidor Azure, ou a pasta SMS/Logs no servidor do sistema do site|
|SMS_Cloud_ProxyConnector.log|Regista detalhes sobre a criação de ligações entre o serviço de gateway de gestão de nuvem e o ponto de ligação de gateway de gestão de nuvem.|Servidor do sistema de sites|
|CMGContentService.log <sup> [Nota 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->Quando permite que um CMG também sirva conteúdo do armazenamento Azure, este registo regista os detalhes desse serviço.|Os **logs %approot%\no** seu servidor Azure, ou a pasta SMS/Logs no servidor do sistema do site|

- Para implementações de resolução de problemas, utilize **CloudMgr.log** e **CMGSetup.log**
- Para a saúde do serviço de resolução de problemas, utilize **CMGService.log** e **SMS_Cloud_ProxyConnector.log**.
- Para resolver problemas o tráfego de clientes, utilize **CMGHttpHandler.log**, **CMGService.log**e **SMS_Cloud_ProxyConnector.log**.

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a>Nota 1: Registos sincronizados do Azure

Estes são ficheiros de registo do Gestor de Configuração local que o gestor de serviço sincronia do armazenamento do Azure a cada cinco minutos. A porta de entrada de gestão de nuvens empurra os troncos para o armazenamento do Azure a cada cinco minutos. Então o atraso máximo é de 10 minutos. Os interruptores verbose afetam os registos locais e remotos. Os nomes reais dos ficheiros incluem o nome do serviço e identificador de instância de funções. Por exemplo, CMG-*ServiceName*-*RoleInstanceID*-CMGSetup.log

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a>Definições de conformidade e acesso a recursos da empresa

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com as definições de compatibilidade e o acesso a recursos da empresa.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Regista os detalhes sobre o processo de remediação e compatibilidade das definições de compatibilidade, atualizações de software e gestão de aplicações.|Cliente|  
|CITaskManager.log|Regista informações sobre o agendamento da tarefa de itens de configuração.|Cliente|  
|DCMAgent.log|Regista informações de alto nível sobre a avaliação, a comunicação de conflitos e a remediação de itens de configuração e aplicações.|Cliente|  
|DCMReporting.log|Regista informações sobre os relatórios de resultados da plataforma de política em mensagens de estado para itens de configuração.|Cliente|  
|DcmWmiProvider.log|Regista informações sobre sincronizações de itens de configuração de leitura da WMI.|Cliente|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a>Consola de Gestor de Configuração

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a consola Do Gestor de Configuração.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Regista a instalação da consola 'Gestor de Configuração'.|Computador que executa a consola De Configuração Manager|  
|SmsAdminUI.log|Regista informações sobre o funcionamento da consola 'Gestor de Configuração'.|Computador que executa a consola De Configuração Manager|  
|Smsprov.log|Regista atividades do Fornecedor sms. As atividades da consola do Gestor de Configuração utilizam o Fornecedor SMS.|Servidor do site ou servidor de sistema de sites|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a>Gestão de conteúdos

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão de conteúdos.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;\>guia .log|Regista os detalhes de um ponto de distribuição baseado na nuvem específico, incluindo informações sobre armazenamento e acesso ao conteúdo.|Servidor do sistema de sites|  
|CloudMgr.log|Regista detalhes sobre o fornecimento de conteúdo, recolha de estatísticas de armazenamento e largura de banda, e ações iniciadas por administradores para parar ou iniciar o serviço de cloud que executa um ponto de distribuição baseado na nuvem.|Servidor do sistema de sites|  
|DataTransferService.log|Regista todas as comunicações BITS para acesso a políticas ou pacotes. Este registo também é utilizado para a gestão de conteúdos por pontos de distribuição de pull-distribution.|Computador que é configurado como um ponto de distribuição de puxar|  
|PullDP.log|Regista os detalhes sobre o conteúdo que o ponto de distribuição de extração transfere dos pontos de distribuição de origem.|Computador que é configurado como um ponto de distribuição de puxar|  
|PrestageContent.log|Regista os detalhes sobre a utilização da ferramenta ExtractContent.exe num ponto de distribuição remoto e pré-encenado. Esta ferramenta extrai o conteúdo exportado para um ficheiro.|Função do sistema de sites|  
|SMSdpmon.log|Regista detalhes sobre a monitorização da saúde dos pontos de distribuição das tarefas programadas que estão configuradas num ponto de distribuição.|Função do sistema de sites|  
|smsdpprov.log|Regista os detalhes sobre a extração de ficheiros comprimidos recebidos de um site primário. Este registo é gerado pelo fornecedor wMI do ponto de distribuição remoto.|Computador de ponto de distribuição que não está colocalizado com o servidor do site|  
|smsdpusage.log|Regista detalhes sobre o smsdpusage.exe que executa e recolhe dados para o relatório de resumo do ponto de distribuição.|Função do sistema de sites|  

### <a name="desktop-analytics"></a>Análise de Computadores

Utilize os seguintes ficheiros de registo para ajudar a resolver problemas com desktop Analytics integrado com o Gestor de Configuração.

Os ficheiros de registo no ponto de `%ProgramFiles%\Configuration Manager\Logs\M365A`ligação de serviço estão no seguinte diretório: .
Os ficheiros de registo do cliente do `%WinDir%\CCM\logs`Gestor de Configuração estão no seguinte diretório: .

| Registar | Descrição |Computador com o ficheiro de registo|
|---------|---------|---------|
| M365ADeploymentPlanWorker.log | Informações sobre sincronização do plano de implementação do serviço de nuvem desktop Analytics para o gestor de configuração no local |Ponto de ligação de serviço|
| M365ADeviceHealthWorker.log | Informações sobre o upload de saúde do dispositivo do Gestor de Configuração para a nuvem da Microsoft |Ponto de ligação de serviço|
| M365AHandler.log | Informações sobre a política de definições de Desktop Analytics |Cliente|
| M365AUploadWorker.log | Informações sobre recolha e upload de dispositivo do Gestor de Configuração para a nuvem da Microsoft |Ponto de ligação de serviço|
| SmsAdminUI.log | Informações sobre a atividade da consola Do Gestor de Configuração, como configurar os serviços de nuvem Azure  |Ponto de ligação de serviço|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a>Descoberta

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a descoberta.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Regista ações da Deteção de Grupos de Segurança do Active Directory.|Servidor do site|  
|adsysdis.log|Regista ações da Deteção de Sistemas do Active Directory.|Servidor do site|  
|adusrdis.log|Regista ações da Deteção de Utilizadores do Active Directory.|Servidor do site|  
|ADForestDisc.Log|Regista ações da Deteção de Florestas do Active Directory.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|InventoryAgent.log|Regista atividades de inventário de hardware, inventário de software e ações de deteção de heartbeat no cliente.|Cliente|  
|netdisc.log|Regista ações da Deteção de Rede.|Servidor do site|  

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a>Proteção de Pontofinal

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Endpoint Protection.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Regista os detalhes sobre a instalação do cliente do Endpoint Protection e a aplicação da política antimalware a esse cliente.|Cliente|  
|EPCtrlMgr.log|Regista detalhes sobre a sincronização de informações de ameaça de malware a partir do servidor de funções de Proteção de Ponto final com a base de dados do Gestor de Configuração.|Servidor do sistema de sites|  
|EPMgr.log|Monitoriza o estado da função do sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EPSetup.log|Fornece informações sobre a instalação da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a>Extensões

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com extensões.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Regista informações sobre a transferência de extensões da Microsoft e sobre a instalação e desinstalação de todas as extensões.|Computador que executa a consola De Configuração Manager|  
|FeatureExtensionInstaller.log|Registmente informações sobre a instalação e remoção de extensões individuais quando estão ativadas ou desativadas na consola Do Gestor de Configuração.|Computador que executa a consola De Configuração Manager|  
|SmsAdminUI.log|Atividade da consola Do Gestor de Configuração de Registos.|Computador que executa a consola De Configuração Manager|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a>Inventário

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o processamento de dados de inventário.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Regista informações sobre o processamento de ficheiros MIF e inventário de hardware na base de dados do Gestor de Configuração.|Servidor do site|  
|invproc.log|Regista o reencaminhamento de ficheiros MIF de um site secundário para o seu site principal.|Servidor do Site Secundário|  
|sinvproc.log|Regista informações sobre o processamento de dados de inventário de software para a base de dados do site.|Servidor do site|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a>Medição

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a medição.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitoriza todos os processos de medição de software.|Cliente|  
|SWMTRReportGen.log|Gera um relatório de dados de uso que é recolhido pelo agente de medição. Estes dados são registados no ficheiro Mtrmgr.log.|Cliente|
|swmproc.log|Regista o processamento de ficheiros e definições de medição.|Servidor do site|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a>Migração

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a migração.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Regista informações sobre ações de migração que envolvam tarefas de migração, pontos de distribuição partilhados e atualizações de pontos de distribuição.|Site de alto nível na hierarquia do Gestor de Configuração, e cada local primário infantil. Numa hierarquia com vários sites primários, utilize o ficheiro de registo criado no site de administração central.|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a>Dispositivos móveis

As seguintes secções listam os ficheiros de registo que contêm informações relacionadas com a gestão de dispositivos móveis.  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a>Inscrição

A tabela seguinte lista registos que contêm informações relacionadas com a inscrição de dispositivos móveis.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Regista a comunicação entre os pontos de gestão ativados para dispositivos móveis e os pontos finais do ponto de gestão.|Servidor do sistema de sites|  
|dmpmsi.log|Regista os dados do Windows Installer para a configuração de um ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DMPSetup.log|Regista a configuração do ponto de gestão quando está ativado para dispositivos móveis.|Servidor do sistema de sites|  
|enrollsrvMSI.log|Regista os dados do Windows Installer para a configuração de um ponto de registo.|Servidor do sistema de sites|  
|enrollmentweb.log|Regista a comunicação entre dispositivos móveis e o ponto proxy de registo.|Servidor do sistema de sites|  
|enrollwebMSI.log|Regista os dados do Windows Installer para a configuração de um ponto proxy de registo.|Servidor do sistema de sites|  
|enrollmentservice.log|Regista a comunicação entre um ponto proxy de registo e um ponto de registo.|Servidor do sistema de sites|  
|SMS_DM.log|Regista a comunicação entre dispositivos móveis, computadores Mac e o ponto de gestão que está ativado para dispositivos móveis e computadores Mac.|Servidor do sistema de sites|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a>Conector de servidor de troca

Os seguintes registos contêm informações relacionadas com o conector do Exchange Server.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Regista as atividades e o estado do conector do Exchange Server.|Servidor do site|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a>Legado de dispositivo móvel

A tabela seguinte lista registos que contêm informações relacionadas com o cliente legado do dispositivo móvel.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Regista os detalhes sobre os dados de inscrição do certificado em clientes legados de dispositivos móveis.|Cliente|  
|DMCertResp.htm|Regista a resposta HTML a partir do servidor de certificado quando o programa de inscrição do cliente legado do dispositivo móvel solicita um certificado PKI.|Cliente|  
|DmClientHealth.log|Regista os GUIDs de todos os clientes legados de dispositivos móveis que comunicam com o ponto de gestão que está ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmClientRegistration.log|Regista os pedidos e respostas de registo de e para clientes legados de dispositivos móveis.|Servidor do sistema de sites|  
|DmClientSetup.log|Regista os dados da configuração do cliente para clientes legados de dispositivos móveis.|Cliente|  
|DmClientXfer.log|Regista os dados de transferência do cliente para clientes legados de dispositivos móveis e para implementações do ActiveSync.|Cliente|  
|DmCommonInstaller.log|Regista a instalação do ficheiro de transferência do cliente para a configuração de ficheiros de transferência de clientes legados de dispositivos móveis.|Cliente|  
|DmInstaller.log|Regista se o DMInstaller chama corretamente o DmClientSetup e se o DmClientSetup sai com sucesso ou falha em clientes legados de dispositivos móveis.|Cliente|  
|DmpDatastore.log|Regista todas as ligações de base de dados do site e consultas efetuadas pelo ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpDiscovery.log|Regista todos os dados de deteção dos clientes legados de dispositivos móveis no ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpHardware.log|Regista dados de inventário de hardware dos clientes legados de dispositivos móveis no ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpIsapi.log|Regista a comunicação do cliente legado de dispositivos móveis com um ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|dmpmsi.log|Regista os dados do Windows Installer para a configuração de um ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DMPSetup.log|Regista a configuração do ponto de gestão quando está ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpSoftware.log|Regista dados de distribuição de software dos clientes legados de dispositivos móveis no ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpStatus.log|Regista dados de mensagens de estado de clientes de dispositivos móveis no ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmSvc.log|Regista a comunicação de cliente dos clientes legados de dispositivos móveis com um ponto de gestão ativado para dispositivos móveis.|Cliente|  
|FspIsapi.log|Regista detalhes sobre comunicações com o ponto de estado de contingência a partir de clientes legados de dispositivos móveis e de computadores cliente.|Servidor do sistema de sites|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a>Implantação de Os

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a implementação do OS.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CAS.log|Regista detalhes quando são encontrados pontos de distribuição para conteúdo referenciado.|Cliente|  
|ccmsetup.log|Regista tarefas ccmsetup para configuração de cliente, atualização de cliente e remoção de cliente. Pode ser utilizado para resolver problemas de instalação de cliente.|Cliente|  
|CreateTSMedia.log|Regista detalhes para a criação de suportes de dados de sequências de tarefas.|Computador que executa a consola De Configuração Manager|  
|Dism.log|Registre as ações de instalação do controlador ou atualizar as ações de aplicação para manutenção offline.|Servidor do sistema de sites|  
|Distmgr.log|Regista detalhes sobre a configuração de permitir um ponto de distribuição para preboot Execution Environment (PXE).|Servidor do sistema de sites|  
|DriverCatalog.log|Regista detalhes sobre controladores de dispositivo importados para o catálogo de controladores.|Servidor do sistema de sites|  
|mcsisapi.log|Regista informações de transferência de pacotes multicast e respostas de pedidos de cliente.|Servidor do sistema de sites|  
|mcsexec.log|Regista verificações de saúde, espaço de nome, criação de sessão e ações de verificação de certificados.|Servidor do sistema de sites|  
|mcsmgr.log|Alterações de registos na configuração, modo de segurança e disponibilidade.|Servidor do sistema de sites|  
|mcsprv.log|Regista a interação do fornecedor de multicast com os Serviços de Implementação do Windows (WDS).|Servidor do sistema de sites|  
|MCSSetup.log|Regista detalhes sobre a instalação da função de servidor multicast.|Servidor do sistema de sites|  
|MCSMSI.log|Regista detalhes sobre a instalação da função de servidor multicast.|Servidor do sistema de sites|  
|Mcsperf.log|Regista detalhes sobre as atualizações do contador de desempenho multicast.|Servidor do sistema de sites|  
|MP_ClientIDManager.log|As respostas de pontode gestão de registos aos pedidos de IDENTIFICAção do cliente que as sequências de tarefas partem do PXE ou dos meios de arranque.|Servidor do sistema de sites|  
|MP_DriverManager.log|Regista as respostas do ponto de gestão a pedidos de ação da sequência de tarefas Aplicar Controlador Automaticamente.|Servidor do sistema de sites|  
|OfflineServicingMgr.log|Regista detalhes dos horários de manutenção offline e a atualização aplicam ações nos ficheiros do formato de imagem do sistema operativo Windows Imaging Format (WIM).|Servidor do sistema de sites|  
|Setupact.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração. Para mais informações, consulte [Ficheiros de Registo](https://docs.microsoft.com/windows/deployment/upgrade/log-files).|Cliente|  
|Setupapi.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração.|Cliente|  
|Setuperr.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração.|Cliente|  
|smpisapi.log|Regista detalhes sobre as ações de captura e restauro do estado de cliente e informações de limiares.|Cliente|  
|Smpmgr.log|Regista detalhes sobre os resultados de verificações do estado de funcionamento do ponto de migração de estado e de alterações de configuração.|Servidor do sistema de sites|  
|smpmsi.log|Regista detalhes da instalação e configuração do ponto de migração de estado.|Servidor do sistema de sites|  
|smpperf.log|Regista as atualizações do contador de desempenho do ponto de migração de estado.|Servidor do sistema de sites|  
|smspxe.log|Regista detalhes sobre as respostas aos clientes que usam botas PXE, e detalhes sobre a expansão de imagens de boot e boot files.|Servidor do sistema de sites|  
|smssmpsetup.log|Regista detalhes da instalação e configuração do ponto de migração de estado.|Servidor do sistema de sites|
| SMS_PhasedDeployment.log| Ficheiro de registo para implementações faseadas|Site de alto nível na hierarquia do Gestor de Configuração|
|Smsts.log|Regista atividades de sequência de tarefas.|Cliente|  
|TSAgent.log|Regista o resultado de dependências de sequência de tarefas antes de iniciar uma sequência de tarefas.|Cliente|  
|TaskSequenceProvider.log|Regista detalhes sobre sequências de tarefas quando são importadas, exportadas ou editadas.|Servidor do sistema de sites|  
|loadstate.log|Regista detalhes sobre a Ferramenta de Migração de Estado de Utilizador (USMT) e o restauro de dados de estado do utilizador.|Cliente|  
|scanstate.log|Regista detalhes sobre a Ferramenta de Migração de Estado de Utilizador (USMT) e a captura de dados de estado do utilizador.|Cliente|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a>Gestão de energia

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão de energia.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|Regista detalhes sobre as atividades de gestão de energia no computador cliente, incluindo a monitorização e a execução de configurações pelo Agente Cliente de Gestão de Energia.|Cliente|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a>Controlo remoto

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com controlo remoto.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Regista detalhes sobre a atividade do visualizador de controlo remoto.|No computador que executa o visualizador de controlo remoto, na pasta %temp%.|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a>Reportagem

A tabela seguinte lista os ficheiros de registo do Gestor de Configuração que contêm informações relacionadas com reportagens.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Regista informações sobre a atividade e o estado do ponto do Reporting Services.|Servidor do sistema de sites|  
|srsrpMSI.log|Regista resultados detalhados do processo de instalação do ponto do Reporting Services a partir da saída MSI.|Servidor do sistema de sites|  
|srsrpsetup.log|Regista resultados do processo de instalação do ponto do Reporting Services.|Servidor do sistema de sites|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a>Administração baseada em funções

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão da administração baseada em funções.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|hman.log|Regista informações sobre alterações na configuração do site e a publicação de informações do site para Serviços de Domínio de Diretório Ativo.|Servidor do site|  
|SMSProv.log|Regista o acesso do fornecedor WMI à base de dados do site.|Computador com o Fornecedor de SMS|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a>Medição de software

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a medição de software.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitoriza todos os processos de medição de software.|Servidor do site|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a>Atualizações de software

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com as atualizações de software.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AlternateHandler.log|Regista detalhes quando o cliente liga para a interface COM click-to-run do Office para descarregar e instalar aplicações microsoft 365 para atualizações de clientes empresariais. É semelhante ao uso do WuaHandler quando chama a API do Agente de Atualização do Windows para descarregar e instalar atualizações do Windows.<!-- SCCMDocs#888 -->|Cliente|
|ccmperf.log|Regista atividades relacionadas com a manutenção e a captura de dados relacionados com os contadores de desempenho do cliente.|Cliente|
|DeltaDownload.log|Regista informações sobre o download de atualizações expressas e atualizações descarregadas através da Otimização de Entrega.|Cliente|  
|PatchDownloader.log|Regista detalhes sobre o processo de transferência de atualizações de software da origem da atualização para o destino da transferência no servidor do site.|Ao descarregar as atualizações manualmente, este ficheiro de registo está localizado no diretório %temporário% do utilizador que executa a consola na máquina que está a executar a consola. Para regras de implementação automática, este ficheiro de registo está localizado no servidor do site em %windir%\CCM\Logs, se o cliente ConfigMgr estiver instalado no servidor do site.|  
|PolicyEvaluator.log|Regista detalhes sobre a avaliação das políticas em computadores cliente, incluindo políticas de atualizações de software.|Cliente|  
|RebootCoordinator.log|Regista detalhes sobre a coordenação de reinícios do sistema em computadores cliente após instalações de atualizações de software.|Cliente|  
|ScanAgent.log|Regista detalhes sobre pedidos de análise de atualizações de software, a localização do WSUS e ações relacionadas.|Cliente|  
|SdmAgent.log|Regista detalhes sobre o rastreio da reparação e conformidade. No entanto, o ficheiro de registo atualiza o software, Updateshandler.log, fornece detalhes mais informativos sobre a instalação das atualizações de software que são necessárias para a conformidade. Este ficheiro de registo é partilhado com definições de compatibilidade.|Cliente|  
|ServiceWindowManager.log|Regista detalhes sobre a avaliação de janelas de manutenção.|Cliente|
|SMS_ISVUPDATES_SYNCAGENT.log| Ficheiro de registo para sincronização de atualizações de software de terceiros.| Ponto de atualização de software de alto nível na hierarquia do Gestor de Configuração.|
|SMS_OrchestrationGroup.log| Arquivo de registo para grupos de orquestração|Servidor do site|
|SmsWusHandler.log|Regista detalhes sobre o processo de análise da Ferramenta de Inventário das Atualizações da Microsoft.|Cliente|  
|StateMessage.log|Regista detalhes sobre mensagens estatais de atualização de software que são criadas e enviadas para o ponto de gestão.|Cliente|  
|SUPSetup.log|Regista detalhes sobre a instalação do ponto de atualização de software. Quando a instalação de ponto de atualização de software estiver concluída, é escrito **Instalação bem-sucedida** neste ficheiro de registo.|Servidor do sistema de sites|  
|UpdatesDeployment.log|Regista detalhes sobre implementações no cliente, incluindo a ativação, avaliação e imposição de atualizações de software. O registo verboso mostra informações adicionais sobre a interação com a interface de utilizador do cliente.|Cliente|  
|UpdatesHandler.log|Regista detalhes sobre a análise de compatibilidade de atualizações de software e sobre a transferência e instalação de atualizações de software no cliente.|Cliente|  
|UpdatesStore.log|Regista detalhes sobre o estado de compatibilidade das atualizações de software que foram analisadas durante o ciclo de análise de compatibilidade.|Cliente|  
|WCM.log|Regista detalhes sobre configurações de pontos de atualização de software e ligações ao servidor WSUS para categorias de atualizações subscritas, classificações e idiomas.|Servidor do site|  
|WSUSCtrl.log|Regista detalhes sobre a configuração, a conectividade de base de dados e o estado de funcionamento do servidor WSUS do site.|Servidor do sistema de sites|  
|wsyncmgr.log|Regista detalhes sobre o processo de sincronização da atualização de software.|Servidor do site|  
|WUAHandler.log|Regista detalhes sobre o Windows Update Agent no cliente quando este procura atualizações de software.|Cliente|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a>Acordar na LAN

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a utilização do Wake On LAN.  

> [!NOTE]  
> Quando complementa o Wake On LAN utilizando o wake-up proxy, esta atividade está registada no cliente. Por exemplo, consulte ccmExec.log e SleepAgent_ *domínio* \> @SYSTEM_0.log<na secção de [operações](#BKMK_ClientOpLogs) do Cliente deste artigo.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Regista detalhes sobre quais os clientes que devem receber pacotes de reativação, o número de pacotes de reativação enviados e o número de pacotes de reativação repetidos.|Servidor do site|  
|wolmgr.log|Regista detalhes sobre procedimentos de reativação automática, tais como a reativação de implementações que estão configuradas para Reativação por LAN.|Servidor do site|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a>Serviço do Windows 10

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a manutenção do Windows 10.  
A manutenção utiliza a mesma infraestrutura e processo que as atualizações de software. Para outros registos aplicáveis ao cenário de manutenção, consulte [as atualizações](#BKMK_SU_NAPLog)do Software .

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CBS.log|Regista falhas de manutenção relacionadas com alterações para Atualizações ou funções do Windows.|Cliente|
|DISM.log|Grava todas as ações usando o DISM. Se necessário, dISM.log apontará para CBS.log para mais detalhes.|Cliente|
|setupact.log|Ficheiro de registo primário para a maioria dos erros que ocorrem durante o processo de instalação do Windows. O ficheiro de registo está localizado\$na pasta %windir% Windows.~BT\sources\panther.|Cliente|

Para mais informações, consulte [ficheiros de registo relacionados](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files)com a manutenção online .

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a>Agente de atualização do Windows

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Windows Update Agent.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Regista detalhes sobre quando o Windows Update Agent se conecta ao servidor WSUS e recupera as atualizações de software para avaliação de conformidade, e se existem atualizações para os componentes do agente.|Cliente|  

Para mais informações, consulte [os ficheiros](https://docs.microsoft.com/windows/deployment/update/windows-update-logs)de registo do Windows Update .

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a>Servidor WSUS

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o servidor WSUS.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|Change.log|Regista detalhes sobre as informações da base de dados do servidor WSUS que mudaram.|Servidor WSUS|  
|SoftwareDistribution.log|Regista detalhes sobre as atualizações de software que estão sincronizadas a partir da fonte de atualização configurada para a base de dados do servidor WSUS.|Servidor WSUS|  

Estes ficheiros de `%ProgramFiles%\Update Services\LogFiles` registo estão localizados na pasta.

## <a name="see-also"></a>Consulte também

- [Acerca dos ficheiros de registo](about-log-files.md)

- [Centro de Suporte OneTrace](../../support/support-center-onetrace.md)

- [Espectador de ficheiro sonorde do Centro de Suporte](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
