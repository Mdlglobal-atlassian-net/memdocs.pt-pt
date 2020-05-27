---
title: Gerir edge para iOS e Android para iOS e Android com Intune
titleSuffix: ''
description: Utilize políticas de proteção de aplicações Intune com Edge para iOS e Android para garantir que os websites corporativos são sempre acedidos com salvaguardas no lugar.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4a13a3e843e6ba0c30cb8397b28fec31ed6b4670
ms.sourcegitcommit: a1da477542fb0ff360685d6eb58ef43e37ac3950
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83853405"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>Gerir o acesso à web utilizando o Edge para iOS e Android com o Microsoft Intune

Edge para iOS e Android é projetado para permitir que os utilizadores naveguem na web e suportem multiidentidades. Os utilizadores podem adicionar uma conta de trabalho, bem como uma conta pessoal, para navegação. Existe uma separação completa entre as duas identidades, que é como o que é oferecido noutras aplicações móveis da Microsoft.

A borda para iOS é suportada no iOS 12.0 e posteriormente. Edge for Android é suportado no Android 5 e mais tarde.

> [!NOTE]
> A borda para iOS e Android não consome configurações que os utilizadores configuram para o navegador nativo nos seus dispositivos, porque o Edge para iOS e Android não consegue aceder a estas configurações.

As capacidades de proteção mais ricas e amplas para os dados do Office 365 estão disponíveis quando subscrever a suite Enterprise Mobility + Security, que inclui funcionalidades Microsoft Intune e Azure Ative Directory Premium, como acesso condicional. No mínimo, pretende implementar uma política de acesso condicional que apenas permite a conectividade ao Edge para iOS e Android a partir de dispositivos móveis e uma política de proteção de aplicações Intune que garanta que a experiência de navegação esteja protegida.

> [!NOTE]
> Novos web clips (aplicações web) em dispositivos iOS serão abertos no Edge para iOS e Android em vez do Navegador Gerido Intune quando necessário abrir num navegador protegido. Para clips web iOS mais antigos, você deve redirecionar estes clips web para garantir que eles abrem no Edge para iOS e Android em vez do Navegador Gerido.

