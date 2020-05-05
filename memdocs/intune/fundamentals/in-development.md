---
title: Em desenvolvimento - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune apresenta-se em desenvolvimento
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0151bfd993c3ad5cc48194da368d3385d8bc32ec
ms.sourcegitcommit: 8a8378b685a674083bfb9fbc9c0662fb0c7dda97
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82619564"
---
# <a name="in-development-for-microsoft-intune"></a>Em desenvolvimento para microsoft Intune

Para ajudar na sua prontidão e planeamento, esta página lista atualizações e funcionalidades intune UI que estão em desenvolvimento mas ainda não foram lançadas. Além das informações nesta página: 

- Se anteciparmos que terá de agir antes de uma mudança, publicaremos um post complementar no Centro de Mensagens do Office.
- Quando uma funcionalidade entra em produção, seja uma pré-visualização ou geralmente disponível, a descrição da funcionalidade passará desta página para [o que é novo](whats-new.md).
- Esta página e a nova página [do What's](whats-new.md) são atualizadas periodicamente. Volte a consultar posteriormente para obter mais atualizações.
- Consulte o roteiro da [Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) para entregas estratégicas e prazos.

> [!NOTE]
> Esta página reflete as nossas expectativas atuais sobre as capacidades intune num próximo lançamento. As datas e as características individuais podem mudar. Esta página não descreve todas as funcionalidades em desenvolvimento.

**Alimentação RSS**: Descubra quando esta página é atualizada copiando e colando o seguinte URL no seu leitor de feed:`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

Este artigo foi atualizado pela última vez na data listada no título acima.

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Gestão de aplicações

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Suporte para várias contas no Portal da Empresa para Mac<!-- 5779449  -->
O Portal da Empresa sobre dispositivos macOS agora caches contas de utilizador, facilitando o início do sessão. Os utilizadores já não precisam de assinar no Portal da Empresa sempre que lançam a aplicação. Além disso, o Portal da Empresa apresentará um picker de conta se várias contas de utilizador estiverem em cache, para que os utilizadores não tenham de introduzir o seu nome de utilizador. 

### <a name="auto-update-vpp-available-apps---3640511----"></a>Atualização automática VPP disponíveis aplicações<!-- 3640511  -->
As aplicações que forem publicadas como Programa de Compra de Volume (VPP) serão automaticamente atualizadas quando as **Atualizações automáticas** de aplicações estiverem ativadas para o token VPP. Atualmente, as aplicações disponíveis vPP não atualizam automaticamente. Em vez disso, os utilizadores finais devem ir ao Portal da Empresa e reinstalar a aplicação se uma versão mais recente estiver disponível. No entanto, as aplicações necessárias suportam atualmente atualizações automáticas.

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>Personalize as ações de dispositivos self-service no Portal da Empresa<!--4393379  -->
Poderá personalizar as ações de dispositivos self-service disponíveis que são mostradas aos utilizadores finais na aplicação e website do Portal da Empresa. Para ajudar a prevenir ações não intencionais do dispositivo, poderá configurar estas definições para a aplicação Portal da Empresa, selecionando**funcionalidades**de**Personalização** > de **Administração** > de Inquilinos**Create** > Hide . Estão disponíveis as seguintes ações:
- Ocultar o botão **Remover** no dispositivo corporativo Windows.
- Ocultar o botão **Reset** em dispositivos windows corporativos.
- Ocultar o botão **Reset** em dispositivos corporativos iOS.
- Ocultar O botão **Remover** em dispositivos iOS corporativos.

Para mais informações, consulte [as ações do dispositivo self-service user a partir do Portal da Empresa](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Entrega unificada de aplicações azure AD Enterprise ou Office Online no Portal da Empresa<!--4404429 -->
Poderá alternar (**Ocultar** ou **Mostrar)** a exposição de aplicações Azure AD Enterprise ou Office Online no Portal da Empresa. Cada utilizador verá todo o seu catálogo de aplicações a partir do serviço da Microsoft escolhido. Por predefinição, cada fonte adicional de aplicação será definida para **Ocultar**. Esta funcionalidade entrará primeiro em vigor no site do Portal da Empresa no lançamento de 2005 com suporte no Windows, iOS/iPadOS e macOS Company Portals que se espera que se sigam. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione a**personalização** da **administração** > do Inquilino para encontrar esta definição futura. Para obter informações relacionadas, consulte [como personalizar as aplicações intune Company Portal, website do Portal da Empresa e aplicação Intune](../apps/company-portal-app.md).

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>Pesquise os docs Intune do Portal da Empresa<!-- 1736480 -->
Agora pode pesquisar a documentação Intune diretamente do Portal da Empresa para aplicação macOS. Na barra de menus, selecione **Help** > **Search** e introduza as palavras-chave da sua pesquisa para encontrar rapidamente respostas às suas perguntas.

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Portal da empresa para Android vai orientar utilizadores a obter aplicações após inscrição no perfil de trabalho <!-- 6103999  -->
Estamos a melhorar a orientação in-app no Portal da Empresa para facilitar aos utilizadores a descoberta e instalação de apps.  Depois de se inscreverem na gestão de perfis de trabalho, os utilizadores verão uma mensagem a dizer-lhes que podem encontrar aplicações sugeridas na versão com insígnias do Google Play. Os utilizadores também verão uma nova ligação de **apps Get** na gaveta do Portal da Empresa à esquerda. Para dar lugar a estas novas e melhoradas experiências, o separador **APPS** será removido. 

### <a name="android-company-portal-user-experience---5736084---"></a>Experiência de utilizador do Portal da Empresa Android<!-- 5736084 -->
No lançamento de 2005 do Portal da Empresa Android, os utilizadores finais de dispositivos Android que são emitidos um aviso, bloqueio ou limpeza por uma política de proteção de aplicações verão uma nova experiência do utilizador. Em vez da experiência atual do diálogo, os utilizadores finais verão uma mensagem de página inteira descrevendo o motivo do aviso, bloqueio ou limpeza e os passos para remediar o problema. Para mais informações, consulte a experiência de proteção de [aplicativos para dispositivos Android](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) e definições de política de proteção de [aplicações Android no Microsoft Intune](../apps/app-protection-policy-settings-android.md).


<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuração do dispositivo

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>As definições e valores do perfil de configuração do dispositivo serão atualizados para plataformas Windows<!-- 4091122 -->
Quando cria perfis de configuração de dispositivos para plataformas Windows **(Perfis** > de configuração de**dispositivos** > **Criar perfil** > qualquer opção **windows** para plataforma), algumas definições e os seus valores são diferentes do CSP, e podem ser confusos. Os nomes de definição e os seus valores serão atualizados para serem mais claros.

Aplica-se a:

- Windows 10 e perfis posteriores de configuração do dispositivo
- Windows Holographic para perfis de configuração de dispositivos empresariais
- Perfis de configuração do dispositivo Windows 8.1
- Perfis de configuração do dispositivo Windows Phone 8.1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Configure a aplicação ATP microsoft defender para macOS  <!-- 5520115  -->
Em breve poderá configurar as [definições](../protect/endpoint-protection-macos.md) da aplicação ATP do Microsoft Defender para dispositivos que executam o macOS como parte de um perfil de configuração de dispositivos de proteção endpoint (Perfis de**configuração** > de**dispositivos** > **Criar perfil,** selecionar **macOS** para a *Plataforma*e, em seguida, **proteção Endpoint** para o *tipo de Perfil).* Haverá oito configurações para a configuração do dispositivo macOS. 

O Defender ATP é suportado no macOS 10.13 (High Sierra) e posteriormente, e a aplicação [ATP Microsoft Defender](../apps/apps-advanced-threat-protection-macos.md) deve ser implementada no dispositivo *após* a aplicação destas definições. As definições devem ser enviadas para o dispositivo antes da aplicação ser implementada. As versões beta do macOS não serão suportadas.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nova definição de FileVault para a política de configuração do dispositivo de proteção de pontofinal macOS<!-- 5459801   -->
Estamos adicionando uma nova definição à categoria FileVault dentro do modelo de proteção de [ponto final macOS:](../protect/endpoint-protection-macos.md) Ocultar a chave de recuperação. (Perfis de**configuração** > de**dispositivos** > **Criar perfil,** selecionar **macOS** para a *Plataforma* e, em seguida, **proteção endpoint** para o *tipo de perfil).* Esta definição esconde a chave pessoal do utilizador final durante a encriptação FileVault 2. Um utilizador do dispositivo pode visualizar a sua chave de recuperação pessoal a qualquer momento a partir da aplicação portal da empresa iOS ou do portal da empresa para o dispositivo macOS encriptado. Para ver a chave de recuperação pessoal, podem ir aos detalhes do dispositivo e clicar na *chave de recuperação do get*.

Esta definição não estará disponível na política previamente criada. Terá de recriar as políticas do FileVault para configurar esta definição para a utilizar. 

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>Configurar extensões do sistema em dispositivos macOS<!-- 6255624  -->
Nos dispositivos macOS, pode criar um perfil de extensões de kernel para configurar as definições ao nível do kernel ( Perfis de**configuração** > de**dispositivos** > **macOS** para plataformas > **extensões kernel** para perfil). A Apple acaba por depreciar as extensões de kernel e substituí-las por extensões do sistema numa futura versão. As extensões do sistema funcionam no espaço do utilizador e não dão acesso ao núcleo. O objetivo é aumentar a segurança e fornecer mais controlo final do utilizador, limitando os ataques ao nível do núcleo. Ambas as extensões de kernel e extensões do sistema permitem que os utilizadores instalem extensões de aplicações que alargam as capacidades nativas do sistema operativo.

Em Intune, pode configurar as extensões de kernel e as extensões do sistema (perfis de**configuração** > de**dispositivos** > **macOS** para **extensões** de > de plataforma para perfil). As extensões de kernel aplicam-se a 10.13.2 e mais recentes. As extensões do sistema aplicam-se às 10.15 e mais recentes. Do macOS 10.15 ao macOS 10.15.4, as extensões de kernel e as extensões do sistema podem ser executadas lado a lado. 

Para saber mais sobre extensões de kernel em dispositivos macOS, consulte [Adicionar extensões de kernel macOS](../configuration/kernel-extensions-overview-macos.md).

Aplica-se a:
- macOS 10.15 e mais recente

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscrição de dispositivos

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Trazer os seus próprios dispositivos pode usar VPN para implementar<!--5015344 -->
Esta funcionalidade pode ser adiada.

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>Intervalo de sincronização automatizada do dispositivo até 12 horas<!--3077535 -->
Para a Inscrição automática de Dispositivos da Apple, o intervalo de sincronização automatizada entre Intune e Apple Business Manager será reduzido de 24 horas para 12 horas. Para obter mais informações sobre sincronização, consulte [os dispositivos geridos pelo Sync](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Suporte de piloto automático para dispositivos Hololens 2<!--6305220-->
O Windows Autopilot irá suportar dispositivos Hololens 2. Para obter mais informações sobre a utilização do Autopilot em Intune, consulte [Os dispositivos DoWindows em Insintonia utilizando o Windows Autopilot](../enrollment/enrollment-autopilot.md).

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>Restrições de inscrição vão apoiar etiquetas de âmbito<!--4209550 -->
Poderá atribuir etiquetas de âmbito às restrições de inscrição. Para isso, vá ao [microsoft Endpoint Manager administrador centro](https://go.microsoft.com/fwlink/?linkid=2109431) > de administração**Dispositivos** > **Restrições** > de inscrição**Criar restrições**de restrição . Crie qualquer tipo de restrição e verá a página scope **tags.**

### <a name="shared-ipads-for-business--6367326---"></a>IPads partilhados para Negócios<!--6367326 -->
Poderá utilizar intune e Apple Business Manager para configurar facilmente e de forma segura o iPad partilhado para que vários colaboradores possam partilhar dispositivos. O [iPad partilhado](https://developer.apple.com/education/shared-ipad/) da Apple proporciona uma experiência personalizada para vários utilizadores, preservando os dados dos utilizadores. Utilizando um ID apple gerido, os utilizadores podem aceder às suas aplicações, dados e configurações depois de assinarem qualquer iPad partilhado na sua organização. O iPad partilhado funciona com identidades federadas.

Para ver esta funcionalidade, vá ao centro > de [administração do Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)**Dispositivos** > **iOS iOS** > **matricula** do programa de**inscrição** > > escolher um token** > **Perfis** > **Criar perfil** > **iOS**. Na página **'Definições** de Gestão', selecione **Inscrever-se sem afinidade** do utilizador e verá a opção **de iPad partilhado.**

**Aplica-se a:** iPadOS 13.4 e posteriormente. Este lançamento adicionou suporte para sessões temporárias com iPad partilhado para que os utilizadores possam aceder a um dispositivo sem um ID da Apple gerido. No início do início, o dispositivo apaga todos os dados do utilizador de modo a que o dispositivo esteja imediatamente pronto para ser utilizado, eliminando a necessidade de uma limpeza do dispositivo. 

<!-- ***********************************************-->
## <a name="device-management"></a>Gestão de dispositivos

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Suporte de scripts PowerShell para dispositivos BYOD<!-- 1862833  -->
Os scripts PowerShell suportarão dispositivos registados em Intune. Para obter mais informações sobre o PowerShell, consulte [scripts PowerShell em dispositivos Windows 10 em Intune](../apps/intune-management-extension.md). Esta funcionalidade não suporta dispositivos que executam a edição home do Windows 10.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>O Log Analytics incluirá o registo de detalhes do dispositivo<!--6014987  -->
Os registos de detalhes do dispositivo insintonizem os registos disponíveis na análise de **registode** > **relatórios**. Pode correlacionar detalhes do dispositivo para construir consultas personalizadas e livros de trabalho azure.

### <a name="new-details-for-the-autopilot-report--5405786---"></a>Novos detalhes para o relatório autopiloto<!--5405786 -->
Para ver os novos detalhes sobre o estado de instalação de App e Policy, vá ao [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), escolha implementações de Monitor**Monitor** > de **Dispositivos** > **Autopilot**.

### <a name="macos-script-support---6376978----"></a>suporte para script saos<!-- 6376978  -->
O suporte para o script para macOS está agora geralmente disponível. Além disso, vamos adicionar suporte tanto para scripts atribuídos ao utilizador como para dispositivos macOS que foram matriculados com a Inscrição automática de dispositivos da Apple (anteriormente Programa de Inscrição de Dispositivos). Para mais informações, consulte [Utilize scripts de concha em dispositivos macOS em Intune](../apps/macos-shell-scripts.md).

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorizar e resolver problemas

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Modelo de relatório de conformidade do POWER BI V2.0<!-- 636958  -->
Os administradores poderão atualizar a versão do modelo de relatório de conformidade do Power BI de V1.0 a V2.0. O V2.0 incluirá um design melhorado, bem como alterações nos cálculos e dados que estão a ser surgidos como parte do modelo. Para obter informações relacionadas, consulte [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Segurança

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Suporte de credenciais derivadas para DISA Purebred em dispositivos Android<!--4839592 -->
Você poderá usar *DISA Purebred* como um fornecedor [de credenciais derivado](../protect/derived-credentials.md) em dispositivos Android Enterprise totalmente geridos (**Conectores** > de**administração** > de inquilinos e**credenciais derivadas**de fichas). O apoio será incluído na recuperação de uma credencial derivada para dISA Purebred. Poderá utilizar uma credencial derivada para autenticação de apps, Wi-Fi, VPN ou s/MIME assinando e/ou encriptação com aplicações que a suportam. 

Em abril, intune acrescentou o apoio à *Entrust Datacard* e *intercede* como fornecedores de credenciais derivadas. 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Definições de preferências de privacidade para dispositivos macOS<!-- 2934232 --> 
Com o lançamento do macOS Catalina 10.15, a Apple adicionou novos melhoramentos de segurança e privacidade. Por defeito, as aplicações e processos não conseguem aceder a dados específicos sem o consentimento do utilizador. Se os utilizadores não fornecerem o consentimento, as aplicações e processos podem não funcionar. A Intune está a adicionar suporte para configurações que permitem aos administradores de TI permitir ou proibir o consentimento de acesso de dados em nome dos utilizadores finais em dispositivos que executam o macOS 10.14 ou posteriormente. Estas definições garantirão que as aplicações e processos continuem a funcionar corretamente e reduzem o número de indicações que os utilizadores finais experimentam.


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplique as suas políticas em Endpoint Security<!-- 5892558   -->
Poderá selecionar uma política que criou no nó de segurança Endpoint do centro de administração do Microsoft Endpoint Manager e, em seguida, duplicar para criar uma cópia.  As políticas que poderá duplicar incluem as que cria para: 

- Antivírus
- Encriptação de disco
- Firewall
- Deteção e resposta de pontofinal
- Redução da superfície de ataque
- Proteção de Conta

A duplicação fará uma cópia da política original, que poderá depois mudar o nome e editar. A cópia não incluirá atribuições do original.

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Enviar notificações push como uma ação para o incumprimento <!-- 1733150   -->
Para as plataformas iOS e Android, estamos a adicionar uma nova ação para o incumprimento que enviará uma notificação push de aplicação através da aplicação Portal da Empresa. Os utilizadores podem clicar nas notificações que irão lançar a aplicação Portal da Empresa que depois exibe a razão pela qual não são compatíveis. Os administradores poderão configurar esta nova ação por incumprimento no centro de administração do Microsoft Endpoint Manager, indo para as**políticas** > de conformidade de **dispositivos** > **Criar a política,** e, em seguida, selecionar a *Ação* para enviar uma notificação push app. 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Novo perfil para a política de firewall de segurança endpoint<!-- 5653324   -->
Como pré-visualização, estamos adicionando um perfil adicional para o Windows 10 e mais tarde para a política de Firewall na segurança Endpoint de Intune ( Política de criação de > **firewall** > de**segurança endpoint****>** selecione Windows **10 e mais tarde).** 

Cada instância deste novo perfil suporta até 150 regras personalizadas do *Microsoft Defender Firewall*. O perfil de regras do Microsoft Defender Firewall permite definir regras granulares do Windows Firewall para permitir ou bloquear portas e aplicações no Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Avisos

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Consulte também

Para mais detalhes sobre os recentes desenvolvimentos, consulte [o que há de novo no Microsoft Intune](whats-new.md).



