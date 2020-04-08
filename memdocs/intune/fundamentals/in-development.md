---
title: Em desenvolvimento - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune apresenta-se em desenvolvimento
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f53096f25b4bb05b80d11246ac2fa01486f6e42
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808177"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>Em desenvolvimento para microsoft Intune - abril 2020

Para ajudar na sua prontidão e planeamento, esta página lista atualizações e funcionalidades intune UI que estão em desenvolvimento mas ainda não foram lançadas. Além das informações nesta página: 

- Se anteciparmos que terá de agir antes de uma mudança, publicaremos um post complementar no Centro de Mensagens do Office.
- Quando uma funcionalidade entra em produção, seja uma pré-visualização ou geralmente disponível, a descrição da funcionalidade passará desta página para [o que é novo](whats-new.md).
- Esta página e a nova página [do What's](whats-new.md) são atualizadas periodicamente. Volte a consultar posteriormente para obter mais atualizações.
- Consulte o roteiro da [Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) para entregas estratégicas e prazos.

> [!NOTE]
> Esta página reflete as nossas expectativas atuais sobre as capacidades intune num lançamento futuro. As datas e as características individuais podem mudar. Esta página não descreve todas as funcionalidades em desenvolvimento.

**Feed RSS**: Descubra quando esta página é atualizada copiando e colando o seguinte URL no leitor de feed: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

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

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Atualização para políticas de configuração de aplicativos Android<!-- 6113334  -->
As políticas de configuração de aplicações Android serão atualizadas para permitir aos administradores selecionaro tipo de inscrição do dispositivo antes de criar um perfil de config de aplicação. A funcionalidade está a ser adicionada para ter em conta os perfis de certificado que se baseiam no tipo de inscrição (Perfil de trabalho ou Proprietário do Dispositivo).  Após a libertação, ocorrerá o seguinte:

- As políticas existentes criadas antes do lançamento desta funcionalidade que não possuam quaisquer perfis de certificado associados à política serão indefinidas no Perfil de Trabalho e perfil do proprietário do dispositivo para o tipo de inscrição do dispositivo.
- As políticas existentes criadas antes do lançamento desta funcionalidade que tenham perfis de certificados associados apenas serão padrão para o Perfil de Trabalho.
- Se for criado um novo perfil e se selecionar o Perfil de Trabalho e o Perfil do Proprietário do Dispositivo para o tipo de inscrição do dispositivo, não poderá associar um perfil de certificado à política de config da aplicação.
- Se for criado um novo perfil e se selecionar apenas o Perfil de Trabalho, as políticas de certificados de perfil de trabalho criadas no âmbito da Configuração do Dispositivo podem ser utilizadas.
- Se for criado um novo perfil e o Proprietário do Dispositivo apenas for selecionado, as políticas de certificados do Proprietário do Dispositivo criadas no âmbito da Configuração do Dispositivo podem ser utilizadas.

As políticas existentes não remediarão nem emitirão novos certificados.

Além disso, estamos adicionando perfis de configuração de gmail e nove e-mails que funcionarão tanto para os tipos de inscrição do Perfil de Trabalho como para os tipos de inscrição do Proprietário do Dispositivo, incluindo a utilização de perfis de certificado em ambos os tipos de configuração de e-mail.  Quaisquer políticas do Gmail ou Nove que tenha criado no âmbito da Configuração do Dispositivo para Perfis de Trabalho continuarão a aplicar-se ao dispositivo e não é necessário movê-las para as políticas de configuração de apps.

No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)pode encontrar políticas de configuração de aplicações selecionando **apps** > polícias de **configuração**de Apps . Para obter mais informações sobre as políticas de configuração de apps, consulte as políticas de configuração da [App para o Microsoft Intune](../apps/app-configuration-policies-overview.md).

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams está agora incluído na Suite Office 365 para macOS<!-- 5903936  -->
Os utilizadores que lhe forem atribuídos microsoft Office para macOS no Microsoft Endpoint Manager passarão a receber Microsoft Teams para além das aplicações existentes do Microsoft Office (Word, Excel, PowerPoint, Outlook e OneNote). A Intune reconhecerá os dispositivos Mac existentes que têm os outros Dispositivos Do Office para aplicações macOS instaladas, e tentará instalar as Microsoft Teams da próxima vez que o dispositivo verificar com o Intune. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)pode encontrar a **Suite Office 365** para macOS selecionando **Apps** > **macOS** > **Add**. Para mais informações, consulte [o SignOffice 365 para dispositivos macOS com](../apps/apps-add-office365-macos.md)o Microsoft Intune .

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>Suporte de grupo para painel de personalização <!-- 4722837  -->
Poderá direcionar as definições no painel de personalização para grupos de utilizadores. A partir do portal Intune, selecione **aplicações do Cliente** > **Personalização.** Para mais informações, consulte [Como personalizar as aplicações intune Company Portal, website do Portal da Empresa e aplicação Intune](empresa-portal-app.md].

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuração do dispositivo

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Perfis de configuração de dispositivos de rede com fios para dispositivos macOS<!-- 3508686  -->
Um novo perfil de configuração do dispositivo macOS estará disponível que configura redes com fios (**configuração** do dispositivo > **Perfis** > **Criar perfil** > **macOS** para plataforma > **Rede Com fios** para tipo de perfil). Utilize esta funcionalidade para criar perfis 802.1x para gerir redes com fios e implementar estas redes com fios para os seus dispositivos macOS.

