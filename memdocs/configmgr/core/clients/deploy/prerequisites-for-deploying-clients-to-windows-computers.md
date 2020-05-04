---
title: Pré-requisitos de implementação do cliente windows
titleSuffix: Configuration Manager
description: Conheça os pré-requisitos para a implementação do cliente do Gestor de Configuração para computadores Windows.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d4cd7ffe38f7191a5361ad2e89817ea80f9f093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713976"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Pré-requisitos para a implementação de clientes para computadores Windows em 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*

A implementação de clientes do Gestor de Configuração no seu ambiente tem as seguintes dependências e dependências externas dentro do produto. Além disso, cada método de implementação de clientes tem as suas próprias dependências, que deverão ser satisfeitas para que as instalações de clientes tenham êxito.  

Para obter mais informações sobre os requisitos mínimos de hardware e OS para o cliente do Gestor de Configuração, consulte [configurações suportadas](../../plan-design/configs/supported-configurations.md).  

> [!NOTE]  
> Os números de versão do software apresentados neste artigo listam apenas os números de versão mínima necessários.  


## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a>Pré-requisitos para clientes Windows  

Utilize as seguintes informações para determinar os pré-requisitos para quando instalar o cliente do Gestor de Configuração nos dispositivos Windows.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Componente|Descrição|  
|---|---|  
|Windows Installer versão 3.1.4000.2435|Necessário para suportar a utilização de ficheiros de atualização do Windows Installer (.msp) para pacotes e atualizações de software.|  
|Serviço de Transferência Inteligente em Segundo Plano Microsoft (BITS) versão 2.5|Necessário para permitir transferências de dados estranguladas entre o computador cliente e os sistemas de site do Gestor de Configuração. O BITS não é automaticamente descarregado durante a instalação do cliente. Quando o BITS é instalado em computadores, normalmente requer um reinício para completar a instalação.<br /><br /> A maioria dos sistemas operativos incluem BITS. Se não o fizerem, instale BITS antes de instalar o cliente do Gestor de Configuração.|  
|Programador de Tarefas Microsoft|Ative este serviço no cliente para que a instalação do cliente esteja concluída.|  
|Suporte de assinatura de código SHA-2|A partir da versão 1906, os clientes requerem suporte para o algoritmo de assinatura de código SHA-2. Para mais informações, consulte o suporte de [assinatura de código SHA-2](#bkmk_sha2).|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a>Suporte de assinatura de código SHA-2

<!--SCCMDocs-pr#3404-->
Devido às fraquezas no algoritmo SHA-1 e a alinhar-se com os padrões da indústria, a Microsoft agora apenas assina binários de Gestor de Configuração usando o algoritmo SHA-2 mais seguro. As versões Legacy Windows OS requerem uma atualização para o suporte de assinatura de código SHA-2. Para mais informações, consulte o requisito de suporte de [assinatura de código SHA-2 2 para Windows e WSUS](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus).

Se não atualizar estas versões DE, não pode instalar a versão cliente do Gestor de Configuração 1906. Este comportamento aplica-se a um novo cliente instalá-lo ou atualizá-lo a partir de uma versão anterior.

Se necessitar de gerir um cliente numa versão do Windows que não seja atualizada, ou mais antiga do que as versões acima listadas, utilize a versão 1902 do cliente de interoperabilidade estendida do Gestor de Configuração (EIC). Para mais informações, consulte o cliente de [interoperabilidade alargado](../../understand/interoperability-client.md).

> [!Tip]  
> Se não utilizar a [atualização automática](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)do cliente e atualizar os clientes com outro mecanismo, certifique-se de atualizar a versão do ccmsetup. Uma versão mais antiga do ccmsetup não pode validar adequadamente o novo certificado de assinatura de código SHA-2 nos binários de clientes da versão 1906. Por exemplo, se copiar ccmsetup.exe para uma parte de ficheiro, ou utilizar ccmsetup.msi com a política de grupo.<!-- 4963362 -->
>
> Os seguintes mecanismos de atualização do cliente não devem ser afetados:
>
> - Instalação push do cliente: Utiliza o pacote de cliente a partir do site
> - Instalação baseada em atualização de software: A atualização do site reedita para a WSUS
> - Dispositivos Windows geridos pelo MDM intune: A versão suportada para este mecanismo já suporta a assinatura de código SHA-2, mas ainda é importante utilizar os mais recentes ccmsetup.msi

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a>Dependências externas ao Gestor de Configuração e automaticamente descarregadas durante a instalação  

O cliente do Gestor de Configuração tem dependências externas. Estas dependências dependem da versão S e do software instalado no computador cliente.  

Se o cliente necessitar destas dependências para completar a instalação, instala-as automaticamente.  

|Componente|Descrição|  
|---|---|  
|Windows Update Agent versão 7.0.6000.363|Necessário para o Windows suportar a deteção e implementação de atualizações.|  
|Microsoft Core XML Services (MSXML) versão 6.20.5002 ou posterior|Necessário para suportar o processamento de documentos XML no Windows.|  
|Compressão de Diferencial Remota da Microsoft (RDC)|Necessário para otimizar a transmissão de dados através da rede.|  
|Microsoft Visual C++ 2013 Redistributable versão 12.0.21005.1|Necessário para suportar operações de cliente. Quando instalar esta atualização nos computadores dos clientes, poderá necessitar de um reinício para concluir a instalação.|  
|Microsoft Visual C++ 2005 Redistributable versão 8.0.50727.42|Para a versão 1606 e anterior, necessário suportar as operações do Microsoft SQL Server Compact.|  
|APIs Windows Imaging 6.0.6001.18000|Necessário para permitir que o Gestor de Configuração gere ficheiros de imagem do Windows (.wim).|  
|Microsoft Policy Platform 1.2.3514.0|Necessário para permitir aos clientes avaliar as definições de compatibilidade.|  
|Microsoft .NET Framework versão 4.5.2|Necessário para suportar operações de cliente. Instalado automaticamente no computador cliente se não tiver a versão 4.5 do Microsoft .NET Framework ou posteriormente instalada. Para obter mais informações, veja [Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2](#dotNet).|  
|Componentes Do Microsoft SQL Server Compact 4.0 SP1|Necessários para armazenar informações relacionadas com operações de cliente.|  

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> Se ainda estiver a utilizar a experiência do utilizador do catálogo de aplicações, o cliente requer o Microsoft Silverlight 5.1.41212.0. O cliente não instala automaticamente silverlight. A funcionalidade principal do catálogo de aplicações está agora incluída no Software Center.<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a>Detalhes adicionais sobre a versão 4.5.2 do Quadro da Microsoft .NET  

> [!NOTE]  
> .NET 4.0, 4.5 e 4.5.1 já não são suportados. Para mais informações, consulte [microsoft .NET Framework Support Lifecycle Policy FAQ](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

A versão 4.5.2 da Microsoft .NET Framework pode necessitar de um reinício para concluir a instalação. O utilizador vê uma notificação **requerida** no tabuleiro do sistema. Os seguintes cenários comuns requerem que os computadores clientes reiniciem:  

- Serviços ou aplicações .NET estão em execução no computador.  

- Uma ou mais atualizações de software necessárias para a instalação do .NET estão em falta.  

- Um reinício do computador está pendente desde a instalação anterior de atualizações do software .NET Framework.  

Depois de instalado o .NET Framework 4.5.2, pode necessitar de atualizações adicionais. Estas atualizações posteriores podem requerer reinícios adicionais do computador.  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

Para mais informações, consulte [Determinar as funções do sistema do site para os clientes.](plan/determine-the-site-system-roles-for-clients.md)  

|Componente|Descrição|  
|---|---|  
|Ponto de gestão|Para implementar o cliente do Gestor de Configuração, não precisa de um ponto de gestão. Os clientes requerem um ponto de gestão para transferir informação com o site. Sem um ponto de gestão, não se pode gerir computadores de clientes.|  
|Ponto de distribuição|O ponto de distribuição é uma função opcional, mas recomendada do sistema de site para a implementação e gestão do cliente. Todos os pontos de distribuição acolhem os ficheiros de origem do cliente. Os clientes encontram o ponto de distribuição mais próximo para descarregar os ficheiros de origem durante a implementação ou atualização do cliente. Se o site não tiver um ponto de distribuição, os computadores descarregam os ficheiros de origem do cliente a partir do seu ponto de gestão.|  
|Ponto de estado de contingência|O ponto de estado de contingência é uma função do sistema de sites opcional mas recomendada para implementação de cliente. O ponto de estado de recuo rastreia a implementação do cliente e permite que os computadores no site do Gestor de Configuração enviem mensagens de Estado quando não conseguem comunicar com um ponto de gestão.|  
|Ponto do Reporting Services|O ponto de serviços de reporte é uma função opcional, mas recomendada do sistema de site. Apresenta relatórios relacionados com a implantação e gestão do cliente. Para mais informações, consulte [Introdução a relatórios.](../../servers/manage/introduction-to-reporting.md)|  

### <a name="installation-method-dependencies"></a>Dependências do método de instalação  

Os pré-requisitos seguintes são específicos para os vários métodos de instalação de cliente.  

#### <a name="client-push-installation"></a>Instalação push do cliente  

- O site utiliza contas de instalação de impulso do cliente para se ligar a computadores para instalar o cliente. Especifique estas contas no separador **Contas** das Propriedades de Instalação push do cliente. A conta tem de ser membro do grupo de administradores local no computador de destino.  

    Se não especificar uma conta de instalação push do cliente, o servidor do site utiliza a sua conta de computador.  

- O site precisa de descobrir o computador no qual está a instalar o cliente. Pelo menos um método de descoberta do Gestor de Configuração é necessário.  

- O computador tem uma partilha ADMIN$.  

- Para empurrar automaticamente o cliente do Gestor de Configuração para os recursos descobertos, selecione a opção de ativar a instalação de push do **cliente para os recursos atribuídos** nas Propriedades de Instalação push do cliente.  

- O computador cliente precisa de comunicar com um ponto de distribuição ou um ponto de gestão para descarregar os ficheiros de origem.  

- Quando você requer a autenticação mútua Kerberos, os clientes devem estar numa floresta de Diretório Ativo confiável. Kerberos no Windows conta com o Diretório Ativo para autenticação mútua.<!--1358204-->  

Para utilizar o impulso do cliente, precisa das seguintes permissões de segurança:  

- Para configurar a conta de instalação push do cliente: **Modificar** e **ler** permissão para o objeto **do Site.**  

- Para utilizar o impulso do cliente para instalar o cliente em coleções, dispositivos e consultas: **Modificar recurso** e **ler** permissão para o objeto **de recolha.**  

A função de segurança predefinida do **Administrador de Infraestrutura** inclui as permissões necessárias para gerir as instalações push do cliente.  

#### <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  

- Se não tiver ampliado o esquema de Diretório Ativo, ou se estiver a instalar clientes de outra floresta, utilize a política do grupo para fornecer parâmetros de instalação para CCMSetup.exe. Para mais informações, consulte [Como fornecer propriedades de instalação de clientes.](deploy-clients-to-windows-computers.md#BKMK_Provision)  

- Publique o cliente do Gestor de Configuração no ponto de atualização do software.  

- Para descarregar os ficheiros de origem, o computador cliente precisa de comunicar com um ponto de distribuição ou um ponto de gestão.  

Para obter as permissões de segurança necessárias para gerir as atualizações de software do Gestor de Configuração, consulte [os pré-requisitos para atualizações](../../../sum/plan-design/prerequisites-for-software-updates.md)de software .  

#### <a name="group-policy-based-installation"></a>Instalação baseada em políticas do grupo  

- Se não tiver ampliado o esquema de Diretório Ativo, ou se estiver a instalar clientes de outra floresta, utilize a política do grupo para fornecer parâmetros de instalação para CCMSetup.exe. Para mais informações, consulte [Como fornecer propriedades de instalação de clientes.](deploy-clients-to-windows-computers.md#BKMK_Provision)  

- Para descarregar os ficheiros de origem, o computador cliente precisa de comunicar com um ponto de distribuição ou um ponto de gestão.  

#### <a name="logon-script-based-installation"></a>Instalação baseada no script de início de sessão  

Para descarregar os ficheiros de origem, o computador cliente precisa de comunicar com um ponto de distribuição ou um ponto de gestão. A menos que tenha especificado CCMSetup.exe com o seguinte parâmetro de linha de comando:`ccmsetup /source`  

#### <a name="manual-installation"></a>Instalação manual  

Para descarregar os ficheiros de origem, o computador cliente precisa de comunicar com um ponto de distribuição ou um ponto de gestão. A menos que tenha especificado CCMSetup.exe com o seguinte parâmetro de linha de comando:`ccmsetup /source`  

#### <a name="microsoft-intune-mdm-installation"></a>Instalação do MICROSOFT Intune MDM

- Requer uma subscrição Microsoft Intune e licenças apropriadas.  

- Requer que o dispositivo tenha acesso à Internet, mesmo que não seja baseado na Internet.  

- Dependendo do caso de utilização, também pode requerer uma ou ambas as seguintes tecnologias:  

    - Azure Active Directory  

    - Gateway de gestão da cloud  

#### <a name="workgroup-computer-installation"></a>Instalação do computador do grupo de trabalho  

Para aceder aos recursos no domínio do servidor do site do Gestor de Configuração, configure uma conta de acesso à rede para o site.  

Para obter mais informações sobre como configurar a conta de acesso à rede, consulte os [conceitos Fundamentais para a gestão](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)de conteúdos.  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Instalação baseada em distribuição de software (apenas para atualizações)  

- Se não tiver ampliado o esquema de Diretório Ativo, ou se estiver a instalar clientes de outra floresta, utilize a política do grupo para fornecer parâmetros de instalação para CCMSetup.exe. Para mais informações, consulte [Como fornecer propriedades de instalação de clientes.](deploy-clients-to-windows-computers.md#BKMK_Provision)

- Para descarregar os ficheiros de origem, o computador cliente precisa de comunicar com um ponto de distribuição ou um ponto de gestão.  

Para as permissões de segurança necessárias para atualizar o cliente do Gestor de Configuração utilizando a gestão da aplicação, consulte segurança e privacidade para a gestão de [aplicações.](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

#### <a name="automatic-client-upgrades"></a>Atualizações automáticas de clientes  

Terá de ser membro da função de segurança **Administrador Total** para configurar atualizações automáticas de clientes.  

### <a name="firewall-requirements"></a>Requisitos de firewall  

Se houver uma firewall entre os servidores do sistema do site e os computadores em que pretende instalar o cliente do Gestor de Configuração, consulte as [definições do Windows Firewall e da porta para os clientes](windows-firewall-and-port-settings-for-clients.md).  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a>Pré-requisitos para clientes de dispositivos móveis  

Quando instalar o cliente do Gestor de Configuração em dispositivos móveis e matriculá-los, utilize estas informações para determinar os pré-requisitos.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager

- Uma autoridade de certificação (AC) empresarial da Microsoft com modelos de certificado para implementar e gerir os certificados necessários para dispositivos móveis.  

    A AC emissora terá de aprovar automaticamente os pedidos de certificados dos utilizadores de dispositivos móveis durante o processo de inscrição.  

    Para obter mais informações sobre os requisitos do certificado, consulte Segurança e privacidade para perfis de [certificados](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

- Um grupo de segurança que contenha os utilizadores que podem inscrever os respetivos dispositivos móveis.  

    Este grupo de segurança é utilizado para configurar o modelo de certificado que é utilizado durante a inscrição de dispositivos móveis.  

- Opcional mas recomendado: um pseudónimo DNS (cname record) chamado **ConfigMgrEnroll**. Configure este pseudónimo para o nome do servidor do ponto de procuração de inscrição.  

    Este pseudónimo DNS é necessário para apoiar a descoberta automática para o serviço de inscrição. Se não configurar este registo dNS, os utilizadores devem especificar manualmente o nome do ponto de procuração de inscrição como parte do processo de inscrição.  

- Dependências de funções do sistema do site para os computadores que executam o ponto de inscrição e as funções do sistema de proxy de ponto de inscrição.  

    Para obter mais informações, consulte [sistemas operativos suportados para servidores](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)do sistema do site .  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager

Para mais informações, consulte [Determinar as funções do sistema do site para os clientes.](plan/determine-the-site-system-roles-for-clients.md)  

- Ponto de gestão configurado para ligações ao cliente HTTPS e ativado para dispositivos móveis  

    É sempre necessário um ponto de gestão para instalar o cliente do Gestor de Configuração em dispositivos móveis. Para além dos requisitos de configuração do HTTPS e habilitados para dispositivos móveis, o ponto de gestão deve ser configurado com um FQDN de internet e aceitar ligações de clientes a partir da internet.  

- Ponto de registo e ponto proxy de registo  

    Um ponto proxy de registo gere os pedidos de inscrição de dispositivos móveis e o ponto de registo conclui o processo de inscrição. O ponto de registo terá de estar na mesma floresta do Active Directory que o servidor de site, mas o ponto proxy de registo poderá estar noutra floresta.  

- Definições de cliente para a inscrição de dispositivos móveis  

    Configure as definições de cliente para permitir que os utilizadores inscrevam dispositivos móveis e configurem pelo menos um perfil de inscrição.  

- Ponto do Reporting Services  

    O ponto do Reporting Services é uma função do sistema de sites opcional mas recomendada, que permite apresentar relatórios relacionados com a inscrição de dispositivos móveis e a gestão de clientes.  

    Para mais informações, consulte [Introdução a relatórios.](../../servers/manage/introduction-to-reporting.md)  

- Para configurar a inscrição de dispositivos móveis, terá de possuir as seguintes permissões de segurança:  

    - Para adicionar, modificar e eliminar as funções do sistema de sites de inscrição: permissão **Modificar** para o objeto **Site**.  

    - Para configurar as definições de cliente para inscrição: as predefinições de cliente precisam da permissão **Modificar** para o objeto **Site** e as definições personalizadas de cliente precisam das permissões **Agente de cliente**.  

    A função de segurança predefinida do **Administrador Completo** inclui as permissões necessárias para configurar as funções do sistema do site de inscrição.  

- Para gerir os dispositivos móveis inscritos, terá de possuir as seguintes permissões de segurança:  

    - Para apagar ou extinguir um dispositivo móvel: **Eliminar recurso** para o objeto **Coleção**.  

    - Para cancelar um comando de eliminação ou extinção: **Eliminar recurso** para o objeto **Coleção**.  

    - Para permitir e bloquear dispositivos móveis: **Modificar recurso** para o objeto **Coleção** .  

    - Bloqueio remoto ou reposição do código de acesso num dispositivo móvel: **Modificar** recurso para o objeto **Coleção**.  

    A função de segurança predefinida do **Administrador de Operações** inclui as permissões necessárias para gerir dispositivos móveis.  

    Para obter mais informações sobre como configurar permissões de segurança, consulte [os fundamentos da administração baseada em papéis](../../understand/fundamentals-of-role-based-administration.md) e [a configuração da administração baseada em papéis.](../../servers/deploy/configure/configure-role-based-administration.md)  

### <a name="firewall-requirements"></a>Requisitos de firewall

Os dispositivos de rede intervenientes, tais como routers e firewalls, e a Firewall do Windows, se for caso disso, têm de permitir o tráfego associado ao registo do dispositivo móvel:  

- Entre os dispositivos móveis e o ponto proxy de registo: HTTPS (por predefinição, TCP 443)  

- Entre o ponto proxy de registo e o ponto de registo: HTTPS (por predefinição, TCP 443)  

Se utilizar um servidor web proxy, deve ser configurado para túneis SSL. A ponte SSL não é suportada para dispositivos móveis.  
