---
title: Novo na versão 1602
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1602 do Gestor de Configuração.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 2e398795a14f5073141f103d93ccd82e61d4d7a8
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904901"
---
# <a name="what39s-new-in-version-1602-of-configuration-manager"></a>O que&#39;novo na versão 1602 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


A atualização 1602 para O Gestor de Configuração só está disponível como uma atualização na consola para sites previamente instalados que executam a versão 1511. A versão 1511 é a versão inicial e de base que utiliza para instalar novos sites do Gestor de Configuração.  


> [!TIP]  
> Saiba mais sobre:  
>   
> - [Instalação de novos sites](../../servers/deploy/install/prepare-to-install-sites.md) (utilizando uma versão de base como 1511)  
> - [Instalação de atualizações em sites](../../servers/manage/updates.md) (como a atualização 1602)  

 As seguintes secções fornecem detalhes sobre alterações e novas capacidades introduzidas na versão 1602 do Gestor de Configuração.  

## <a name="site-infrastructure"></a>Infraestrutura do local  

###  <a name="in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a>No local atualize o sistema operativo dos servidores do site que executam o Windows Server 2008 R2  
 Os sites do Gestor de Configuração que executam a versão 1602 ou posteriormente suportam a atualização no local do sistema operativo dos servidores do site do Windows Server 2008 R2 para o Windows Server 2012 R2.  

> [!WARNING]  
>  Antes de atualizar para o Windows Server 2012 R2, tem de desinstalar o WSUS 3.2 do servidor.  
>   
>  Para obter mais informações sobre este passo crítico, consulte a secção "Nova e alterada funcionalidade" na visão geral dos Serviços de [Atualização](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality)do Servidor do Windows .  

 Para atualizar um servidor, utilize os procedimentos de atualização R2 do Windows Server 2012. Não é necessário executar um servidor de servidor do Gestor de Configuração após a atualização. Para saber quais são os procedimentos de atualização, veja [Opções de Atualização do Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)) na documentação do Windows Server.  

