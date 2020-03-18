---
title: Gerir o Microsoft Edge para iOS e Android com Intune
titleSuffix: ''
description: Utilize as políticas de proteção de aplicações Intune com o Microsoft Edge para garantir que os websites corporativos são sempre acedidos com salvaguardas no lugar.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/02/2020
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
ms.openlocfilehash: 3cf77349508144498b847236598abda6bced52b0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332137"
---
# <a name="manage-web-access-by-using-microsoft-edge-with-microsoft-intune"></a>Gerir o acesso à web utilizando o Microsoft Edge com o Microsoft Intune

A utilização de políticas de proteção de aplicações Intune com o Microsoft Edge ajuda a garantir que os websites corporativos são sempre acedidos com salvaguardas no lugar. As seguintes funcionalidades da empresa Microsoft Edge ativadas pelas políticas Intune estão disponíveis:

- **Dupla identidade.** Os utilizadores podem adicionar uma conta de trabalho, bem como uma conta pessoal, para navegação. Não há uma separação total entre as duas identidades, semelhante à arquitetura e à experiência no Office 365 e no Outlook. Os administradores intonantes podem definir as políticas desejadas para uma experiência de navegação protegida dentro da conta de trabalho.
- **Intune app protection policy integration.** Como o Microsoft Edge está integrado com o Intune SDK, pode direcionar as políticas de proteção de aplicações para proteger contra a perda de dados. Estas capacidades incluem o controlo do corte, cópia e pasta, prevenindo capturas de ecrã e garantindo que os links selecionados pelo utilizador se abrem apenas em outras aplicações geridas.
- **Integração de Procuração de Aplicação Azure.** Pode controlar o acesso ao software como um serviço (SaaS) apps e aplicações web. Isto ajuda a garantir que as aplicações baseadas no navegador apenas funcionam no navegador Microsoft Edge seguro, quer os utilizadores finais se conectem a partir da rede corporativa ou se conectem a partir da internet.
- **Configuração da aplicação.** Pode utilizar as definições de configuração da aplicação para fortalecer a postura de segurança da sua organização e configurar funcionalidades de facilidade de utilização para os utilizadores finais. Por exemplo, pode definir marcadores, um atalho de página inicial, sites permitidos ou bloqueados, e procuração de aplicação de Diretório Ativo Azure (Azure AD).

As políticas de proteção do Microsoft Intune para o Microsoft Edge ajudam a proteger os dados e recursos da sua organização. A utilização destas políticas com o Microsoft Edge garante que os recursos da sua empresa estão protegidos não só dentro de aplicações instaladas de forma nativa, mas também quando acedidos através do navegador web.

## <a name="getting-started"></a>Introdução

Você e os seus utilizadores finais podem descarregar o Microsoft Edge de lojas de aplicações públicas para serem utilizados nas suas organizações. Os requisitos do sistema operativo para as políticas do navegador são qualquer um dos seguintes requisitos:
- Android 4 e posterior
- iOS 8.0 e posterior

## <a name="application-protection-policies-for-microsoft-edge"></a>Políticas de proteção de aplicações para Microsoft Edge

Como o Microsoft Edge está integrado com o Intune SDK, pode aplicar-lhes políticas de proteção de aplicações.

Pode aplicar estas definições a:
- Dispositivos matriculados com Intune.
- Dispositivos que estão matriculados com outro produto de gestão de dispositivos móveis.
- Dispositivos não geridos.

Se o Microsoft Edge não for direcionado para a política Intune, os utilizadores não podem usá-lo para aceder a dados de outras aplicações geridas pelo Intune, como aplicações do Office. 

## <a name="conditional-access-for-microsoft-edge"></a>Acesso Condicional para Microsoft Edge