Aplica-se a:
- macOS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>As definições e valores do perfil de configuração do dispositivo serão atualizados para plataformas Windows<!-- 4091122 -->
Quando cria perfis de configuração de dispositivos para plataformas Windows **(Dispositivos** > Perfis de **Configuração** > **Criar perfil** > qualquer opção **do Windows** para plataforma), algumas definições e os seus valores são diferentes do CSP, e podem ser confusos. Os nomes de definição e os seus valores serão atualizados para serem mais claros.

Aplica-se a:

- Windows 10 e perfis posteriores de configuração do dispositivo
- Windows Holographic para perfis de configuração de dispositivos empresariais
- Perfis de configuração do dispositivo Windows 8.1
- Perfis de configuração do dispositivo Windows Phone 8.1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Configure a aplicação ATP microsoft defender para macOS  <!-- 5520115  -->
Em breve poderá configurar as [definições](../protect/endpoint-protection-macos.md) da aplicação ATP do Microsoft Defender para dispositivos que executam o macOS como parte de um perfil de configuração de dispositivos de proteção endpoint **(Dispositivos** > perfis de **configuração** > **Criar perfil,** selecionar **o macOS** para a *Plataforma*e, em seguida, **proteção Endpoint** para o *tipo de Perfil).* Haverá oito configurações para a configuração do dispositivo macOS. 

O Defender ATP é suportado no macOS 10.13 (High Sierra) e posteriormente, e a aplicação [ATP Microsoft Defender](../apps/apps-advanced-threat-protection-macos.md) deve ser implementada no dispositivo *após* a aplicação destas definições. As definições devem ser enviadas para o dispositivo antes da aplicação ser implementada. As versões beta do macOS não serão suportadas.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nova definição de FileVault para a política de configuração do dispositivo de proteção de pontofinal macOS<!-- 5459801   -->
Estamos adicionando uma nova definição à categoria FileVault dentro do modelo de proteção de [ponto final macOS:](../protect/endpoint-protection-macos.md) Ocultar a chave de recuperação. **(Dispositivos** > perfis de **configuração** > **Criar perfil,** selecione **o macOS** para a *Plataforma* e, em seguida, a **proteção endpoint** para o *tipo de perfil).* Esta definição esconde a chave pessoal do utilizador final durante a encriptação FileVault 2. Um utilizador do dispositivo pode visualizar a sua chave de recuperação pessoal a qualquer momento a partir da aplicação portal da empresa iOS ou do portal da empresa para o dispositivo macOS encriptado. Para ver a chave de recuperação pessoal, podem ir aos detalhes do dispositivo e clicar na *chave de recuperação do get*.

