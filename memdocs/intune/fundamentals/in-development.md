---
title: Em desenvolvimento - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune apresenta-se em desenvolvimento
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220137"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>Em desenvolvimento para microsoft Intune - março 2020

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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>Portal da empresa para o iOS para apoiar o modo paisagístico<!--6048329  -->
Os utilizadores poderão inscrever os seus dispositivos, encontrar aplicações e obter suporte de TI utilizando a orientação do ecrã à sua escolha. A aplicação detetará e ajustará automaticamente os ecrãs para encaixar no retrato ou no modo de paisagem, a menos que os utilizadores bloqueiem o ecrã no modo retrato.

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Melhor experiência de inscrição no Portal da Empresa para Android<!-- 6103997  -->
Estamos a atualizar o layout de vários ecrãs de acesso no aplicativo Portal da Empresa para Android para tornar a experiência mais moderna, simples e limpa para os utilizadores.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuração do dispositivo

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Perfis de configuração de dispositivos de rede com fios para dispositivos macOS<!-- 3508686  -->
Um novo perfil de configuração do dispositivo macOS estará disponível que configura redes com fios (**configuração** do dispositivo > **Perfis** > **Criar perfil** > **macOS** para plataforma > **Rede Com fios** para tipo de perfil). Utilize esta funcionalidade para criar perfis 802.1x para gerir redes com fios e implementar estas redes com fios para os seus dispositivos macOS.

Aplica-se a:
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>Melhoria da experiência de interface do utilizador ao criar perfis de configuração em dispositivos iOS/iPadOS e macOS<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
Quando criar um perfil para dispositivos iOS/iPadOS ou macOS, a experiência no Endpoint Management Admin Center será atualizada. Esta alteração impacta os seguintes perfis de configuração do dispositivo **(Dispositivos** > Perfis de **Configuração** > **Criar perfil** > **iOS** ou **macOS** para a plataforma):

- Personalizado: iOS/iPadOS, macOS
- Funcionalidades do dispositivo: iOS/iPadOS, macOS
- Restrições ao dispositivo: iOS/iPadOS, macOS
- Proteção endpoint: macOS
- Extensões: macOS
- Ficheiro preferencial: macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Melhoria da experiência de interface do utilizador ao criar perfis de configuração OEMConfig em dispositivos Android Enterprise<!-- 5568645   -->
Quando cria ou edita um perfil OEMConfig para dispositivos Android Enterprise, a experiência no centro de administração endpoint Management é atualizada. A experiência atualizada fornecerá um resumo das definições que configurado num ápice. Esta alteração afeta o perfil de configuração do dispositivo OEMConfig (**Dispositivos** > perfis de **configuração** > **Criar perfil** > **Android Enterprise** para plataforma > **OEMConfig** para o tipo de perfil).

Esta funcionalidade aplica-se a:
- Android Enterprise 

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>As definições e valores do perfil de configuração do dispositivo serão atualizados para plataformas Windows<!-- 4091122 -->
Quando cria perfis de configuração de dispositivos para plataformas Windows **(Dispositivos** > Perfis de **Configuração** > **Criar perfil** > qualquer opção **do Windows** para plataforma), algumas definições e os seus valores são diferentes do CSP, e podem ser confusos. Os nomes de definição e os seus valores serão atualizados para serem mais claros.

Aplica-se a:

- Windows 10 e perfis posteriores de configuração do dispositivo
- Windows Holographic para perfis de configuração de dispositivos empresariais
- Perfis de configuração do dispositivo Windows 8.1
- Perfis de configuração do dispositivo Windows Phone 8.1

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Melhoria da experiência de interface de utilizador ao criar perfis de restrições de dispositivos em dispositivos Android e Android Enterprise<!-- 5841361 -->
Quando criar um perfil para dispositivos Android ou Android Enterprise, a experiência no centro de administração endpoint Management será atualizada. Esta alteração impacta os seguintes perfis de configuração do dispositivo **(Dispositivos** > Perfis de **Configuração** > **Criar perfil** > **administrador de dispositivos Android** ou Android **Enterprise** para plataforma):

- Restrições ao dispositivo: Administrador de dispositivos Android
- Restrições ao dispositivo: Proprietário de dispositivos Android Enterprise
- Restrições ao dispositivo: Perfil de trabalho Android Enterprise

