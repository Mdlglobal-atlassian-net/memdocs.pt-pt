---
title: Contas utilizadas
titleSuffix: Configuration Manager
description: Identifique e gerencie os grupos Windows, contas e objetos SQL utilizados no 'Gestor de Configuração'.
ms.date: 05/08/2020
ms.prod: configuration-manager
ms.technology: Configuration Manager-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bd1284b96e1739126b8d6ee19f20699d47e5880
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83267997"
---
# <a name="accounts-used-in-configuration-manager"></a>Contas utilizadas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as seguintes informações para identificar os grupos Windows, contas e objetos SQL que são utilizados no 'Gestor de Configuração', como são utilizados e quaisquer requisitos.  

- [Grupos do Windows Criados e Utilizados pelo Configuration Manager](#bkmk_groups)  
  - [Configuração Manager_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [Configuração Manager_DViewAccess](#configmgr_dviewaccess)  
  - [Utilizadores de controlo remoto do Gestor de Configuração](#configmgr_rcusers)  
  - [Admins de SMS](#sms-admins)  
  - [código de site SMS_SiteSystemToSiteServerConnection_MP_ &lt;\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_ &lt; código de site\>](#bkmk_remoteprov)  
  - [código de site SMS_SiteSystemToSiteServerConnection_Stat_ &lt;\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_ &lt; código de site\>](#bkmk_filerepl)  

- [Contas que o Configuration Manager Utiliza](#bkmk_accounts)
  - [Conta de descoberta de grupo de diretório ativo](#active-directory-group-discovery-account)  
  - [Conta de descoberta do sistema de diretório ativo](#active-directory-system-discovery-account)  
  - [Conta de descoberta de utilizadores de Diretório Ativo](#active-directory-user-discovery-account)  
  - [Conta florestal de Diretório Ativo](#active-directory-forest-account)  
  - [Conta de ponto de registo de certificado](#certificate-registration-point-account)  
  - [Capturar conta de imagem de OS](#capture-os-image-account)  
  - [Conta de instalação push do cliente](#client-push-installation-account)  
  - [Conta de ligação ao ponto de inscrição](#enrollment-point-connection-account)  
  - [Conta de ligação do Servidor de Troca](#exchange-server-connection-account)  
  - [Conta de ligação de ponto de gestão](#management-point-connection-account)  
  - [Conta de ligação multicast](#multicast-connection-account)  
  - [Conta de acesso à rede](#network-access-account)  
  - [Conta de acesso ao pacote](#package-access-account)  
  - [Conta de ponto de serviços de reporte](#reporting-services-point-account)  
  - [Ferramentas remotas permitidas contas de espectadores](#remote-tools-permitted-viewer-accounts)  
  - [Conta de instalação do site](#site-installation-account)
  - [Conta de instalação do sistema do site](#site-system-installation-account)  
  - [Conta de servidor proxy do sistema do site](#site-system-proxy-server-account)  
  - [Conta de ligação ao servidor SMTP](#smtp-server-connection-account)  
  - [Conta de ligação de ponto de atualização de software](#software-update-point-connection-account)  
  - [Conta de site de origem](#source-site-account)  
  - [Conta de base de dados do site de origem](#source-site-database-account)  
  - [Grupo de sequência de tarefas junta-se à conta](#task-sequence-domain-join-account)  
  - [Conta de ligação de rede de sequência de tarefas](#task-sequence-network-folder-connection-account)  
  - [Sequência de tarefas executada como conta](#task-sequence-run-as-account)  

- [Objetos de utilizador que o Gestor de Configuração utiliza no SQL](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Funções de base de dados que o Gestor de Configuração utiliza no SQL](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a>Grupos Windows que o Gestor de Configuração cria e utiliza  

O Gestor de Configuração cria automaticamente, e em muitos casos mantém automaticamente, os seguintes grupos Windows:  

> [!NOTE]  
> Quando o Gestor de Configuração cria um grupo num computador que é membro do domínio, o grupo é um grupo de segurança local. Se o computador for um controlador de domínio, o grupo é um grupo local de domínio. Este tipo de grupo é partilhado entre todos os controladores de domínio no domínio.  


### <a name="configuration-manager_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a>Configuração Manager_CollectedFilesAccess

O Gestor de Configuração utiliza este grupo para conceder acesso a ficheiros de visualização recolhidos pelo inventário de software.  

Para mais informações, consulte [Introdução ao inventário de software](../../clients/manage/inventory/introduction-to-software-inventory.md).

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no servidor do site primário.

Ao desinstalar um site, este grupo não é automaticamente removido. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Membership
O Gestor de Configuração gere automaticamente a adesão ao grupo. A associação inclui os utilizadores administrativos que recebem permissão para **Ver Ficheiros Recolhidos** relativamente ao objeto com capacidade de segurança **Recolha** de uma função de segurança atribuída.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem a permissão **de Leitura** para a seguinte pasta no servidor do site:`C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configuration-manager_dviewaccess"></a><a name="configmgr_dviewaccess"></a>Configuração Manager_DViewAccess  

Este grupo é um grupo de segurança local que o Gestor de Configuração cria no servidor de base de dados do site ou no servidor de réplica de base de dados para um site primário infantil. O site cria-o quando utiliza vistas distribuídas para replicação de bases de dados entre sites numa hierarquia. Contém o servidor do site e contas de computador SQL Server do site da administração central.

Para mais informações, consulte [transferências de dados entre sites](data-transfers-between-sites.md).


### <a name="configuration-manager-remote-control-users"></a><a name="configmgr_rcusers"></a>Utilizadores de controlo remoto do Gestor de Configuração  

As ferramentas remotas do Gestor de Configuração utilizam este grupo para armazenar as contas e grupos que configura na lista de **Espectadores Permitidos.** O site atribui esta lista a cada cliente.  

Para mais informações, consulte [Introdução ao controlo remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no cliente do Gestor de Configuração quando o cliente recebe uma política que permite ferramentas remotas.

Depois de desativar ferramentas remotas para um cliente, este grupo não é automaticamente removido. Elimine-o manualmente depois de desativar as ferramentas remotas.

#### <a name="membership"></a>Membership
Por predefinição, não existem membros neste grupo. Quando adiciona os utilizadores à lista de **Espectadores Permitidos,** são automaticamente adicionados a este grupo.

Utilize a lista de **Espectadores Permitidos** para gerir a adesão deste grupo em vez de adicionar utilizadores ou grupos diretamente a este grupo.

Além de ser um espectador permitido, um utilizador administrativo deve ter a permissão de **Controlo Remoto** para o objeto **de Recolha.** Atribua esta permissão utilizando a função de segurança do operador de **ferramentas remotas.**  

#### <a name="permissions"></a>Permissões
Por padrão, este grupo não tem permissões para quaisquer localizações no computador. É usado apenas para manter a lista de **espectadores permitidos.**  


### <a name="sms-admins"></a>Admins de SMS  

O Gestor de Configuração utiliza este grupo para conceder acesso ao Fornecedor SMS através do WMI. O acesso ao Fornecedor SMS é necessário para visualizar e alterar objetos na consola Do Gestor de Configuração.  

> [!NOTE]  
> A configuração da administração baseada em funções de um utilizador administrativo determina quais os objetos que podem visualizar e gerir ao utilizar a consola Do Gestor de Configuração.  

Para mais informações, consulte [Plan for the SMS Provider](plan-for-the-sms-provider.md).

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado em cada computador que tem um Provedor sms. 

Ao desinstalar um site, este grupo não é automaticamente removido. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Membership
O Gestor de Configuração gere automaticamente a adesão ao grupo. Por predefinição, cada utilizador administrativo numa hierarquia e na conta de computador do servidor do site são membros do grupo **SMS Admins** em cada computador do SMS Provider num site.

#### <a name="permissions"></a>Permissões
Pode ver os direitos e permissões do grupo SMS Admins no snap-in do **WMI Control** MMC. Por predefinição, este grupo é concedido **Conta Ativa** e **Viação Remota** no espaço de nome `Root\SMS` WMI. Os utilizadores autenticados têm **Métodos de Execução,** **Escrita do Fornecedor**e Conta Ativa **.**

Quando utilizar uma consola de Configuração Remota, configure as permissões dCOM de **ativação remota** tanto no computador do servidor do site como no Fornecedor SMS. Conceda estes direitos ao grupo **SMS Admins.** Esta ação simplifica a administração em vez de conceder esses direitos diretamente aos utilizadores ou grupos. Para mais informações, consulte [as permissões do DCOM configurar para as consolas remote Configuration Manager](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a>código de site SMS_SiteSystemToSiteServerConnection_MP_ &lt;\>  
 
Os pontos de gestão que são remotos do servidor do site utilizam este grupo para se conectarem à base de dados do site. Este grupo fornece acesso de ponto de gestão às pastas a receber no servidor do site e na base de dados do site.  

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado em cada computador que tem um Provedor sms.

Ao desinstalar um site, este grupo não é automaticamente removido. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Membership
O Gestor de Configuração gere automaticamente a adesão ao grupo. Por predefinição, a associação inclui as contas de computador de computadores remotos que têm um ponto de gestão para o site.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **Read**, **Read & executar**, e lista a permissão de conteúdo da **pasta** para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes` . Este grupo tem a permissão adicional da **Write** para subpastas abaixo **das caixas**de entrada , às quais o ponto de gestão escreve os dados do cliente.


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_ &lt; código de site\>  
 
Os computadores Remote SMS Provider utilizam este grupo para se ligarem ao servidor do site.  

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no servidor do site.

Ao desinstalar um site, este grupo não é automaticamente removido. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Membership
O Gestor de Configuração gere automaticamente a adesão ao grupo. Por predefinição, a subscrição inclui a conta de computador ou uma conta de utilizador de domínio. Utiliza esta conta para se ligar ao servidor do site a partir de cada Fornecedor SMS remoto.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **Read**, **Read & executar**, e lista a permissão de conteúdo da **pasta** para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes` . Este grupo tem as permissões adicionais de **Write** and **Modify** para subpastas abaixo das caixas de entrada. O Fornecedor SMS requer acesso a estas pastas.

Este grupo também tem permissão **de leitura** para as subpastas no servidor do site abaixo `C:\Program Files\Microsoft Configuration Manager\OSD\Bin` . 

Tem também as seguintes permissões para as subpastas `C:\Program Files\Microsoft Configuration Manager\OSD\boot` abaixo:
- **Leitura**  
- **Ler & executar**  
- **Listar conteúdos de pastas**  
- **Escrita**  
- **Modificar**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a>código de site SMS_SiteSystemToSiteServerConnection_Stat_ &lt;\>  

O componente do gestor de despacho de ficheiros nos computadores do sistema remoto do Gestor de Configuração utiliza este grupo para se ligar ao servidor do site.  

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no servidor do site.

Ao desinstalar um site, este grupo não é automaticamente removido. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Membership
O Gestor de Configuração gere automaticamente a adesão ao grupo. Por predefinição, a subscrição inclui a conta de computador ou a conta de utilizador de domínio. Utiliza esta conta para se ligar ao servidor do site a partir de cada sistema de site remoto que executa o gestor de despacho de ficheiros.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **Read**, **Read & executar**, e lista a permissão de conteúdo da **pasta** para a seguinte pasta e as suas subpastas no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes` . 

Este grupo tem as permissões adicionais de **Escrever** e **Modificar** para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box` .


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a>SMS_SiteToSiteConnection_ &lt; código de site\>  
O Gestor de Configuração utiliza este grupo para permitir a replicação baseada em ficheiros entre sites numa hierarquia. Para cada site remoto que transfere diretamente ficheiros para este site, este grupo tem contas configuradas como conta de replicação de **ficheiros**.  

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no servidor do site.

#### <a name="membership"></a>Membership
Quando instala um novo site como criança de outro site, o Gestor de Configuração adiciona automaticamente a conta de computador do novo servidor do site a este grupo no servidor do site principal. O Gestor de Configuração também adiciona a conta de computador do site-mãe ao grupo no novo servidor do site. Se especificar outra conta para transferências baseadas em ficheiros, adicione essa conta a este grupo no servidor do site de destino.

Ao desinstalar um site, este grupo não é automaticamente removido. Elimine-o manualmente depois de desinstalar um site.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **controlo total** para a seguinte pasta: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive` .



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a>Contas que o Gestor de Configuração utiliza  

Pode configurar as seguintes contas para O Gestor de Configuração.  

> [!TIP]
> Não utilize o carácter percentual na `%` palavra-passe para contas que especifica na consola 'Gestor de Configuração'. A conta não autenticará.<!-- SCCMDocs#1032 -->

### <a name="active-directory-group-discovery-account"></a>Conta de descoberta de grupo de diretório ativo  

O site utiliza a conta de descoberta do **grupo Ative Directory** para descobrir os seguintes objetos a partir dos locais nos Serviços de Domínio de Diretório Ativo que especifica:
- Grupos de segurança locais, globais e universais
- A adesão dentro destes grupos
- A adesão dentro dos grupos de distribuição
  - Grupos de distribuição não são descobertos como recursos de grupo

Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Deve ter **a permissão de** acesso ao Diretório Ativo que especifica para descoberta.  

Para mais informações, consulte a descoberta do [grupo Ative Directory.](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)


### <a name="active-directory-system-discovery-account"></a>Conta de descoberta do sistema de diretório ativo  

O site utiliza a conta de descoberta do **sistema Ative Directory** para descobrir computadores a partir dos locais dos Serviços de Domínio de Diretório Ativo que especifica.  

Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Deve ter **a permissão de** acesso ao Diretório Ativo que especifica para descoberta.  

Para mais informações, consulte a descoberta do [sistema de Diretório Ativo.](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)


### <a name="active-directory-user-discovery-account"></a>Conta de descoberta de utilizadores de Diretório Ativo  
 
O site utiliza a conta de descoberta de **utilizadores do Ative Directory** para descobrir contas de utilizadores a partir das localizações nos Serviços de Domínio do Diretório Ativo que especifica.  

Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Deve ter **a permissão de** acesso ao Diretório Ativo que especifica para descoberta.  

Para mais informações, consulte a descoberta do [utilizador do Ative Directy.](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) 


### <a name="active-directory-forest-account"></a>Conta florestal de Diretório Ativo  

O site utiliza a **conta florestal do Diretório Ativo** para descobrir infraestruturas de rede a partir de florestas de Diretório Ativo. Os sites da administração central e os sites primários também o utilizam para publicar dados do site para Serviços de Domínio de Diretório Ativo para uma floresta.  

> [!NOTE]  
> Os sites secundários utilizam sempre a conta de computador de servidor do site secundário para publicar no Active Directory.  

Para descobrir e publicar em florestas não confiáveis, a conta florestal do Diretório Ativo deve ser uma conta global. Se não utilizar a conta de computador do servidor do site, pode selecionar apenas uma conta global.  

Esta conta tem de ter permissões de **Leitura** para cada floresta do Active Directory onde pretende detetar infraestruturas de rede.  

Esta conta deve ter permissões **de Controlo Completo** para o recipiente de Gestão de **Sistemas** e todos os seus objetos infantis em cada floresta de Diretório Ativo onde pretende publicar os dados do site. Para mais informações, consulte Prepare o [Diretório Ativo para a publicação](../network/extend-the-active-directory-schema.md)do site.  

Para mais informações, consulte a [descoberta da floresta de DirectórioActivo.](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)


### <a name="certificate-registration-point-account"></a>Conta de ponto de registo de certificado  

O ponto de registo do certificado utiliza a conta de ponto de **registo do Certificado** para se ligar à base de dados do Gestor de Configuração. Utiliza a sua conta de computador por padrão, mas pode configurar uma conta de utilizador. Quando o ponto de registo do certificado estiver num domínio não confiável do servidor do site, deve especificar uma conta de utilizador. Esta conta requer apenas **ler** o acesso à base de dados do site, porque o sistema de mensagens estatais lida com tarefas de escrita.  

Para mais informações, consulte [Introdução aos perfis de certificados](../../../protect/deploy-use/introduction-to-certificate-profiles.md).


### <a name="capture-os-image-account"></a>Capturar conta de imagem de OS  

Ao capturar uma imagem de OS, o Gestor de Configuração utiliza a conta de **imagem De captura de OS** para aceder à pasta onde armazena imagens capturadas. Se adicionar o passo de **Imagem de Captura OS** numa sequência de tarefas, esta conta é necessária.  

A conta deve ter permissões **de Leitura** e **Escrita** na partilha da rede onde armazena imagens capturadas.  

Se alterar a palavra-passe para a conta no Windows, atualize a sequência de tarefas com a nova palavra-passe. O cliente do Gestor de Configuração recebe a nova palavra-passe quando descarregue a política do cliente.  

Se precisar de utilizar esta conta, crie uma conta de utilizador de domínio. Conceda-lhe permissões mínimas para aceder aos recursos de rede necessários, e use-os para todas as sequências de tarefas de captura.  

> [!IMPORTANT]  
> Não atribua permissões interativas de inscrição nesta conta.  
>   
> Não utilize a conta de acesso à rede para esta conta.  

Para mais informações, consulte Criar uma sequência de [tarefas para capturar um OS](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).


### <a name="client-push-installation-account"></a>Conta de instalação push do cliente  

Quando implementa clientes utilizando o método de instalação push do cliente, o site utiliza a conta de **instalação push Cliente** para se conectar aos computadores e instalar o software cliente do Gestor de Configuração. Se não especificar esta conta, o servidor do site tenta utilizar a sua conta de computador.  

Esta conta deve ser um membro do grupo de **Administradores locais** nos computadores-alvo dos clientes. Esta conta não requer direitos **de Administração do Domínio.**  

Pode especificar mais do que uma conta de instalação push do cliente. O Gestor de Configuração tenta cada um por sua vez até que se tenha sucesso.  

> [!TIP]  
> Se tiver um grande ambiente de Diretório Ativo e precisar de alterar esta conta, utilize o seguinte processo para coordenar mais eficazmente esta atualização da conta: 
> 1. Criar uma nova conta com um nome diferente   
> 2. Adicione a nova conta à lista de contas de instalação push do cliente no Gestor de Configuração  
> 3. Dê tempo suficiente para que os Serviços de Domínio de Diretório Ativo reproduzam a nova conta  
> 4. Em seguida, remova a conta antiga do Gestor de Configuração e dos Serviços de Domínio de Diretório Ativo  

> [!IMPORTANT]  
> Não conceda a esta conta o direito de assinar localmente.  

Para mais informações, consulte a [instalação do impulso do Cliente.](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)


### <a name="enrollment-point-connection-account"></a>Conta de ligação ao ponto de inscrição  

O ponto de inscrição utiliza a conta de ligação do **ponto de inscrição** para ligar à base de dados do site do Gestor de Configuração. Utiliza a sua conta de computador por padrão, mas pode configurar uma conta de utilizador. Quando o ponto de inscrição estiver num domínio não confiável a partir do servidor do site, deve especificar uma conta de utilizador. Esta conta requer **acesso de Leitura** e **Escrita** à base de dados do site.  

Para mais informações, consulte Instalar as funções do sistema do [site para o MDM no local.](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)


### <a name="exchange-server-connection-account"></a>Conta de ligação do Servidor de Troca  

O servidor do site utiliza a conta de **ligação** do Exchange Server para se ligar ao servidor de câmbio especificado. Utiliza esta ligação para encontrar e gerir dispositivos móveis que se ligam ao Exchange Server. Esta conta necessita de cmdlets do Exchange PowerShell que forneçam as permissões necessárias ao computador do Exchange Server. Para obter mais informações sobre os cmdlets, consulte [Instalar e configurar o conector De Troca](../../../mdm/deploy-use/install-configure-exchange-connector.md).  


### <a name="management-point-connection-account"></a>Conta de ligação de ponto de gestão  

O ponto de gestão utiliza a conta de ligação do ponto de **gestão** para ligar à base de dados do site do Gestor de Configuração. Utiliza esta ligação para enviar e recuperar informações para os clientes. O ponto de gestão utiliza a sua conta de computador por padrão, mas pode configurar uma conta de utilizador. Quando o ponto de gestão estiver num domínio não confiável a partir do servidor do site, deve especificar uma conta de utilizador.  

Crie a conta como uma conta local de baixos direitos no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
> Não conceda direitos de inscrição interativos a esta conta.  


### <a name="multicast-connection-account"></a>Conta de ligação multicast  

Os pontos de distribuição multicast-habilitados utilizam a conta de **ligação Multicast** para ler informações da base de dados do site. O servidor utiliza a sua conta de computador por padrão, mas pode configurar uma conta de utilizador. Quando a base de dados do site estiver numa floresta não fidedigna, deve especificar uma conta de utilizador. Por exemplo, se o seu centro de dados tiver uma rede de perímetro numa floresta diferente do servidor do site e da base de dados do site, utilize esta conta para ler as informações multicast a partir da base de dados do site.  

Se precisar desta conta, crie-a como uma conta local de baixos direitos no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
> Não conceda direitos de inscrição interativos a esta conta.  

Para mais informações, consulte [Utilizar o Multicast para implementar o Windows sobre a rede](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).


### <a name="network-access-account"></a>Conta de acesso à rede  

Os computadores clientes usam a conta de acesso à **rede** quando não podem usar a sua conta de computador local para aceder a conteúdos em pontos de distribuição. Aplica-se principalmente a clientes e computadores de grupos de trabalho de domínios não confiáveis. Esta conta também é usada durante a implementação do SISTEMA, quando o computador que está a instalar o SISTEMA ainda não tem uma conta de computador no domínio.  

> [!Important]  
> A conta de acesso à rede nunca é usada como contexto de segurança para executar programas, instalar atualizações de software ou executar sequências de tarefas. É usado apenas para aceder a recursos na rede.  

Um cliente do Gestor de Configuração tenta primeiro utilizar a sua conta de computador para descarregar o conteúdo. Se falhar, tenta automaticamente a conta de acesso à rede.  

Se configurar o site para HTTPS ou [Enhanced HTTP,](enhanced-http.md)um grupo de trabalho ou um cliente com a AD azure pode aceder de forma segura a conteúdos a partir de pontos de distribuição sem a necessidade de uma conta de acesso à rede. Este comportamento inclui cenários de implementação de OS com uma sequência de tarefas que funciona a partir de suportes de arranque, PXE ou Software Center.<!--1358228,1358278--> Para mais informações, consulte cliente para a comunicação de pontos de [gestão.](communications-between-endpoints.md#bkmk_client2mp)<!-- SCCMDocs#1345 -->

> [!Note]  
> Se ativar o **HTTP melhorado** para não necessitar da conta de acesso à rede, o ponto de distribuição tem de ser executar o Windows Server 2012 ou mais tarde. <!--SCCMDocs-pr issue #2696-->
>  
> Atualize os clientes para pelo menos a versão 1806 antes de ativar esta funcionalidade. Se permitir apenas ligações **HTTP melhoradas,** os clientes mais velhos não podem autenticar usando este método, por isso não podem descarregar o pacote de upgrade do cliente a partir de um ponto de distribuição. <!--vso2841213-->   

#### <a name="permissions"></a>Permissões

Conceda a esta conta o menor número possível de permissões ao nível do conteúdo de que o cliente necessita para aceder ao software. A conta deve ter o **Acesso a este computador da rede** diretamente no ponto de distribuição. Pode configurar até 10 contas de acesso à rede por site.  

Crie a conta em qualquer domínio que forneça o acesso necessário aos recursos. A conta de acesso à rede deve incluir sempre um nome de domínio. A segurança de passagem não é suportada para esta conta. Se existirem pontos de distribuição em vários domínios, crie a conta num domínio fidedigno.  

> [!TIP]  
> Para evitar bloqueios de conta, não altere a palavra-passe numa conta de acesso à rede existente. Em vez disso, crie uma nova conta e crie a nova conta no Gestor de Configuração. Quando tiver passado o tempo suficiente para todos os clientes receberem os detalhes da nova conta, remova a conta antiga das pastas partilhadas da rede e elimine a conta.  

> [!IMPORTANT]  
> Não conceda direitos de inscrição interativos a esta conta.  
>   
> Não conceda a esta conta o direito de se juntar aos computadores ao domínio. Se tiver de juntar computadores ao domínio durante uma sequência de tarefas, utilize a conta de união do [domínio da sequência de tarefas](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Configure a conta de acesso à rede  

1.  Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Em seguida, selecione o site.  

2.  No grupo **Definições** da fita, **selecione Configurar componentes**do site, e escolha a Distribuição de **Software**.  

3.  Escolha o separador de conta de acesso à **Rede.** Configurar uma ou mais contas e, em seguida, escolher **OK**.  


### <a name="package-access-account"></a>Conta de acesso ao pacote  

Uma conta de acesso ao **Pacote** permite definir permissões NTFS para especificar os utilizadores e grupos de utilizadores que podem aceder ao conteúdo do pacote em pontos de distribuição. Por predefinição, o Gestor de Configuração dá acesso apenas às contas genéricas de acesso **Utilizador** e **Administrador**. Pode controlar o acesso aos computadores clientes utilizando contas ou grupos windows adicionais. Os dispositivos móveis recuperam sempre o conteúdo do pacote de forma anónima, para que não utilizem uma conta de acesso ao pacote.  

Por predefinição, quando o Gestor de Configuração copia os ficheiros de conteúdo para um ponto de distribuição, concede acesso ao **Read** ao grupo **de Utilizadores** locais e **controlo total** ao grupo de **Administradores locais.** As permissões reais necessárias dependem do pacote. Se tiver clientes em grupos de trabalho ou em florestas não confiáveis, esses clientes utilizam a conta de acesso à rede para aceder ao conteúdo do pacote. Certifique-se de que a conta de acesso à rede tem permissões para o pacote utilizando as contas de acesso definidas ao pacote.  

Utilize contas de um domínio que tenham acesso aos pontos de distribuição. Se criar ou modificar a conta depois de criar a embalagem, terá de redistribuir a embalagem. Atualizar o pacote não altera as permissões ntfs no pacote.  

Não é preciso adicionar a conta de acesso à rede como uma conta de acesso a pacote, porque a adesão ao grupo **Utilizadores** adiciona-a automaticamente. Restringir a conta de acesso ao pacote apenas à conta de acesso à rede não impede que os clientes acedam ao pacote.  

#### <a name="manage-package-access-accounts"></a>Gerir contas de acesso a pacotes  

1.  Na consola De Configuração, escolha a Biblioteca de **Software.**  

2.  No espaço de trabalho da Biblioteca de **Software,** determine o tipo de conteúdo para o qual pretende gerir as contas de acesso e siga os passos fornecidos:  

    - **Aplicação**: Expandir gestão de **aplicações,** escolher **Aplicações,** e, em seguida, selecionar a aplicação para a gestão das contas de acesso.  

    - **Pacote**: Expandir gestão de **aplicações,** escolher **Pacotes**e, em seguida, selecionar o pacote para o qual gerir contas de acesso.  

    - **Pacote de implementação**de atualização de software : Expandir Atualizações de **Software,** escolher **Pacotes de Implementação**e, em seguida, selecionar o pacote de implementação para o qual gerir contas de acesso.  

    - **Pacote do controlador**: Expandir **sistemas operativos,** escolher **Pacotes de Condutor,** e, em seguida, selecionar o pacote do controlador para o qual gerir contas de acesso.  

    - **Imagem OS**: Expandir **sistemas operativos,** escolher **Imagens do Sistema Operativo**e, em seguida, selecionar a imagem do sistema operativo para a qual gerir contas de acesso.  

    - **Pacote de atualização osso**: Expandir **sistemas operativos,** escolher pacotes de **atualização do sistema operativo**e, em seguida, selecionar o pacote de atualização do OS para o qual gerir contas de acesso.  

    - **Imagem de arranque**: Expandir **sistemas operativos,** escolher **Imagens de Arranque**e, em seguida, selecionar a imagem de arranque para a qual gerir contas de acesso.  

3.  Clique no objeto selecionado e, em seguida, escolha **'Gerir contas de acesso'.**  

4.  Na caixa de diálogo **'Conta Adicionar',** especifique o tipo de conta que terá acesso ao conteúdo e, em seguida, especifique os direitos de acesso associados à conta.  

    > [!NOTE]  
    > Quando adiciona um nome de utilizador para a conta, e o Gestor de Configuração encontra uma conta de utilizador local e uma conta de utilizador de domínio com esse nome, o Gestor de Configuração define direitos de acesso para a conta de utilizador de domínio.  


### <a name="reporting-services-point-account"></a>Conta de ponto de serviços de reporte  
 
Os Serviços de Relato do Servidor SQL utilizam a conta de ponto de **ponto de reporte** para recuperar os dados dos relatórios do Gestor de Configuração da base de dados do site. A conta de utilizador do Windows e a palavra-passe que especificar são encriptadas e armazenadas na base de dados do SQL Server Reporting Services.  

> [!NOTE]  
> A conta que especifica deve ter registo de permissões **locais** no computador que acolhe a base de dados dos Serviços de Informação SQL.

> [!NOTE]  
> A conta é automaticamente concedida todos os direitos necessários sendo adicionado ao smsschm_users Função base de dados SQL na base de dados do Gestor de Configuração.

Para mais informações, consulte [Introdução a relatórios.](../../servers/manage/introduction-to-reporting.md)


### <a name="remote-tools-permitted-viewer-accounts"></a>Ferramentas remotas permitidas contas de espectadores  

As contas que especificar como **Visualizadores Autorizados** para o controlo remoto são uma lista de utilizadores autorizados a utilizar a funcionalidade de ferramentas remotas em clientes.  

Para mais informações, consulte [Introdução ao controlo remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).


### <a name="site-installation-account"></a>Conta de instalação do site
<!--SCCMDocs issue #572-->
Utilize uma conta de utilizador de domínio para iniciar sessão no servidor onde executa a configuração do 'Gestor de Configuração' e instale um novo site.

Esta conta requer os seguintes direitos:  

- **Administrador** nos seguintes servidores:
    - O servidor do site  
    - Cada servidor que acolhe a base de dados do site  
    - Cada instância do Fornecedor sms para o site  

- **Sysadmin** na instância do SQL Server que acolhe a base de dados do site  

A configuração do Gestor de Configuração adiciona automaticamente esta conta ao grupo [SMS Admins.](#sms-admins)

Após a instalação, esta conta é o único utilizador com direitos à consola 'Gestor de Configuração'. Se precisar de remover esta conta, certifique-se de adicionar os seus direitos a outro utilizador primeiro.

Ao expandir um site autónomo para incluir um site de administração central, esta conta requer direitos de administração baseados em funções de **Administrador Completo** ou Administrador de **Infraestruturas** no local primário autónomo.


### <a name="site-system-installation-account"></a>Conta de instalação do sistema do site  

O servidor do site utiliza a conta de **instalação** do sistema Site para instalar, reinstalar, desinstalar e configurar sistemas de site. Se configurar o sistema de site para exigir que o servidor do site inicie ligações a este sistema de site, o Gestor de Configuração também utiliza esta conta para retirar dados do sistema do site depois de instalar o sistema do site e quaisquer funções. Cada sistema de site pode ter uma conta de instalação diferente, mas você pode configurar apenas uma conta de instalação para gerir todas as funções no sistema de site.  

Esta conta requer permissões administrativas locais nos sistemas do site alvo. Além disso, esta conta deve ter **acesso a este computador a partir da rede** na política de segurança nos sistemas de site alvo.  

> [!TIP]  
> Se tiver muitos controladores de domínio e estas contas forem utilizadas em domínios, antes de configurar o sistema de site, verifique se o Ative Directory replicou estas contas.  
>   
> Quando especifica uma conta local em cada sistema de site a ser gerida, esta configuração é mais segura do que usar contas de domínio. Limita os danos que os atacantes podem fazer se a conta estiver comprometida. No entanto, as contas de domínio são mais fáceis de gerir. Considere a troca entre a segurança e a administração eficaz.  


### <a name="site-system-proxy-server-account"></a>Conta de servidor proxy do sistema do site
<!--SCCMDocs issue #648-->
As seguintes funções do sistema do site utilizam a conta proxy **do sistema site** para aceder à internet através de um servidor de procuração ou firewall que requer acesso autenticado:

- Ponto de sincronização do Asset Intelligence
- Conector do Exchange Server
- Ponto de ligação de serviço
- Ponto de atualização de software

> [!IMPORTANT]  
> Especifique uma conta que tenha o menor número possível de permissões para a firewall ou o servidor proxy necessário.  

Para mais informações, consulte o [suporte do servidor Proxy](../network/proxy-server-support.md).


### <a name="smtp-server-connection-account"></a>Conta de ligação ao servidor SMTP  

O servidor do site utiliza a conta de ligação do **servidor SMTP** para enviar alertas de e-mail quando o servidor SMTP necessitar de acesso autenticado.  

> [!IMPORTANT]  
> Especifique uma conta que tenha o menor número possível de permissões para enviar mensagens de correio eletrónico.  

Para mais informações, consulte [Alertas de Utilização e o sistema de estado](../../servers/manage/use-alerts-and-the-status-system.md).


### <a name="software-update-point-connection-account"></a>Conta de ligação de ponto de atualização de software  

O servidor do site utiliza a conta de ligação de ponto de **atualização** do Software para os seguintes dois serviços de atualização de software:  

- Serviços de Atualização do Servidor do Windows (WSUS), que configura definições como definições de produtos, classificações e definições a montante.  

- WSUS Synchronization Manager, que pede a sincronização a um servidor WSUS a montante ou ao Microsoft Update.  

A conta de [instalação](#site-system-installation-account) do sistema do site pode instalar componentes para atualizações de software, mas não pode executar funções específicas de atualização de software no ponto de atualização do software. Se não puder utilizar a conta do computador do servidor do site para esta funcionalidade porque o ponto de atualização do software está numa floresta não confiável, deve especificar esta conta para além da conta de instalação do sistema do site.  

Esta conta deve ser um administrador local no computador onde instala o WSUS. Deve também fazer parte do grupo local de **administradores da WSUS.**  

Para mais informações, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md)de software .


### <a name="source-site-account"></a>Conta de site de origem  

O processo de migração utiliza a **conta do site Source** para aceder ao Fornecedor SMS do site de origem. Esta conta precisa de permissões de **Leitura** a objetos de site no site de origem para recolher dados para tarefas de migração.  

Se tiver pontos de distribuição do Gestor de Configuração 2007 ou sites secundários com pontos de distribuição colocalizados, quando os atualiza para pontos de distribuição do Gestor de Configuração (filial atual), esta conta também deve ter permissões **de Exclusão** para a classe **Site.** Esta permissão é remover com sucesso o ponto de distribuição do site 'Gestor de Configuração 2007' durante a atualização.  

> [!NOTE]  
> Tanto a conta do site de origem como a conta de base de dados do [site de origem](#source-site-database-account) são identificadas como **Gestorde Migração** no nó de **Contas** do espaço de trabalho da **Administração** na consola do Gestor de Configuração.  

Para obter mais informações, consulte os [dados migrados entre hierarquias](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Conta de base de dados do site de origem  

O processo de migração utiliza a conta de base de dados do **site Source** para aceder à base de dados do SQL Server para o site de origem. Para recolher dados da base de dados do Servidor SQL do site de origem, a conta de base de dados do site de origem deve ter as permissões **de Leitura** e **Execução** para a base de dados do Servidor SQL do site de origem.  

Se utilizar a conta de computador Do Gestor de Configuração (ramo atual), certifique-se de que todos os seguintes são verdadeiros para esta conta:  
  
- É um membro do grupo de segurança distribuído **supor utilizadores com o** mesmo domínio que o site 'Gestor de Configuração' 2007  
- É um membro do grupo de segurança **SMS Admins**  
- Tem a permissão **de Leitura** para todos os objetos do Gestor de Configuração 2007  

> [!NOTE]  
> Tanto a conta do site de origem como a conta de base de dados do [site de origem](#source-site-database-account) são identificadas como **Gestorde Migração** no nó de **Contas** do espaço de trabalho da **Administração** na consola do Gestor de Configuração.  

Para obter mais informações, consulte os [dados migrados entre hierarquias](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Grupo de sequência de tarefas junta-se à conta 

O Windows Setup utiliza a conta de união de ficheiros de **sequência de tarefas** para se juntar a um computador recém-imagem do domínio. Esta conta é exigida pelo passo da sequência de tarefas [do Domínio de Join ou](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) do Grupo de Trabalho com a opção Join a **domain.** Esta conta também pode ser configurada com o passo de Definições de [Rede Aplicada,](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings) mas não é necessário.  

Esta conta requer o **Domínio Unir-se** diretamente no domínio alvo.  

> [!TIP]  
> Crie uma conta de utilizador de domínio com as permissões mínimas para se juntar ao domínio e use-a para todas as sequências de tarefas.  

> [!IMPORTANT]  
> Não atribua permissões interativas de inscrição nesta conta.  
>   
> Não utilize a conta de acesso à rede para esta conta.  


### <a name="task-sequence-network-folder-connection-account"></a>Conta de ligação de rede de sequência de tarefas  

O motor de sequência de tarefas utiliza a conta de ligação da **sequência de tarefas** para ligar a uma pasta partilhada na rede. Esta conta é exigida pelo passo de sequência de tarefas [connect to Network Folder.](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

Esta conta requer permissões para aceder à pasta partilhada especificada. Deve ser uma conta de utilizador de domínio.  

> [!TIP]  
> Crie uma conta de utilizador de domínio com permissões mínimas para aceder aos recursos de rede necessários e use-a para todas as sequências de tarefas.  

> [!IMPORTANT]  
> Não atribua permissões interativas de inscrição nesta conta.  
>   
> Não utilize a conta de acesso à rede para esta conta.  


### <a name="task-sequence-run-as-account"></a>Sequência de tarefas executada como conta  

O motor de sequência de tarefas utiliza a sequência de **tarefas como conta** para executar linhas de comando ou scripts PowerShell com credenciais diferentes da conta do Sistema Local. Esta conta é exigida pela Linha de [Comando executar](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) e executar passos de sequência de [script powershell](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) com a opção **Executar este passo como a seguinte conta** escolhida.  

Configurar a conta para dispor das permissões mínimas necessárias para executar a linha de comando que especifica na sequência de tarefas. A conta requer direitos de inscrição interativos. Geralmente requer a capacidade de instalar software e aceder a recursos de rede. Para a tarefa do Script Run PowerShell, esta conta requer permissões de administrador local. 

> [!IMPORTANT]  
> Não utilize a conta de acesso à rede para esta conta.  
>   
> Nunca faça da conta um administrador de domínio.  
>   
> Nunca configurar perfis de roaming para esta conta. Quando a sequência de tarefas é executado, descarrega o perfil de roaming para a conta. Isto deixa o perfil vulnerável ao acesso no computador local.  
>   
> Limite o âmbito da conta. Por exemplo, criar diferentes sequências de tarefas executadas como explicações para cada sequência de tarefas. Então, se uma conta estiver comprometida, apenas os computadores clientes a que essa conta tem acesso estão comprometidos.  
>   
> Se a linha de comando necessitar de acesso administrativo no computador, considere criar uma conta de administrador local apenas para esta conta em todos os computadores que executam a sequência de tarefas. Apague a conta uma vez que já não precise.  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a>Objetos de utilizador que o Gestor de Configuração utiliza no SQL 
<!--SCCMDocs issue #1160-->
O Gestor de Configuração cria e mantém automaticamente os seguintes objetos de utilizador no SQL.  Estes objetos estão localizados na base de dados do Gestor de Configuração em Segurança/Utilizadores.  

> [!IMPORTANT]  
>  Modificar ou remover estes objetos pode causar problemas drásticos dentro de um ambiente de Gestor de Configuração.  Recomendamos que não faça alterações a estes objetos.


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

Este objeto é usado para executar consultas sob o contexto apenas de leitura.  Este objeto é alavancado com vários procedimentos armazenados.


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

Este objeto é utilizado para fornecer permissões para declarações Dinâmicas SQL.


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

Este objeto é usado para executar execuções de reporte SQL.  O seguinte procedimento armazenado é utilizado com esta função: spSRExecQuery.


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Funções de base de dados que o Gestor de Configuração utiliza no SQL
<!--SCCMDocs issue #1160-->
O Gestor de Configuração cria e mantém automaticamente os seguintes objetos de função no SQL. Estas funções fornecem acesso a procedimentos, tabelas, visualizações e funções específicos armazenados para executar as ações necessárias de cada função para recuperar dados ou inserir dados de e para a base de dados do Gestor de Configuração. Estes objetos estão localizados na base de dados do Gestor de Configuração sob funções de segurança/roles/base de dados.

> [!IMPORTANT]  
> Modificar ou remover estes objetos pode causar problemas drásticos dentro de um ambiente de Gestor de Configuração. Não mude estes objetos. A lista que se segue é apenas para fins informantes.

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Importações de licenças de volume de inteligência de ativos. O Gestor de Configuração concede esta permissão às contas dos utilizadores com base no acesso da RBA para poder importar licença de volume para ser usada com inteligência de ativos.  Esta conta poderia ser adicionada por uma função de administrador completo ou por uma função de Gestor de Ativos.

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Sincronização de atualização de inteligência de ativos. O Gestor de Configuração concede à conta de computador que acolhe o acesso à conta de Sincronização de Informação de Ativos para obter dados de procuração de Inteligência de Ativos e para visualizar dados de IA pendentes para upload.

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

Fora da Gestão de Bandas. Esta função é usada pela função AMT do Gestor de Configuração para recuperar dados em dispositivos que suportavam a Intel AMT.

> [!NOTE]  
> Este papel é depreciado em lançamentos mais recentes do Gestor de Configuração.

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

Ponto de registo de certificado suster Protocolo de Inscrição simples de Certificado (SCEP). O Gestor de Configuração concede permissão à conta de computador do sistema de site que suporta o Ponto de Registo de Certificado para suporte SCEP para assinatura e renovação de certificados.

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

Suporte PFX ponto de registo do certificado. O Gestor de Configuração concede permissão à conta de computador do sistema do site que suporta o Ponto de Registo de Certificado configurado para suporte PFX para assinatura e renovação.

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

Ponto de gestão de dispositivos. O Gestor de Configuração concede esta permissão à conta de computador para um Ponto de Gestão que tem a opção: "Permitir que dispositivos móveis e Computador Mac usem este ponto de gestão", a capacidade de fornecer suporte para dispositivos matriculados em MDM.

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

Ponto de ligação de serviço. O Gestor de Configuração concede esta permissão à conta de computador que acolhe o Ponto de Ligação de Serviço para recuperar e fornecer dados de telemetria, gerir serviços na nuvem e recuperar atualizações de serviço.

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

Vistas distribuídas. O Gestor de Configuração concede esta permissão à conta de computador dos Servidores do Site Primário no CAS quando a opção de visualizações distribuídas pelo SQL Server é selecionada nas propriedades do link de replicação.

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

Armazém de Dados. O Gestor de Configuração concede esta permissão à conta de computador que acolhe o papel de Data Warehouse.

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 Ponto de matrícula. O Gestor de Configuração concede esta permissão à conta de computador que acolhe o Ponto de Inscrição para permitir a inscrição do dispositivo através do MDM.

### <a name="smsdbrole_extract"></a>smsdbrole_extract

Proporciona acesso a todas as vistas de esquemas estendidas.

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

Serviço de Gerente de Hierarquia. O Gestor de Configuração concede permissões a esta conta para gerir as mensagens de estado failover e as transações de SQL Server Broker entre sites dentro de uma hierarquia.

> [!NOTE]  
> O papel smdbrole_WebPortal é um membro deste papel por defeito.

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

Serviço Multicast. O Gestor de Configuração concede esta permissão à conta de computador do Ponto de Distribuição que suporta o multicast.

### <a name="smsdbrole_mp"></a>smsdbrole_MP

Ponto de gestão. O Gestor de Configuração concede esta permissão à conta de computador que acolhe a função Management Point para fornecer suporte aos clientes do Gestor de Configuração.

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

Ponto de gestão Microsoft BitLocker Administration and Monitoring. O Gestor de Configuração concede esta permissão à conta de computador que acolhe o Ponto de Gestão que gere o MBAM para um ambiente.

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

Pedido de pedido de pedido de ponto de gestão. O Gestor de Configuração concede esta permissão à conta de computador que acolhe o Ponto de Gestão para apoiar pedidos de aplicação baseados no utilizador.

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

Provedor de SMS. O Gestor de Configuração concede esta permissão à conta de computador que acolhe uma função de Provedor de SMS.  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

Servidor do site. O Gestor de Configuração concede esta permissão à conta de computador que acolhe o Sítio Principal ou CAS.

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

Ponto de atualização de software. O Gestor de Configuração concede esta permissão à conta de computador que acolhe o Ponto de Atualização de Software para trabalhar com atualizações de terceiros.

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

Ponto do web site do catálogo de aplicações. O Gestor de Configuração concede permissão à conta de computador que acolhe o Ponto do Web Site do Catálogo de Aplicações para fornecer a implementação da aplicação baseada no utilizador.

### <a name="smsschm_users"></a>smsschm_users

Acesso ao relatório do utilizador. O Gestor de Configuração concede acesso à conta utilizada para a conta ponto de reporte de Serviços de Informação para permitir o acesso às visualizações de relatórios sms para exibir os dados de relatórios do Gestor de Configuração.  Os dados são ainda restringidos com a utilização da RBA.

## <a name="elevated-permissions"></a>Permissões elevadas

<!-- SCCMDocs#405 -->

O Gestor de Configuração requer que algumas contas tenham permissões elevadas para operações em curso. Por exemplo, consulte [os pré-requisitos para a instalação de um local primário](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_PrereqPri). A lista que se segue resume estas permissões e as razões pelas quais são necessárias.

- A conta de computador do servidor do site primário e do servidor do site da administração central requer:

  - Direitos do Administrador Local em todos os servidores do sistema do site. Esta permissão é gerir, instalar e remover serviços do sistema. O servidor do site também atualiza os grupos locais no sistema do site quando adiciona ou remove funções.

  - Acesso sysadmin à instância SQL para a base de dados do site. Esta permissão é configurar e gerir o SQL para o site. O Gestor de Configuração integra-se firmemente com o SQL, não é apenas uma base de dados.

- As contas de utilizador na função de Administrador Completo requerem:

  - Direitos do Administrador Local em todos os servidores do site. Esta permissão é visualizar, editar, remover e instalar serviços de sistema, chaves e valores de registo e objetos WMI.

  - Acesso sysadmin à instância SQL para a base de dados do site. Esta permissão é instalar e atualizar a base de dados durante a configuração ou recuperação. Também é necessário para manutenção e operações SQL. Por exemplo, reindexar e atualizar estatísticas.

    > [!NOTE]
    > Algumas organizações podem optar por remover o acesso à sysadmina e apenas concedê-la quando é necessário. Este comportamento é por vezes referido como "acesso just-in-time (JIT)". Neste caso, os utilizadores com a função de Administrador Completo devem ainda ter acesso a procedimentos de leitura, atualização e execução na base de dados do Gestor de Configuração. Estas permissões permitem-lhes resolver a maioria dos problemas sem acesso total à sisadmina.