###  <a name="sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a>Grupos de disponibilidade do Servidor SQL AlwaysOn  
 Utilize os grupos de disponibilidade do SQL Server AlwaysOn para alojar a base de dados do site em sites primários, e o site da administração central como uma solução de alta disponibilidade e recuperação de desastres.  

 Para mais detalhes, consulte [o SQL Server AlwaysOn para obter uma base de dados de site altamente disponível para o Gestor de Configuração](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

### <a name="windows-10-servicing"></a>Serviço do Windows 10  
 As seguintes melhorias para a manutenção do Windows 10 foram adicionadas na versão 1602 do Gestor de Configuração:  

-   Estão disponíveis novas opções de filtro para planos de manutenção que lhe permitem filtrar para **Idioma,** **Obrigatório**, e **Título**. Apenas as atualizações que cumprem os critérios especificados serão adicionadas à implementação associada.  

-   Quando selecionar a classificação **de Atualizações** para atualizações de software sincronizada, é apresentado um aviso. Este aviso permite-lhe saber que é necessário o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para o Windows Server Update Services (WSUS) 4.0 antes de poder sincronizar com sucesso as atualizações de software e para que o Serviço de Assistência do Windows 10 funcione corretamente. A partir da mensagem de aviso, pode ir ao artigo da base de conhecimentos associado.  

-   As atualizações disponíveis do Windows 10 passam a ser apresentadas apenas no **Windows 10 A servir**todas as atualizações do Windows 10 da consola Do Gestor de  \  **All Windows 10 Updates** Configuração. Estas atualizações já não são apresentadas no nó de **Atualizações**de  \  **Software Todas as atualizações** de software da consola.  

-   Um plano de manutenção é considerado uma implementação de alto risco, e a janela **Select Collection** exibe apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site. Para mais informações, consulte [Definições para gerir implementações de alto risco para O Gestor de Configuração](../../servers/manage/settings-to-manage-high-risk-deployments.md).  

-   Os utilizadores que iniciarem um pacote de upgrade do Windows 10 recebem agora uma mensagem de que estarão a atualizar o seu sistema operativo.  

## <a name="application-management"></a>Gestão de aplicações  

### <a name="ios-app-configuration-policies"></a>Políticas de configuração de aplicações iOS  
 Utilize as políticas de configuração do Gestor de Configuração para fornecer definições que possam ser necessárias quando o utilizador executa uma aplicação iOS. Por exemplo, uma aplicação pode exigir que o utilizador especifique um número de porta personalizado, idioma, definições de segurança ou definições de marca (como um logotipo da empresa). Se estas definições forem incorretamente inseridas, isso pode aumentar o fardo no seu balcão de ajuda, e também atrasar a adoção de novas apps.  

 As políticas de configuração de aplicações podem ajudá-lo a eliminar estes problemas, permitindo-lhe implementar estas definições para os utilizadores numa política, antes de executar a aplicação. As definições são fornecidas automaticamente e o utilizador não precisa de tomar qualquer medida.

### <a name="manage-volume-purchased-ios-apps"></a>Gerir aplicações iOS adquiridas em volume  
 O Gestor de Configuração pode ajudá-lo a implementar e gerir aplicações que adquiriu em volume a partir do Programa de Compra de Volume da Apple (VPP). O Gestor de Configuração importa as informações da licença da loja de aplicações e rastreia quantas das licenças utilizou.  


### <a name="automatic-creation-of-office-mobile-apps"></a>Criação automática de aplicações móveis do Office  
 Quando atualiza sé 1602 a partir de 1511, o Gestor de Configuração cria automaticamente as seguintes aplicações móveis do Microsoft Office para Android e iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (apenas iOS)  

-   Microsoft Outlook  

Encontrará estas aplicações no nó de **Aplicações** da consola 'Gestor de Configuração'.  

 Para obter mais informações sobre a implementação de aplicações, consulte [como implementar aplicações com o Gestor de Configuração](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Atualizações de software  

### <a name="manage-office-365-client-updates"></a>Gerir atualizações de clientes do Office 365  
 O Gestor de Configuração tem a capacidade de gerir as atualizações de clientes do Office 365 utilizando o fluxo de trabalho de gestão de atualizações de software. Para mais informações, consulte [as atualizações do Manage Office 365 ProPlus com o Gestor de Configuração](../../../sum/deploy-use/manage-office-365-proplus-updates.md).  

## <a name="compliance-settings"></a>Definições de compatibilidade  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Definições de conformidade para dispositivos que executam o Windows 10 Team  
 Foram adicionadas novas definições ao artigo de configuração **do Windows 8.1 e Windows 10.** Estas definições ajudam-no a controlar dispositivos que executam o Windows 10 Team, como um dispositivo Surface Hub.  

 Para mais detalhes, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Gestor de Configuração](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Definições do modo quiosque para dispositivos Android Samsung KNOX Standard  
 O modo quiosque permite-lhe bloquear um dispositivo de modo a que apenas certas funcionalidades funcionem. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo ou para um dispositivo com a finalidade de desempenhar apenas uma função, como um dispositivo de ponto de venda. No 'Gestor de Configuração', já pode especificar as definições do modo do quiosque para dispositivos Samsung KNOX Standard.  


## <a name="conditional-access"></a>Acesso condicional  

### <a name="conditional-access-for-pcs-managed-by-configuration-manager"></a>Acesso condicional para Computadores geridos pelo Gestor de Configuração  
 Antes desta versão, para estabelecer acesso condicional a um PC, o PC teve de ser matriculado em Intune ou teve de ser um PC de domínio. A partir da atualização de 1602, o acesso condicional para Computadores geridos pelo Gestor de Configuração é suportado. Para os seus PCs que são geridos pelo Gestor de Configuração, pode restringir o acesso ao Exchange Online e Ao SharePoint Online apenas a dispositivos que estejam em conformidade com as políticas de conformidade que definiu.  


### <a name="restricting-access-based-on-the-health-of-devices"></a>Restringir o acesso com base na saúde dos dispositivos  
 Pode agora restringir o acesso a e-mails e serviços do Office 365 com base na saúde dos dispositivos, conforme reportado pelo Serviço de Atestados de Saúde. Além disso, os dispositivos geridos pela Intune estão incluídos nos relatórios de saúde do dispositivo.  

 A consola 'Gestor de Configuração' apresenta uma nova regra de conformidade que lhe permite especificar se os dispositivos devem ser permitidos ou bloqueados de acesso com base no seu estado de saúde. Para mais detalhes sobre o Serviço de Atestação de Saúde e como a saúde dos dispositivos é reportada em Intune, consulte a [atestar de saúde para o Gestor](../../../core/servers/manage/health-attestation.md)de Configuração .  

### <a name="new-compliance-policy-rules"></a>Novas regras de política de conformidade  
 Foram adicionadas novas regras de política de conformidade, como atualizações automáticas e que exigem uma palavra-passe para desbloquear dispositivos, para suportar melhores requisitos de segurança.


### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Certifique-se de que os dispositivos matriculados e conformes têm sempre acesso ao Exchange on-pre-preser  
 Quando verificar a seguinte opção, os dispositivos que estão matriculados no Intune e em conformidade com as políticas de conformidade, podem aceder à Exchange on-pre-preser: Predefinição da regra padrão - Permita sempre que **dispositivos inscritos e conformes intune acedam ao Exchange on-pre-pre-**. Esta regra está disponível na **página geral** do Assistente de Política de Acesso **Condicional configure** para troca no local.

 Esta regra substitui a regra padrão, o que significa que mesmo que estabeleça a regra padrão para quarentena ou bloquear o acesso, os dispositivos matriculados e conformes continuarão a poder aceder ao Exchange on-premis. Utilize esta definição quando quiser que os dispositivos matriculados e conformes tenham sempre acesso a e-mail através do Exchange on-pre-preser.   

 Para obter a passagem detalhada, consulte [Gerir o acesso ao email.](../../../mdm/understand/what-happened-to-hybrid.md)  

## <a name="client-management"></a>Gestão de clientes  

### <a name="client-online-status"></a>Estado online do cliente  
 Um novo estatuto para os clientes está disponível para monitorização se um computador estiver ou não online. Um computador é considerado on-line se estiver ligado ao seu ponto de gestão atribuído. Para indicar que o computador está online, o cliente envia mensagens semelhantes a ping para o ponto de gestão. Se o ponto de gestão não receber uma mensagem após 5 minutos, o cliente é considerado offline.  

 Para mais detalhes, consulte [Como monitorizar os clientes](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar a política de máquina seleção de PC e utilizador do Centro de Software  
 Uma nova opção, **Sync Policy,** foi adicionada à página de Manutenção de **Options**  >  **Computadores** opções do Centro de Software que faz com que o PC refresque a sua máquina de Configuração e a sua política de utilizador.  

### <a name="software-center-branding-changes"></a>Mudanças de marca do Software Center  
 Pode alterar a cor, o nome da organização e o ícone que aparecem no Centro de Software. Estas definições são aplicadas de acordo com as seguintes regras:  

- Se a função de site de ponto do catálogo de aplicações não for instalada, então o Software Center exibe o nome da organização especificado na definição do cliente do **Agente informático** chamado nome de Organização apresentado no Centro de **Software**.  

- Se a função do site do site do Catálogo de Aplicações for instalada, então o Software Center exibe o nome e a cor da organização especificados nas propriedades da função do site do site do Catálogo de Aplicações.  

- Se uma subscrição do Microsoft Intune estiver configurada e ligada ao ambiente do Gestor de Configuração, então o Software Center exibe o nome, cor e logotipo da empresa especificado nas propriedades de subscrição intune.  

### <a name="health-attestation"></a>Atestado de Saúde  
 Os administradores podem ver o estado do Atestado de Estado de Funcionamento do Dispositivo Windows 10 na consola do Configuration Manager. Isto está disponível para O Gestor de Configuração, bem como para o Gestor de Configuração com o Microsoft Intune. O atestado de estado de funcionamento permite ao administrador garantir que os computadores cliente têm as seguintes configurações fidedignas de BIOS, TPM e software de arranque ativadas:  

-   Antimalware de início antecipado  

-   BitLocker  

-   Arranque Seguro  

-   Integridade do Código  

Para mais detalhes, consulte [A estação de saúde para O Gestor de Configuração](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Melhorias às definições antimalware de proteção de pontofinal  
 1602 adiciona as seguintes novas definições na política antimalware Endpoint Protection para Windows Defender:  

-   Proteção em tempo real: Bloqueie aplicações potencialmente indesejadas no download, antes da instalação.  

-   Configurações de digitalização: Scan mapeadas unidades de rede durante uma varredura completa.  

-   Definições automáticas de submissão de ficheiros de amostra:  

     O motor antimalware pode solicitar que as amostras de ficheiros sejam enviadas para a Microsoft para análise sueste. Por predefinição, será sempre apresentado um aviso antes de enviar esses exemplos. Os administradores podem agora gerir as seguintes definições para configurar este comportamento:  

    -   Avançado: Ativar a submissão automática de ficheiros de amostra para ajudar a Microsoft a determinar se certos itens detetados são maliciosos.  

    -   Avançado: Permitir que os utilizadores modifiquem as definições automáticas de submissão de ficheiros de amostra.  

    Além disso, na secção "Definições de Exclusão" da política antimalware de proteção de pontofinal, a definição de **ficheiros e pastas** existentes permite agora exclusões do dispositivo.  

Para mais detalhes, consulte [Como criar e implementar políticas antimalware para proteção de pontos finais](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="ios-activation-lock"></a>Bloqueio de ativação do iOS  
 O Gestor de Configuração pode ajudá-lo a gerir o iOS Activation Lock, uma funcionalidade da aplicação Find My iPhone para dispositivos iOS 7.1 e posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Depois de estar ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:  

-   Desligue encontrar o meu iPhone.  

-   Apagar o dispositivo.  

-   Reativar o dispositivo.  

O Gestor de Configuração pode solicitar o estado de bloqueio de ativação de dispositivos supervisionados e não supervisionados que executam o iOS 7.1 e posteriormente. Para dispositivos supervisionados, o Gestor de Configuração pode recuperar o código de bypass do Bloqueio de Ativação e emiti-lo diretamente para o dispositivo.  

### <a name="monitor-terms-and-conditions-deployments"></a>Monitorizar as implementações de termos e condições  
 Pode monitorizar as implementações de termos e condições na consola Do Gestor de Configuração.  

 Selecione os termos e condições de implantação da lista de implementações. A área de resumo mostra as seguintes estatísticas:  

-   **Conformidade**: Os utilizadores aceitaram a versão mais recente dos termos e condições.  

-   **Erro**  

-   **Incompatível**: Os utilizadores aceitaram uma versão dos termos e condições, mas não a versão mais recente.  

-   **Desconhecido**: Os utilizadores nunca aceitaram os termos e condições, incluindo os que não têm um dispositivo matriculado.  