## <a name="apply-conditional-access"></a>Aplicar acesso condicional
As organizações podem utilizar as políticas de Acesso Condicional Azure AD para garantir que os utilizadores só podem aceder a conteúdos de trabalho ou de escola usando o Edge para iOS e Android. Para isso, necessitará de uma política de acesso condicional que direcione todos os potenciais utilizadores. Os detalhes sobre a criação desta política podem ser encontrados na Política de Proteção de Aplicações Require para acesso a [aplicações na nuvem com Acesso Condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Siga o Cenário 2: As aplicações do [navegador requerem aplicações aprovadas com políticas](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies)de proteção de aplicações , que permite o Edge para iOS e Android, mas bloqueia outros navegadores de dispositivos móveis da ligação ao Office 365 endpoints.

   >[!NOTE]
   > Esta política garante que os utilizadores móveis podem aceder a todos os pontos finais do Office 365 a partir de Edge para iOS e Android. Esta política também impede que os utilizadores utilizem o InPrivate para aceder ao Office 365 pontos finais.

Com acesso condicional, também pode direcionar sites no local que expôs a utilizadores externos através do Proxy de [Aplicação AD Azure](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="create-intune-app-protection-policies"></a>Criar políticas de proteção de aplicativos Intune

As Políticas de Proteção de Aplicações (APP) definem quais as aplicações que são permitidas e as ações que podem tomar com os dados da sua organização. As opções disponíveis na APP permitem às organizações adaptar a proteção às suas necessidades específicas. Para alguns, pode não ser óbvio quais as definições de política necessárias para implementar um cenário completo. Para ajudar as organizações a priorizar o endurecimento do ponto final do cliente móvel, a Microsoft introduziu taxonomia para o seu quadro de proteção de dados APP para a gestão de aplicações móveis iOS e Android.

O quadro de proteção de dados da APP é organizado em três níveis distintos de configuração, com cada nível de construção fora do nível anterior:

- **A proteção básica de dados da empresa** (Nível 1) garante que as aplicações estão protegidas com um PIN e encriptadas e realizam operações de limpeza seletiva. Para dispositivos Android, este nível valida o atestado do dispositivo Android. Esta é uma configuração de nível de entrada que fornece um controlo de proteção de dados semelhante nas políticas de caixa de correio Exchange Online e introduz TI e a população utilizadora para APP.
- **A empresa reforçada proteção de dados** (Nível 2) introduz mecanismos de prevenção de fugas de dados de APP e requisitos mínimos de SO. Esta é a configuração que é aplicável à maioria dos utilizadores móveis que acedem a dados do trabalho ou da escola.
- **A alta proteção de dados** da empresa (Nível 3) introduz mecanismos avançados de proteção de dados, configuração PIN melhorada e APP Mobile Threat Defense. Esta configuração é desejável para os utilizadores que acedem a dados de alto risco.

Para ver as recomendações específicas para cada nível de configuração e as aplicações mínimas que devem ser protegidas, reveja o quadro de proteção de dados utilizando políticas de proteção de [aplicações](app-protection-framework.md).

Independentemente de o dispositivo estar matriculado numa solução unificada de gestão de pontos finais (UEM), é necessário criar uma política de proteção de aplicações Intune tanto para aplicações iOS como Android, utilizando os passos em Como criar e atribuir políticas de proteção de [aplicações.](app-protection-policies.md) Estas políticas, no mínimo, devem satisfazer as seguintes condições:

1. Incluem todas as aplicações móveis da Microsoft, tais como Outlook, OneDrive, Office ou Teams, uma vez que isso irá garantir que os utilizadores podem aceder e manipular dados de trabalho ou escolas dentro de qualquer aplicação da Microsoft de forma segura.

2. São atribuídos a todos os utilizadores. Isto garante que todos os utilizadores estão protegidos, independentemente de utilizarem o Edge para iOS ou Android.

3. Determine qual o nível de enquadramento que satisfaz os seus requisitos. A maioria das organizações deve implementar as definições definidas na Enterprise reforçou a **proteção de dados** (Nível 2), uma vez que permite controlos de proteção de dados e requisitos de acesso.

Para obter mais informações sobre as definições disponíveis, consulte [as definições](app-protection-policy-settings-android.md) de políticas de proteção de aplicações Android e as definições da política de proteção de [aplicações iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Para aplicar políticas de proteção de aplicações Intune contra aplicações em dispositivos Android que não estejam inscritos no Intune, o utilizador também deve instalar o Portal da Empresa Intune. Para mais informações, consulte o que esperar quando a sua aplicação Android for gerida por políticas de proteção de [aplicações.](../fundamentals/end-user-mam-apps-android.md)

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Entrada única para aplicações web ligadas a AD Azure em navegadores protegidos por políticas

A vantagem para iOS e Android pode aproveitar o único sign-on (SSO) para todas as aplicações web (SaaS e no local) que estejam ligadas a Azure AD. O SSO permite que os utilizadores acedam a aplicações web ligadas a AD através do Edge para iOS e Android, sem terem de reintroduzir as suas credenciais.

O SSO exige que o seu dispositivo seja registado pela aplicação Microsoft Authenticator para dispositivos iOS, ou pelo Portal da Empresa Intune no Android. Quando os utilizadores têm algum destes, são solicitados a registar o seu dispositivo quando se destinam a uma aplicação web ligada à AD Azure num browser protegido por políticas (isso só é verdade se o seu dispositivo ainda não tiver sido registado). Depois de o dispositivo ser registado na conta do utilizador gerida pela Intune, essa conta tem OSO ativado para aplicações web ligadas a AD Azure.

> [!NOTE]
> O registo do dispositivo é uma simples verificação do serviço Azure AD. Não requer inscrição completa do dispositivo, e não dá nenhum privilégio adicional no dispositivo.

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>Utilize a configuração da aplicação para gerir a experiência de navegação

O edge para iOS e Android suporta configurações de aplicações que permitem uma gestão unificada de pontofinal, como o Microsoft Endpoint Manager, administradores para personalizar o comportamento da app.

A configuração da aplicação pode ser entregue através do canal operativo operativo (MDM) em dispositivos matriculados (canal[de configuração de aplicações gerido](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) para iOS ou Android no canal [Enterprise](https://developer.android.com/work/managed-configurations) para Android) ou através do canal Intune App Protection Policy (APP). Edge para iOS e Android suporta os seguintes cenários de configuração:

- Apenas permitir contas de trabalho ou escola
- Definições gerais de configuração de aplicativos
- Definições de proteção de dados

> [!IMPORTANT]
> Para cenários de configuração que exijam a inscrição do dispositivo no Android, os dispositivos devem ser matriculados no Android Enterprise e o Edge para Android deve ser implementado através da loja Managed Google Play. Para mais informações, consulte [Configurar a inscrição de dispositivos de perfil de trabalho Android Enterprise](../enrollment/android-work-profile-enroll.md) e adicionar políticas de configuração de [aplicações para dispositivos Android Enterprise geridos](app-configuration-policies-use-android.md).

Cada cenário de configuração realça os seus requisitos específicos. Por exemplo, se o cenário de configuração requer inscrição do dispositivo, e assim funciona com qualquer fornecedor UEM, ou requer Políticas de Proteção de Aplicações Intune.

> [!NOTE]
> Com o Microsoft Endpoint Manager, a configuração da aplicação entregue através do canal MDM OS é referida como uma Política de Configuração de Aplicações de **Dispositivos Geridos** (ACP); a configuração da aplicação entregue através do canal app Protection Policy é referida como uma Política de Configuração de **Apps Geridas.**

## <a name="only-allow-work-or-school-accounts"></a>Apenas permitir contas de trabalho ou escola

Respeitar as políticas de segurança e conformidade de dados dos nossos maiores e altamente regulados clientes é um pilar fundamental para o valor da Microsoft 365. Algumas empresas têm a obrigação de capturar todas as informações de comunicações dentro do seu ambiente corporativo, bem como garantir que os dispositivos são usados apenas para comunicações corporativas. Para suportar estes requisitos, o Edge para iOS e Android em dispositivos matriculados pode ser configurado apenas para permitir que uma única conta corporativa seja aprovisionada dentro da app.

Pode saber mais sobre a configuração do modo de definição de modo de contas permitida pelo org aqui:

- [Configuração android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [definição de iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Este cenário de configuração funciona apenas com dispositivos matriculados. No entanto, qualquer fornecedor uEM é apoiado. Se não estiver a utilizar o Microsoft Endpoint Manager, tem de consultar a documentação do UEM sobre como implementar estas chaves de configuração.

## <a name="general-app-configuration-scenarios"></a>Cenários gerais de configuração de aplicativos

O edge para iOS e Android oferece aos administradores a capacidade de personalizar a configuração padrão para várias configurações in-app. Esta capacidade só é atualmente oferecida quando o Edge para iOS e Android tiver uma Política de Proteção de Aplicações Intune aplicada ao trabalho ou conta escolar que é assinada na app.

> [!IMPORTANT]
> O Edge para Android não suporta as definições de Crómio que estão disponíveis no Managed Google Play.

O edge suporta as seguintes definições para configuração:

- Novas experiências da Página de Separadores
- Experiências bookmark
- Experiências de comportamento de aplicativos
- Experiências no modo quiosque

Estas definições podem ser implementadas na aplicação independentemente do estado de inscrição do dispositivo.

### <a name="new-tab-page-experiences"></a>Novas experiências da Página de Separadores

Edge para iOS e Android oferece às organizações várias opções para ajustar a experiência New Tab Page.

#### <a name="organization-logo-and-brand-color"></a>Logotipo da organização e cor da marca

Estas configurações permitem personalizar a Nova Página de Separadores para Edge para iOS e Android para mostrar o logótipo e a cor da marca da sua organização como o fundo da página.

Para fazer upload do logótipo e da cor da sua organização, complete primeiro os seguintes passos:
1. Dentro [do Microsoft Endpoint Manager,](https://endpoint.microsoft.com)navegue para a Empresa de Personalização da Empresa de Personalização da **Administração**de  ->  **Customization**  ->  **Inquilinos.**
2. Para definir o logótipo da sua marca, ao lado do **Show em cabeçalho,** escolha "Apenas logotipo da organização". Recomenda-se a consumação de logotipos de fundo transparentes.
3. Para definir a cor de fundo da sua marca, selecione uma **cor tema**. Edge para iOS e Android aplica um tom mais claro da cor na Página de Novos Separadores, que garante que a página tem alta legibilidade.

Em seguida, utilize os seguintes pares chave/valor para puxar a marca da sua organização para Edge para iOS e Android:

|    Chave    |    Valor    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    **verdadeiro** mostra logotipo da marca da organização<br>**falso** (padrão) não vai expor um logotipo    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    **mostra a** cor da marca da organização<br>**falso** (padrão) não vai expor uma cor    |

#### <a name="homepage-shortcut"></a>Atalho de página inicial

Esta definição permite configurar um atalho inicial para Edge para iOS e Android. O atalho inicial que configura ruma aparece como o primeiro ícone por baixo da barra de pesquisa quando o utilizador abre um novo separador no Edge para iOS e Android. O utilizador não pode editar ou apagar este atalho no seu contexto gerido. O atalho da página inicial mostra o nome da sua organização para distingui-lo. 

|    Chave    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Especifique um URL válido. Os URLs incorretos são bloqueados como medida de segurança.<br>Por exemplo: `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>Atalhos de vários sites superiores

Da mesma forma, configurar um atalho inicial, pode configurar vários atalhos de topo em novas páginas de separadores em Edge para iOS e Android. O utilizador não pode editar ou eliminar estes atalhos num contexto gerido. Nota: pode configurar um total de 8 atalhos, incluindo um atalho de página inicial. Se configurar um atalho inicial, isso irá anular o primeiro site de topo configurado. 

|    Chave    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    Especifique o conjunto de URLs de valor. Cada atalho do site superior consiste num título e URL. Separe o título e a URL com o `|` personagem.<br>Por exemplo: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>Notícias da indústria

Pode configurar a experiência New Tab Page dentro do Edge para iOS e Android para mostrar notícias da indústria que são relevantes para a sua organização. Ao ativar esta funcionalidade, o Edge para iOS e Android utiliza o nome de domínio da sua organização para agregar notícias da web sobre a sua organização, indústria da organização e concorrentes, para que os seus utilizadores possam encontrar notícias externas relevantes, todas a partir das novas páginas centralizadas de separadores dentro do Edge para iOS e Android. A Industry News está desligada por defeito. 

|    Chave    |    Valor    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **verdadeiros** mostra notícias da indústria na nova página de tab<br>**falso** (padrão) esconde notícias da indústria da nova página de separadores    |

### <a name="bookmark-experiences"></a>Experiências bookmark

Edge para iOS e Android oferece às organizações várias opções para gerir marcadores.

#### <a name="managed-bookmarks"></a>Marcadores geridos

Para facilitar o acesso, pode configurar marcadores que gostaria que os seus utilizadores disponibilizassem quando estiverem a utilizar o Edge para iOS e Android.

- Os marcadores só aparecem na conta de trabalho ou escolar e não estão expostos a contas pessoais.
- Os marcadores não podem ser eliminados ou modificados pelos utilizadores.
- Os favoritos aparecem no topo da lista. Quaisquer marcadores que os utilizadores criem aparecem abaixo destes marcadores.
- Se tiver ativado a reorientação do Proxy de Aplicação, pode adicionar aplicações web proxy aplicação utilizando o seu URL interno ou externo.
- Certifique-se de que prefixa todos os URLs com **http://** ou **https://** ao inseri-los na lista.
- Os marcadores são criados numa pasta com o nome da organização que é definida no Diretório Ativo Azure.

|    Chave    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    O valor para esta configuração é uma lista de marcadores. Cada marcador é composto pelo título de marcador e pelo URL do marcador. Separe o título e a URL com o `|` personagem.<br> Por exemplo: `Microsoft Bing|https://www.bing.com`<p>Para configurar vários marcadores, separe cada par com o carácter duplo `||` .<br>Por exemplo:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>O meu marcador de aplicativos

Por padrão, os utilizadores têm o bookmark my Apps configurado dentro da pasta da organização dentro do Edge para iOS e Android.

|    Chave    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **true** (padrão) mostra As Minhas Apps dentro do Edge para os bookmarks iOS e Android<br>**falsas** esconde as minhas apps dentro do Edge para iOS e Android    |

### <a name="app-behavior-experiences"></a>Experiências de comportamento de aplicativos

Edge para iOS e Android oferece às organizações várias opções para gerir o comportamento da app.

#### <a name="default-protocol-handler"></a>Manipulador de protocolo padrão

Por padrão, o Edge para iOS e Android utiliza o manipulador de protocolo HTTPS quando o utilizador não especifica o protocolo no URL. Geralmente, esta é considerada uma boa prática, mas pode ser desativada.

|    Chave    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     **verdadeiro** (padrão) manipulador de protocolo padrão é HTTPS<br>**manipulador de** protocolo de padrão falso é HTTP     |

#### <a name="disable-data-sharing-for-personalization"></a>Desativar a partilha de dados para personalização

Por padrão, o Edge para iOS e Android leva os utilizadores a utilizarem a recolha de dados e a partilharem o histórico de navegação para personalizarem a sua experiência de navegação. As organizações podem desativar esta partilha de dados evitando que esta solicitação seja mostrada aos utilizadores finais.

|    Chave    |    Valor    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     **verdadeiro** desativa este pedido de exibição para utilizadores finais<br>**utilizadores falsos** (padrão) são solicitados a partilhar dados de utilização    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     **verdadeiro** desativa este pedido de exibição para utilizadores finais<br>**utilizadores falsos** (padrão) são solicitados a partilhar o histórico de navegação     |

#### <a name="disable-specific-features"></a>Desativar funcionalidades específicas

A borda para iOS e Android permite que as organizações desativem certas funcionalidades que são ativadas por padrão. Para desativar estas funcionalidades, configure a seguinte definição:

|    Chave    |    Valor    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    **password** desativa solicitações que oferecem para guardar palavras-passe para o utilizador final<br>**inprivate** desativa a navegação inprivate<p>Para desativar várias funcionalidades, separa valores com `|` . Por exemplo, desativa tanto o armazenamento inprivate como o armazenamento de `inprivate|password` senhas.     |

> [!NOTE]
> Edge for Android não suporta desativar o gestor de passwords.

#### <a name="disable-extensions"></a>Desativar extensões

Pode desativar a estrutura de extensão dentro do Edge para android para evitar que os utilizadores instalem quaisquer extensões de aplicações. Para tal, configure a seguinte definição:

|    Chave    |    Valor    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    **verdadeiramente** desativa o quadro de extensão<br>**falso** (padrão) permite o quadro de extensão    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Experiências no modo quiosque em dispositivos Android

O edge para Android pode ser ativado como uma aplicação de quiosque com as seguintes definições:

|    Chave    |    Valor    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    **true** permite o modo quiosque para Edge para Android<br>**falso** (padrão) desativa modo quiosque    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    **verdadeiro** mostra a barra de endereço si em modo quiosque<br> **falso** (padrão) esconde a barra de endereço no modo quiosque    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    **verdadeiro** mostra a barra de ação inferior no modo quiosque<br> **falso** (padrão) esconde a barra inferior no modo quiosque    |

## <a name="data-protection-app-configuration-scenarios"></a>Cenários de configuração de aplicativos de proteção de dados

O Edge para iOS e Android suporta as políticas de configuração de aplicações para as seguintes definições de proteção de dados quando a aplicação é gerida pelo Microsoft Endpoint Manager com uma Política de Proteção de Aplicações Intune aplicada ao trabalho ou conta escolar que é assinada na app:

- Gerir a sincronização da conta
- Gerir web sites restritos
- Gerir a configuração do proxy
- Gerir sites de inscrição individual NTLM

Estas definições podem ser implementadas na aplicação independentemente do estado de inscrição do dispositivo.

### <a name="manage-account-synchronization"></a>Gerir a sincronização da conta

Por padrão, o microsoft Edge sync permite que os utilizadores acedam aos seus dados de navegação em todos os seus dispositivos de entrada. Os dados suportados por sync incluem:

- Favoritos
- Palavras-passe
- Endereços e muito mais (entrada de formulário de preenchimento automático)

A funcionalidade Sync está ativada através do consentimento do utilizador e os utilizadores podem ligar ou desligar a sincronização de cada um dos tipos de dados acima indicados. Para mais informações consulte [o Microsoft Edge Sync](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync).

As organizações têm a capacidade de desativar a sincronização do Edge no iOS e Android. 

|Chave  |Valor  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |**verdadeiro** (padrão) permite sincronização de Borda<br>**falso** desativa sincronização edge          |

### <a name="manage-restricted-web-sites"></a>Gerir web sites restritos

As organizações podem definir quais os sites que os utilizadores podem aceder dentro do contexto de trabalho ou conta escolar no Edge para iOS e Android. Se utilizar uma lista de autorizações, os seus utilizadores só podem aceder aos sites explicitamente listados. Se utilizar uma lista bloqueada, os utilizadores podem aceder a todos os sites, exceto aqueles explicitamente bloqueados. Só deve impor uma lista permitida ou bloqueada, não as duas. Se impor os dois, só a lista permitida é honrada.

A organização também define o que acontece quando um utilizador tenta navegar para um web site restrito. Por defeito, as transições são permitidas. Se a organização o permitir, os sites restritos podem ser abertos no contexto da conta pessoal, no contexto InPrivate da conta Azure AD, ou se o site está totalmente bloqueado. Para obter mais informações sobre os vários cenários que são suportados, consulte [transições restritas de websites no telemóvel Microsoft Edge](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333). Ao permitir experiências de transição, os utilizadores da organização permanecem protegidos, mantendo os recursos corporativos seguros.

> [!NOTE]
> A borda para iOS e Android só pode bloquear o acesso aos sites quando são acedidos diretamente. Não bloqueia o acesso quando os utilizadores utilizam serviços intermédios (como um serviço de tradução) para aceder ao site.

Utilize os seguintes pares de chaves/valor para configurar uma lista de sites permitida ou bloqueada para Edge para iOS e Android. 

|Chave  |Valor  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |O valor correspondente da chave é uma lista de URLs. Introduza todos os URLs que pretende permitir como um único valor, separados por um personagem de `|` tubo.<p>**Exemplos:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |O valor correspondente da chave é uma lista de URLs. Introduza todos os URLs que pretende bloquear como um único valor, separadopor um personagem de `|` tubo.<br>**Exemplos:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |**true** (padrão) permite que Edge para iOS e Android transvide sites restritos. Quando as contas pessoais não são desativadas, os utilizadores são solicitados a mudar para o contexto pessoal para abrir o site restrito, ou adicionar uma conta pessoal. Se com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked está definido como verdadeiro, os utilizadores têm a capacidade de abrir o site restrito no contexto InPrivate.<p>**falso** impede edge para iOS e Android de utilizadores em transição. Os utilizadores são simplesmente mostrados uma mensagem afirmando que o site a que estão a tentar aceder está bloqueado.         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |**true** permite que sites restritos sejam abertos no contexto InPrivate da conta Azure AD. Se a conta Azure AD for a única conta configurada no Edge para iOS e Android, o site restrito é aberto automaticamente no contexto InPrivate. Se o utilizador tiver uma conta pessoal configurada, o utilizador é solicitado a escolher entre abrir o InPrivate ou mudar para a conta pessoal.<p> **falso** (predefinido) requer que o site restrito seja aberto na conta pessoal do utilizador. Se as contas pessoais forem desativadas, o site está bloqueado.<p>Para que esta definição faça efeito,com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock deve ser configurado como verdadeiro.          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | Insira o número de segundos que os utilizadores verão a notificação do snack bar "Link aberto com o modo InPrivate. A sua organização requer o uso do modo InPrivate para este conteúdo." Por predefinição, a notificação do snack-bar é mostrada durante 7 segundos.

Os seguintes sites são sempre permitidos independentemente das definições definidas da lista de permitir ou bloquear lista:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>Formatos URL para lista de site permitido e bloqueado 

Pode utilizar vários formatos DE URL para construir as listas de sites permitidos/bloqueados. Estes padrões permitidos são detalhados na tabela seguinte.

- Certifique-se de que prefixa todos os URLs com **http://** ou **https://** ao inseri-los na lista.
- Pode utilizar o símbolo wildcard ( ) de acordo com as regras na lista de \* padrões permitidas a seguir.
- Um wildcard só pode coincidir com um componente inteiro do nome de anfitrião (separado por períodos) ou partes inteiras do caminho (separados por cortes para a frente). Por exemplo, `http://*contoso.com` **não** é suportado.
- Pode especificar os números da porta no endereço. Se não especificar um número da porta, os valores utilizados são:
  - Porta 80 para http
  - Porta 443 para https
- A utilização de wildcards para o número da porta **não** é suportada. Por exemplo, `http://www.contoso.com:*` e `http://www.contoso.com:*/` não são suportados. 

    |    URL    |    Detalhes    |    Correspondências    |    Não corresponde    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Corresponde a uma única página    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Corresponde a uma única página    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    Corresponde a todos os URLs que começam com `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Corresponde a todos os subdomínios abaixo`contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Corresponde a todos os subdomínios que terminam com`contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    Corresponde a uma única pasta    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Corresponde a uma única página, usando um número de porta    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Corresponde a uma única página segura    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Corresponde a uma única pasta e a todas as subpastas    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Seguem-se exemplos de algumas das inputs que não pode especificar:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - Endereços IP
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>Gerir a configuração do proxy

Pode utilizar o Edge para iOS e Android e [Aplicação AD Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) em conjunto para dar aos utilizadores acesso a sites intranet nos seus dispositivos móveis. Por exemplo: 

- Um utilizador está a utilizar a aplicação móvel Outlook, que está protegida pela Intune. Em seguida, clicam num link para um site intranet num e-mail, e o Edge para iOS e Android reconhece que este site intranet foi exposto ao utilizador através do Application Proxy. O utilizador é automaticamente encaminhado através do Proxy de Aplicação, para autenticar com qualquer autenticação multifactor aplicável e acesso condicional, antes de chegar ao site intranet. O utilizador pode agora aceder a sites internos, mesmo nos seus dispositivos móveis, e o link no Outlook funciona como esperado.
- Um utilizador abre o Edge para iOS e Android no seu iOS ou dispositivo Android. Se o Edge para iOS e Android estiver protegido com Intune, e o Application Proxy estiver ativado, o utilizador pode ir a um site intranet utilizando o URL interno a que estão habituados. A borda para iOS e Android reconhece que este site intranet foi exposto ao utilizador através do Application Proxy. O utilizador é automaticamente encaminhado através do Proxy de Aplicação, para autenticar antes de chegar ao site intranet. 

Antes de começar:

- Instale as suas aplicações internas através do Proxy de Aplicação AD Azure.
  - Para configurar o Proxy de Aplicações e publicar aplicações, veja a [documentação de configuração](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).
- A aplicação Edge para iOS e Android deve ter uma política de proteção de [aplicações Intune](app-protection-policy.md) atribuída.
- As aplicações da Microsoft devem ter uma política de proteção de aplicações que tenha restringido a transferência de **conteúdos web com outras aplicações** de definição de transferência de dados definida para **o Microsoft Edge**.

> [!NOTE]
> Os dados atualizados de reorientação do Proxy de aplicação podem demorar até 24 horas a entrar em vigor no Edge para iOS e Android.

Borda de destino para iOS com o seguinte par chave/valor, para ativar o Proxy de Aplicação:

|    Chave    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **true** permite cenários de redirecionamento da App AD Azure Proxy<br>**falso** (padrão) impede cenários de procuração de aplicações da AD Azure    |

> [!NOTE]
> A borda para Android não consome esta chave. Em vez disso, o Edge for Android consome automaticamente a configuração de Proxy de Aplicação AD Azure, desde que a conta AD assinada em Azure tenha uma Política de Proteção de Aplicações aplicada.

Para obter mais informações sobre como utilizar o Edge para iOS e Android e Android e Azure Application Proxy em conjunto para acesso perfeito (e protegido) a aplicações web no local, consulte [Better together: Intune and Azure Ative Directory team up to improve us access](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). Esta publicação de blog refere-se ao Navegador Gerido Intune, mas o conteúdo aplica-se também ao Edge para iOS e Android.

### <a name="manage-ntlm-single-sign-on-sites"></a>Gerir sites de inscrição individual NTLM

As organizações podem exigir que os utilizadores autentiem com a NTLM para aceder em web sites intranet. Por padrão, os utilizadores são solicitados a introduzir credenciais cada vez que acedem a um site que requer a autenticação NTLM, uma vez que o cache credencial NTLM é desativado. 

As organizações podem permitir o cache cessão credencial ntLM para sites específicos. Para estes sites, depois de o utilizador introduzir credenciais e autenticar com sucesso, as credenciais são cached por padrão durante 30 dias.


|Chave  |Valor  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |O valor correspondente da chave é uma lista de URLs. Introduza todos os URLs que pretende permitir como um único valor, separados por um personagem de `|` tubo.<p>**Exemplos:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>Para obter mais informações sobre os tipos de formatos DEURL que são suportados, consulte [os formatos URL para a lista](#url-formats-for-allowed-and-blocked-site-list)de sites permitida e bloqueada .         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |Número de horas para cache credenciais, padrão é de 720 horas         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Implementar cenários de configuração de apps com o Microsoft Endpoint Manager

Se estiver a utilizar o Microsoft Endpoint Manager como fornecedor de gestão de aplicações móveis, os seguintes passos permitem-lhe criar uma política de configuração de apps gerida. Após a configuração ser criada, pode atribuir as suas definições a grupos de utilizadores.

1. Assine no [Microsoft Endpoint Manager](https://endpoint.microsoft.com).

2. Selecione **Apps** e, em seguida, selecione políticas de configuração de **Aplicativos**.

3. Na lâmina de configuração da **aplicação,** escolha **Adicionar** e selecione **aplicações geridas.**

4. Na secção **Basics,** introduza um **Nome**e **descrição** opcional para as definições de configuração da aplicação.

5. Para **aplicações públicas,** escolha **selecionar aplicações públicas**, e depois, na lâmina de **aplicações direcionadas,** escolha **Edge para iOS e Android** selecionando as aplicações da plataforma iOS e Android. Clique em **Selecionar** para guardar as aplicações públicas selecionadas.

6. Clique em **Seguir** para completar as definições básicas da política de configuração da aplicação.

7. Na secção **Definições,** expanda as definições de **configuração edge**.

8. Se pretender gerir as definições de proteção de dados, configure as definições desejadas em conformidade:

    - Para **reorientação**do proxy da aplicação, escolha entre as opções disponíveis: **Ativar**, **Desativar** (predefinido).

    - Para o URL de **atalho inicial,** especifique um URL válido que inclua o prefixo de *http://* ou *https://*. Os URLs incorretos são bloqueados como medida de segurança.

    - Para **marcadores geridos,** especifique o título e um URL válido que inclua o prefixo de *http://* ou *https://*.

    - Para **URLs permitidos,** especifique um URL válido (apenas estes URLs são permitidos; nenhum outro sítio pode ser acedido). Para obter mais informações sobre os tipos de formatos DEURL que são suportados, consulte [os formatos URL para a lista](#url-formats-for-allowed-and-blocked-site-list)de sites permitida e bloqueada .

    - Para **URLs bloqueados,** especifique um URL válido (apenas estes URLs estão bloqueados). Para obter mais informações sobre os tipos de formatos DEURL que são suportados, consulte [os formatos URL para a lista](#url-formats-for-allowed-and-blocked-site-list)de sites permitida e bloqueada .

    - Para **redirecionar sites restritos para contexto pessoal,** escolha entre as opções disponíveis: **Ativar** (predefinido), **Desativar**.

    > [!NOTE]
    > Quando tanto os URLs permitidos como os URLs Bloqueados são definidos na política, apenas a lista permitida é honrada.

9. Se pretender configurações adicionais de configuração de aplicações não expostas na política acima, expanda o nó de **configurações gerais** e introduza nos pares de valor chave em conformidade.

10. Quando terminar de configurar as definições, escolha **Seguinte**.

11. Na secção **De tarefas,** escolha **Selecione grupos para incluir**. Selecione o grupo Azure AD ao qual pretende atribuir a política de configuração da aplicação e, em seguida, escolha **Select**.

12. Quando terminar as atribuições, escolha **Next**.

13. Na política de configuração da **aplicação Create Review + Criar** lâmina, reveja as definições configuradas e escolha **Criar**.

A política de configuração recém-criada é apresentada na lâmina de configuração da **App.**

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>Use edge para iOS e Android para aceder a registos de aplicações geridas

Os utilizadores com Edge para iOS e Android instalados no seu iOS ou dispositivo Android podem ver o estado de gestão de todas as aplicações publicadas pela Microsoft. Podem enviar registos para resolver problemas com as suas aplicações geridas para iOS ou Android utilizando os seguintes passos:

1. Open Edge para iOS e Android no seu dispositivo.
2. Escreva `about:intunehelp` na caixa de endereço.
3. Edge para iOS e Android lança modo de resolução de problemas.

Para obter uma lista das definições armazenados nos registos das aplicações, veja [Review app protection logs in the Managed Browser (Rever os registos de proteção das aplicações no Managed Browser)](app-protection-policy-settings-log.md).

Para ver como visualizar registos em dispositivos Android, consulte [Enviar registos para o seu administrador de TI por e-mail](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android).

## <a name="next-steps"></a>Passos seguintes

- [O que são as políticas de proteção de aplicações?](app-protection-policy.md) 