Esta definição não estará disponível na política previamente criada. Terá de recriar as políticas do FileVault para configurar esta definição para a utilizar. 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Enviar notificações push como uma ação para o incumprimento <!-- 1733150   -->
Para as plataformas iOS e Android, estamos a adicionar uma nova ação para o incumprimento que enviará uma notificação push de aplicação através da aplicação Portal da Empresa. Os utilizadores podem clicar nas notificações, que lançarão a aplicação Portal da Empresa que depois exibe a razão pela qual não são compatíveis. Os administradores poderão configurar esta nova ação por incumprimento no centro de administração do Microsoft Endpoint Manager, indo para **dispositivos** > **políticas** de conformidade > **Criar políticas,** e, em seguida, selecionar a *Ação* para enviar uma notificação push app.

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Teste de pré-lançamento para aplicações geridas do Google Play<!-- 2681933  -->
As organizações que estão a usar as [faixas de teste fechadas do Google Play para testes de pré-lançamento](https://support.google.com/googleplay/android-developer/answer/3131213) de aplicações poderão gerir estas faixas com o Intune. Poderá atribuir seletivamente aplicações line of business que são publicadas nas faixas de pré-produção da Google Play a grupos piloto para realizar testes. Em Intune, também poderá ver se uma aplicação tem uma pista de teste de pré-produção publicada, bem como ser capaz de atribuir essa faixa a grupos de utilizadores ou dispositivos AAD. Esta funcionalidade está disponível para todos os nossos cenários Android Enterprise atualmente suportados (perfil de trabalho, totalmente gerido e dedicado). No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)pode adicionar uma aplicação gerida pela Google Play selecionando **Apps** > **Android** > **Add.** Para mais informações, consulte [adicionar aplicações do Google Play geridas para dispositivos Android Enterprise com Intune](../apps/apps-add-android-for-work.md).

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>Gerir as definições de S/MIME para Outlook no Android<!-- 6517085   -->
Poderá utilizar as políticas de configuração da App para gerir a definição S/MIME para outlook em dispositivos que executam o Android Enterprise. Também poderá escolher se permite ou não que os utilizadores do dispositivo ativem ou desativem S/MIME nas definições do Outlook. Para utilizar a política de configuração de Aplicativos para Android, no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) vai para **apps** > políticas de **configuração** de apps > **adicionar** > **dispositivos geridos**.

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>Opções adicionais nos perfis de extensão de apps SSO e SSO em dispositivos iOS/iPadOS<!-- 6504155  -->
Nos dispositivos iOS/iPadOS, pode:

- Nos perfis SSO (**Dispositivos** > Perfis de **Configuração** > **Criar perfil** > **iOS/iPadOS** para **funcionalidades** de plataforma > Dispositivo para perfil > **single sign-on**), definiu o nome principal kerberos como o nome da conta Security Account Manager (SAM) nos perfis SSO. 
- Nos perfis de extensão da aplicação SSO (**Dispositivos** > Perfis de **Configuração** > **Criar perfis** > **iOS/iPadOS** para as **funcionalidades** do dispositivo para o perfil > extensão de **aplicação de assinatura única),** configure a extensão iOS/iPadOS Microsoft Azure AD com menos cliques utilizando um novo tipo de extensão de aplicação SSO. Pode ativar a extensão da AD Azure para dispositivos partilhados e enviar dados específicos para a extensão.

Aplica-se a:
- iOS/iPadOS 13.0+