Pode utilizar o Azure AD Conditional Access para redirecionar os seus utilizadores para aceder em conteúdos corporativos apenas através do Microsoft Edge. Isto restringe o acesso do navegador móvel a aplicações web ligadas a AD Azure a Microsoft Edge protegidos por políticas. Isto bloqueia o acesso a partir de quaisquer outros navegadores desprotegidos, como o Safari ou o Chrome. Pode aplicar acesso condicional a recursos do Azure como O Exchange Online e o SharePoint Online, o centro de administração da Microsoft 365 e até mesmo sites no local que expôs a utilizadores externos através do Proxy de [Aplicação AD Azure](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

Para restringir aplicações web ligadas a AD Azure para usar o Microsoft Edge no iOS e Android:
1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Sob o nó Intune, selecione **Acesso Condicional** > **Nova política.**
3. **Selecione Grant** da secção de **controlos** de acesso do painel.
4. Selecione **Requer aplicação aprovada do cliente**.
5. Escolha **Selecione** no painel **Grant.** Esta política tem de ser atribuída às aplicações na cloud que pretende que sejam acessíveis apenas a partir da aplicação Intune Managed Browser.

    ![Screenshot da política de acesso condicional - Grant](./media/manage-microsoft-edge/manage-microsoft-edge-01.png)

6. Na secção De Atribuição, selecione **Condições** > **Apps**. O painel de **Apps** aparece.
7. Em **Configuração, selecione** **Sim** para aplicar a política a aplicações específicas do cliente.
8. Certifique-se de que a opção **Browser** está selecionada como uma aplicação cliente.

    ![Screenshot da política de acesso condicional - Selecione aplicações para clientes](./media/manage-microsoft-edge/manage-microsoft-edge-02.png)

    > [!NOTE]
    > Se quiser restringir as aplicações nativas (aplicações não baseadas no browser) que podem aceder a estas aplicações na cloud, também pode selecionar **Aplicações móveis e clientes de ambiente de trabalho**.

9. Na secção **De Missões,** selecione **Utilizadores e grupos,** e depois escolha os utilizadores ou grupos que pretende atribuir a esta política.

10. Na secção **Atribuições**, selecione **Aplicações na cloud** para selecionar que aplicações quer proteger com esta política.

Depois de configurada a política acima, os utilizadores são obrigados a usar o Microsoft Edge para aceder às aplicações web ligadas ao Azure AD que você protegeu com esta política. Se os utilizadores tentarem utilizar um navegador não gerido neste cenário, recebem uma mensagem de que devem utilizar o Microsoft Edge.

> [!TIP]
> O Acesso Condicional é uma tecnologia Azure AD. O nó de Acesso Condicional acessado a partir de Intune é o mesmo nó a que o Azure AD acessado.

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Entrada única para aplicações web ligadas a AD Azure em navegadores protegidos por políticas

O Microsoft Edge no iOS e Android pode aproveitar o único sign-on (SSO) para todas as aplicações web (SaaS e no local) que estejam ligadas ao Azure AD. O SSO permite que os utilizadores acedam a aplicações web ligadas a AD através do Microsoft Edge, sem terem de reintroduzir as suas credenciais.

O SSO exige que o seu dispositivo seja registado pela aplicação Microsoft Authenticator para dispositivos iOS, ou pelo Portal da Empresa Intune no Android. Quando os utilizadores têm algum destes, são solicitados a registar o seu dispositivo quando se destinam a uma aplicação web ligada a AD Azure num navegador protegido por políticas. (Isto só é verdade se o seu dispositivo ainda não tiver sido registado.) Depois de o dispositivo ser registado na conta do utilizador gerida pela Intune, essa conta tem OSO ativado para aplicações web ligadas a AD Azure.

> [!NOTE]
> O registo do dispositivo é uma simples verificação do serviço Azure AD. Não requer inscrição completa do dispositivo, e não dá nenhum privilégio adicional no dispositivo.

## <a name="create-a-protected-browser-app-configuration"></a>Criar uma configuração da aplicação de browser protegido

Para criar a configuração da aplicação para o Microsoft Edge:

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps** > políticas de **configuração** de apps > **adicionar**.
3. No painel de política de **configuração Adicionar,** introduza um **Nome** e **uma descrição** opcional para as definições de configuração da aplicação.
4. Para o tipo de **Inscrição de dispositivos**, selecione **Aplicações geridas**.
5. Escolha **Selecione a aplicação necessária**. Em seguida, no painel de **aplicações direcionados,** escolha o **Navegador Ou** **Edge** Gerido para iOS/iPadOS, para Android, ou para ambos.
6. Selecione **OK** para voltar ao painel de política de **configuração Adicionar.**
7. Selecione **Definições de configuração**. No painel de **configuração,** define os pares de chaves e de valor para fornecer configurações para o Microsoft Edge. Utilize as secções mais adiante neste artigo para saber mais sobre os diferentes pares de chave e valor que pode definir.

    > [!NOTE]
    > O Microsoft Edge utiliza os mesmos pares de chave e valor que o Managed Browser. No Android, o Microsoft Edge deve ser direcionado com políticas de proteção de aplicações para as políticas de configuração de apps para produzir efeito.

8. Quando terminar, selecione **OK**.
9. No painel de política de **configuração Adicionar,** escolha **Adicionar**.<br>
    A nova configuração é criada e exibida no painel de configuração da **App.**

## <a name="assign-the-configuration-settings-you-created"></a>Atribuir as definições de configuração que criou 

Atribui as definições a grupos de utilizadores em Azure AD. Se esse utilizador tiver a aplicação de browser protegido de destino instalada, a aplicação será gerida pelas definições que especificou.

1. No **painel** apps do painel de gestão de aplicações móveis Intune, selecione políticas de configuração de **Aplicações**.
2. Na lista de configurações de aplicações, selecione aquela que pretende atribuir.
3. No painel seguinte, selecione **Atribuições**.
4. No painel **de Tarefas,** selecione o grupo Azure AD ao qual pretende atribuir a configuração da aplicação e, em seguida, selecione **OK**.

## <a name="direct-users-to-microsoft-edge-instead-of-the-intune-managed-browser"></a>Utilizadores diretos para o Microsoft Edge em vez do Navegador Gerido Intune 

Tanto o Navegador Gerido Intune como o Microsoft Edge podem ser usados como navegadores protegidos por políticas. Para garantir que os seus utilizadores estão a ser direcionados para utilizar a aplicação correta do navegador, direcione todas as suas aplicações geridas por Intune (por exemplo, Outlook, OneDrive e SharePoint) com a seguinte definição de configuração:

|    Chave    |    Valor    |
|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.useEdge`    |    O valor `true` irá direcionar os seus utilizadores para o download e utilização do Microsoft Edge.<br>O valor `false` permitirá que os seus utilizadores utilizem o Navegador Gerido intune.    |

Se este valor **de** configuração da aplicação não for definido, a seguinte lógica definirá qual o navegador que será usado para abrir links corporativos.

No Android:
- O Intune Managed Browser é lançado se um utilizador tiver o Navegador Gerido Intune e o Microsoft Edge descarregados no seu dispositivo. 
- O Microsoft Edge é lançado se apenas o Microsoft Edge for descarregado no dispositivo, e é direcionado com a política intune.
- O Navegador Gerido é lançado se apenas o Navegador Gerido estiver no dispositivo, e é direcionado com a política Intune.

No iOS/iPadOS, para apps que integraram o Intune SDK para iOS v. 9.0.9+:
- O Navegador Gerido Intune é lançado se tanto o Navegador Gerido como o Microsoft Edge estiverem no dispositivo.  
- O Microsoft Edge é lançado se apenas o Microsoft Edge estiver no dispositivo, e é direcionado com a política Intune.
- O Navegador Gerido é lançado se apenas o Navegador Gerido estiver no dispositivo, e é direcionado com a política Intune.

## <a name="configure-application-proxy-settings-for-microsoft-edge"></a>Configurar as definições de proxy de aplicação para o Microsoft Edge

Pode utilizar o Microsoft Edge e [o Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) em conjunto para dar aos utilizadores acesso a sites intranet nos seus dispositivos móveis. 

Estes são alguns exemplos dos cenários que o Proxy de Aplicação AD da Azure permite: 

- Um utilizador está a utilizar a aplicação móvel Outlook, que está protegida pela Intune. Em seguida, clicam num link para um site intranet num e-mail, e o Microsoft Edge reconhece que este site intranet foi exposto ao utilizador através do Proxy de Aplicação. O utilizador é automaticamente encaminhado através do Proxy de Aplicação, para autenticar com qualquer autenticação multifactor aplicável e acesso condicional, antes de chegar ao site intranet. O utilizador pode agora aceder a sites internos, mesmo nos seus dispositivos móveis, e o link no Outlook funciona como esperado.
- Um utilizador abre o Microsoft Edge no seu iOS ou dispositivo Android. Se o Microsoft Edge estiver protegido com o Intune e o Proxy da Aplicação estiver ativado, o utilizador pode ir a um site intranet utilizando o URL interno a que estão habituados. O Microsoft Edge reconhece que este site intranet foi exposto ao utilizador através do Proxy da Aplicação. O utilizador é automaticamente encaminhado através do Proxy de Aplicação, para autenticar antes de chegar ao site intranet. 

### <a name="before-you-start"></a>Antes de começar

- Instale as suas aplicações internas através do Proxy de Aplicação AD Azure.
  - Para configurar o Proxy de Aplicações e publicar aplicações, veja a [documentação de configuração](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).
- A aplicação Microsoft Edge deve ter a política de proteção de [aplicações Intune](app-protection-policy.md) atribuída.

> [!NOTE]
> Os dados atualizados de redirecionamento do Proxy de Aplicações podem demorar até 24 horas a entrar em vigor no Managed Browser e no Microsoft Edge.

#### <a name="step-1-enable-automatic-redirection-to-microsoft-edge-from-outlook"></a>Passo 1: Permitir a reorientação automática para o Microsoft Edge a partir do Outlook
Configure o Outlook com uma política de proteção de aplicações que permita a definição **de conteúdos web do Share com navegadores geridos por políticas.**

![Screenshot da política de proteção de aplicativos - Partilhe conteúdo web com navegadores geridos por políticas](./media/manage-microsoft-edge/manage-microsoft-edge-03.png)

#### <a name="step-2-set-the-app-configuration-setting-to-enable-app-proxy"></a>Passo 2: Definir a definição de configuração da aplicação para ativar o proxy da aplicação
Target Microsoft Edge com o seguinte par chave/valor, para ativar o Proxy de aplicação para o Microsoft Edge:

|    Chave    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    true    |

Para obter mais informações sobre como utilizar o Microsoft Edge e o Azure AD Application Proxy em conjunto para acesso perfeito (e protegido) a aplicações web no local, consulte [Better together: Intune and Azure Ative Directory team up to improve us access](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). Esta publicação de blog refere-se ao Navegador Gerido intune, mas o conteúdo também se aplica ao Microsoft Edge.

## <a name="configure-a-homepage-shortcut-for-microsoft-edge"></a>Configure um atalho inicial para o Microsoft Edge

Esta definição permite-lhe configurar um atalho inicial para o Microsoft Edge. O atalho inicial que configura ruma aparece como o primeiro ícone por baixo da barra de pesquisa quando o utilizador abre um novo separador no Microsoft Edge. O utilizador não pode editar ou apagar este atalho no seu contexto gerido. O atalho da página inicial mostra o nome da sua organização para distingui-lo. 

Utilize o seguinte par chave/valor para configurar um atalho inicial:

|    Chave    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Especifique um URL válido. Os URLs incorretos são bloqueados como medida de segurança.<br>**Exemplo:**  <`https://www.bing.com`>     |

## <a name="configure-multiple-top-site-shortcuts-for-new-tab-pages-in-microsoft-edge"></a>Configure vários atalhos de topo para novas páginas de separadores no Microsoft Edge 
Da mesma forma, configurar um atalho inicial, pode configurar vários atalhos de topo do site em novas páginas de separadores no Microsoft Edge. O utilizador não pode editar ou eliminar estes atalhos num contexto gerido. Nota: pode configurar um total de 8 atalhos, incluindo um atalho de página inicial. Se configurar um atalho inicial, isso irá anular o primeiro site de topo configurado. 

|    Chave    |    Valor    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    Especifique o conjunto de URLs de valor. Cada atalho do site superior consiste num título e URL. Separe o título e a URL com o carácter `|`. Por exemplo: <br> `GitHub | https://github.com/||LinkedIn|https://www.linkedin.com`    |

## <a name="configure-your-organizations-logo-and-brand-color-for-new-tab-pages-in-microsoft-edge"></a>Configure o logótipo da sua organização e a cor da marca para novas páginas de separadores no Microsoft Edge

Estas definições permitem personalizar a Nova Página de Separadores para o Microsoft Edge para mostrar o logótipo e a cor da marca da sua organização como o fundo da página.

Para fazer upload do logótipo e da cor da sua organização, complete primeiro os seguintes passos:
- Dentro do portal Azure, navegue para o centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) -> A Administração de **Inquilinos** -> **Branding e personalização** -> Marca de **Identidade da Empresa.**
- Para definir o logótipo da sua marca, em "Display", escolha "Apenas logotipo da empresa". Recomenda-se a consumação de logotipos de fundo transparentes. 
- Para definir a cor de fundo da sua marca, em "Display" escolha "Cor tema". O Microsoft Edge aplica um tom mais claro da cor na Página de Novos Separadores, que garante que a página tem uma alta legibilidade. 