Para obter mais informações sobre as restrições do dispositivo, pode configurar, consulte o [administrador do dispositivo Android](../configuration/device-restrictions-android.md) e o Android [Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Configure a aplicação ATP microsoft defender para macOS  <!-- 5520115  -->
Em breve poderá configurar as [definições](../protect/endpoint-protection-macos.md) da aplicação ATP do Microsoft Defender para dispositivos que executam o macOS como parte de um perfil de configuração de dispositivos de proteção endpoint **(Dispositivos** > perfis de **configuração** > **Criar perfil,** selecionar **o macOS** para a *Plataforma*e, em seguida, **proteção Endpoint** para o *tipo de Perfil).* Haverá oito configurações para a configuração do dispositivo macOS. 

O Defender ATP é suportado no macOS 10.13 (High Sierra) e posteriormente, e a aplicação [ATP Microsoft Defender](../apps/apps-advanced-threat-protection-macos.md) deve ser implementada no dispositivo *após* a aplicação destas definições. As definições devem ser enviadas para o dispositivo antes da aplicação ser implementada. As versões beta do macOS não serão suportadas.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nova definição de FileVault para a política de configuração do dispositivo de proteção de pontofinal macOS<!-- 5459801   -->
Estamos adicionando uma nova definição à categoria FileVault dentro do modelo de proteção de [ponto final macOS:](../protect/endpoint-protection-macos.md) Ocultar a chave de recuperação. **(Dispositivos** > perfis de **configuração** > **Criar perfil,** selecione **o macOS** para a *Plataforma* e, em seguida, a **proteção endpoint** para o *tipo de perfil).* Esta definição esconde a chave pessoal do utilizador final durante a encriptação FileVault 2. Um utilizador do dispositivo pode visualizar a sua chave de recuperação pessoal a qualquer momento a partir da aplicação portal da empresa iOS ou do portal da empresa para o dispositivo macOS encriptado. Para ver a chave de recuperação pessoal, podem ir aos detalhes do dispositivo e clicar na *chave de recuperação do get*.

Esta definição não estará disponível na política previamente criada. Terá de recriar as políticas do FileVault para configurar esta definição para a utilizar. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Configure o agente de otimização de entrega ao descarregar conteúdo da aplicação Win32<!-- 5410945  -->
Poderá configurar o agente de Otimização de Entregas para descarregar conteúdo da aplicação Win32, tanto em segundo plano como em modo de primeiro plano, com base na atribuição. Para as aplicações Win32 existentes, os conteúdos continuarão a descarregar em modo de fundo. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione **Apps** > **Todas as aplicações** > *selecionar a aplicação Win32* > **Properties**. **Selecione Editar** ao lado de **Atribuições**.  Editar a atribuição selecionando **Incluir** em **modo** na secção **Requerida.**  Encontrará a nova definição na secção de **definições** da App quando estiver disponível. Para mais informações sobre a Otimização de Entregas, consulte a [gestão da aplicação Win32 - Otimização de Entrega](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Gestão de dispositivos

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Alterar o utilizador primário para dispositivos Windows <!-- 3794742 -->
Poderá alterar o Utilizador Principal para dispositivos híbridos windows e Azure AD. Para tal, vá a **Intune** > **Devices** > **Todos os dispositivos** > escolha um dispositivo > **Propriedades** > **Utilizador Primário**.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Suporte de scripts PowerShell para dispositivos BYOD<!-- 1862833  -->
Os scripts PowerShell suportarão dispositivos registados em Intune. Para obter mais informações sobre o PowerShell, consulte [scripts PowerShell em dispositivos Windows 10 em Intune](../apps/intune-management-extension.md). Esta funcionalidade não suporta dispositivos que executam a edição home do Windows 10.

### <a name="new-information-in-device-details---5604099---"></a>Novas informações sobre detalhes do dispositivo<!-- 5604099 -->
As seguintes informações estarão na página **'Overview'** para dispositivos:

- Capacidade de armazenamento (quantidade de armazenamento físico no dispositivo)
- Capacidade de memória (quantidade de memória física no dispositivo)

### <a name="script-support-for-macos-devices---4280361----"></a>Suporte de script para dispositivos macOS<!-- 4280361  -->
Poderá adicionar e implementar scripts para dispositivos macOS. Este suporte alarga a sua capacidade de configurar dispositivos macOS para além do que é possível utilizando capacidades nativas de MDM em dispositivos macOS.

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