Para obter mais informações sobre a utilização de um único sinal nos dispositivos iOS/iPadOS, consulte a visão geral da [extensão](../configuration/device-features-configure.md#single-sign-on-app-extension) da aplicação de assinatura única e a [lista de definições de inscrição única](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscrição de dispositivos

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Trazer os seus próprios dispositivos pode usar VPN para implementar<!--5015344 -->
O novo perfil autopiloto **Skip Domain Connectivity Toggle** permite-lhe implementar dispositivos Hybrid Azure AD Join sem acesso à sua rede corporativa utilizando o seu próprio cliente Win32 VPN de terceiros. Para ver o novo alternância, vá ao [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices**  > **Windows** > windows ** > ** Perfis de **implementação** > **Criar perfis** de perfil > **experiência Out-of-box (OOBE)** .

<!-- ***********************************************-->
## <a name="device-management"></a>Gestão de dispositivos

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Suporte de scripts PowerShell para dispositivos BYOD<!-- 1862833  -->
Os scripts PowerShell suportarão dispositivos registados em Intune. Para obter mais informações sobre o PowerShell, consulte [scripts PowerShell em dispositivos Windows 10 em Intune](../apps/intune-management-extension.md). Esta funcionalidade não suporta dispositivos que executam a edição home do Windows 10.

### <a name="script-support-for-macos-devices---4280361----"></a>Suporte de script para dispositivos macOS<!-- 4280361  -->
Poderá adicionar e implementar scripts para dispositivos macOS. Este suporte alarga a sua capacidade de configurar dispositivos macOS para além do que é possível utilizando capacidades nativas de MDM em dispositivos macOS.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>O Log Analytics incluirá o registo de detalhes do dispositivo<!--6014987  -->
Os registos de detalhes do dispositivo insintonizem os registos disponíveis nos **relatórios** > análise de **registo**. Pode correlacionar detalhes do dispositivo para construir consultas personalizadas e livros de trabalho azure.

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>Notificação push quando o tipo de propriedade do dispositivo é alterado<!-- 5575875  -->
Poderá configurar uma notificação push para enviar aos utilizadores do Portal do Portal do Android e iOS quando o seu tipo de propriedade do dispositivo tiver sido alterado de Personal para Corporate como cortesia de privacidade. Esta definição pode ser encontrada no Microsoft Endpoint Manager selecionando a **administração do Inquilino** > **Personalização**. Para saber mais sobre como a propriedade do dispositivo afeta os seus utilizadores finais, consulte a [propriedade do dispositivo Change](../enrollment/corporate-identifiers-add.md#change-device-ownership).

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Segurança

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Suporte de credenciais derivadas em dispositivos geridos totalmente pelo Android<!--4839592-->
Poderá utilizar credenciais derivadas em dispositivos geridos pela Android Enterprise. O apoio será incluído para recuperar uma credencial derivada para Entrust Datacard, Intercede e DISA Purebred. Poderá utilizar uma credencial derivada para autenticação de apps, Wi-Fi, VPN ou s/MIME assinando e/ou encriptação com aplicações que a suportam.

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Definições de preferências de privacidade para dispositivos macOS<!-- 2934232 --> 
Com o lançamento do macOS Catalina 10.15, a Apple adicionou novos melhoramentos de segurança e privacidade. Por defeito, as aplicações e processos não conseguem aceder a dados específicos sem o consentimento do utilizador. Se os utilizadores não fornecerem o consentimento, as aplicações e processos podem não funcionar. A Intune está a adicionar suporte para configurações que permitem aos administradores de TI permitir ou proibir o consentimento de acesso de dados em nome dos utilizadores finais em dispositivos que executam o macOS 10.14 ou posteriormente. Estas definições garantirão que as aplicações e processos continuem a funcionar corretamente e reduzem o número de indicações que os utilizadores finais experimentam.

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Texto e etiquetas ui atualizados para definições de perfil de proteção de ponto final do Windows 10<!-- 5983747 -->
Estamos a atualizar o texto para várias definições que configura como perfis de configuração do dispositivo Windows 10 para facilitar a compreensão das definições pretendidas e resultados.

As definições que estamos a atualizar incluem perfis de configuração do dispositivo Windows 10 para:

- [Restrições](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) ao dispositivo > Microsoft Defender Antivírus  
- [Proteção endpoint](../protect/endpoint-protection-windows-10.md) > Microsoft Defender Antivírus

As definições que são suportadas com Intune não estão a mudar. Esta é apenas uma atualização para o texto UI no Microsoft Endpoint Management Admin Center.

<!-- ***********************************************-->
## <a name="notices"></a>Avisos

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Veja também

Para mais detalhes sobre os recentes desenvolvimentos, consulte [o que há de novo no Microsoft Intune](whats-new.md).



