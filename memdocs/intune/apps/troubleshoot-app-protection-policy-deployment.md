---
title: Como resolver problemas a implementação da política de proteção de aplicações Intune
description: Discute como resolver problemas que poderá experimentar quando implementar políticas de proteção de aplicações Intune.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: conceptual
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 3b4c02e366f4778e65b4fe4c853ed147fcdb1df3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82072757"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Implementação da política de proteção de aplicações de resolução de problemas em Intune

## <a name="introduction"></a>Introdução

Este artigo ajuda-o a compreender e a resolver problemas quando aplica políticas de proteção de aplicações no Microsoft Intune. Siga as secções aplicáveis à sua situação.

## <a name="basic-steps"></a>Passos básicos

### <a name="collect-initial-data"></a>Recolher dados iniciais

Antes de começar a resolver problemas, deve recolher algumas informações básicas que o possam ajudar a compreender melhor o problema e reduzir o tempo para encontrar uma resolução.

Recolha as seguintes informações:

- Que definição de política não é aplicada? Alguma política é aplicada?
- Qual é a experiência do utilizador? Os utilizadores instalaram e iniciaram a aplicação direcionada?
- Quando começou o problema? A proteção de aplicativos já funcionou?
- Qual a plataforma (Android ou iOS) que tem o problema?
- Quantos utilizadores são afetados? Todos os dispositivos ou apenas alguns dispositivos são afetados?
- Quantos dispositivos são afetados? Todos os dispositivos ou apenas alguns dispositivos são afetados?
- Embora a política de proteção de aplicações Intune não exija um serviço de gestão de dispositivos móveis (MDM), os utilizadores afetados são utilizadores afetados usando Intune ou um EMM de terceiros?
- Todas as aplicações geridas ou apenas aplicações específicas são afetadas? Por exemplo, as aplicações LOB que têm [Intune App SDK afetadas,](../developer/app-sdk-get-started.md) mas as aplicações de loja não são?

Agora, pode começar a resolver problemas com base nas respostas a estas perguntas.

### <a name="verify-prerequisites"></a>Verificar os pré-requisitos

O próximo passo na resolução de problemas é verificar se todos os pré-requisitos são cumpridos.

Embora possa utilizar políticas de proteção de aplicações Intune independentes de qualquer solução MDM, devem ser cumpridos os seguintes pré-requisitos:

- O utilizador deve ter uma licença Intune atribuída.
- O utilizador deve pertencer a um grupo de segurança que seja alvo de uma política de proteção de aplicações. A mesma política de proteção de aplicações deve visar a aplicação específica que é usada.
- Para dispositivos Android, a aplicação Portal da Empresa é necessária para receber políticas de proteção de aplicações.
- Se utilizar aplicações [Word, Excel ou PowerPoint,](https://products.office.com/business/office) devem ser cumpridos os seguintes requisitos adicionais:
    - O utilizador deve ter uma licença para [aplicações Microsoft 365 para negócios ou empresa](https://products.office.com/business/compare-more-office-365-for-business-plans) ligadas à conta Azure Ative Directory (Azure AD) do utilizador. A subscrição tem de incluir as aplicações do Office para dispositivos móveis e pode incluir uma conta de armazenamento na cloud com o [OneDrive para Empresas](https://onedrive.live.com/about/business/). As licenças do Office 365 podem ser atribuídas no centro de administração da [Microsoft 365](https://admin.microsoft.com) seguindo [estas instruções](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).
    - O utilizador deve ter uma localização gerida que esteja configurada utilizando o **Ecorânico Save como** funcionalidade. Este comando está localizado sob a definição da definição da definição da definição da política de proteção de aplicações **Save Copy of Org Data.** Por exemplo, se a localização gerida for [oneDrive,](https://onedrive.live.com/about/)a aplicação OneDrive deve ser configurada na aplicação Word, Excel ou PowerPoint do utilizador.
    - Se a localização gerida for o OneDrive, a aplicação deve ser direcionada pela política de proteção de aplicações que é implementada para o utilizador.

  > [!NOTE]
  > Atualmente, as aplicações móveis do Office suportam apenas o SharePoint Online e não o SharePoint no local.

- Se utilizar as políticas de proteção de aplicações Intune juntamente com os recursos no local (Microsoft Skype para Business e Microsoft Exchange Server), deve ativar a [Autenticação Moderna Híbrida (HMA) para o Skype para Negócios e Intercâmbio](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

As políticas de proteção de aplicações intonantes requerem que a identidade do utilizador seja consistente entre a app e o [Intune App SDK](../developer/app-sdk-get-started.md). A única forma de garantir esta consistência é através da autenticação moderna. Existem cenários em que as aplicações podem funcionar numa configuração no local sem autenticação moderna. No entanto, os resultados não são consistentes ou garantidos.

Para obter mais informações sobre como permitir as configurações híbridas e no local do Skype para o Skype para o Business, consulte os seguintes artigos:

- **Híbrido**<br>
[Hybrid Modern Auth for SfB and Exchange vai GA](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **No local**<br>
[Moderno Auth para SfB OnPrem com AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>Verifique o estado da política de proteção de aplicativos

Para verificar o estado de proteção da aplicação, siga estes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **o** > estado de proteção da**aplicação****monitor** > de apps e, em seguida, selecione o azulejo dos **utilizadores atribuídos.**
3. Na página **Relatório da aplicação**, selecione **Selecionar utilizador** para abrir uma lista de utilizadores e grupos.
4. Procure e selecione um dos utilizadores afetados da lista e, em seguida, **selecione Selecione o utilizador**. No topo do painel de relatórios da App, pode ver se o utilizador está licenciado para proteção de aplicações e tem uma licença para O365. Também pode ver o estado da aplicação para todos os dispositivos do utilizador.
5. Tome nota de informações tão importantes como as aplicações direcionadas, tipos de dispositivos, políticas, estado de check-in do dispositivo e última hora de sincronização.

> [!NOTE]
> As políticas de proteção de aplicações só são aplicadas quando as aplicações são utilizadas no contexto de trabalho. Por exemplo, quando o utilizador está a aceder a apps através de uma conta de trabalho.

Para mais informações, consulte [como validar a sua configuração](../apps/app-protection-policies-validate.md)da política de proteção de aplicações no Microsoft Intune .

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Verifique se a identidade do utilizador é consistente entre app e Intune App SDK

Na maioria dos cenários, os utilizadores iniciam sessão nas suas contas utilizando o seu nome principal de utilizador (UPN). No entanto, em alguns ambientes (como cenários no local), os utilizadores podem utilizar outra forma de credenciais de inscrição. Nestes casos, pode descobrir que a UPN que é usada na aplicação não corresponde ao objeto UPN em Azure AD. Quando este problema ocorre, as políticas de proteção de aplicações não são aplicadas como esperado.

As melhores práticas recomendadas pela Microsoft são combinar a UPN com o endereço SMTP primário. Esta prática permite que os utilizadores iniciem sessão em aplicações geridas, proteção de aplicações Intune e outros recursos da AD Azure, tendo uma identidade consistente. Para mais informações, consulte a [população de Utilizadores ad da Azure.](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname)

Se o seu ambiente necessitar de métodos alternativos de login, consulte [configurar o ID de login alternativo,](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)especificamente [a autenticação moderna híbrida com id alternativo](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Verifique se o utilizador é alvo

As políticas de proteção de aplicações intonizadas devem ser direcionadas aos utilizadores. Se não atribuir uma política de proteção de aplicações a um utilizador ou grupo de utilizadores, a política não é aplicada.

Para verificar se a política é aplicada ao utilizador visado, siga estas etapas:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione o estado de proteção da**aplicação****do Monitor** > de **Aplicações** > , e, em seguida, selecione o azulejo do **estado do utilizador** (com base na plataforma OS do dispositivo).
No painel de **relatórios** da App que se abre, **selecione Selecione selecione** o utilizador para procurar um utilizador.
3. Selecione o utilizador na lista. Pode ver os detalhes para esse utilizador.

Ao atribuir a apólice a um grupo de utilizadores, certifique-se de que o utilizador está no grupo de utilizadores. Para tal, siga estes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Grupos > Todos os grupos**, e depois procure e selecione o grupo que é usado para a sua atribuição de políticas de proteção de aplicações.
3. Na secção **Gerir,** selecione **Membros**.
4. Se o utilizador afetado não estiver listado, reveja [a aplicação Manage e o acesso a recursos utilizando grupos de Diretórios Ativos Do Azure](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) e as regras de adesão ao grupo. Certifique-se de que o utilizador afetado está incluído no grupo.
5. Certifique-se de que o utilizador afetado não se está em nenhum dos grupos excluídos para a apólice.

> [!IMPORTANT]
> - A política de proteção de aplicações Intune deve ser atribuída a grupos de utilizadores e não a grupos de dispositivos.
> - Se o dispositivo afetado utilizar o Programa de Inscrição de Dispositivos Apple (DEP), certifique-se de que a **Affinity do Utilizador** está ativada. A afinidade de utilizador é necessária para qualquer aplicação que requer autenticação do utilizador no DEP.
> - Se o dispositivo afetado utilizar o Android Enterprise, apenas os perfis de trabalho irão suportar políticas de proteção de aplicações.


### <a name="verify-that-the-managed-app-is-targeted"></a>Verifique se a aplicação gerida é direcionada

Quando configurar as políticas de proteção de aplicações Intune, as aplicações direcionadas devem utilizar [o Intune App SDK](../developer/app-sdk-get-started.md). Caso contrário, as políticas de proteção de aplicações podem não funcionar corretamente.

Certifique-se de que a aplicação direcionada está listada em [aplicações protegidas](../apps/apps-supported-intune-apps.md)microsoft Intune . Para aplicações LOB ou personalizadas, verifique se as aplicações utilizam a versão mais recente do [Intune App SDK](../developer/app-sdk-get-started.md). Tenha em atenção o seguinte:

Para o iOS, esta prática é importante porque cada versão contém correções que afetam a forma como estas políticas são aplicadas e como funcionam. Para mais informações, consulte as [versões intune App SDK iOS](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
Para o Android, esta prática não é tão importante. No entanto, os utilizadores devem ter a versão mais recente da aplicação Portal da Empresa instalada porque a aplicação Portal da Empresa funciona como agente corretor de políticas.

> [!NOTE]
> A partir de setembro de 2019, a Intune passará a apoiar aplicações iOS que tenham versões Intune App SDK 8.1.1 e versões posteriores. As aplicações construídas utilizando versões SDK que sejam mais precoces do que 8.1.1 deixarão de ser suportadas. 

## <a name="more-information"></a>Mais informações

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Requisitos especiais para dispositivos geridos por MDM intune

Quando cria uma política de proteção de aplicações, pode direcioná-la para todos os tipos de aplicações ou para os seguintes tipos de aplicações:

- Aplicativos em dispositivos não geridos
- Aplicativos em dispositivos geridos por Intune
- Aplicativos no Perfil de Trabalho Android

> [!NOTE] 
> Para especificar os tipos de aplicações, detete **o Target para todos os tipos de aplicações** para **Não**, e, em seguida, selecione na lista de tipos de **aplicações.**

Para o iOS, são necessárias as seguintes definições adicionais de configuração de [aplicações](../apps/app-configuration-policies-use-ios.md) para direcionar as definições da política de proteção de aplicações (APP) para aplicações em dispositivos matriculados no Intune:

- As aplicações geridas por **IntuneMAMUPN** devem ser configuradas para todas as aplicações geridas por MDM (Intune ou um EMM de terceiros). Para mais informações, consulte a configuração upn do utilizador Configure para a Microsoft Intune ou EMM de terceiros.
- **O IntuneMAMDeviceID** deve ser configurado para todas as aplicações geridas por TERCEIROS e LOB MDM.
- **O IntuneMAMDeviceID** deve ser configurado como símbolo de identificação do dispositivo. Por exemplo, key=IntuneMAMDeviceID, value={{deviceID}}. Para obter mais informações, veja [Adicionar políticas de configuração da aplicação para dispositivos iOS geridos](../apps/app-configuration-policies-use-ios.md).
- Se apenas o valor **IntuneMAMDeviceID** estiver configurado, a Intune APP considerará o dispositivo como não gerido.

### <a name="scenario-policy-changes-are-not-working"></a>Cenário: As mudanças de política não estão a funcionar
O [Intune App SDK](../developer/app-sdk-get-started.md) verifica regularmente as alterações de políticas. No entanto, este processo pode ser adiado por qualquer uma das seguintes razões:

- A aplicação ainda não fez o check-in com o serviço.
- A aplicação Portal da Empresa foi removida do dispositivo.

A política de proteção de aplicações intonou assenta na identidade do utilizador. Por isso, é necessário um login válido que utilize uma conta de trabalho ou escola para a app e uma ligação consistente ao serviço. Se o utilizador não tiver assinado a aplicação, ou se a aplicação do Portal da Empresa tiver sido removida do dispositivo, as atualizações de políticas não se aplicarão.

Além disso, alterações e atualizações da política de proteção de aplicações podem demorar até 8 horas a aplicar. Se aplicável, fechar todas as aplicações e reiniciar o dispositivo normalmente obriga a atualização de política a aplicar mais cedo.

Para verificar o estado de proteção da aplicação, siga estes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **o** > estado de proteção da**aplicação****monitor** > de apps e, em seguida, selecione o azulejo dos **utilizadores atribuídos.**
3. Na página de relatórios da App, selecione **Selecione o utilizador para** abrir uma lista de utilizadores e grupos.
4. Procure e selecione um dos utilizadores afetados da lista e, em seguida, **selecione Selecione o utilizador**.
5. Reveja as políticas que são atualmente aplicadas, incluindo o estado e o último tempo de sincronização.
6. Se o estado não for **verificado**, ou se o visor indicar que não houve uma sincronização recente, verifique se o utilizador tem uma ligação de rede consistente. Para os utilizadores Android, certifique-se de que têm a versão mais recente da aplicação Portal da Empresa instalada.

> [!IMPORTANT]
> O [Intune App SDK](../developer/app-sdk-get-started.md) verifica a cada 30 minutos para limpeza seletiva. No entanto, as alterações à política existente para os utilizadores que já estão inscritos podem não aparecer até 8 horas. Para acelerar este processo, faça com que o utilizador faça login fora da aplicação e, em seguida, faça login ou reinicie os seus dispositivos.

A política de proteção de aplicações intune inclui suporte multi-identidade. Intune pode aplicar políticas de proteção de aplicativos apenas para o trabalho ou conta escolar que está inscrito na app. No entanto, apenas uma conta de trabalho ou escola por dispositivo é suportada.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Cenário: A política é aplicada, mas os utilizadores do iOS ainda podem transferir ficheiros de trabalho para aplicações não geridas
A funcionalidade **de gestão open-in** (botão ![](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg) Open-in) para dispositivos iOS pode limitar as transferências de ficheiros entre aplicações que são implementadas através do canal MDM. O utilizador poderá transferir ficheiros de trabalho de locais geridos, como o OneDrive e o Exchange, para aplicações ou locais não geridos, dependendo da configuração. A funcionalidade de gestão do iOS **Open-in** funciona fora de outros métodos de transferência de dados. Portanto, não é afetado pelas definições **de Save as** e **Copy/Paste.**

Pode utilizar políticas de proteção de aplicações Intune juntamente com a funcionalidade **de gestão iOS Open-in** para proteger os dados da empresa da seguinte forma:

- **Dispositivos pertencentes a funcionários que não são geridos por uma solução MDM**: Pode definir as definições da política de proteção de aplicações para **permitir que a app transfira dados apenas para aplicações geridas**por políticas . Configurado desta forma, o comportamento **Open-in** numa aplicação gerida por políticas fornece apenas outras aplicações geridas por políticas como opções de partilha. Por exemplo, se um utilizador tentar enviar um ficheiro protegido como anexo do OneDrive na aplicação de correio nativo, esse ficheiro é ilegível.

- **Dispositivos geridos por soluções MDM**– Para dispositivos que estão matriculados em soluções de MDM intune ou de terceiros, a partilha de dados entre apps utilizando políticas de proteção de aplicações e outras aplicações geridas para iOS que são implementadas através do MDM é controlada pela Intune APP e pela funcionalidade de gestão do iOS **Open-in.**<br/><br/>
Para garantir que as aplicações que implementa utilizando uma solução MDM também estão associadas às suas políticas de proteção de aplicações Intune, configure a configuração UPN do utilizador conforme descrito na [configuração upn do utilizador Configure](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).<br/><br/>Para especificar como pretende permitir a transferência de dados para outras aplicações, ative os **dados do Send Org para outras aplicações**e, em seguida, selecione o seu nível de partilha preferido.<br/><br/>Para especificar como pretende permitir que uma aplicação receba dados de outras aplicações, ative **o Receber dados de outras apps**e, em seguida, selecione o seu nível preferido de receber dados.

Para obter mais informações sobre como receber e partilhar dados de aplicações, consulte as definições de [deslocalização de Dados](../apps/app-protection-policy-settings-ios.md#data-protection).

Para obter mais informações, veja [Como gerir a transferência de dados entre aplicações iOS no Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md).

## <a name="references"></a>Referências

Se ainda procura uma solução para um problema relacionado, ou para mais informações sobre intune, publique uma pergunta no nosso [fórum Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Muitos engenheiros de apoio, MVPs e membros da nossa equipa de desenvolvimento visitam os fóruns. Então, há uma boa hipótese de encontrares alguém que tenha a informação de que precisas.

Para abrir um pedido de suporte para a equipa de suporte ao produto Microsoft Intune, consulte como obter suporte para o [Microsoft Intune](../fundamentals/get-support.md).

Para obter mais informações sobre a política de proteção de aplicações Intune, consulte os seguintes artigos:

- [Resolver problemas da gestão de aplicações móveis](../apps/troubleshoot-mam.md)
- [Perguntas mais frequentes sobre a MAM e a proteção de aplicações](../apps/mam-faq.md)
- [Dica de suporte: Resolução de problemas Na política de proteção de aplicações Intune utilizando ficheiros de registo em dispositivos locais](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

Para todas as novidades, informações e dicas tecnológicas, vá aos nossos blogs oficiais:

- [O Blog da Equipa de Apoio intune da Microsoft](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [O Microsoft Enterprise Mobility and Security Blog](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>Passos seguintes

- Para obter informações adicionais de resolução de problemas, veja [Utilizar o portal de resolução de problemas para ajudar os utilizadores na sua empresa](../fundamentals/help-desk-operators.md). 
- Saiba mais sobre os problemas conhecidos no Microsoft Intune. Para mais informações, consulte [Intune Customer Success](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Precisa de ajuda adicional? Veja [Como obter suporte para o Microsoft Intune](../fundamentals/get-support.md).
