---
title: Em desenvolvimento - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune apresenta-se em desenvolvimento
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764208"
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

**Este artigo foi atualizado pela última vez na data listada no título acima.**

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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Portal da empresa para Android vai orientar utilizadores a obter aplicações após inscrição no perfil de trabalho <!-- 6103999  -->
Estamos a melhorar a orientação in-app no Portal da Empresa para facilitar aos utilizadores a descoberta e instalação de apps.  Depois de se inscreverem na gestão de perfis de trabalho, os utilizadores verão uma mensagem a dizer-lhes que podem encontrar aplicações sugeridas na versão com insígnias do Google Play. Os utilizadores também verão uma nova ligação de **apps Get** na gaveta do Portal da Empresa à esquerda. Para dar lugar a estas novas e melhoradas experiências, o separador **APPS** será removido. 

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuração do dispositivo

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>As definições e valores do perfil de configuração do dispositivo serão atualizados para plataformas Windows<!-- 4091122 -->
Quando cria perfis de configuração de**Devices**dispositivos para plataformas Windows (Perfis de configuração de  >  **dispositivos**  >  **Criar perfis** > qualquer opção **windows** para plataforma), algumas definições e os seus valores são diferentes do CSP, e podem ser confusos. Os nomes de definição e os seus valores serão atualizados para serem mais claros.

Aplica-se a:

- Windows 10 e perfis posteriores de configuração do dispositivo
- Windows Holographic para perfis de configuração de dispositivos empresariais
- Perfis de configuração do dispositivo Windows 8.1
- Perfis de configuração do dispositivo Windows Phone 8.1

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nova definição de FileVault para a política de configuração do dispositivo de proteção de pontofinal macOS<!-- 5459801   -->
Estamos adicionando uma nova definição à categoria FileVault dentro do modelo de proteção de [ponto final macOS:](../protect/endpoint-protection-macos.md) Ocultar a chave de recuperação. **(Dispositivos**  >  **Perfis de**  >  configuração **Criar perfil,** selecionar **macOS** para a *Plataforma* e, em seguida, **proteção Endpoint** para o *tipo de perfil).* Esta definição esconde a chave pessoal do utilizador final durante a encriptação FileVault 2. Um utilizador do dispositivo pode visualizar a sua chave de recuperação pessoal a qualquer momento a partir da aplicação portal da empresa iOS ou do portal da empresa para o dispositivo macOS encriptado. Para ver a chave de recuperação pessoal, podem ir aos detalhes do dispositivo e clicar na *chave de recuperação do get*.

Esta definição não estará disponível na política previamente criada. Terá de recriar as políticas do FileVault para configurar esta definição para a utilizar. 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscrição de dispositivos

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Trazer os seus próprios dispositivos pode usar VPN para implementar<!--5015344 -->
Esta funcionalidade pode ser adiada.

### <a name="shared-ipads-for-business--6367326---"></a>IPads partilhados para Negócios<!--6367326 -->
Poderá utilizar intune e Apple Business Manager para configurar facilmente e de forma segura o iPad partilhado para que vários colaboradores possam partilhar dispositivos. O [iPad partilhado](https://developer.apple.com/education/shared-ipad/) da Apple proporciona uma experiência personalizada para vários utilizadores, preservando os dados dos utilizadores. Utilizando um ID apple gerido, os utilizadores podem aceder às suas aplicações, dados e configurações depois de assinarem qualquer iPad partilhado na sua organização. O iPad partilhado funciona com identidades federadas.

Para ver esta funcionalidade, vá ao centro de [administração do Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Dispositivos**  >  **iOS**  >  **iOS matricula**do programa de inscrição  >  **Enrollment program tokens** > escolher um token** > **Perfis**  >  **Criar perfil**  >  **iOS**. Na página **'Definições** de Gestão', selecione **Inscrever-se sem afinidade** do utilizador e verá a opção **de iPad partilhado.**

**Aplica-se a:** iPadOS 13.4 e posteriormente. Este lançamento adicionou suporte para sessões temporárias com iPad partilhado para que os utilizadores possam aceder a um dispositivo sem um ID da Apple gerido. No início do início, o dispositivo apaga todos os dados do utilizador de modo a que o dispositivo esteja imediatamente pronto para ser utilizado, eliminando a necessidade de uma limpeza do dispositivo. 

<!-- ***********************************************-->
## <a name="device-management"></a>Gestão de dispositivos

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Suporte de scripts PowerShell para dispositivos BYOD<!-- 1862833  -->
Os scripts PowerShell suportarão dispositivos registados em Intune. Para obter mais informações sobre o PowerShell, consulte [scripts PowerShell em dispositivos Windows 10 em Intune](../apps/intune-management-extension.md). Esta funcionalidade não suporta dispositivos que executam a edição home do Windows 10.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>O Log Analytics incluirá o registo de detalhes do dispositivo<!--6014987  -->
Os registos de detalhes do **Reports**dispositivo insintonizem os registos disponíveis na análise de  >  **registode relatórios**. Pode correlacionar detalhes do dispositivo para construir consultas personalizadas e livros de trabalho azure.


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


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplique as suas políticas em Endpoint Security<!-- 5892558   -->
Poderá selecionar uma política que criou no nó de segurança Endpoint do centro de administração do Microsoft Endpoint Manager e, em seguida, duplicar para criar uma cópia.  As políticas que poderá duplicar incluem as que cria para: 

- Antivírus
- Disk encryption (Encriptação de discos)
- Firewall
- Endpoint detection and response (Deteção e resposta de pontos finais)
- Attack surface reduction (Redução da superfície de ataque)
- Account protection (Proteção de contas)

A duplicação fará uma cópia da política original, que poderá depois mudar o nome e editar. A cópia não incluirá atribuições do original.

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Novo perfil para a política de firewall de segurança endpoint<!-- 5653324   -->
Como pré-visualização, estamos adicionando um perfil adicional para o Windows 10 e mais tarde para a política de Firewall na segurança endpoint de Intune (**Endpoint security**  >  **Firewall**  >  **Create Policy** > selecione Windows **10 e mais tarde).** 

Cada instância deste novo perfil suporta até 150 regras personalizadas do *Microsoft Defender Firewall*. O perfil de regras do Microsoft Defender Firewall permite definir regras granulares do Windows Firewall para permitir ou bloquear portas e aplicações no Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Avisos

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Veja também

Para mais detalhes sobre os recentes desenvolvimentos, consulte [o que há de novo no Microsoft Intune](whats-new.md).