Em seguida, utilize os seguintes pares chave/valor para puxar a marca das suas organizações para o Microsoft Edge:

|    Chave    |    Valor    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    Verdadeiro    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    Verdadeiro    |

## <a name="display-relevant-industry-news-on-new-tab-pages"></a>Mostrar notícias relevantes da indústria em Novas Páginas de Separadores

Pode configurar a experiência New Tab Page dentro do telemóvel do Microsoft Edge para mostrar notícias da indústria que são relevantes para a sua organização. Ao ativar esta funcionalidade, o Microsoft Edge mobile utiliza o nome de domínio da sua organização para agregar notícias da web sobre a sua organização, indústria da organização e concorrentes, para que os seus utilizadores possam encontrar notícias externas relevantes, todas a partir do novo centralizado páginas de separadores dentro do Microsoft Edge. O Industry News é desligado por defeito, e você pode usar para optar por ele para a sua organização. 

|    Chave    |    Valor    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **True** mostrará A Indústria Notícias na página móvel do Microsoft Edge New Tab Page.<p>**Falso** (padrão) esconderá notícias da indústria da página new tab.    |

## <a name="configure-managed-bookmarks-for-microsoft-edge"></a>Configure marcadores geridos para o Microsoft Edge

Para facilitar o acesso, pode configurar marcadores que gostaria que os seus utilizadores tivessem disponível quando estiverem a utilizar o Microsoft Edge. 

