---
title: Novidades no Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Descobrir as novidades do Intune no portal do Azure
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: c737de8a991bc8d96e38d729292be721c6bdd1cf
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791849"
---
# <a name="whats-new-in-microsoft-intune"></a>Novidades do Microsoft Intune

Saiba quais são as novidades todas as semanas no Microsoft Intune no [Microsoft Endpoint Manager no centro de administração](https://go.microsoft.com/fwlink/?linkid=2109431). Também pode encontrar [avisos importantes, lançamentos](#notices) [anteriores](whats-new-archive.md)e informações sobre [como as atualizações de serviço intune são lançadas.](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) 

> [!Note]
> Cada [atualização mensal](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) pode demorar até três dias a ser lançada e estará na seguinte ordem:
>
> - Dia 1: Ásia-Pacífico (APAC)
> - Dia 2: Europa, Médio Oriente, África (EMEA)
> - Dia 3: América do Norte
> - Dia 4+: Insintonização para governo
>
> É possível que algumas funcionalidades sejam implementadas durante várias semanas e que não estejam disponíveis para todos os clientes na primeira semana.
>
> Consulte a [página de desenvolvimento in](in-development.md) para obter uma lista de funcionalidades futuras num lançamento.

**Alimentação RSS**: Seja notificado quando esta página for atualizada copiando e colando o seguinte URL no leitor de feed:`https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot

<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>Semana de 11 de maio de 2020 (lançamento do Serviço de 2005)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Personalize as ações de dispositivos self-service no Portal da Empresa<!--4393379 -->
Pode personalizar as ações de dispositivos self-service disponíveis que são mostradas aos utilizadores finais na aplicação e website do Portal da Empresa. Para ajudar a prevenir ações não intencionais do dispositivo, pode configurar estas definições para a aplicação Portal da Empresa selecionando a Personalização **da**  >  **Administração**de Inquilinos . Estão disponíveis as seguintes ações:
- Ocultar o botão **Remover** no dispositivo corporativo Windows.
- Ocultar o botão **Reset** em dispositivos windows corporativos.
- Ocultar o botão **Reset** em dispositivos corporativos iOS.
- Ocultar O botão **Remover** em dispositivos iOS corporativos.
Para mais informações, consulte [as ações do dispositivo self-service user a partir do Portal da Empresa](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

#### <a name="auto-update-vpp-available-apps---3640511----"></a>Atualização automática VPP disponíveis aplicações<!-- 3640511  -->
As aplicações que forem publicadas como Programa de Compra de Volume (VPP) serão automaticamente atualizadas quando as **Atualizações automáticas** de aplicações estiverem ativadas para o token VPP. Anteriormente, as aplicações disponíveis vPP não atualizam automaticamente. Em vez disso, os utilizadores finais tiveram de ir ao Portal da Empresa e reinstalar a aplicação se uma versão mais recente estivesse disponível. As aplicações necessárias continuam a suportar atualizações automáticas.


#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---4404429-----"></a>Entrega unificada de aplicações Azure AD Enterprise e Office Online no Portal da Empresa<!-- 4404429   -->
*Esta funcionalidade foi adiada.*
No painel de **personalização** de Intune, pode selecionar para **Ocultar** ou **mostrar** tanto **as aplicações Da Azure AD Enterprise** como as **aplicações Office Online** no Portal da Empresa. Cada utilizador final verá todo o seu catálogo de aplicações a partir do serviço da Microsoft escolhido. Por predefinição, cada fonte adicional de aplicação será definida para **Ocultar**. Esta funcionalidade entrará primeiro em vigor no site do Portal da Empresa, com suporte nos Portais windows, iOS/iPadOS e macOS Company. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione a personalização da **administração do Inquilino**para encontrar esta  >  **Customization** definição de configuração. Para obter informações relacionadas, consulte [como personalizar as aplicações intune Company Portal, website do Portal da Empresa e aplicação Intune](../apps/company-portal-app.md).

#### <a name="android-company-portal-user-experience---5736084----"></a>Experiência de utilizador do Portal da Empresa Android<!-- 5736084  -->
No lançamento de 2005 do Portal da Empresa Android, os utilizadores finais de dispositivos Android que são emitidos um aviso, bloqueio ou limpeza por uma política de proteção de aplicações verão uma nova experiência do utilizador. Em vez da experiência atual do diálogo, os utilizadores finais verão uma mensagem de página inteira descrevendo o motivo do aviso, bloqueio ou limpeza e os passos para remediar o problema. Para mais informações, consulte a experiência de proteção de [aplicativos para dispositivos Android](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) e definições de política de proteção de [aplicações Android no Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>Suporte a várias contas no Portal da Empresa para o macOS<!-- 5779449  -->
O Portal da Empresa sobre dispositivos macOS agora caches contas de utilizador, facilitando o início do sessão. Os utilizadores já não precisam de assinar no Portal da Empresa sempre que lançam a aplicação. Além disso, o Portal da Empresa apresentará um picker de conta se várias contas de utilizador estiverem em cache, para que os utilizadores não tenham de introduzir o seu nome de utilizador. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Aplicações protegidas recentemente disponíveis<!-- 7060934   -->
As seguintes aplicações protegidas já estão disponíveis:
- Papéis de conselho
- Breezy para Intune
- Hearsay Relacionar-se com Intune
- ISEC7 Delegado de Intercâmbio Móvel para Intune
- Lexmark para Intune
- Empreendimento Meetio
- Placa branca da Microsoft
- Agora® Móvel - Intune
- Qlik Sense Mobile 
- ServiceNow® Agente - Intune
- ServiçoAgora® Onboarding - Intune
- Smartcrypt para Intune
- Tato para Intune
- Zero - e-mail para advogados

Para obter mais informações sobre aplicações protegidas, consulte [aplicações protegidas](../apps/apps-supported-intune-apps.md)microsoft Intune .

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>Pesquise os docs Intune do Portal da Empresa<!-- 1736480   -->
Agora pode pesquisar a documentação Intune diretamente do Portal da Empresa para aplicação macOS. Na barra de menus, selecione **Help**  >  **Search** e introduza as palavras-chave da sua pesquisa para encontrar rapidamente respostas às suas perguntas.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuração do dispositivo

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Melhorias no suporte da OEMConfig para dispositivos da Zebra Technologies<!-- 4184154 -->
Intune suporta totalmente todas as funcionalidades fornecidas pela Zebra OEMConfig. Os clientes que gerem dispositivos Zebra Technologies com Android Enterprise e OEMConfig podem implementar vários perfis OEMConfig para um dispositivo. Os clientes também podem ver relatórios ricos sobre o estado dos seus perfis Zebra OEMConfig.

Para mais informações, consulte [A implementação de vários perfis OEMConfig para dispositivos Zebra no Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md).

Não há alteração no comportamento da OEMConfig para outras OEMs.

Aplica-se a:
- Android Enterprise
- Dispositivos da Zebra Technologies que suportam a OEMConfig. Para obter detalhes específicos sobre o suporte, contacte a Zebra.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>Configurar extensões do sistema em dispositivos macOS<!-- 6255624 -->
Nos dispositivos macOS, pode criar um perfil de extensões de kernel para configurar as definições ao nível do kernel (**Perfis**de configuração de  >  **dispositivos**  >  **macOS** para extensões de > **kernel** para perfil). A Apple acaba por depreciar as extensões do kernel e substituí-las por extensões do sistema numa versão futura.

As extensões do sistema funcionam no espaço do utilizador e não têm acesso ao núcleo. O objetivo é aumentar a segurança e fornecer mais controlo final do utilizador, limitando os ataques ao nível do núcleo. Ambas as extensões de kernel e extensões do sistema permitem que os utilizadores instalem extensões de aplicações que alargam as capacidades nativas do sistema operativo.

Em Intune, pode configurar as extensões de**Devices**kernel e as extensões do sistema (perfis de configuração de  >  **dispositivos**  >  **macOS** para **extensões** de sistema de > plataforma para perfil). As extensões de kernel aplicam-se a 10.13.2 e mais recentes. As extensões do sistema aplicam-se às 10.15 e mais recentes. Do macOS 10.15 ao macOS 10.15.4, as extensões de kernel e as extensões do sistema podem ser executadas lado a lado. 

Para saber mais sobre estas extensões em dispositivos macOS, consulte [Adicionar extensões macOS](../configuration/kernel-extensions-overview-macos.md).

Aplica-se a:
- macOS 10.15 e mais recente

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>Configure as preferências de privacidade da aplicação e do processo em dispositivos macOS<!-- 2934232   --> 
Com o lançamento do macOS Catalina 10.15, a Apple adicionou novos melhoramentos de segurança e privacidade. Por defeito, as aplicações e processos não conseguem aceder a dados específicos sem o consentimento do utilizador. Se os utilizadores não fornecerem o consentimento, as aplicações e processos podem não funcionar. A Intune está a adicionar suporte para configurações que permitem aos administradores de TI permitir ou proibir o consentimento de acesso de dados em nome dos utilizadores finais em dispositivos que executam o macOS 10.14 ou posteriormente. Estas definições garantirão que as aplicações e processos continuem a funcionar corretamente e reduzam o número de solicitações. 

Para mais informações sobre as definições que pode gerir, consulte as preferências de [privacidade do macOS.](../configuration/device-restrictions-macos.md#privacy-preferences)

Aplica-se a:
- macOS 10.14 e mais recente

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscrição de dispositivos

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Restrições de inscrição suportam etiquetas de âmbito<!--4209550  -->
Agora pode atribuir etiquetas de âmbito às restrições de inscrição. Para isso, vá ao [microsoft Endpoint Manager administrador centro](https://go.microsoft.com/fwlink/?linkid=2109431)de administração  >  **Dispositivos**  >  **Restrições**de inscrição  >  **Criar restrições**de restrição . Crie qualquer tipo de restrição e verá a página scope **tags.** Para mais informações, consulte [As restrições de inscrição definidas](../enrollment/enrollment-restrictions-set.md).

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Suporte de piloto automático para dispositivos Hololens 2<!--6305220  -->
O Windows Autopilot suporta agora dispositivos Hololens 2. Para obter mais informações sobre a utilização do Piloto Automático para Hololens, consulte [o Windows Autopilot para HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>Utilize a ação remota sincronizada a granel para iOS<!--6440956  idmiss-->
Agora pode utilizar a ação remota sincronizada em até 100 dispositivos iOS de cada vez. Para ver esta funcionalidade, vá ao [microsoft Endpoint Manager administrador](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **dispositivos**todas as ações do  >  **All devices**  >  **dispositivo Bulk**. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Intervalo de sincronização automatizada do dispositivo até 12 horas<!--3077535  -->
Para a Inscrição automática de Dispositivos da Apple, o intervalo de sincronização automatizada entre Intune e Apple Business Manager foi reduzido de 24 horas para 12 horas. Para obter mais informações sobre sincronização, consulte [os dispositivos geridos pelo Sync](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Segurança do dispositivo

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Suporte de credenciais derivadas para DISA Purebred em dispositivos Android<!-- 6939073     -->
Agora pode utilizar *o DISA Purebred* como fornecedor [de credenciais derivados](../protect/derived-credentials.md) em dispositivos geridos totalmente pela Android Enterprise. O suporte inclui a recuperação de uma credencial derivada para dISA Purebred. Pode utilizar uma credencial derivada para autenticação de aplicações, Wi-Fi, VPN ou s/MIME assinando e/ou encriptação com aplicações que a suportam. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Enviar notificações push como uma ação por incumprimento <!-- 1733150   -->
Pode agora configurar uma [ação por incumprimento](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) que envia uma notificação push a um utilizador quando o seu dispositivo não cumprir as condições de uma política de conformidade. A nova ação é **Enviar notificação push para utilizador final**, e é suportado em dispositivos Android e iOS.

Quando os utilizadores selecionam a notificação push no seu dispositivo, o Portal da Empresa ou a aplicação Intune abre para mostrar detalhes sobre o motivo pelo qual não são conformes.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Conteúdo de segurança endpoint e novas funcionalidades<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

A documentação para Intune [Endpoint Security](../protect/endpoint-security.md) já está disponível. No nó de segurança final do centro de administração do Microsoft Endpoint Manager pode:

- Crie e implemente políticas de segurança focadas nos seus dispositivos geridos
- Configure a integração com a Microsoft Defender Advanced Threat Protection e gereas tarefas de segurança ajudam a remediar os riscos para dispositivos de risco identificados pela sua equipa ATP
- Configurar as linhas de base de segurança
- Gerir as políticas de conformidade do dispositivo e de acesso condicional
- Veja o estado de conformidade de todos os seus dispositivos tanto do Intune como do Gestor de Configuração quando o Gestor de Configuração estiver configurado para a anexação do cliente.

Além da disponibilidade de conteúdos, os seguintes são novidade para a Endpoint Security este mês:

- [**As políticas**](../protect/endpoint-security-policy.md) de segurança do ponto final **estão fora de** ***pré-visualização*** e estão agora prontas a ser utilizadas em ambientes de produção, como *geralmente disponível,* com duas exceções:

  - Numa nova *pré-visualização pública,* pode utilizar o perfil de [ **regras do Microsoft Defender Firewall** ](../protect/endpoint-security-firewall-policy.md#firewall-profiles) para a política de Firewall do Windows 10. A cada instância deste perfil pode configurar até 150 regras de firewall para complementar os perfis do Microsoft Defender Firewall. 
  - A política de segurança da proteção de contas permanece em pré-visualização. 

- Agora pode [**criar uma duplicação de políticas de segurança**](../protect/endpoint-security-policy.md#duplicate-a-policy)de ponto final. Os duplicados mantêm a configuração de configurações da política original, mas obtêm um novo nome. Em seguida, a nova instância política não inclui quaisquer atribuições a grupos até editar a nova instância política para adicioná-las. Pode duplicar as seguintes políticas:
  - Antivírus
  - Disk encryption (Encriptação de discos)
  - Firewall
  - Endpoint detection and response (Deteção e resposta de pontos finais)
  - Attack surface reduction (Redução da superfície de ataque)
  - Account protection (Proteção de contas)

- Agora pode [**criar uma duplicação de uma linha de base de segurança.**](../protect/security-baselines.md#duplicate-a-security-baseline) Os duplicados mantêm a configuração das configurações da linha de base original, mas obtêm um novo nome. A nova instância de base não inclui quaisquer atribuições a grupos até editar a nova instância de base para adicioná-las.

- Está disponível um novo relatório para a política antivírus de segurança final: [**Windows 10 pontos finais pouco saudáveis**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). Este relatório é uma nova página que pode selecionar ao visualizar a sua política de antivírus de segurança final. O relatório apresenta o estado antivírus dos seus dispositivos Windows 10 geridos pelo MDM.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Suporte para certificados de assinatura e encriptação S/MIME com Outlook no Android<!-- 7207474  -->
Agora pode utilizar certificados para a assinatura e encriptação S/MIME com o Outlook no Android. Com este suporte, pode fornecer estes certificados utilizando perfis de certificados importados SCEP, PKCS e PKCS. As seguintes plataformas Android são suportadas:

- Perfil de trabalho da empresa android
- Administrador de dispositivos Android

O suporte para dispositivos Android Enterprise Totalmente Geridos está para breve.

Para obter mais informações sobre este suporte, consulte [a rotulagem de sensibilidade e proteção no Outlook para iOS e Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) na documentação Exchange.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorizar e resolver problemas

#### <a name="device-reports-ui-update---6269408---"></a>Dispositivo reporta atualização ui<!-- 6269408 -->
O painel de visão geral dos relatórios irá agora fornecer um **resumo** e um separador **Relatórios.** No centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), selecione **Relatórios,** e, em seguida, selecione o separador **Relatórios** para ver os tipos de relatório disponíveis. Para obter informações relacionadas, consulte [os relatórios Intune](../fundamentals/reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Scripting

#### <a name="macos-script-support---6376978----"></a>suporte para script saos<!-- 6376978  -->
O suporte para o script para macOS está agora geralmente disponível. Além disso, adicionámos suporte tanto para scripts atribuídos ao utilizador como para dispositivos macOS que foram matriculados com a Inscrição automática de dispositivos da Apple (anteriormente Programa de Inscrição de Dispositivos). Para mais informações, consulte [Utilize scripts de concha em dispositivos macOS em Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Semana de 4 de maio de 2020  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Portal da empresa para Android guia utilizadores a obter aplicações após inscrição no perfil de trabalho <!-- 6103999 -->
Melhorámos a orientação in-app no Portal da Empresa para facilitar aos utilizadores a descoberta e instalação de apps. Depois de se inscreverem na gestão de perfis de trabalho, os utilizadores receberão uma mensagem explicando como encontrar aplicações sugeridas na versão com insígnias do Google Play. O último passo no [dispositivo De Inscrição com perfil Android](../user-help/enroll-device-android-work-profile.md) foi atualizado para mostrar a nova mensagem. Os utilizadores também verão uma nova ligação **Get Apps** na gaveta do Portal da Empresa à esquerda. Para dar lugar a estas novas e melhoradas experiências, o separador **APPS** foi removido. Para ver os ecrãs atualizados, vá a [atualizações de UI para aplicações de utilizador final Intune](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Semana de 20 de abril de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Anexo de inquilino do Microsoft Endpoint Manager: As ações de sincronização e dispositivos do dispositivo<!-- 6317104, CM3555758  -->
O Microsoft Endpoint Manager está a reunir o Diretor de Configuração e o Intune numa única consola. A partir da versão de 'Gestor de Configuração' de 2002, pode carregar os seus dispositivos de Gestor de Configuração para o serviço de nuvem e tomar ações sobre eles no centro de administração. Para mais informações, consulte o inquilino do [Microsoft Endpoint Manager anexar: Sincronização de dispositivos e ações](../../configmgr/tenant-attach/device-sync-actions.md)do dispositivo . 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Microsoft Office 365 ProPlus renome<!-- 6368143 -->
O Microsoft Office 365 ProPlus está a ser renomeado para aplicações microsoft **365 para empresa**. Para saber mais, consulte a [mudança de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Na nossa documentação, geralmente vamos referir-nos a ela como Aplicações Microsoft 365. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)pode encontrar o conjunto de aplicações selecionando **apps**  >  **Windows**  >  **Add**. Para obter informações sobre a adição de apps, consulte [Adicionar aplicações ao Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>Semana de 13 de abril de 2020 (lançamento de serviço de 2004)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Gerir as definições de S/MIME para Outlook em dispositivos Android Enterprise<!-- 6517085   -->
Pode utilizar políticas de configuração de aplicações para gerir a definição S/MIME para o Outlook em dispositivos que executam o Android Enterprise. Também pode escolher se permite ou não que os utilizadores do dispositivo ativem ou desativem S/MIME nas definições do Outlook. Para utilizar as políticas de configuração de apps para Android, no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) vai para as políticas de configuração de **Apps**  >  **App**  >  **Adicionar**  >  **dispositivos Geridos**. Para obter mais informações sobre configurar as definições para o Outlook, consulte as definições de [configuração do Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Teste de pré-lançamento para aplicações geridas do Google Play<!-- 2681933  -->
As organizações que estão a usar [as faixas de teste fechadas do Google Play para testes de pré-lançamento](https://support.google.com/googleplay/android-developer/answer/3131213) de aplicações podem gerir estas faixas com o Intune. Pode atribuir seletivamente aplicações que são publicadas nas faixas de pré-produção do Google Play a grupos piloto para realizar testes. Em Intune, você pode ver se uma aplicação tem uma pista de teste de construção pré-produção publicada para ela, bem como ser capaz de atribuir essa faixa a grupos de utilizadores ou dispositivos AAD. Esta funcionalidade está disponível para todos os nossos cenários Android Enterprise atualmente suportados (perfil de trabalho, totalmente gerido e dedicado). No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)pode adicionar uma aplicação gerida pelo Google Play selecionando **apps**  >  **Android**  >  **Add**. Para mais informações, consulte [Trabalhar com o Google Play Closed Testing Tracks](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams está agora incluído na Suite Office 365 para macOS<!-- 5903936  -->
Os utilizadores que lhe forem atribuídos microsoft Office para macOS no Microsoft Endpoint Manager passarão a receber Microsoft Teams para além das aplicações existentes do Microsoft Office (Word, Excel, PowerPoint, Outlook e OneNote). A Intune reconhecerá os dispositivos Mac existentes que têm os outros Dispositivos Do Office para aplicações macOS instaladas, e tentará instalar as Microsoft Teams da próxima vez que o dispositivo verificar com o Intune. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)pode encontrar a **Suite Office 365** para macOS selecionando **apps**  >  **macOS**  >  **Add**. Para mais informações, consulte [o SignOffice 365 para dispositivos macOS com](../apps/apps-add-office365-macos.md)o Microsoft Intune .

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Atualização para políticas de configuração de aplicativos Android<!-- 6113334  -->
As políticas de configuração de aplicações Android foram atualizadas para permitir que os administradores selecionem o tipo de inscrição do dispositivo antes de criar um perfil de config de aplicação. A funcionalidade está a ser adicionada para ter em conta os perfis de certificado que se baseiam no tipo de inscrição (Perfil de trabalho ou Proprietário do Dispositivo).  Esta atualização fornece o seguinte:

1. Se for criado um novo perfil e se selecionar o Perfil de Trabalho e o Perfil do Proprietário do Dispositivo para o tipo de inscrição do dispositivo, não poderá associar um perfil de certificado à política de config da aplicação.
2. Se for criado um novo perfil e se selecionar apenas o Perfil de Trabalho, as políticas de certificados de perfil de trabalho criadas no âmbito da Configuração do Dispositivo podem ser utilizadas.
3. Se for criado um novo perfil e o Proprietário do Dispositivo apenas for selecionado, as políticas de certificados do Proprietário do Dispositivo criadas no âmbito da Configuração do Dispositivo podem ser utilizadas. 

> [!IMPORTANT]
> As políticas existentes criadas antes do lançamento desta funcionalidade (versão abril de 2020 - 2004) que não possuam quaisquer perfis de certificado associados à política serão indefinidas para o Perfil de Trabalho e Perfil do Proprietário do Dispositivo para o tipo de inscrição do dispositivo. Além disso, as políticas existentes criadas antes do lançamento desta funcionalidade que têm perfis de certificados associados apenas serão padrão para o Perfil de Trabalho.

Além disso, estamos adicionando perfis de configuração de gmail e nove e-mails que funcionarão tanto para os tipos de inscrição do Perfil de Trabalho como para os tipos de inscrição do Proprietário do Dispositivo, incluindo a utilização de perfis de certificado em ambos os tipos de configuração de e-mail.  Quaisquer políticas do Gmail ou Nove que tenha criado no âmbito da Configuração do Dispositivo para Perfis de Trabalho continuarão a aplicar-se ao dispositivo e não é necessário movê-las para as políticas de configuração de apps.

No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)pode encontrar políticas de configuração de aplicações selecionando políticas de **Apps**  >  **configuração**de Apps App . Para obter mais informações sobre as políticas de configuração de apps, consulte as políticas de configuração da [App para o Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Notificação push quando o tipo de propriedade do dispositivo é alterado<!-- 5575875 -->
Pode configurar uma notificação push para enviar para os utilizadores do Portal da Empresa Android e iOS quando o seu tipo de propriedade do dispositivo foi alterado de Personal para Corporate como cortesia de privacidade. Esta notificação push é definida para ser cancelada por defeito. A definição pode ser encontrada no Microsoft Endpoint Manager selecionando a **personalização**da  >  **administração**do Inquilino . Para saber mais sobre como a propriedade do dispositivo afeta os seus utilizadores finais, consulte a [propriedade do dispositivo Change](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Suporte de grupo para painel de personalização<!-- 4722837  -->
Pode direcionar as definições no painel de **personalização** para grupos de utilizadores. Para encontrar estas definições em Intune, navegue para o centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione A personalização da **administração do Inquilino**  >  **Customization**. Para mais informações sobre personalização, consulte [Como personalizar as aplicações intune Company Portal, website do Portal da Empresa e aplicação Intune](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuração do dispositivo

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>Múltiplas regras VPN "Avaliar cada tentativa de ligação" a pedido suportadas no iOS, iPadOS e macOS<!-- 6424615  -->
A experiência do utilizador Intune permite múltiplas regras vpN a pedido no mesmo perfil VPN com a ação de tentativa de **ligação (** Perfis de configuração de**Devices**  >  **dispositivos**  >  **Criar perfil**  >  **iOS/iPadOS** ou **macOS** para plataforma > **VPN** para perfil > **VPN Automática**  >  **On-demand).**

Só honrou a primeira regra da lista. Este comportamento é corrigido, e Intune avalia todas as regras da lista. Cada regra é avaliada na ordem que aparece na lista de regras a pedido.

> [!NOTE]
> Se tiver perfis VPN existentes que utilizam estas regras VPN a pedido, a correção aplica-se da próxima vez que alterar o perfil VPN. Por exemplo, fazer uma pequena alteração, como alterar a ligação do nome e, em seguida, guardar o perfil.
>
> Se estiver a utilizar certificados SCEP para autenticação, esta alteração faz com que os certificados para este perfil VPN sejam reemitidos.

Aplica-se a:
- iOS/iPadOS
- macOS

Para obter mais informações sobre os perfis VPN, consulte [Create VPN perfis](../configuration/vpn-settings-configure.md).

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>Opções adicionais nos perfis de extensão de apps SSO e SSO em dispositivos iOS/iPadOS<!-- 6504155   -->

Nos dispositivos iOS/iPadOS, pode:
- Nos perfis SSO (**Perfis**de configuração de  >  **dispositivos**  >  **Criar perfis**de perfil  >  **iOS/iPadOS** para **funcionalidades** de dispositivo de > de plataforma para perfis > **único sinal),** definir o nome principal kerberos como o nome de conta Security Account Manager (SAM) nos perfis SSO. 
- Nos perfis de extensão da aplicação SSO ( Perfis de configuração de**dispositivos**Criar perfis de  >  **Configuration profiles**  >  **perfil**  >  **iOS/iPadOS** para as **funcionalidades** do dispositivo > de perfil para perfis > **extensão de aplicação de entrada única),** configure a extensão iOS/iPadOS Microsoft Azure AD com menos cliques utilizando um novo tipo de extensão de aplicação SSO. Pode ativar a extensão Da AD Azure para dispositivos no modo de dispositivo partilhado e enviar dados específicos para a extensão para a extensão.

Aplica-se a:
- iOS/iPadOS 13.0+

Para obter mais informações sobre a utilização de um único sinal nos dispositivos iOS/iPadOS, consulte a visão geral da [extensão](../configuration/device-features-configure.md#single-sign-on-app-extension) da aplicação de assinatura única e a [lista de definições de inscrição única](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscrição de dispositivos

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Eliminar o token de inscrição automática do dispositivo da Apple quando o perfil padrão estiver presente<!--6393220 -->
Anteriormente, não podia eliminar um perfil predefinido, o que significava que não podia eliminar o token de inscrição automática de dispositivos associado ao mesmo. Agora, pode apagar o símbolo quando:
- nenhum dispositivo é atribuído ao símbolo
- um perfil predefinido está presente Para o fazer, apagar o perfil predefinido e, em seguida, apagar o token associado.
Para mais informações, consulte [Delete um token ADE de Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-ade-token-from-intune).

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Suporte reforçado para a Inscrição de Dispositivos Automatizados da Apple e dispositivos, perfis e tokens Apple Configurator 2<!--3542402 -->
Para ajudar a distribuir departamentos e organizações de TI, a Intune suporta agora até 1000 perfis de inscrição por token, 2000 fichas de inscrição automática de dispositivos (anteriormente conhecidas como DEP) por conta Intune, e 75.000 dispositivos por token. Não existe um limite específico para dispositivos por perfil de inscrição, abaixo do número máximo de dispositivos por token.

Intune agora suporta até 1000 perfis Apple Configurator 2.

Para mais informações, consulte [o volume suportado](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Todas as alterações de entrada da página de todos os dispositivos<!--6967616 -->
Na página Todos os **dispositivos,** as entradas para a **Managed por** coluna mudaram:
- *Intune* é agora exibido em vez de *MDM*
- *Cogerido* é agora apresentado em vez de *MDM/Agente ConfigMgr*

Os valores de exportação mantêm-se inalterados.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>Informação de versão trusted Platform Manager (TPM) agora na página de Hardware do Dispositivo<!--6224914 idmiss -->
Pode agora ver o número da versão TPM na página de hardware de um dispositivo[(Dispositivos](https://go.microsoft.com/fwlink/?linkid=2109431)de administrador do Microsoft Endpoint Manager  >  **Devices** > escolher um dispositivo > **Hardware** > olhar sob o recinto do **Sistema).**

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorizar e resolver problemas

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>Colete registos para melhor resolução de scripts atribuídos a dispositivos macOS<!-- 6359853  -->
Agora pode recolher registos para uma melhor resolução de problemas de scripts atribuídos aos dispositivos macOS. Pode recolher registos até 60 MB (comprimido) ou 25 ficheiros, o que ocorrer primeiro. Para mais informações, consulte as políticas de script de [concha saque de Problemas do MacOS utilizando a recolha](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection)de registos .
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Segurança

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Credenciais derivadas para fornecer dispositivos Android Enterprise Totalmente Geridos com certificados<!--4839592    -->
Intune agora suporta o uso de [credenciais derivadas](../protect/derived-credentials.md) como um método de autenticação para dispositivos Android. As credenciais derivadas são uma implementação da norma 800-157 do Instituto Nacional de Normalização e Tecnologia (NIST) para a implementação de certificados para dispositivos. O nosso suporte para Android expande-se no nosso suporte para dispositivos que executam o iOS/iPadOS.

As credenciais derivadas dependem da utilização de um cartão de verificação de identidade pessoal (PIV) ou cartão de acesso comum (CAC), como um cartão inteligente. Para obter uma credencial derivada para o seu dispositivo móvel, os utilizadores começam na aplicação Microsoft Intune e seguem um fluxo de trabalho de inscrição que é exclusivo do fornecedor que utiliza. Comum a todos os fornecedores é a obrigação de utilizar um cartão inteligente num computador para autenticar o prestador de credenciais derivado. Esse fornecedor emite então um certificado para o dispositivo derivado do cartão inteligente do utilizador.

Pode utilizar credenciais derivadas como método de autenticação para perfis de configuração do dispositivo para VPN e WiFi. Também pode usá-las para autenticação de apps e assinatura e encriptação S/MIME para aplicações que a suportem.

Intune agora suporta os seguintes fornecedores de credenciais derivados com Android:
- Entrust Datacard
- Interceto

Um terceiro fornecedor, o DISA Purebred, estará disponível para Android num futuro lançamento.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>A linha de base de segurança do Microsoft Edge já está geralmente disponível<!--6586139 -->

Uma nova versão da linha de base de segurança do [Microsoft Edge](../protect/security-baselines.md#available-security-baselines) já está disponível e é lançada como geralmente disponível (GA). A linha de base anterior do Edge estava em Pré-visualização.  A nova versão de base em abril de 2020 (versão Edge 80 e mais tarde). 

Com o lançamento desta nova linha de base, já não será sacar perfis com base nas versões de base anteriores, mas pode continuar a utilizar perfis que criou com essas versões. Também pode optar por [atualizar os seus perfis existentes para utilizar a versão base mais recente](../protect/security-baselines.md#change-the-baseline-version-for-a-profile). 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>Semana de 6 de abril de 2020

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>Novas definições de script shell para dispositivos macOS<!-- 6884363 -->
Ao configurar scripts de conchas para dispositivos macOS, pode agora configurar as seguintes novas definições: 
- Ocultar notificações de script em dispositivos
- Frequência do script
- Número máximo de vezes para voltar a tentar se o guião falhar

Para mais informações, consulte [Utilize scripts de concha em dispositivos macOS em Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Semana de 30 de março de 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Novo URL para o centro de administração do Microsoft Endpoint Manager<!-- 3704810 -->
Para alinhar com o anúncio do Microsoft Endpoint Manager na Ignite no ano passado, alterámos o URL para o centro de administração do Microsoft Endpoint Manager (anteriormente Microsoft 365 Device Management) para [https://endpoint.microsoft.com](https://endpoint.microsoft.com) . O antigo URL do centro de administração [https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com) () continuará a funcionar, mas recomendamos que comece a aceder ao centro de administração do Microsoft Endpoint Manager utilizando o novo URL.

Para obter mais informações, consulte as [tarefas de TI simplificadas utilizando o centro de administração do Microsoft Endpoint Manager](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### <a name="app-management"></a>Gestão de aplicações  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>Portal da empresa para iOS suporta modo paisagístico<!--6048329  -->   
Os utilizadores podem agora inscrever os seus dispositivos, encontrar aplicações e obter suporte de TI utilizando a orientação do ecrã à sua escolha. A aplicação detetará e ajustará automaticamente os ecrãs para encaixar no retrato ou no modo de paisagem, a menos que os utilizadores bloqueiem o ecrã no modo retrato.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>Suporte de script para dispositivos macOS (Pré-visualização pública)<!-- 4280361  -->
Pode adicionar e implementar scripts para dispositivos macOS. Este suporte alarga a sua capacidade de configurar dispositivos macOS para além do que é possível utilizando capacidades nativas de MDM em dispositivos macOS. Para mais informações, consulte [Utilize scripts de concha em dispositivos macOS em Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>Semana de 24 de março de 2020

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Melhoria da experiência de interface de utilizador ao criar perfis de restrições de dispositivos em dispositivos Android e Android Enterprise<!-- 5841361 -->
Quando cria um perfil para dispositivos Android ou Android Enterprise, a experiência no centro de administração endpoint Management é atualizada. Esta alteração impacta os seguintes perfis de configuração do dispositivo **(Os**perfis de configuração de  >  **dispositivos**  >  **Criam**o administrador do dispositivo Android de perfil  >  **Android device administrator** ou o **Android Enterprise** para a plataforma):

- Restrições ao dispositivo: Administrador de dispositivos Android
- Restrições ao dispositivo: Proprietário de dispositivos Android Enterprise
- Restrições ao dispositivo: Perfil de trabalho Android Enterprise

Para obter mais informações sobre as restrições do dispositivo, pode configurar, consulte o [administrador do dispositivo Android](../configuration/device-restrictions-android.md) e o Android [Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>Melhoria da experiência de interface do utilizador ao criar perfis de configuração em dispositivos iOS/iPadOS e macOS<!-- 5569002 5568997 -->
Quando cria um perfil para dispositivos iOS ou macOS, a experiência no centro de administração da Endpoint Management é atualizada. Esta alteração impacta os seguintes perfis de configuração do dispositivo **(Os**perfis de configuração dos  >  **dispositivos**  >  **Criam perfis**de perfil  >  **iOS/iPadOS** ou **macOS** para a plataforma):

- Personalizado: iOS/iPadOS, macOS
- Funcionalidades do dispositivo: iOS/iPadOS, macOS
- Restrições ao dispositivo: iOS/iPadOS, macOS
- Proteção endpoint: macOS
- Extensões: macOS
- Ficheiro preferencial: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>Ocultar da configuração da configuração do utilizador nas funcionalidades do dispositivo em dispositivos macOS<!-- 6524869 -->

Quando cria um dispositivo que possui um perfil de configuração nos dispositivos macOS, existe um novo **Hide a partir da definição de configuração do utilizador** ( Os perfis de configuração do**dispositivo**Criam o macOS de  >  **Configuration profiles**  >  **perfil**  >  **macOS** para **as funcionalidades** do dispositivo > de plataforma para itens de **login**de perfil >).

Esta funcionalidade define a marca de verificação de ocultação de uma aplicação na lista de itens de login dos **Grupos & utilizadores** em dispositivos macOS. Os perfis existentes mostram esta definição dentro da lista como não configurada. Para configurar esta definição, os administradores podem atualizar os perfis existentes.

Quando definido para **Ocultar,** a caixa de verificação de ocultação é verificada para a aplicação e os utilizadores não podem alterá-la. Também esconde a aplicação dos utilizadores depois de os utilizadores iniciarem sessão nos seus dispositivos.

> [!div class="mx-imgBorder"]
> ![Ocultar aplicações em dispositivos macOS após os utilizadores iniciarem sessão no dispositivo no Microsoft Intune e Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Para obter mais informações sobre a definição que pode configurar, consulte as definições de funcionalidades do [dispositivo macOS](../configuration/macos-device-features-settings.md).

Esta funcionalidade aplica-se a:

- macOS

## <a name="week-of-march-16-2020-2003-service-release"></a>Semana de 16 de março de 2020 (lançamento do Serviço de 2003)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>atualizações do Portal macOS e iOS da empresa<!-- 5779439, 5780234  -->
O painel de perfil do portal macOS e iOS company foi atualizado para incluir o botão de saída. Adicionalmente, foram introduzidas melhorias na UI no painel de perfis no Portal da Empresa macOS. Para mais informações sobre o Portal da Empresa, consulte [como configurar a aplicação Microsoft Intune Company Portal](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Redirecione os web clips para o Microsoft Edge em dispositivos iOS<!-- 5455276   -->
Os clips web recentemente implantados (aplicações web fixas) em dispositivos iOS que são necessários para abrir num navegador protegido, serão abertos no Microsoft Edge em vez do Navegador Gerido intune. Tem de redirecionar os web clips pré-existentes para garantir que se abrem no Microsoft Edge em vez do Navegador Gerido. Para mais informações, consulte Gerir o acesso à Web utilizando o Microsoft Edge com o [Microsoft Intune](../apps/manage-microsoft-edge.md) e [adicionar aplicações web ao Microsoft Intune](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Utilize a ferramenta de diagnóstico Intune com o Microsoft Edge para Android<!-- 4735244  -->
O Microsoft Edge para Android está agora integrado com a ferramenta de diagnóstico Intune. Da mesma forma que a experiência no Microsoft Edge para iOS, a introdução de "cerca de:intunehelp" na barra de URL (a caixa de endereços) do Microsoft Edge no dispositivo iniciará a ferramenta de diagnóstico Intune. Esta ferramenta fornecerá registos detalhados. Os utilizadores podem ser guiados para recolher e enviar estes registos para o seu departamento de TI, ou ver registos de MAM para aplicações específicas.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Atualizações para marca Intune e personalização<!-- 5236032  -->
Atualizámos o painel Intune que foi nomeado "Branding e personalização" com melhorias, incluindo:

- Renomear o painel para **personalização.**
- Melhorar a organização e o design das configurações.
- Melhorar o texto de definições e as pontas de ferramentas.

Para encontrar estas definições em Intune, navegue para o centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione A personalização da **administração do Inquilino**  >  **Customization**. Para obter informações sobre a personalização existente, consulte [como configurar a aplicação Microsoft Intune Company Portal](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Chave de recuperação encriptada pessoal do utilizador<!-- 6273943  -->
Uma nova funcionalidade Intune está disponível que permite aos utilizadores recuperarem a sua chave de recuperação de **FileVault** encriptada pessoal para dispositivos Mac através da aplicação Portal da Empresa Android ou através da aplicação Android Intune. Existe um link tanto na aplicação Portal da Empresa como na aplicação Intune que abrirá um navegador Chrome para o Portal da Empresa Web onde o utilizador pode ver a chave de recuperação **do FileVault** necessária para aceder aos seus dispositivos Mac. Para obter mais informações sobre encriptação, consulte [Utilize a encriptação do dispositivo com Intune](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>Inscrição otimizada de dispositivodedicado <!-- 6114580  -->
Estamos a otimizar a inscrição para dispositivos dedicados android enterprise e a facilitar aos certificados SCEP associados ao Wi-Fi a aplicação a dispositivos dedicados matriculados antes de 22 de novembro de 2019. Para novas matrículas, a aplicação Intune continuará a instalar-se, mas os utilizadores finais deixarão de precisar de executar o passo **enable intune Agent** durante a inscrição. A prestação irá acontecer em segundo plano automaticamente e os certificados SCEP associados ao Wi-Fi podem ser implementados e definidos sem interação do utilizador final.  

Estas alterações serão lançadas numa base faseada ao longo do mês de março, à medida que o backend do serviço Intune se instala. Todos os inquilinos terão este novo comportamento no final de março. Para obter informações relacionadas, consulte [Suporte para certificados SCEP em dispositivos dedicados ao Android Enterprise](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuração do dispositivo

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Nova experiência do utilizador ao criar modelos administrativos em dispositivos Windows<!--5096036 -->
Com base no feedback do cliente, e na nossa mudança para a nova experiência de ecrã completo do Azure, reconstruímos a experiência de perfil dos Modelos Administrativos com uma visão de pasta. Não fizemos alterações a nenhuma definição ou perfis existentes. Assim, os seus perfis existentes permanecerão os mesmos, e serão utilizáveis na nova visão. Ainda pode navegar em todas as opções de definições selecionando **Todas as Definições**e utilizando a procura. A vista para a árvore é dividida por configurações de computador e utilizador. Encontrará as definições de Windows, Office e Edge nas suas pastas associadas.  

Aplica-se a:
- Windows 10 e mais recente

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>Perfis VPN com ligações VPN IKEv2 podem usar sempre com dispositivos iOS/iPadOS<!-- 1947932   -->
Nos dispositivos iOS/iPadOS, pode criar um perfil VPN que utiliza uma ligação IKEv2 **(Perfis**de Configuração de  >  **Dispositivos**  >  **Crie o perfil**  >  **iOS/iPadOS** para a plataforma > **VPN** para o tipo de perfil). Agora, pode configurar sempre com IKEv2. Quando configurados, os perfis VPN IKEv2 ligam-se automaticamente e mantêm-se ligados (ou reconectarem-se rapidamente) à VPN. Mantém-se ligado mesmo quando se desloca entre redes ou dispositivos de reinício.

No iOS/iPadOS, a VPN sempre on-on está limitada aos perfis IKEv2.

Para ver as definições IKEv2 que pode configurar, vá adicionar [definições VPN em dispositivos iOS no Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Aplica-se a:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Eliminar pacotes e conjuntos de pacotes em perfis de configuração de dispositivos OEMConfig em dispositivos Android Enterprise<!-- 5550355   -->
Nos dispositivos Android Enterprise, cria e atualiza os perfis OEMConfig (**Os**perfis de configuração de  >  **dispositivos**  >  **Criam o perfil**Android  >  **Enterprise** para a plataforma > **OEMConfig** para o tipo de perfil). Os utilizadores podem agora eliminar pacotes e conjuntos de pacotes utilizando o designer de **configuração** em Intune.

Para obter mais informações sobre os perfis da OEMConfig, consulte [use e gerencie dispositivos Android Enterprise com OEMConfig no Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Aplica-se a:
- Android Enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>Configure a extensão da aplicação iOS/iPadOS Microsoft Azure AD SSO<!-- 5672534   -->
A equipa da Microsoft Azure AD criou uma extensão de aplicação de inscrição única (SSO) para permitir aos utilizadores do iOS/iPadOS 13.0+ terem acesso a aplicações e websites da Microsoft com um único registo. Todas as aplicações que anteriormente tinham intermediado a autenticação com a aplicação Microsoft Authenticator continuarão a receber SSO com a nova extensão SSO. Com a versão da extensão da aplicação Azure AD SSO, pode configurar a extensão SSO com o tipo de extensão de aplicação SSO redirecionado **(Perfis**de configuração de  >  **dispositivos**  >  **Criar perfis**de perfil  >  **iOS/iPadOS** para as **funcionalidades** do dispositivo > plataforma para o tipo de perfil > **extensão de aplicação de inscrição única).**

Aplica-se a:
- iOS 13.0 e mais recente
- iPadOS 13.0 e mais recente

Para obter mais informações sobre as extensões da aplicação iOS SSO, consulte a extensão da [aplicação de inscrição única](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>Definição de modificação de definições de regulação da aplicação da empresa é removida dos perfis de restrição do dispositivo iOS/iPadOS<!-- 6225131   -->
Nos dispositivos iOS/iPadOS, cria-se um perfil de restrições de dispositivos **(Os**perfis de configuração de  >  **dispositivos**  >  **Criam perfis**de perfil  >  **iOS/iPadOS** para **restrições** de dispositivo si > para o tipo de perfil). A definição de modificação de definições de regulação da **aplicação Enterprise** é removida pela Apple e é removida do Intune. Se utilizar atualmente esta definição num perfil, não tem impacto e é removido dos perfis existentes. Esta definição também é removida de qualquer relatório em Intune.

Aplica-se a:
- iOS/iPadOS

Para ver as definições que pode restringir, vá às definições do [dispositivo iOS e iPadOS para permitir ou restringir as funcionalidades](../configuration/device-restrictions-ios.md).

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Resolução de problemas: Notificação de política pendente do MAM alterada para ícone informativo<!--6348954 -->
O ícone de notificação de uma política de MAM pendente na lâmina de resolução de problemas foi alterado para um ícone informativo.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Atualização da UI ao configurar a política de conformidade<!-- 3961639    -->

Atualizámos o UI para [criar políticas](../protect/create-compliance-policy.md#create-the-policy) de conformidade no gestor do Microsoft Endpoint (Políticas de Conformidade de**Dispositivos**Criar  >  **Compliance policies**  >  **Policies**  >  **políticas).** Temos uma nova experiência de utilizador que inclui as mesmas definições e detalhes que utilizou anteriormente. A nova experiência segue um processo semelhante a um assistente para criar a política de conformidade e inclui uma página onde pode adicionar *Atribuições* para a apólice, e uma página *Review + Create* onde pode rever a sua configuração antes de criar a apólice.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Dispositivos não conformes de aposentadoria<!-- 1827291       -->
Adicionámos uma nova ação para dispositivos não conformes que pode adicionar a qualquer política, para [retirar o dispositivo não conforme.](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance)  A nova ação, **Retire o dispositivo não conforme,** resulta na remoção de todos os dados da empresa do dispositivo, e também remove o dispositivo de ser gerido pela Intune.  Esta ação funciona quando o valor configurado em dias é atingido e nessa altura o dispositivo torna-se elegível para ser reformado. O valor mínimo é de 30 dias.  A aprovação explícita da administração de TI será necessária para retirar os dispositivos utilizando a secção *de dispositivos não conformes* com aposentadoria, onde os administradores podem reformar todos os dispositivos elegíveis.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Suporte para WPA e WPA2 nos perfis wi-fi da empresa iOS<!--6215273   -->
[Os perfis Wi-Fi da empresa para iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) suportam agora o campo *do tipo de Segurança.* Para o tipo de *Segurança,* pode selecionar uma empresa da **WPA** enterprise ou **da WPA/WPA2 Enterprise,** e, em seguida, especificar uma seleção para o *tipo EAP*.  **(Dispositivos**  >  **Perfis de**  >  configuração **Crie o perfil** e selecione **iOS/iPadOS** para *plataforma* e, em seguida, **Wi-Fi** para *Perfil).* 

As novas opções da Enterprise são como as que estão disponíveis para um perfil Wi-Fi Básico para iOS.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Nova experiência de utilizador para certificado, e-mail, VPN e Wi-Fi, perfis VPN<!-- 5615208   -->
Atualizámos a [experiência](../configuration/device-profile-create.md) do utilizador no Endpoint Management Admin Center ( Perfis de Configuração de**Devices**  >  **Dispositivos**  >  **Criar perfil**) para criar e modificar os seguintes tipos de perfis. A nova experiência apresenta as mesmas definições de antes, mas usa uma experiência semelhante a um assistente que não requer tanto scrolling horizontal. Não terá de modificar as configurações existentes com a nova experiência.

- Credencial derivada
- E-mail
- Certificado PKCS
- Certificado PKCS importado
- Certificado SCEP
- Certificado fidedigno
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscrição de dispositivos

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Configure se a inscrição estiver disponível no Portal da Empresa para Android e iOS<!-- 4260128  -->
Pode configurar se a inscrição de dispositivos no Portal da Empresa em dispositivos Android e iOS está disponível com solicitações, disponíveis sem avisos ou indisponíveis para os utilizadores. Para encontrar estas definições em Intune, navegue para o centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e, selecione a **administração do Inquilino,**  >  a inscrição no Dispositivo de**Customization**  >  **Edição**de Personalização  >  **Device enrollment**.  

O suporte para a definição de inscrição do dispositivo requer que os utilizadores finais tenham estas versões do Portal da Empresa:
-    Portal da Empresa no iOS: versão 4.4 ou posterior
-    Portal da empresa no Android: versão 5.0.4715.0 ou posterior

Para obter mais informações sobre a personalização do Portal da Empresa existente, consulte [como configurar a aplicação Microsoft Intune Company Portal](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Novo relatório Android na página de visão geral dos Dispositivos Android<!-- 5435435   -->
Adicionámos um relatório à consola de administração do Microsoft Endpoint Manager na página de visão geral dos Dispositivos Android que mostra quantos dispositivos Android foram matriculados em cada solução de gestão de dispositivos. Este gráfico (como o mesmo gráfico já na consola Azure) mostra o perfil de trabalho, totalmente gerido, dedicado e administrador de dispositivos inscrito seleções. Para ver o relatório, escolha **Dispositivos**  >  **Android**  >  **Overview**.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Orientar os utilizadores da gestão de administrador de dispositivos Android para a gestão de perfis de trabalho<!--5857738   -->
Estamos a lançar uma nova definição de conformidade para a plataforma de administrador de dispositivos Android. Esta definição permite-lhe tornar um dispositivo incompatível se for gerido com o administrador do dispositivo.

Nestes dispositivos não conformes, na página de **definições** do dispositivo Update os utilizadores verão a **mensagem de configuração de move para nova gestão de dispositivos.** Se tocarem no botão **Resolver,** serão guiados através de:

1. Não se matriculando na gestão do administrador de dispositivos
2. Matriculamento na gestão de perfil de trabalho
3. Resolução de questões de conformidade 
 
A Google está a diminuir o suporte do administrador de dispositivos em novas versões Android, num esforço para se mudar para uma gestão moderna, mais rica e segura de dispositivos com o Android Enterprise.  A Intune só pode fornecer suporte total para dispositivos Android geridos por administrador de dispositivos que executam o Android 10 e, posteriormente, através do Q2 CY2020. Dispositivos geridos por administrador de dispositivos (exceto Samsung) que estão a executar o Android 10 ou mais tarde depois desta época não serão capazes de ser totalmente geridos. Em particular, os dispositivos com impacto não receberão novos requisitos de senha.

Para obter mais informações sobre esta definição, consulte [mover dispositivos Android do administrador do dispositivo para a gestão de perfis](../enrollment/android-move-device-admin-work-profile.md)de trabalho. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorizar e resolver problemas

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>O Data Warehouse agora fornece o endereço MAC<!-- 6123680  -->
O Intune Data Warehouse fornece o endereço MAC como um novo imóvel ( `EthernetMacAddress` ) na entidade para permitir que os administradores se `device` correlacionadam entre o endereço mac do utilizador e do hospedeiro. Esta propriedade ajuda a alcançar utilizadores específicos e incidentes de resolução de problemas que ocorrem na rede. Os administradores também podem usar esta propriedade em [relatórios power BI](../developer/reports-proc-get-a-link-powerbi.md) para construir relatórios mais ricos. Para mais informações, consulte a entidade do [dispositivo](../developer/intune-data-warehouse-collections.md#devices) Intune Data Warehouse.

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Propriedades adicionais de inventário de dispositivos de armazém de dados<!-- 6125732  -->
Propriedades adicionais de inventário de dispositivos estão disponíveis usando o Intune Data Warehouse. As seguintes propriedades são agora expostas através da coleção beta dos [dispositivos:](../developer/reports-ref-devices.md#devices)
- `ethernetMacAddress`- O identificador de rede único deste dispositivo.
- `model`- O modelo do dispositivo.
- `office365Version`- A versão do Office 365 que está instalada no dispositivo.
- `windowsOsEdition`- A versão do Sistema Operativo.

As seguintes propriedades são agora expostas através da coleção beta do [dispositivoPropertyHistory:](../developer/reports-ref-devices.md#devicepropertyhistories)
- `physicalMemoryInBytes`- A memória física em bytes.
- `totalStorageSpaceInBytes`- Capacidade total de armazenamento em bytes.

Para mais informações, consulte a [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Ajuda e suporte atualização de fluxo de trabalho para apoiar serviços adicionais<!-- 5654170   -->
Atualizámos a página de Ajuda e Suporte no centro de administração do Microsoft Endpoint Manager, onde agora escolhe o tipo de [gestão que utiliza](../fundamentals/get-support.md#options-to-access-help-and-support). Com esta alteração poderá selecionar entre os seguintes tipos de gestão:

- Gestor de Configuração (inclui Desktop Analytics)
- Intune
- Cogestão

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Segurança

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Utilize uma pré-visualização de políticas focadas no administrador de segurança como parte da segurança endpoint<!--6131401  -->
Como pré-visualização pública, adicionámos vários novos grupos políticos sob o nó de segurança Endpoint no centro de administração da Microsoft Endpoint Management. Como administrador de segurança, pode utilizar estas novas políticas para se concentrar em aspetos específicos da segurança do dispositivo para gerir grupos discretos de configurações relacionadas sem a sobrecarga do maior organismo de política de configuração do dispositivo.

Com exceção da nova *política antivírus para* o Antivírus do Microsoft Defender (ver abaixo), as definições em cada uma das novas políticas e perfis de pré-visualização são as mesmas definições que pode já configurar através dos perfis de [configuração do Dispositivo](../configuration/device-profile-create.md) hoje em dia.

Seguem-se os novos tipos de políticas que estão todos em pré-visualização e os seus tipos de perfil disponíveis:

- **Antivírus (Pré-visualização)**:
  - macOS:
    - **Antivírus** - Gerencie as definições de [política antivírus](../protect/antivirus-microsoft-defender-settings-macos.md) para o macOS gerir o [Microsoft Defender ATP para Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

  - Windows 10 e mais tarde:
    - **Microsoft Defender Antivírus** - Gerencie as definições de [política antivírus](../protect/antivirus-microsoft-defender-settings-windows.md) para proteção de nuvens, exclusões antivírus, reparação, opções de digitalização e muito mais.

      O perfil Antivírus do Antivírus do *Microsoft Defender antivírus* é uma exceção que introduz um novo exemplo de definições que são encontradas como parte de um perfil de restrição do dispositivo. Estas novas definições antivírus:

        - São as mesmas definições encontradas nas restrições do dispositivo, mas suportam uma terceira opção para configuração que não está disponível quando configurada como uma restrição do dispositivo.
        - Aplicar-se a dispositivos cogeridos com o Gestor de Configuração, quando o slider de [cogestão](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) para a Proteção de Endpoint estiver definido para Intune.

     Planeie utilizar *Antivirus*o novo perfil  >  *Antivírus Microsoft Defender Antivírus* em vez de configurá-los através de um perfil de restrição do dispositivo.

  - **Experiência de Segurança do Windows** - Gerir as definições de Segurança do Windows que os utilizadores finais podem visualizar no centro de Segurança do Microsoft Defender e nas notificações que recebem. Estas definições são inalteradas das disponíveis como um perfil de proteção de ponto final de configuração do dispositivo.

- **Encriptação do disco (Pré-visualização)**:
  - macOS:
    - **FileVault**
  - Windows 10 e mais tarde:
    - **BitLocker**
- **Firewall (Pré-visualização)**:
  - macOS:
    - **firewall macOS**
  - Windows 10 e mais tarde:
    - **Microsoft Defender Firewall**
- **Deteção e resposta de pontofinal (Pré-visualização)**:
  - Windows 10 e mais tarde: - **Windows 10 Intune**
- Redução da superfície de **ataque (Pré-visualização)**:
  - Windows 10 e mais tarde:
    - **App e isolamento do navegador**
    - **Proteção web**
    - **Controlo de aplicações**
    - **Regras de redução da superfície de ataque**
    - **Controlo do dispositivo**
    - **Exploit Protection**
- **Proteção da conta (Pré-visualização)**:
  - Windows 10 e mais tarde:
    - **Account protection (Proteção de contas)**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Semana de 9 de março de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Configure o agente de otimização de entrega ao descarregar conteúdo da aplicação Win32<!-- 5410945 -->

Pode configurar o agente de otimização de entrega para descarregar conteúdo da aplicação Win32, tanto em segundo plano como em primeiro plano, com base na atribuição. Para as aplicações Win32 existentes, os conteúdos continuarão a descarregar em modo de fundo. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione **Apps**  >  **Todas as aplicações**  >  *selecionam a aplicação Win32*  >  **Properties**. **Selecione Editar** ao lado de **Atribuições**.  Editar a atribuição selecionando **Incluir** em **modo** na secção **Requerida.**  Encontrará a nova definição na secção de definições da **App.** Para mais informações sobre a Otimização de Entregas, consulte a [gestão da aplicação Win32 - Otimização de Entrega](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Alterar o utilizador primário para dispositivos Windows<!-- 3794742   -->
Pode alterar o Utilizador Primário para dispositivos híbridos windows e Azure AD. Para tal, vá a Dispositivos **Intune**  >  **Devices**  >  **Todos os dispositivos** > escolha um dispositivo > Utilizador Primário de **Propriedades**  >  **Primary User**. Para mais informações, consulte [Alterar o utilizador principal de um dispositivo](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

Foi também criada uma nova permissão RBAC (Dispositivos Geridos / set primary user) para esta tarefa. A permissão foi adicionada a funções incorporadas, incluindo Helpdesk Operator, School Administrator e Endpoint Security Manager.

Esta funcionalidade está a ser lançada para os clientes globalmente em pré-visualização. Deve ver a funcionalidade nas próximas semanas.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Semana de 2 de março de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Anexo de inquilino do Microsoft Endpoint Manager: As ações de sincronização e dispositivos do dispositivo<!-- 6317104, CM3555758-->
O Microsoft Endpoint Manager está a reunir o Diretor de Configuração e o Intune numa única consola. A partir da versão de pré-visualização técnica do Gestor de Configuração 2002.2, pode carregar os seus dispositivos de Gestor de Configuração para o serviço de cloud e tomar ações sobre eles no centro de administração. Para mais informações, consulte [funcionalidades na versão de pré-visualização técnica do Gestor de Configuração 2002.2](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Reveja o artigo de [pré-visualização técnica do Gestor](https://docs.microsoft.com/configmgr/core/get-started/technical-preview) de Configuração antes de instalar esta atualização. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback.

#### <a name="bulk-remote-actions--4576882--"></a>Ações remotas a granel<!--4576882-->
Pode agora emitir comandos a granel para as seguintes ações remotas: reiniciar, mudar o nome, reiniciar o Piloto Automático, limpar e eliminar. Para ver as novas ações a granel, vá ao [microsoft Endpoint Manager administrador](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **dispositivos**  >  todas as ações em massa dos**dispositivos**  >  **Bulk actions**.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Todos os dispositivos listam melhor pesquisa, classificação e filtro<!--6179023-->
A lista de todos os dispositivos foi melhorada para um melhor desempenho, pesquisa, triagem e filtragem. Para mais informações, consulte [esta Dica de Suporte](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### <a name="app-management"></a>Gestão de aplicações  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Melhor experiência de inscrição no Portal da Empresa para Android    
Atualizámos o layout de vários ecrãs de acesso no aplicativo Portal da Empresa para Android para tornar a experiência mais moderna, simples e limpa para os utilizadores. Para ver as melhorias, veja [What's New na app UI](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui).

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Semana de 24 de fevereiro de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>melhorias na experiência do utilizador do portal da empresa macOS<!-- 5568987 -->
Fizemos melhorias na experiência de inscrição de dispositivos macOS e na aplicação Do Portal da Empresa para mac. Verá as seguintes melhorias:
- Uma melhor experiência do Microsoft **AutoUpdate** durante a inscrição que irá garantir que os seus utilizadores tenham a versão mais recente do Portal da Empresa.
- Um passo de verificação de conformidade melhorado durante a inscrição.
- Suporte para IDs de incidentecopiados, para que os seus utilizadores possam enviar erros dos seus dispositivos para a sua equipa de suporte da empresa mais rapidamente.

Para obter mais informações sobre a inscrição e a aplicação Portal da Empresa para Mac, consulte [Inscrever o seu dispositivo macOS utilizando a aplicação Portal da Empresa.](../user-help/enroll-your-device-in-intune-macos-cp.md)

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>As políticas de proteção de aplicações para Better Mobile suportam agora iOS e iPadOS<!-- 6224512  -->

Em outubro de 2019, a política de proteção de aplicações Intune adicionou a capacidade de usar dados dos nossos parceiros de Defesa de Ameaças da Microsoft. Com esta atualização, pode agora utilizar uma política de proteção de aplicações para bloquear ou limpar seletivamente os dados corporativos dos utilizadores com base na saúde de um dispositivo que utiliza o Better Mobile no iOS e iPadOS.  Para mais informações, consulte [Create Mobile Threat Defense protection policy with Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Exportações da lista de todos os dispositivos agora em formato CSV zipped<!--6343117-->
Exportações dos **Dispositivos**  >  **Todos os dispositivos** estão agora em formato CSV zipped.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Semana de 17 de fevereiro de 2020 (lançamento de serviço de 2002)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>Aplicação microsoft Defender Advanced Threat Protection (ATP) para macOS<!-- 5424618 -->
A Intune fornece uma forma fácil de implementar a aplicação Microsoft Defender Advanced Threat Protection (ATP) para o macOS para gerir dispositivos Mac. Para mais informações, consulte [adicionar atP do Microsoft Defender aos dispositivos macOS utilizando](../apps/apps-advanced-threat-protection-macos.md) a Microsoft Intune e o Microsoft Defender Advanced Threat Protection para [Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuração do dispositivo

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Ativar o controlo de acesso à rede (NAC) com a Cisco AnyConnect VPN em dispositivos iOS<!-- 4860111  -->
Nos dispositivos iOS, pode criar um perfil VPN e utilizar diferentes tipos de ligação, incluindo cisco AnyConnect ( Perfis de**configuração**do dispositivo  >  **Profiles**  >  **Criar**  >  **perfil iOS** para plataforma > **VPN** para o tipo de perfil > **Cisco AnyConnect** para o tipo de ligação).

Pode ativar o controlo de acesso à rede (NAC) com o Cisco AnyConnect. Para utilizar esta funcionalidade:

1. No Guia de Administrador de Motores de [Serviços de Identidade da Cisco,](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)utilize os passos na configuração do **Microsoft Intune como um servidor MDM** para configurar o Motor de Serviços de Identidade da Cisco (ISE) em Azure.
2. No perfil de configuração do dispositivo Intune, selecione a definição de Controlo de Acesso à **Rede ativa (NAC).**

Para ver todas as definições de VPN disponíveis, vá a [Configurar as definições VPN nos dispositivos iOS](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscrição de dispositivos

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Número de série na página de certificado Apple MDM Push<!--5947765  -->
A página do certificado Apple MDM Push mostra agora o número de série. O número de série é necessário para recuperar o acesso ao certificado Apple MDM Push se o acesso ao Apple ID que criou o certificado for perdido. Para ver o número de série, vá ao **certificado**Apple MDM Push de inscrição no  >  **IOS**  >  **iOS**  >  **Apple MDM Push certificate**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Novas opções de calendário de atualizações para empurrar atualizações do OS para dispositivos iOS/iPadOS inscritos<!--5879689  -->
Pode escolher entre as seguintes opções ao agendar atualizações do sistema operativo para dispositivos iOS/iPadOS. Estas opções aplicam-se a dispositivos que utilizaram os tipos de matrículas do Apple Business Manager ou do Apple School Manager.
- Atualização no próximo check-in
- Atualização durante o horário programado
- Atualização fora do horário programado

Para as duas últimas opções, pode criar várias janelas de tempo.

Para ver as novas opções, vá ao MEM > **As**políticas de atualização do  >  **iOS/iPadOS**  >  **Update policies for iOS/iPadOS**  >  **Criam perfil**.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Escolha quais as atualizações iOS/iPadOS para empurrar para dispositivos matriculados<!--5879689  -->
Pode escolher uma atualização específica do iOS/iPadOS (exceto a mais recente atualização) para empurrar para dispositivos que tenham matriculado utilizando o Apple Business Manager ou o Apple School Manager. Estes dispositivos devem ter uma política de configuração do dispositivo definida para atrasar a visibilidade da atualização do software durante alguns dias. Para ver esta funcionalidade, vá ao MEM > **Dispositivos**  >  **iOS**  >  **Atualização das políticas para iOS/iPadOS**  >  **Criar perfil**.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Segurança do dispositivo

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Experiência melhorada de reporte intune<!-- 3791418   -->
Intune agora fornece uma experiência de reporte melhorada, incluindo novos tipos de relatórios, melhor organização de relatórios, opiniões mais focadas, melhor funcionalidade de relatório, bem como dados mais consistentes e oportunos. A experiência de reporte passará da pré-visualização pública para a GA (disponibilidade geral). Além disso, o lançamento da GA fornecerá suporte de localização, correções de bugs, melhorias de design e dados agregados de conformidade de dispositivos em azulejos no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Os novos tipos de relatórios concentram-se nas seguintes informações:

- **Operacional** - Fornece novos registos com foco negativo para a saúde. 
- **Organizacional** - Fornece um resumo mais amplo do estado geral.
- **Histórico** - Fornece padrões e tendências ao longo de um período de tempo.
- **Especialista** - Permite-lhe utilizar dados brutos para criar os seus próprios relatórios personalizados.

O primeiro conjunto de novos relatórios centra-se na conformidade do dispositivo. Para mais informações, consulte blog [- Microsoft Intune reporting framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) and [Intune reports](reports.md).

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Consolidado a localização das linhas de base de segurança na UI<!-- 6177074   -->
Consolidamos os caminhos para encontrar [as linhas de segurança](../protect/security-baselines.md) no centro de administração do Microsoft Endpoint Manager, removendo as linhas de *segurança* de vários locais da UI. Para encontrar as linhas de base de segurança, utilize agora o seguinte caminho: Bases de segurança de **segurança de ponto final**  >  **Security baselines**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>Apoio alargado aos certificados PKCS importados<!-- 6044197  -->
Expandimos o suporte para usar [certificados PKCS importados](../protect/certificates-imported-pfx-configure.md#supported-platforms) para suportar *dispositivos geridos pela Android Enterprise.* Geralmente, a importação de certificados PFX é usada para cenários de encriptação S/MIME, onde os certificados de encriptação de um utilizador são exigidos em todos os seus dispositivos para que a desencriptação de e-mail possa ocorrer.

As seguintes plataformas apoiam a importação de certificados PFX:

- Android - Administrador de Dispositivos
- Android Enterprise - Totalmente Gerido
- Android Enterprise - Perfil de trabalho
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Ver a configuração de segurança do ponto final para dispositivos<!-- 6206460  -->
Atualizámos o nome da opção no centro de administração do Microsoft Endpoint Manager, para visualizar [configurações](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)de segurança de ponto final que se aplicam a um dispositivo específico . Esta opção é renomeada para configuração de **segurança Endpoint** porque mostra linhas de base de segurança aplicáveis e políticas adicionais criadas fora das linhas de base de segurança. Anteriormente, esta opção chamava-se Linhas de Base de *Segurança.*

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Controlo de acesso baseado em funções

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Intune Roles alterações na interface do utilizador<!--5801612   -->
A interface de utilizador do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)administrador a administração Do  >  **inquilinroles**  >  **Roles** foi melhorada para um design mais fácil de usar e intuitivo. Esta experiência fornece as mesmas definições e detalhes que utiliza agora, no entanto a nova experiência emprega um processo semelhante ao de um assistente.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>Semana de 17 de fevereiro de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="microsofts-new-office-app---5859926---"></a>Nova app do Office da Microsoft<!-- 5859926 -->
A nova aplicação do Office da Microsoft está agora geralmente disponível para download e utilização. A aplicação Office é uma experiência consolidada onde os seus utilizadores podem trabalhar através do Word, Excel e PowerPoint dentro de uma única aplicação. Pode direcionar a aplicação com uma política de proteção de aplicações para garantir que os dados a serem acedidos estão protegidos.

Para mais informações, consulte como ativar as políticas de [proteção de aplicações Intune com a aplicação de pré-visualização móvel do Office](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>Semana de 10 de fevereiro de 2020

### <a name="windows-7-ends-extended-support--3042987---"></a>Windows 7 termina suporte alargado<!--3042987 -->
O Windows 7 chegou ao fim do suporte alargado a 14 de janeiro de 2020. Intune deprecated suporte para dispositivos que executam o Windows 7 ao mesmo tempo. A assistência técnica e as atualizações automáticas que ajudam a proteger o seu PC deixaram de estar disponíveis. Deve fazer o upgrade para o Windows 10. Para mais informações, consulte o post do [blog Plan for Change](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Microsoft Edge versão 77 e mais tarde em dispositivos Windows 10<!-- 5843584 -->
Intune agora suporta desinstalar a versão 77 do Microsoft Edge e mais tarde nos dispositivos do Windows 10. Para mais informações, consulte [Adicionar o Microsoft Edge para o Windows 10 ao Microsoft Intune](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>Ecrã removido do Portal da Empresa, inscrição de perfil de trabalho Android<!--6103987 -->
O **ecrã What's Next?** Foi removido do fluxo de inscrição de perfil de trabalho Android no Portal da Empresa para agilizar a experiência do utilizador. Vá ao [Enroll with Android work profile](../user-help/enroll-device-android-work-profile.md) para ver o fluxo de inscrição de perfil android atualizado.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>App do Portal da Empresa melhorou o desempenho<!-- 6178652 -->
A aplicação Portal da Empresa foi atualizada para suportar um melhor desempenho para dispositivos que utilizam processadores ARM64, como o Surface Pro X. Anteriormente, o Portal da Empresa operava num modo ARM32 emulado. Agora, na versão 10.4.7080.0 ou superior, a aplicação Portal da Empresa é compilada de forma nativa para arm64. Para obter mais informações sobre a aplicação Portal da Empresa, consulte [como configurar a aplicação Microsoft Intune Company Portal](../apps/company-portal-app.md).

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>Semana de 27 de janeiro de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>Suporte intune para canal adicional de implementação da versão 77 do Microsoft Edge para o macOS<!-- 5983950  -->
O Microsoft Intune suporta agora o canal de implementação **stable** adicional para a aplicação Microsoft Edge para macOS. O canal **Estável** é o canal recomendado para a implementação do Microsoft Edge em ambientes empresariais. Atualiza a cada seis semanas, cada versão incorporando melhorias do canal **Beta.** Além dos canais **Stable** e **Beta,** o Intune suporta um canal **Dev.** A pré-visualização pública oferece canais estáveis e dev para a versão 77 do Microsoft Edge e mais tarde para o macOS. As atualizações automáticas do navegador estão on por padrão. Para mais informações, consulte [Adicionar Microsoft Edge para dispositivos macOS utilizando o Microsoft Intune](../apps/apps-edge-macos.md).

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>Aposentadoria do Navegador Gerido Intune<!--5728447 -->
O Navegador Gerido Intune será retirado. Utilize o Microsoft Edge para a sua experiência de navegador Intune protegida. 

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>Semana de 20 de janeiro de 2020 (lançamento de serviço de 2001)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>Mudança de experiência do utilizador ao adicionar apps ao Intune<!-- 4705829   -->
Verá uma nova experiência de utilizador ao adicionar aplicações via Intune. Esta experiência fornece as mesmas definições e detalhes que utilizou anteriormente, no entanto a nova experiência segue um processo semelhante a um assistente antes de adicionar uma aplicação ao Intune. Esta nova experiência também fornece uma página de revisão antes de adicionar a app. A partir do centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione **Apps**  >  **Todas as aplicações**  >  **Add**. Para obter mais informações, veja [Adicionar aplicações ao Microsoft Intune](../apps/apps-add.md).

#### <a name="require-win32-apps-to-restart----5622282-----"></a>Exigir aplicações Win32 para reiniciar <!-- 5622282   -->
Pode exigir que uma aplicação Win32 reinicie após uma instalação bem sucedida. Além disso, pode escolher a quantidade de tempo (o período de graça) antes de ocorrer o reinício.

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>Mudança de experiência do utilizador ao configurar aplicações em Intune<!-- 4207990   -->
Verá uma nova experiência de utilizador ao criar políticas de configuração de aplicações no Intune. Esta experiência fornece as mesmas definições e detalhes que utilizou anteriormente, no entanto a nova experiência segue um processo semelhante a um assistente antes de adicionar uma apólice ao Intune. A partir do centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione **políticas**de  >  **configuração**de apps  >  **Add**. Para mais informações, consulte as políticas de [configuração da App para o Microsoft Intune](../apps/app-configuration-policies-overview.md). 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>Suporte intune para adicional Microsoft Edge para canal de implementação do Windows 10<!-- 5861774 -->
O Microsoft Intune suporta agora o canal de implementação **adicional do Estável** para o Microsoft Edge (versão 77 e mais tarde) para a aplicação do Windows 10. O canal **Stable** é o canal recomendado para a implementação do Microsoft Edge para o Windows 10 em ambientes empresariais. Este canal atualiza-se de seis em seis semanas, cada versão incorporando melhorias do canal **Beta.** Além dos canais **Stable** e **Beta,** o Intune suporta um canal **Dev.** Para mais informações, consulte o [Microsoft Edge para windows 10 - Configurar as definições](../apps/apps-windows-edge.md#configure-app-settings)das aplicações .

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuração do dispositivo

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>Melhoria da experiência de interface do utilizador ao configurar o conector Exchange ActiveSync no local UI<!-- 5695492   -->
Atualizámos a experiência para [configurar o conector Exchange ActiveSync no local.](../protect/exchange-connector-install.md) A experiência atualizada utiliza um único painel para configurar, editar e resumir os detalhes dos seus conectores no local.

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>Adicione configurações automáticas de procuração aos perfis Wi-Fi para perfis de trabalho Android Enterprise<!-- 4490822   -->
Nos dispositivos Android Enterprise Work Profile, pode criar perfis Wi-Fi. Ao escolher o tipo Wi-Fi Enterprise, também pode introduzir o tipo de Protocolo de Autenticação Extensível (EAP) utilizado na sua rede Wi-Fi.

Agora, quando escolher o tipo Enterprise, também pode introduzir definições automáticas de procuração, incluindo um URL de servidor proxy, como `proxy.contoso.com` .

Para ver as definições de Wi-Fi atuais que pode configurar, vá a [adicionar configurações wi-fi para dispositivos que executam o Android Enterprise e o quiosque Android no Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only).

Aplica-se a:
- Perfil de trabalho android Enterprise

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscrição de dispositivos

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>Bloqueie as inscrições do Android pelo fabricante de dispositivos<!--5197392  -->
Pode bloquear os dispositivos de inscrição com base no fabricante do dispositivo. Esta funcionalidade aplica-se ao administrador de dispositivos Android e aos dispositivos de perfil de trabalho Android Enterprise. Para ver restrições de inscrição, vá ao centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Devices**  >  **Dispositivos restrições**de inscrição .

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>Melhorias no iOS/iPadOS Criar perfil de tipo de inscrição UI<!-- 6055005 -->
Para a inscrição do utilizador iOS/iPadOS, a página de **Definições** do perfil de **inscrição Create** foi simplificada para melhorar o processo de escolha do **tipo de inscrição,** mantendo a mesma funcionalidade. Para ver o novo UI, vá ao [microsoft Endpoint Manager administrador centro](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **dispositivos**  >  **iOS**  >  **iOS inscrição**tipos de  >  **inscrição**Criar página de Definições de  >  **perfil.**  >  **Settings** Para mais informações, consulte Criar um perfil de [Inscrição do Utilizador no Intune](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="new-information-in-device-details---4471759-5604099----"></a>Novas informações sobre detalhes do dispositivo<!-- 4471759 5604099  -->
As seguintes informações estão agora na página **'Overview'** para dispositivos:
- Capacidade de memória (quantidade de memória física no dispositivo)
- Capacidade de armazenamento (quantidade de armazenamento físico no dispositivo) 
- Arquitetura CPU

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>IOS bypass ativação lock ação remota renomeada para bloqueio de ativação desativação <!--5904591  -->
O bloqueio de **ativação** de bypass de ação remota foi renomeado para **desativação**do bloqueio de ativação . Para mais informações, consulte [Desativar o bloqueio de ativação do iOS com intune](../remote-actions/device-activation-lock-disable.md).

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>Suporte de implementação de funcionalidades do Windows 10 para dispositivos Autopilot<!-- 5948137   -->
Intune agora suporta direcionar dispositivos registados para o Autopilot utilizando implementações de atualizações de [funcionalidades do Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates).

As políticas de atualização de funcionalidades do Windows 10 não podem ser aplicadas durante o Autopilot fora da experiência da caixa (OOBE) e só serão aplicadas na primeira análise do Windows Update depois de um dispositivo ter terminado o fornecimento (que normalmente é um dia).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorizar e resolver problemas

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Relatórios de implementação do Windows Autopilot (pré-visualização) <!-- 3856172   -->
Um novo relatório detalha cada dispositivo implantado através do Windows Autopilot. Para mais informações, consulte o [relatório de implantação do Autopilot](../enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Controlo de acesso baseado em funções

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>Novo intune embutido gerente de segurança Endpoint<!--4253397   -->
Um novo papel intune incorporado está disponível: o gestor de segurança Endpoint. Esta nova função dá aos administradores acesso total ao nó de Endpoint Manager em Intune e acesso pronto apenas a outras áreas. O papel é uma expansão do papel de "Administrador de Segurança" da Azure AD. Se atualmente apenas tem a Global Admins como papéis, então não são necessárias alterações. Se usar papéis, e quiser a granularidade que o Gestor de Segurança endpoint proporciona, então atribua esse papel quando estiver disponível. Para obter mais informações sobre papéis incorporados, consulte [o controlo de acesso baseado em Funções.](role-based-access-control.md)

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>Semana de 6 de janeiro de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>Suporte S/MIME para Microsoft Outlook para iOS<!-- 2669398 -->
O Intune suporta a entrega de certificados de assinatura e encriptação S/MIME que podem ser utilizados com o Outlook para iOS em dispositivos iOS. Para mais informações, consulte a [rotulagem e proteção de sensibilidade no Outlook para iOS e Android](https://aka.ms/omsmime).

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>Conteúdo da aplicação Cache Win32 utilizando o servidor Cache Conectado da Microsoft<!-- 6030314 -->
Pode instalar um servidor De Cache ligado ao Microsoft no seu Gestor de Configuração para cache O conteúdo da aplicação Intune Win32. Para mais informações, consulte o Microsoft Connected Cache no Gestor de [Configuração - Suporte para aplicações Intune Win32](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Controlo de acesso baseado em funções

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Os perfis de modelos administrativos do Windows 10 (ADMX) suportam agora etiquetas de âmbito <!--5137390 -->
Agora pode atribuir etiquetas de âmbito a perfis de modelo administrativo (ADMX). Para isso, vá aos perfis de configuração de dispositivos **intune**> escolha um perfil de  >  **Devices**  >  **Configuration profiles** modelos administrativos na lista > **etiquetas**de  >  **âmbito**de propriedades . Para obter mais informações sobre etiquetas de âmbito, consulte etiquetas de [mira de atribuir para outros objetos](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>Semana de 30 de dezembro de 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>Recuperar a chave de recuperação pessoal dos dispositivos macOS encriptados mEM<!-- 4851745 -->
Os utilizadores finais podem recuperar a sua chave de recuperação pessoal (chave FileVault) utilizando a aplicação portal da empresa iOS. O dispositivo que tenha a chave de recuperação pessoal deve ser matriculado com Intune e encriptado com fileVault através de Intune. Utilizando a aplicação portal da empresa iOS, um utilizador final pode recuperar a sua chave de recuperação pessoal no seu dispositivo macOS encriptado clicando na **tecla Get Recovery**. Também pode recuperar a chave de recuperação de Intune selecionando **Dispositivos**  >  *o dispositivo macOS encriptado e inscrito*Obtenha a chave de  >  **recuperação**. Para mais informações sobre fileVault, consulte [a encriptação FileVault para macOS](../protect/encrypt-devices-filevault.md).

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>aplicações VPP licenciadas por utilizadores iOS e iPadOS<!-- 5619268 -->
Para dispositivos iOS e iPadOS matriculados pelos utilizadores, os utilizadores finais deixarão de ser apresentados com aplicações VPP recém-criadas, licenciadas por dispositivos, conforme disponível. No entanto, os utilizadores finais continuarão a ver todas as aplicações VPP licenciadas pelo utilizador dentro do Portal da Empresa. Para obter mais informações sobre aplicações VPP, consulte [como gerir aplicações iOS e macOS adquiridas através do Apple Volume Purchase Program com](../apps/vpp-apps-ios.md)o Microsoft Intune .

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>Semana de 23 de dezembro de 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>Aviso - Windows 10 1703 (RS2) vai sair do suporte <!-- 5026679 -->
A partir de 9 de outubro de 2018, o Windows 10 1703 (RS2) saiu do suporte da plataforma da Microsoft para edições Home, Pro e Pro for Workstations. Para as edições da Empresa e da Educação do Windows 10, o Windows 10 1703 (RS2) saiu do suporte da plataforma a 8 de outubro de 2019. A partir de 26 de dezembro de 2019, vamos atualizar a versão mínima da aplicação Portal da Empresa Windows para o Windows 10 1709 (RS3). Os computadores que executam versões antes de 1709 deixarão de receber versões atualizadas para a aplicação a partir da Microsoft Store. Já comunicámos esta alteração aos clientes que estão a gerir versões mais antigas do Windows 10 através do centro de mensagens. Para mais informações, consulte [a ficha técnica do ciclo](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)de vida do Windows .

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>Semana de 16 de dezembro de 2019

### <a name="device-configuration"></a>Configuração do dispositivo

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Atualizações aos modelos administrativos para dispositivos Windows 10 <!-- 5941568 -->

Pode utilizar modelos ADMX no Microsoft Intune para controlar e gerir as definições para Microsoft Edge, Office e Windows. Os modelos administrativos em Intune fizeram as seguintes atualizações de definição de políticas:

- Suporte adicional para as versões 78 e 79 do Microsoft Edge.
- Inclui os ficheiros ADMX de 11 de novembro de 2019 em [ficheiros de Modelo Administrativo (ADMX/ADML) e ferramenta de personalização do Office 365 ProPlus, Office 2019 e Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

Para obter mais informações sobre os modelos ADMX em Intune, consulte [utilizar os modelos do Windows 10 para configurar as definições](../configuration/administrative-templates-windows.md)de política de grupo no Microsoft Intune .

Aplica-se a:

- Windows 10 e posterior

## <a name="week-of-december-9-2019-1912-service-release"></a>Semana de 9 de dezembro de 2019 (lançamento de Serviço de 1912)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>Migrar para o Microsoft Edge para cenários de navegação geridos<!-- 5173762 -->
À medida que nos aproximamos da reforma do Navegador Gerido Intune, fizemos alterações às políticas de proteção de aplicações para simplificar os passos necessários para transferir os seus utilizadores para edge. Atualizámos as opções para a definição da política de proteção de aplicações Restringir a **transferência de conteúdos web com outras aplicações** para ser uma das seguintes:

- Qualquer aplicação
- Browser Gerido do Intune
- Microsoft Edge
- Navegador não gerido 

Quando selecionar o **Microsoft Edge,** os seus utilizadores finais verão mensagens de acesso condicional notificando-os de que o Microsoft Edge é necessário para cenários de navegação geridos. Serão solicitados a descarregar e iniciar sessão no Microsoft Edge com as suas contas AAD, caso ainda não o tenham feito.  Isto será o equivalente a ter direcionado as suas aplicações ativadas pelo MAM com a definição de config da aplicação `com.microsoft.intune.useEdge` definida para **True**. As políticas de proteção de aplicações existentes que utilizaram a definição de **navegadores geridos** pela Política terão agora o **Navegador Gerido Intune** selecionado, e não verá nenhuma alteração de comportamento. Isto significa que os utilizadores verão mensagens para utilizar o Microsoft Edge se definirem a definição de configuração da aplicação **UseEdge** para **True**. Encorajamos todos os clientes que alavancam cenários de navegação geridos para atualizar as suas políticas de proteção de aplicações com a Transferência de **conteúdos web Restrito com outras aplicações** para garantir que os utilizadores estão a ver as orientações adequadas para a transição para o Microsoft Edge, independentemente da aplicação a partir da qual estejam a lançar links. 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>Configurar conteúdo de notificação de aplicativos para contas de organização<!-- 2576686  -->
Intune app protection policies (APP) em dispositivos Android e iOS permitem controlar conteúdo de notificação de aplicações para contas Org. Pode selecionar uma opção (Permitir, bloquear org Dados ou Bloquear) para especificar como as notificações para as contas org são mostradas para a aplicação selecionada. Esta funcionalidade requer apoio das aplicações e pode não estar disponível para todas as aplicações ativadas pela APP. As perspetivas para a versão 4.15.0 (ou posterior) do iOS e o Outlook para Android 4.83.0 (ou mais tarde) irão suportar esta definição. A definição está disponível na consola, mas a funcionalidade começará a entrar em vigor após 16 de dezembro de 2019. Para mais informações sobre app, veja [o que são as políticas de proteção de aplicações?](../apps/app-protection-policy.md)

#### <a name="microsoft-app-icons-update--4677605----"></a>Atualização de ícones de aplicativos da Microsoft<!--4677605  -->
Os ícones utilizados para aplicações da Microsoft na aplicação que visam o painel para políticas de proteção de aplicações e políticas de configuração de aplicações foram atualizados.

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>Exigir a utilização de teclados aprovados no Android<!--4761794  -->
Como parte de uma política de proteção de aplicações, pode especificar a definição de [**teclados aprovados**](../apps/app-protection-policy-settings-android.md#data-protection) para gerir quais os teclados Android que podem ser usados com aplicações android geridas. Quando um utilizador abre a aplicação gerida e ainda não utiliza um teclado aprovado para essa aplicação, é solicitado que altere para um dos teclados aprovados já instalados no seu dispositivo. Se necessário, é-lhes apresentado um link para descarregar um teclado aprovado a partir da Google Play Store, que podem instalar e configurar. O utilizador só pode editar campos de texto numa aplicação gerida quando o seu teclado ativo não é um dos teclados aprovados.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuração do dispositivo

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>Experiência de inscrição única atualizada para apps e websites nos seus dispositivos iOS, iPadOS e macOS<!-- 4999578  -->
A Intune adicionou mais definições de inscrição única (SSO) para dispositivos iOS, iPadOS e macOS. Agora pode configurar as extensões de aplicações SSO redirecionadas escritas pela sua organização ou pelo seu fornecedor de identidade. Utilize estas configurações para configurar uma experiência de inscrição única perfeita para apps e websites que utilizam métodos modernos de autenticação, como o OAuth e o SAML2. 

Estas novas definições expandem-se nas definições anteriores para as extensões de apps SSO e na extensão Kerberos incorporada da Apple (**Perfis**de configuração de  >  **dispositivos**Criam perfis de  >  **Profiles**  >  **perfil**  >  **iOS/iPadOS** ou **macOS** para o tipo de plataforma > **funcionalidades do dispositivo** para o tipo de perfil). 

Para ver toda a gama de definições de extensão de aplicações SSO que pode configurar, vá ao [SSO no iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) e [SSO no macOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Aplica-se a:

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>Atualizámos duas definições de restrição de dispositivos para dispositivos iOS e iPadOS para corrigir o seu comportamento<!-- 5701352    -->
Para dispositivos iOS, pode criar perfis de restrição de dispositivos que **permitem atualizações pKI de ar** e bloqueia o modo **restrito USB** **(Perfis**de configuração do dispositivo Criar perfis de  >  **Device configuration**  >  **Profiles**  >  **perfil**  >  **iOS/iPadOS** para **restrições** de plataforma > Dispositivo para o tipo de perfil). Antes desta versão, as definições e descrições da UI para as seguintes definições estavam incorretas e foram agora corrigidas. A partir desta versão, o comportamento das definições é o seguinte:

**Bloqueie atualizações PKI over-the-air**: **O bloco** impede que os seus utilizadores recebam atualizações de software a menos que o dispositivo esteja ligado a um computador. **Não configurado** (predefinido): permite que um dispositivo receba atualizações de software sem estar ligado a um computador.
- Anteriormente, esta definição permite-lhe configurá-lo como: **Permitir**, que permite que os seus utilizadores recebam atualizações de software sem ligar os seus dispositivos a um computador.
**Permitir acessórios USB enquanto o dispositivo estiver bloqueado:** **Permitir que** os acessórios USB troquem dados com um dispositivo que está bloqueado há mais de uma hora. **Não configurado** (predefinido) não atualiza o modo USB Restrito no dispositivo, e os acessórios USB serão bloqueados da transferência de dados do dispositivo se estiverem bloqueados durante mais de uma hora.
- Anteriormente, esta definição permite-lhe configurá-lo como: **Bloqueie** para desativar o modo restrito USB em dispositivos supervisionados.

Para obter mais informações sobre a definição pode configurar, consulte as definições do [dispositivo iOS e iPadOS para permitir ou restringir as funcionalidades utilizando o Intune](../configuration/device-restrictions-ios.md).

Esta funcionalidade aplica-se a:

- OS/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Perfis de configuração de dispositivos de rede com fios para dispositivos macOS<!-- 3508686  -->
   > [!NOTE]
   > Esta funcionalidade foi adiada, mas será lançada em breve.

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>Bloqueie os utilizadores de configurar credenciais de certificado na loja de chaves gerida em dispositivos proprietários de dispositivos Android Enterprise<!-- 3311998 -->
Nos dispositivos do Proprietário do dispositivo Android Enterprise, pode configurar uma nova definição que impede os utilizadores de configurarem as suas credenciais de certificado na keystore gerida ( Os perfis de**configuração**do dispositivo  >  **Profiles**  >  **Criam o perfil**Android  >  **Enterprise** para a plataforma > **Proprietário do Dispositivo Apenas > Restrições** de Dispositivo para o tipo de perfil > **Utilizadores + Contas).**

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="protected-wipe-action-now-available--51150000---"></a>Ação de limpeza protegida já disponível<!--51150000 -->
Tem agora a opção de utilizar a ação do dispositivo Wipe para efetuar uma limpeza protegida de um dispositivo. As toalhetes protegidas são as mesmas que as toalhetes padrão, exceto que não podem ser contornadas ao desligar o dispositivo. Uma limpeza protegida continuará a tentar redefinir o dispositivo até ser bem sucedido. Em algumas configurações, esta ação pode deixar o dispositivo incapaz de reiniciar. Para mais informações, consulte [Retire ou limpe os dispositivos](../remote-actions/devices-wipe.md).

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>Endereço MAC do dispositivo adicionado à página de visão geral do dispositivo<!--5562275 -->
Pode agora ver o endereço Ethernet MAC de um dispositivo na página de detalhes do dispositivo (**Dispositivos**  >  **Todos os dispositivos** > escolher um dispositivo > **visão geral**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Segurança do dispositivo

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>Melhoria da experiência num dispositivo partilhado quando as políticas de acesso condicional baseadas em dispositivos são ativadas<!-- 1734096  -->
Melhorámos a experiência num dispositivo partilhado com vários utilizadores que são direcionados para a política de acesso condicional baseada no dispositivo, verificando a mais recente avaliação de conformidade para o utilizador ao aplicar a política. Para mais informações, consulte os seguintes artigos de visão geral:
- [Visão geral do Azure para acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Visão geral de conformidade do dispositivo intonizado](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>Utilize perfis de certificadoS PKCS para dispositivos de fornecimento com certificados<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
Agora pode utilizar perfis de certificadoS PKCS para emitir certificados para *dispositivos* que executam Android para Trabalho, iOS/iPadOS e Windows, quando associados a perfis como os de Wi-Fi e VPN. Anteriormente, estas três plataformas suportavam apenas certificados baseados no utilizador, com o suporte baseado no dispositivo a limitar-se ao macOS.

> [!NOTE]
> Os perfis de certificadoS PKCS não são suportados com perfis Wi-Fi. Em vez disso, utilize perfis de certificado SCEP quando utilizar um [tipo EAP](../configuration/wi-fi-settings-windows.md#enterprise-profile).

Para utilizar um certificado baseado no dispositivo, ao mesmo tempo que cria um perfil de [certificado PKCS](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) para as plataformas suportadas, selecione **Definições**. Verá agora a definição para o **tipo de Certificado,** que suporta as opções para Dispositivo, ou Utilizador.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorizar e resolver problemas

#### <a name="centralized-audit-logs--5603185-5697164---"></a>Registos de auditoria centralizados<!--5603185, 5697164 -->
Uma nova experiência centralizada de registo de auditoria agora recolhe registos de auditoria para todas as categorias numa página. Pode filtrar os registos para obter os dados que procura. Para ver os registos de auditoria, aceda aos registos de auditoria da **administração do Arrendatário.**  >  **Audit logs** 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>Informações de etiquetas de âmbito incluídas nos detalhes da atividade do registo de auditoria<!--5763534 -->
Os detalhes da atividade do registo de auditoria agora incluem informações de etiquetas de âmbito (para objetos Intune que suportam etiquetas de âmbito). Para obter mais informações sobre registos de auditoria, consulte Utilize registos de [auditoria para acompanhar e monitorizar os eventos](monitor-audit-logs.md).

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>Semana de 2 de dezembro de 2019

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>Novo licenciamento de cogestão do Microsoft Endpoint Configuration Manager<!--5027281-->
Os clientes do Gestor de Configuração com Garantia de Software podem obter a cogestão intune para pCs windows 10 sem ter que comprar uma licença intune adicional para cogestão. Os clientes já não precisam de atribuir licenças individuais Intune/EMS aos seus utilizadores finais para cogestão do Windows 10.
- Os dispositivos geridos pelo Gestor de Configuração e matriculados na cogestão têm quase os mesmos direitos que os Computadores Geridos por MDM autónomos intune. No entanto, após a reposição, não podem ser reprovisionados usando o Autopilot.
- Os dispositivos Windows 10 matriculados no Intune utilizando outros meios requerem licenças Intune completas.
- Os dispositivos de outras plataformas ainda requerem licenças Intune completas.

Para mais informações, consulte [os termos de licenciamento.](https://www.microsoft.com/en-us/Licensing/product-licensing/products)

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>Semana de 18 de novembro de 2019 (lançamento do Serviço de 1911)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>Atualização da UI ao limpar seletivamente os dados da aplicação<!-- 4102028 -->
A UI para limpar seletivamente os dados das aplicações em Intune foi atualizada. As alterações ui incluem:
- Uma experiência simplificada utilizando um formato de estilo de feiticeiro condensado dentro de um painel.
- Uma atualização para o fluxo de criação para incluir atribuições.
- Uma página resumida de todas as coisas definidas ao visualizar propriedades, antes de criar uma nova política ou ao editar uma propriedade. Além disso, ao editar propriedades, o resumo apenas mostrará uma lista de itens da categoria de propriedades que estão a ser editadas.

Para obter mais informações, veja [Como eliminar apenas dados empresariais de aplicações geridas pelo Intune](../apps/apps-selective-wipe.md).

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>suporte para teclado iOS e iPadOS<!-- 4922950 -->
Em março de 2019, anunciou a remoção do apoio à política de proteção de aplicações iOS que definia "teclados de terceiros". A funcionalidade está a regressar a Intune com suporte para iOS e iPadOS. Para ativar esta definição, visite o separador de **proteção de dados** de uma nova ou existente política de proteção de aplicações iOS/iPadOS e encontre a definição de **teclados de terceiros** no âmbito **da Transferência de Dados**.

O comportamento desta definição de política difere ligeiramente da implementação anterior. Em aplicações multi-identidades utilizando a versão SDK 12.0.16 e posteriormente, direcionadas por políticas de proteção de aplicações com esta configuração configurada para **o Block,** os utilizadores finais não poderão optar por teclados de terceiros tanto na sua organização como nas suas contas pessoais. As aplicações que utilizam as versões SDK 12.0.12 e anteriormente continuarão a exibir o comportamento documentado no nosso título de post de blog, [edição conhecida: Os teclados de terceiros não estão bloqueados no iOS para contas pessoais.](https://aka.ms/3rdparty_iOS_Intune)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuração do dispositivo

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>Grupos de utilizadores macOS alvo para exigir gestão do Jamf<!-- 4061739  --> 
Pode direcionar grupos específicos de utilizadores que obterão os seus [dispositivos macOS geridos pelo Jamf](../protect/conditional-access-integrate-jamf.md). Este alvo permite-lhe aplicar a integração de conformidade do Jamf a um subconjunto de dispositivos macOS enquanto outros dispositivos são geridos pela Intune. Se já estiver a utilizar a integração do Jamf, todos os Utilizadores serão direcionados para a integração por padrão.

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>Novas definições do Exchange ActiveSync ao criar um perfil de configuração de dispositivo de email em dispositivos iOS<!-- 4892824   --> 
Nos dispositivos iOS/iPadOS, pode configurar a conectividade de e-mail num perfil de configuração do dispositivo (Perfis de**configuração**do dispositivo Criar perfis de  >  **Profiles**  >  **perfil**  >  **iOS/iPadOS** para plataforma > **Email** para o tipo de perfil). 

Existem novas definições exchange ActiveSync disponíveis, incluindo:
- **Troque dados para sincronizar:** Escolha os serviços de Troca para sincronizar (ou bloquear a sincronização) para Calendário, Contactos, Lembretes, Notas e E-mail.
- **Permitir que os utilizadores alterem as definições**de sincronização : Permitir (ou bloquear) os utilizadores alteraras as definições de sincronização destes serviços nos seus dispositivos.  

Para mais informações sobre estas definições, vá às definições de perfil de [e-mail para dispositivos iOS em Intune](../configuration/email-settings-ios.md). 

Aplica-se a:

- iOS 13.0 e mais recente
- iPadOS 13.0 e mais recente

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>Impedir que os utilizadores adicionem contas pessoais do Google ao Android Enterprise totalmente geridos e dedicados dispositivos<!-- 5353228   -->
No Android Enterprise totalmente gerido e dedicado dispositivos, existe uma nova configuração que impede os utilizadores de criarem contas pessoais da Google ( Os perfis de**configuração**do dispositivo  >  **Profiles**  >  **Criam o perfil**Android  >  **Enterprise** para a plataforma > **Dispositivo Proprietário apenas > Restrições** de dispositivos para o tipo de perfil > As **definições**  >  **pessoais do Google Accounts).**

Para ver as definições que pode configurar, vá às definições do [dispositivo Android Enterprise para permitir ou restringir funcionalidades usando Intune](../configuration/device-restrictions-android-for-work.md).

Aplica-se a:

- Dispositivos geridos pela Android Enterprise
- Dispositivos dedicados android Enterprise

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>A definição de sessão de registo do lado do servidor para comandos Siri é removida no perfil de restrições de dispositivos iOS/iPadOS <!-- 5468501   -->
Nos dispositivos iOS e iPadOS, o registo do lado do Servidor para a definição de **comandos Siri** é removido da consola de administração do Microsoft Endpoint Manager ( Perfis de**configuração**do dispositivo  >  **Profiles**  >  **Criar perfis**  >  **de perfil iOS/iPadOS** para **restrições** de dispositivo seleto de plataforma > dispositivo para o tipo de perfil > **aplicações incorporadas).** 

Esta definição não tem qualquer efeito nos dispositivos. Para remover a definição dos perfis existentes, abra o perfil, faça qualquer alteração e, em seguida, guarde o perfil. O perfil é atualizado e a definição é eliminada dos dispositivos.

Para ver todas as definições que pode configurar, consulte as definições do [dispositivo iOS e iPadOS para permitir ou restringir as funcionalidades utilizando o Intune](../configuration/device-restrictions-ios.md).

Aplica-se a:

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Atualizações de funcionalidades do Windows 10 (pré-visualização pública)<!-- 2384877 -->
Já é possível implementar atualizações de [funcionalidades do Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) para dispositivos Windows 10. As atualizações de funcionalidades do Windows 10 são uma nova política de atualização de software que define a versão do Windows 10 que pretende que os dispositivos instalem e permaneçam. Pode utilizar este novo tipo de política juntamente com os anéis de atualização do Windows 10 existentes.

Os dispositivos que receberem a política de atualizações de funcionalidades do Windows 10 instalarão a versão especificada do Windows e permanecerão nessa versão até que a política seja editada ou removida. Os dispositivos que executam uma versão posterior do Windows permanecem na sua versão atual. Os dispositivos que se encontram numa versão específica do Windows ainda podem instalar atualizações de qualidade e segurança para essa versão a partir de anéis de atualização do Windows 10.

Este novo tipo de política começa a ser lançado aos inquilinos esta semana. Se esta apólice ainda não estiver disponível para o seu inquilino, será em breve.

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>Adicionar e alterar informações chave em ficheiros de listas para aplicações macOS<!-- 4736278 -->
Nos dispositivos macOS, pode agora criar um perfil de configuração do dispositivo que faça upload de um ficheiro de lista de propriedades (.plist) associado a uma aplicação ou com o dispositivo (**Perfis**de Configuração de  >  **Dispositivos**Criar o  >  **Create profile**  >  **macOS** de perfil para a plataforma > **Ficheiro Preferencial** para o tipo de perfil).

Apenas algumas aplicações suportam preferências geridas, e estas aplicações podem não permitir que você gere todas as configurações. Certifique-se de que faz o upload de um ficheiro de lista de propriedades que configura as definições do canal do dispositivo e não as definições do canal do utilizador.

Para obter mais informações sobre esta funcionalidade, consulte Adicionar um ficheiro de lista de [propriedades aos dispositivos macOS utilizando o Microsoft Intune](../configuration/preference-file-settings-macos.md).

Aplica-se a:

- dispositivos macOS com 10,7 e mais recentes

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestão de dispositivos

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>Editar valor de nome do dispositivo para dispositivos Autopilot<!-- 2640074 -->
Pode editar o valor de nome do dispositivo para dispositivos de piloto automático ad ad..  Para mais informações, consulte [atributos](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes)do dispositivo Edit Autopilot .

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>Editar valor de etiqueta de grupo para dispositivos autopiloto<!-- 4816775   -->
Pode editar o valor de Etiqueta de Grupo para dispositivos Autopilot. Para mais informações, consulte [atributos](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes)do dispositivo Edit Autopilot .

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorizar e resolver problemas

#### <a name="updated-support-experience---5012398---"></a>Experiência de suporte atualizada<!-- 5012398 -->

A partir de hoje, uma experiência atualizada e simplificada na consola para [obter ajuda e suporte para Intune](get-support.md) está a ser lançada para os inquilinos. Se esta nova experiência ainda não estiver disponível para si, será em breve.

Melhorámos a pesquisa e feedback nas consolas para questões comuns e o fluxo de trabalho que utiliza para contactar o suporte. Ao abrir um problema de suporte, você verá estimativas em tempo real para quando você pode esperar uma resposta de callback ou e-mail, e os clientes de suporte Premier e Unificado podem facilmente especificar uma gravidade para o seu problema, para ajudar a obter suporte mais rápido.

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>Experiência melhorada de reporte intune (pré-visualização pública) <!-- 3791418 -->
Intune agora fornece uma experiência de reporte melhorada, incluindo novos tipos de relatórios, melhor organização de relatórios, opiniões mais focadas, melhor funcionalidade de relatório, bem como dados mais consistentes e oportunos. Os novos tipos de relatórios centram-se nos seguintes exemplos:

- **Operacional** - Fornece novos registos com foco negativo para a saúde. 
- **Organizacional** - Fornece um resumo mais amplo do estado geral.
- **Histórico** - Fornece padrões e tendências ao longo de um período de tempo.
- **Especialista** - Permite-lhe utilizar dados brutos para criar os seus próprios relatórios personalizados.

O primeiro conjunto de novos relatórios centra-se na conformidade do dispositivo. Para mais informações, consulte blog [- Microsoft Intune reporting framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) and [Intune reports](reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Controlo de acesso baseado em funções

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>Duplicar papéis personalizados ou incorporados <!-- 1081938   -->
Agora pode copiar papéis embutidos e personalizados. Para mais informações, consulte [Copiar um papel](../fundamentals/create-custom-role.md#copy-a-role).

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>Novas permissões para o papel de administrador da escola <!-- 5621805  -->  
Duas novas permissões, **perfil de atribuição** e dispositivo **Sync,** foram adicionadas ao papel de administrador da escola > programas de inscrição de **permissões.**  >  **Enrollment programs** A permissão de perfil de sincronização permite que os administradores do grupo sincronizem os dispositivos Do Piloto Automático do Windows. A permissão de perfil de atribuição permite-lhes eliminar perfis de inscrição da Apple iniciados pelo utilizador. Também lhes dá permissão para gerir as atribuições de dispositivos Autopilot e atribuições de perfil de implementação do Autopilot. Para obter uma lista de todas as permissões de administrador/administração do grupo escolar, consulte os administradores do [grupo Deatribuição](https://docs.microsoft.com/intune-education/group-admin-delegate).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Segurança

#### <a name="bitlocker-key-rotation---2564951----"></a>Rotação da chave BitLocker<!-- 2564951  -->
Pode utilizar uma ação do dispositivo Intune para rodar remotamente as teclas de [recuperação bitLocker](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) para dispositivos geridos que executam a versão 1909 do Windows ou mais tarde. Para se qualificar para ter as teclas de recuperação rodadas, os dispositivos devem ser configurados para suportar a rotação da chave de recuperação.  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>Atualizações para inscrição dedicada de dispositivos para apoiar a implementação de certificados de dispositivo SCEP <!-- 5198878  -->
A Intune agora suporta a implementação de certificados de dispositivoS SCEP para dispositivos android enterprise dedicados para acesso baseado em certificados aos perfis Wi-Fi. A aplicação Microsoft Intune deve estar presente no dispositivo para ser implantada. Como resultado, atualizámos a experiência de inscrição para dispositivos dedicados ao Android Enterprise. As novas matrículas ainda começam as mesmas (com QR, NFC, Zero-touch ou identificador de dispositivos) mas agora têm um passo que exige que os utilizadores instalem a aplicação Intune. Os dispositivos existentes começarão a instalar a aplicação automaticamente numa base de rolamento.

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>Registos de auditoria intune para colaboração entre negócios<!--5670211 -->
A colaboração business-to-business (B2B) permite-lhe partilhar de forma segura as aplicações e serviços da sua empresa com utilizadores convidados de qualquer outra organização, mantendo ao mesmo tempo o controlo sobre os seus próprios dados corporativos. Intune agora suporta registos de auditoria para utilizadores convidados B2B. Por exemplo, quando os utilizadores de hóspedes fizerem alterações, o Intune será capaz de capturar estes dados através de registos de auditoria. Para mais informações, consulte [O que é o acesso dos utilizadores convidados no Azure Ative Directory B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>Semana de 11 de novembro de 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestão de aplicações  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>Melhor experiência de inscrição no MacOS no Portal da Empresa <!-- 5074349  -->  
O Portal da Empresa para a experiência de inscrição no MacOS tem um processo de inscrição mais simples que se alinha mais de perto com o Portal da Empresa para a experiência de inscrição do iOS. Os utilizadores do dispositivo agora vêem:  

- Uma interface de utilizador elegante.  
- Uma lista de verificação de inscrições melhorada.  
- Instruções mais claras sobre como matricular os seus dispositivos.  
- Melhores opções de resolução de problemas.  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>Aplicações web lançadas a partir da aplicação Portal da Empresa Windows<!-- 5030972 -->
Os utilizadores finais podem agora lançar aplicações web diretamente a partir da aplicação Portal da Empresa do Windows. Os utilizadores finais podem selecionar a aplicação web e, em seguida, escolher a opção **Open no navegador**. O URL publicado na Web é aberto diretamente num navegador web. Esta funcionalidade será lançada ao longo da próxima semana. Para obter mais informações sobre aplicações Web, consulte [Adicionar aplicações web ao Microsoft Intune](../apps/web-app.md).  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Nova coluna de tipo de atribuição no Portal da Empresa para o Windows 10 <!-- 5459950  -->
A coluna de atribuição de **apps instalada**seleções > Portal da Empresa foi  >  **Assignment type** renomeada **para Requerida pela sua organização.**  Sob essa coluna, os utilizadores verão um valor **Sim** ou **Não** para indicar que uma aplicação é necessária ou tornada opcional pela sua organização. Estas alterações foram feitas porque os utilizadores de dispositivos estavam confusos sobre o conceito de aplicações disponíveis. Os seus utilizadores podem encontrar mais informações sobre a instalação de apps do Portal da Empresa na [Instalação e partilhar aplicações no seu dispositivo.](../user-help/install-apps-cpapp-windows.md) Para obter mais informações sobre a configuração da aplicação Portal da Empresa para os seus utilizadores, consulte [como configurar a aplicação Microsoft Intune Company Portal](../apps/company-portal-app.md).  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>Semana de 4 de novembro de 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Segurança do dispositivo

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>As linhas de base de segurança são suportadas no Governo do Microsoft Azure<!-- 4062552 -->

Os casos de Intune que estão hospedados no *Microsoft Azure Government* podem agora usar linhas de base de [segurança](../protect/security-baselines.md) para o ajudar a proteger e proteger os seus utilizadores e dispositivos.

## <a name="whats-new-archive"></a>O que é novo arquivo
Para meses anteriores, consulte o [novo arquivo What's New.](whats-new-archive.md)

## <a name="notices"></a>Avisos

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