Aqui estão alguns detalhes:

- Estes marcadores só aparecem para os utilizadores quando estão a utilizar o [modo corporativo](https://docs.microsoft.com/intune/apps/app-configuration-managed-browser#how-to-configure-bookmarks-for-a-protected-browser) do Microsoft Edge. 
- Estes marcadores não podem ser eliminados ou modificados pelos utilizadores.
- Estes marcadores aparecem no topo da lista. Quaisquer marcadores que os utilizadores criem aparecem abaixo destes marcadores.
- Se tiver ativado a reorientação do Proxy de Aplicação, pode adicionar aplicações web proxy aplicação utilizando o seu URL interno ou externo.
- Certifique-se de que prefixa todos os URLs com **http://** ou **https://** ao inseri-los na lista.

Utilize o seguinte par chave/valor para configurar os marcadores geridos:

|    Chave    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    O valor para esta configuração é uma lista de marcadores. Cada marcador é composto pelo título de marcador e pelo URL do marcador. Separe o título e a URL com o carácter `|`.      Exemplo:<br>`Microsoft Bing|https://www.bing.com`<br>Para configurar vários marcadores, separe cada par com o carácter duplo `||`.<p>Exemplo:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

## <a name="display-myapps-within-microsoft-edge-bookmarks"></a>Exiba MyApps dentro dos favoritos do Microsoft Edge

Por padrão, os seus utilizadores são mostrados os sites MyApps que estão configurados dentro de uma pasta dentro dos marcadores do Microsoft Edge. A pasta está marcada com o nome da sua organização.

|    Chave    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **True** shows MyApps dentro dos bookmarks do Microsoft Edge.<p>**Falsas** ocultas MyApps dentro do Microsoft Edge.    |
    
## <a name="use-https-protocol-as-default"></a>Utilize o protocolo HTTPS como padrão

Pode configurar o microsoft Edge mobile para o padrão de utilização do protocolo HTTPS quando o utilizador não especificar um. Geralmente, esta é considerada uma boa prática. Utilize o seguinte par chave/valor para ativar https como o protocolo predefinido:

|    Chave    |    Valor    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.defaultHTTPS`     |     **True** define o protocolo padrão para usar HTTPS     |


## <a name="specify-allowed-or-blocked-sites-list-for-microsoft-edge"></a>Especificar lista de sites permitidos ou bloqueados para o Microsoft Edge
Pode utilizar a configuração da aplicação para definir quais os sites a que os seus utilizadores podem aceder quando utilizar o seu perfil de trabalho. Se utilizar uma lista de autorizações, os seus utilizadores só podem aceder aos sites que enumerou explicitamente. Se utilizar uma lista bloqueada, os seus utilizadores podem aceder a todos os sites, exceto aqueles que bloqueou explicitamente. Só deve impor uma lista permitida ou bloqueada, não as duas. Se impor os dois, a lista permitida é honrada.  

Utilize os seguintes pares de chaves/valor para configurar uma lista de site permitida ou bloqueada para o Microsoft Edge. 

|    Chave    |    Valor    |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Escolha entre:<p>1. Especificar URLs permitidos (apenas estes URLs são permitidos; nenhum outro sítio pode ser acedido):<br>`com.microsoft.intune.mam.managedbrowser.AllowListURLs`<p>2. Especificar URLs bloqueados (todos os outros sites podem ser acedidos):<br>`com.microsoft.intune.mam.managedbrowser.BlockListURLs`    |    O valor correspondente da chave é uma lista de URLs. Introduza todos os URLs que pretende permitir ou bloquear como um único valor, separados por um tubo `|` personagem.<br>**Exemplos:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`  |

### <a name="url-formats-for-allowed-and-blocked-site-list"></a>Formatos URL para lista de site permitido e bloqueado 
Pode utilizar vários formatos DE URL para construir as listas de sites permitidos/bloqueados. Estes padrões permitidos são detalhados na tabela seguinte. Algumas notas antes de começar: 
- Certifique-se de que prefixa todos os URLs com **http://** ou **https://** ao inseri-los na lista.
- Pode utilizar o símbolo wildcard (\*) de acordo com as regras da lista de padrões permitidas.
- Um wildcard só pode coincidir com um componente inteiro do nome de anfitrião (separado por períodos) ou partes inteiras do caminho (separados por cortes para a frente). Por exemplo, `http://*contoso.com` **não** é apoiado.
- Pode especificar os números da porta no endereço. Se não especificar um número da porta, os valores utilizados são:
  - Porta 80 para http
  - Porta 443 para https
- A utilização de wildcards para o número da porta **não** é suportada. Por exemplo, `http://www.contoso.com:*` e `http://www.contoso.com:*/` não são suportados. 

    |    URL    |    Detalhes    |    Correspondências    |    Não corresponde    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Corresponde a uma única página    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Corresponde a uma única página    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    Corresponde a todos os URLs que começam com `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Corresponde a todos os subdomínios em `contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Combina com todos os subdomínios que terminam com `contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
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

## <a name="transition-users-to-their-personal-context-when-trying-to-access-a-blocked-site"></a>Transferiu os utilizadores para o seu contexto pessoal ao tentar aceder a um site bloqueado

Com o modelo de dupla identidade integrado no Microsoft Edge, pode permitir uma experiência mais flexível para os seus utilizadores finais do que era possível com o Navegador Gerido Intune. Quando os utilizadores atingem um site bloqueado no Microsoft Edge, pode pedir-lhes que abram o link no seu contexto pessoal em vez do seu contexto de trabalho. Isto permite-lhes manter-se protegidos, mantendo os recursos corporativos seguros. Por exemplo, se um utilizador for enviado um link para um artigo de notícias através do Outlook, pode abrir o link no seu contexto pessoal ou num separador InPrivate. O seu contexto de trabalho não permite sites de notícias. Por defeito, estas transições são permitidas.

Utilize o seguinte par chave/valor para configurar se estas transições suaves são permitidas:

|    Chave    |    Valor    |
|-------------------------------------------------------------------|-------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock`    |    **True** (padrão) permite que o Microsoft Edge transe os utilizadores para o seu contexto pessoal para abrir sites bloqueados.<p>**Falso** impede o Microsoft Edge de transitar os utilizadores. Os utilizadores são simplesmente mostrados uma mensagem afirmando que o site a que estão a tentar aceder está bloqueado.    |

## <a name="disable-inprivate-and-microsoft-accounts-msa-to-restrict-personal-browsing"></a>Desativar contas inprivadas e microsoft (MSA) para restringir a navegação pessoal
Alguns clientes de indústrias altamente reguladas que estão a usar o Microsoft Edge podem querer pesquisar os utilizadores apenas no seu contexto AAD. Pode utilizar as seguintes definições de config de aplicação para desativar as Contas microsoft ou a navegação inPrivate.

|    Chave    |    Valor    |
|-------------------------------------------------------------------|-------------------------------------------------------|
|     `com.microsoft.intune.mam.managedbrowser.disabledFeatures`    |    **inprivate** irá desativar navegador InPrivate. <br> **A msa** irá desativar a capacidade dos utilizadores de adicionarem contas pessoais de MSA ao Microsoft Edge.<br> Para desativar as contas InPrivate e MSA, use `inprivate| msa`    |  


Caso não esteja a implementar políticas de proteção de aplicações, também pode restringir os utilizadores a utilizarem as Contas Microsoft e apenas permitir a navegação a partir de uma conta de trabalho ou de escola em dispositivos matriculados. Pode saber mais sobre as chaves para configurar o modo apenas para o Microsoft Edge aqui:
- [Android org-account](https://docs.microsoft.com/intune/apps/app-configuration-policies-use-android#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS org-accounts-only](https://docs.microsoft.com/intune/apps/app-configuration-policies-use-ios#allow-only-configured-organization-accounts-in-multi-identity-apps)

## <a name="open-restricted-links-directly-in-inprivate-tab-pages"></a>Abrir links restritos diretamente nas páginas de separadores InPrivate

Pode configurar se as ligações restritas devem ser abertas diretamente na navegação InPrivate, o que proporciona aos utilizadores uma experiência de navegação mais perfeita. Isto pouparia aos utilizadores o passo de terem de transitar para o seu contexto pessoal para verem um site. A navegação inPrivate é considerada não gerida, pelo que os utilizadores não poderão aceder ao modo de navegação InPrivate.  Nota: Para que esta definição tenha efeito, também deve ter configurado a definição acima `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock` **verdadeiramente**.

|    Chave    |    Valor    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked`    |    **True** abrirá automaticamente os sites diretamente num separador InPrivate, sem pedir ao utilizador que faça a troca para a sua conta pessoal. <p> **Falso** (predefinido) bloqueará o site dentro do Microsoft Edge e o utilizador será solicitado a mudar para a sua conta pessoal para visualizar.    |


## <a name="disable-microsoft-edge-features-to-customize-the-end-user-experience-for-your-organizations-needs"></a>Desative as funcionalidades do Microsoft Edge para personalizar a experiência final do utilizador para as necessidades da sua organização

### <a name="disable-prompts-to-share-usage-data-for-personalization"></a>Desativar as solicitações para partilhar dados de uso para personalização 

Por padrão, o Microsoft Edge solicita aos utilizadores a recolha de dados de utilização para personalizarem a sua experiência de navegação. É capaz de desativar a partilha destes dados evitando que esta solicitação seja mostrada aos utilizadores finais. 

|    Chave    |    Valor    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableShareUsageData`    |     **true** irá desativar esta solicitação de exibição para utilizadores finais.    |

### <a name="disable-prompts-to-share-browsing-history"></a>Desativar as solicitações para partilhar o histórico de navegação 

Por padrão, o Microsoft Edge solicita aos utilizadores que naveguem na recolha de dados de histórico para personalizarem a sua experiência de navegação. É capaz de desativar a partilha destes dados evitando que esta solicitação seja mostrada aos utilizadores finais.

|    Chave    |    Valor    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     `com.microsoft.intune.man.managedbrowser.disableShareBrowsingHistory`    |     **true** irá desativar esta solicitação de exibição para utilizadores finais.     |

### <a name="disable-prompts-that-offer-to-save-passwords"></a>Desativar as solicitações que oferecem para guardar senhas

Por padrão, o Microsoft Edge no iOS oferece-se para guardar as palavras-passe dos seus utilizadores para o porta-chaves. Se quiser desativar esta solicitação para a sua organização, configure a seguinte definição:

|    Chave    |    Valor    |
|-----------------------|-----------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableFeatures`    |    **a palavra-passe** irá desativar as solicitações que oferecem para guardar palavras-passe para o utilizador final.    |

### <a name="disable-inprivate-browsing-and-microsoft-accounts-to-restrict-browsing-to-work-only-contexts"></a>Desativar a navegação inPrivate e as Contas Microsoft para restringir a navegação a contextos apenas de trabalho

Se a sua organização operar numa indústria altamente regulada ou utilizar uma VPN por aplicação para permitir que os utilizadores acedam a recursos de trabalho com o Microsoft Edge, poderá optar por utilizar o Microsoft Edge apenas para um contexto protegido pelo MAM. Esta funcionalidade é fornecida apenas para dispositivos matriculados em MDM.

|    Chave    |    Valor    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.disableFeatures`    |    **inprivate** desativa a navegação inprivate, <br> **Msa** impede os utilizadores de adicionar as suas contas pessoais da Microsoft (MSA) às aplicações do Microsoft Edge. <br> Para desativar várias funcionalidades, separa maque-a com `|`. Por exemplo, `inprivate|msa` bloqueará contas privadas e pessoais.   |

### <a name="restrict-microsoft-edge-use-to-allowed-accounts-only"></a>Restringir o uso do Microsoft Edge apenas para contas permitidas

Além de bloquear a navegação inPrivate e MSA, só pode permitir a utilização do Microsoft Edge quando o utilizador estiver a iniciar sessão com a sua conta AAD. Esta funcionalidade só está disponível para utilizadores inscritos no MDM. Pode saber mais sobre configurar esta configuração aqui:

- [Configuração android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [definição de iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

## <a name="use-microsoft-edge-on-ios-to-access-managed-app-logs"></a>Use o Microsoft Edge no iOS para aceder a registos de aplicações geridos

Os utilizadores com o Microsoft Edge instalados no seu dispositivo iOS podem ver o estado de gestão de todas as aplicações publicadas pela Microsoft. Podem enviar registos para resolver problemas das respetivas aplicações iOS geridas. Eis como:

1. Abra o Microsoft Edge no seu dispositivo iOS.
2. Escreva `about:intunehelp` na caixa de endereço.
3. O Microsoft Edge lança o modo de resolução de problemas.

Para obter uma lista das definições armazenados nos registos das aplicações, veja [Review app protection logs in the Managed Browser (Rever os registos de proteção das aplicações no Managed Browser)](app-protection-policy-settings-log.md).

Para ver como visualizar registos em dispositivos Android, consulte [Enviar registos para o seu administrador de TI por e-mail](https://docs.microsoft.com/user-help/send-logs-to-your-it-admin-by-email-android).

## <a name="security-and-privacy-for-microsoft-edge"></a>Segurança e privacidade para microsoft Edge

Seguem-se considerações adicionais de segurança e privacidade para o Microsoft Edge:

- O Microsoft Edge não consome configurações que os utilizadores configuram para o navegador nativo https://docs.microsoft.com/en-us/intune/apps/app-configuration-policies-use-android#allow-only-configured-organization-accounts-in-multi-identity-apps nos seus dispositivos, porque o Microsoft Edge não consegue aceder a estas definições.
- Pode configurar a opção **Exigir UM PIN simples para acesso** ou exigir **credenciais corporativas para acesso** numa política de proteção de aplicações associada ao Microsoft Edge. Se um utilizador selecionar o link de ajuda na página de autenticação, pode navegar em quaisquer sites de internet, independentemente de terem sido adicionados a uma lista bloqueada na política.
- O Microsoft Edge só pode bloquear o acesso aos sites quando estes são acedidos diretamente. Não bloqueia o acesso quando os utilizadores utilizam serviços intermédios (como um serviço de tradução) para aceder ao site.
- Para permitir a autenticação e acesso à documentação Intune, * **.microsoft.com** está isento das definições da lista de permitir ou bloquear. É sempre permitido.
- Os utilizadores podem desativar a recolha de dados. A Microsoft recolhe automaticamente dados anónimos sobre o desempenho e a utilização do Managed Browser para melhorar os produtos e serviços Microsoft. Os utilizadores podem desativar a recolha de dados com a definição **Dados de Utilização** nos respetivos dispositivos. OS utilizadores não têm controlo sobre a recolha destes dados. Nos dispositivos iOS, os websites que os utilizadores visitam que tenham um certificado expirado ou não fidedigno não podem ser abertos.

## <a name="next-steps"></a>Próximos passos

- [O que são as políticas de proteção de aplicações?](app-protection-policy.md) 