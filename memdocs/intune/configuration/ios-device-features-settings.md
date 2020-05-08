---
title: Funcionalidades de dispositivos iOS/iPadOS no Microsoft Intune - Azure / Microsoft Docs
description: Consulte todas as definições para configurar dispositivos iOS e iPadOS para AirPrint, layout de ecrã principal, notificações de aplicações, dispositivos partilhados, definições de entrada única e filtro de conteúdo web no Microsoft Intune. Utilize estas definições num perfil de configuração do dispositivo para configurar dispositivos iOS/iPadOS para utilizar estas funcionalidades da Apple na sua organização.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fce26aab90989f31ee56a9abd58f617c780d9c4b
ms.sourcegitcommit: 0f02742301e42daaa30e1bde8694653e1b9e5d2a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82943880"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>Definições de dispositivos iOS e iPadOS para utilizar funcionalidades comuns do iOS/iPadOS em Intune

Intune inclui algumas definições incorporadas para permitir que os utilizadores de iOS/iPadOS utilizem diferentes funcionalidades da Apple nos seus dispositivos. Por exemplo, pode controlar impressoras AirPrint, adicionar apps e pastas às páginas do dock e do ecrã principal, mostrar notificações de apps, mostrar detalhes de etiquetas de ativo no ecrã de bloqueio, usar a autenticação de sinal único e usar a autenticação do certificado.

Utilize estas funcionalidades para controlar dispositivos iOS/iPadOS como parte da sua solução de gestão de dispositivos móveis (MDM).

Este artigo lista estas definições e descreve o que cada definição faz. Para mais informações sobre estas funcionalidades, vá a adicionar definições de funcionalidades de [dispositivos iOS/iPadOS ou macOS](device-features-configure.md).

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [funcionalidades de dispositivoiOS/iPadOS](device-features-configure.md).

> [!NOTE]
> Estas configurações aplicam-se a diferentes tipos de matrículas, com algumas definições aplicáveis a todas as opções de inscrição. Para obter mais informações sobre os diferentes tipos de matrículas, consulte a [inscrição do iOS/iPadOS.](../enrollment/ios-enroll.md)

## <a name="airprint"></a>Impressão Aérea

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

> [!NOTE]
> Certifique-se de adicionar todas as impressoras ao mesmo perfil. A Apple impede que vários perfis airPrint direcionem o mesmo dispositivo.

- **Endereço IP**: Introduza o endereço IPv4 ou IPv6 da impressora. Se utilizar nomes de anfitriões para identificar impressoras, pode obter o endereço IP pingando a impressora no terminal. Obtenha o endereço IP e o caminho (neste artigo) fornece mais detalhes.
- **Caminho**: O caminho `ipp/print` é normalmente para impressoras na sua rede. Obtenha o endereço IP e o caminho (neste artigo) fornece mais detalhes.
- **Porta**: Introduza a porta de escuta do destino AirPrint. Se deixar esta propriedade em branco, o AirPrint utiliza a porta predefinida. Disponível no iOS 11.0+, e iPadOS 13.0+.
- **TLS**: **Ativar** as ligações AirPrint com a Segurança da Camada de Transporte (TLS). Disponível no iOS 11.0+, e iPadOS 13.0+.

Para adicionar servidores AirPrint, pode:

- **Adicione** adiciona o servidor AirPrint à lista. Muitos servidores AirPrint podem ser adicionados.
- **Importar** um ficheiro separado de vírem (.csv) com esta informação. Ou **exportar** para criar uma lista dos servidores AirPrint que adicionou.

### <a name="get-server-ip-address-resource-path-and-port"></a>Obtenha endereço IP do servidor, caminho de recursos e porta

Para adicionar servidores AirPrinter, precisa do endereço IP da impressora, do caminho dos recursos e da porta. Os seguintes passos mostram-lhe como obter esta informação.

1. Num Mac que esteja ligado à mesma rede local (subnet) que as impressoras AirPrint, **terminal** aberto (de **/Aplicações/Utilitários).**
2. No Terminal, `ippfind`digite e selecione entrar.

    Repare na informação da impressora. Por exemplo, pode devolver `ipp://myprinter.local.:631/ipp/port1`algo semelhante a . A primeira parte é o nome da impressora. A última`ipp/port1`parte () é o caminho dos recursos.

3. No Terminal, `ping myprinter.local`digite e selecione entrar.

   Note o endereço IP. Por exemplo, pode devolver `PING myprinter.local (10.50.25.21)`algo semelhante a .

4. Utilize os valores do endereço IP e do caminho dos recursos. Neste exemplo, o endereço `10.50.25.21`IP é , `/ipp/port1`e o caminho dos recursos é .

## <a name="home-screen-layout"></a>Esquema do ecrã principal

Esta funcionalidade aplica-se a:

- iOS 9.3 ou mais recente
- iPadOS 13.0 e mais recente

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

### <a name="dock"></a>Doca

Utilize as definições **da Doca** para adicionar seis itens ou pastas à doca no ecrã. Muitos dispositivos suportam menos itens. Por exemplo, os dispositivos do iPhone suportam até quatro itens. Neste caso, apenas os quatro primeiros itens que adiciona são mostrados nos dispositivos.

Pode adicionar até **seis** itens (apps e pastas combinadas) para a doca do dispositivo.

- **Adicione**: Adicione aplicações ou pastas à doca em dispositivos.
- **Tipo:** Adicionar uma **app** ou uma **pasta:**

  - **App**: Escolha esta opção para adicionar aplicações à doca no ecrã. Introduza:

    - Nome da **aplicação**: Insira um nome para a aplicação. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager. *Não está* presente no dispositivo iOS/iPadOS.
    - Id do **pacote de aplicativos**: Introduza o id do pacote da aplicação. Consulte [iDs de pacote para aplicações incorporadas para iOS/iPadOS,](bundle-ids-built-in-ios-apps.md) para alguns exemplos.

  - **Pasta**: Escolha esta opção para adicionar uma pasta à doca no ecrã.

    As aplicações que adiciona a uma página numa pasta estão dispostas da esquerda para a direita e na mesma ordem que a lista. Se adicionar mais apps do que pode caber numa página, as aplicações são transferidas para outra página.

    - **Nome**da pasta : Introduza o nome da pasta. Este nome será apresentado nos dispositivos dos utilizadores.
    - **Lista de páginas**: **Adicione** uma página e introduza as seguintes propriedades:

      - **Nome da página**: Introduza um nome para a página. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager. *Não está* presente no dispositivo iOS/iPadOS.
      - Nome da **aplicação**: Insira um nome para a aplicação. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager. *Não está* presente no dispositivo iOS/iPadOS.
      - Id do **pacote de aplicativos**: Introduza o id do pacote da aplicação. Consulte [iDs de pacote para aplicações incorporadas para iOS/iPadOS,](bundle-ids-built-in-ios-apps.md) para alguns exemplos.

      Pode adicionar até **20** páginas para a doca do dispositivo.

> [!NOTE]
> Quando utiliza as definições de Layout do Ecrã Inicial para adicionar páginas, ou adicionar páginas e aplicações à Doca, os ícones no Ecrã Principal e páginas estão bloqueados. Não podem ser movidos ou apagados. Este comportamento pode ser por design com as políticas do iOS/iPadOS e do MDM da Apple.

#### <a name="example"></a>Exemplo

No exemplo seguinte, o ecrã da doca mostra as aplicações Safari, Mail e Stocks. A aplicação Mail é selecionada para mostrar as suas propriedades:

> [!div class="mx-imgBorder"]
> ![Experimente as definições da doca de layout do ecrã principal iOS/iPadOS em Intune](./media/ios-device-features-settings/dock-screen-mail-app.png)

Ao atribuir a apólice a um iPhone, a doca parece semelhante à seguinte imagem:

> [!div class="mx-imgBorder"]
> ![Prove iOS/iPadOS do tacho da doca no iPhone](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>Páginas

Adicione as páginas que deseja mostradas no ecrã principal e as aplicações que pretende mostrar em cada página. As aplicações que adiciona a uma página estão dispostas da esquerda para a direita, na mesma ordem que a lista. Se adicionar mais apps do que pode caber numa página, as aplicações são transferidas para outra página.

> [!TIP]
> Para reencomendar itens em qualquer ecrã Principal e listas de páginas, pode arrastá-los e deixá-los cair.

Pode adicionar até **40** páginas num dispositivo.

- **Lista de páginas**: **Adicione** uma página e introduza as seguintes propriedades:

  - **Nome da página**: Introduza um nome para a página. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager, e *não está* mostrado no dispositivo iOS/iPadOS.

  Pode adicionar até **60** itens (apps e pastas combinadas) num dispositivo.

  - **Adicionar**: Adicione aplicações ou pastas a uma página nos dispositivos.

    - **Tipo:** Adicionar uma **app** ou uma **pasta:**

      - **App**: Escolha esta opção para adicionar apps a uma página no ecrã. Introduza também:

        - Nome da **aplicação**: Insira um nome para a aplicação. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager. *Não está* presente no dispositivo iOS/iPadOS.
        - Id do **pacote de aplicativos**: Introduza o id do pacote da aplicação. Consulte [iDs de pacote para aplicações incorporadas para iOS/iPadOS,](bundle-ids-built-in-ios-apps.md) para alguns exemplos.

      - **Pasta**: Escolha esta opção para adicionar uma pasta à doca no ecrã.

        As aplicações que adiciona a uma página numa pasta estão dispostas da esquerda para a direita e na mesma ordem que a lista. Se adicionar mais apps do que pode caber numa página, as aplicações são transferidas para outra página.

        - **Nome**da pasta : Introduza um nome para a pasta. Este nome é mostrado aos utilizadores em dispositivos.
        - **Adicionar**: Adicionar páginas à pasta. Introduza também as seguintes propriedades:

          - **Nome da página**: Introduza um nome para a página. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager. *Não está* presente no dispositivo iOS/iPadOS.
          - Nome da **aplicação**: Insira um nome para a aplicação. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager. *Não está* presente no dispositivo iOS/iPadOS.
          - Id do **pacote de aplicativos**: Introduza o id do pacote da aplicação. Consulte [iDs de pacote para aplicações incorporadas para iOS/iPadOS,](bundle-ids-built-in-ios-apps.md) para alguns exemplos.

#### <a name="example"></a>Exemplo

No exemplo seguinte, é adicionada uma nova página chamada **Contoso.** A página mostra as aplicações Find Friends and Settings:

> [!div class="mx-imgBorder"]
> ![iOS/iPadOS Configurações de nova página e exemplo em Intune](./media/ios-device-features-settings/page-find-friends-settings-apps.png)

A aplicação Definições é selecionada para mostrar as suas propriedades:

> [!div class="mx-imgBorder"]
> ![layout de ecrã inicial iOS/iPadOS Configurações de aplicações exemplo em Intune](./media/ios-device-features-settings/page-settings-app-properties.png)

Ao atribuir a apólice a um iPhone, a página parece semelhante à seguinte imagem:

> [!div class="mx-imgBorder"]
> ![dispositivo iOS/iPadOS com ecrã principal modificado em Intune](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>Notificações de aplicação

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Adicionar**: Adicionar notificações para apps:

  > [!div class="mx-imgBorder"]
  > ![Adicione notificação de aplicativo no perfil iOS/iPadOS em Intune](./media/ios-device-features-settings/ios-ipados-app-notifications.png)

  - Id pacote **de aplicativos**: Introduza o Id do Pacote de **Aplicações** da app que pretende adicionar. Consulte [iDs de pacote para aplicações incorporadas para iOS/iPadOS,](bundle-ids-built-in-ios-apps.md) para alguns exemplos.
  - Nome da **aplicação**: Introduza o nome da aplicação que pretende adicionar. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager. *Não é* mostrado nos dispositivos.
  - **Editor**: Insira o editor da app que está a adicionar. Este nome é utilizado para a sua referência no centro de administração do Microsoft Endpoint Manager. *Não é* mostrado nos dispositivos.
  - **Notificações**: **Ativar** ou **desativar** a aplicação do envio de notificações para dispositivos.
    - **Mostrar no Centro**de Notificações : **Ativar** permite que a aplicação mostre notificações no Centro de Notificação do dispositivo. **Desativar** impede que a aplicação apareça notificações no Centro de Notificação.
    - **Mostra no Ecrã de Bloqueio**: **Ativar** mostra notificações de aplicações no ecrã de bloqueio do dispositivo. **Desativar** impede que a aplicação apareça notificações no ecrã de bloqueio.
    - **Tipo**de alerta : Quando os dispositivos estiverem desbloqueados, escolha como a notificação é mostrada. As opções são:
      - **Nenhuma**: Não é mostrada nenhuma notificação.
      - **Banner**: Um banner é brevemente mostrado com a notificação.
      - **Modal**: A notificação é mostrada e os utilizadores devem descartá-la manualmente antes de continuar a utilizar o dispositivo.
    - **Crachá no ícone da aplicação**: Selecione **Ativar** para adicionar um crachá ao ícone da aplicação. O crachá significa que a aplicação enviou uma notificação.
    - **Sons**: **Selecione Ativar** para reproduzir um som quando uma notificação for entregue.

## <a name="lock-screen-message"></a>Mensagem de tela de bloqueio

Esta funcionalidade aplica-se a:

- iOS 9.3 e posterior
- iPadOS 13.0 e mais recente

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Informações**sobre etiquetas de ativo : Introduza informações sobre a etiqueta de ativo do dispositivo. Por exemplo, introduza: `Owned by Contoso Corp` ou `Serial Number: {{serialnumber}}`.

  O texto em que introduz é mostrado no sinal na janela e no ecrã de bloqueio nos dispositivos.

- **Nota**de rodapé do ecrã de bloqueio : Se os dispositivos forem perdidos ou roubados, introduza uma nota que possa ajudar a retornar o dispositivo. Pode introduzir qualquer texto que quiser. Por exemplo, introduza algo como `If found, call Contoso at ...`.

  As fichas do dispositivo também podem ser usadas para adicionar informações específicas do dispositivo a estes campos. Por exemplo, para mostrar o `Serial Number: {{serialnumber}}`número de série, insira . No ecrã de bloqueio, o `Serial Number 123456789ABC`texto mostra semelhante a . Ao introduzir variáveis, certifique-se de `{{ }}`que utiliza suportes encaracolados . [Os tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) de configuração da aplicação incluem uma lista de variáveis que podem ser usadas. Também pode `deviceName` utilizar ou qualquer outro valor específico do dispositivo.

  > [!NOTE]
  > As variáveis não são validadas na UI, e são sensíveis ao caso. Como resultado, pode ver perfis guardados com entrada incorreta. Por exemplo, se `{{DeviceID}}` introduzir `{{deviceid}}`em vez de , então a corda literal é mostrada em vez do ID único do dispositivo. Certifique-se de introduzir a informação correta.

## <a name="single-sign-on"></a>Início de sessão único

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Reino**: Introduza a parte de domínio do URL. Por exemplo, introduza `contoso.com`.
- Nome principal de **Kerberos**: Intune procura este atributo para cada utilizador em Azure AD. Intonou então o respetivo campo (como upn) antes de gerar o XML que é instalado em dispositivos. As opções são:

  - **Não configurado**: Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA irá solicitar aos utilizadores um nome principal da Kerberos quando o perfil for implantado nos dispositivos. É necessário um nome principal para que os MDMs instalem perfis SSO.
  - **Nome principal do utilizador**: O nome principal do utilizador (UPN) é analisado da seguinte forma:

    > [!div class="mx-imgBorder"]
    > ![iOS/iPadOS Username SSO atribui em Intune](./media/ios-device-features-settings/User-name-attribute.png)

    Também pode substituir o âmbito pelo texto que introduzir na caixa de texto **Âmbito**.

    Por exemplo, Contoso tem várias regiões, incluindo a Europa, Ásia e América do Norte. Contoso quer que os seus utilizadores asiáticos utilizem O SSO, e a aplicação requer a UPN no `username@asia.contoso.com` formato. Quando seleciona o Nome Principal do **Utilizador,** o reino para `contoso.com`cada utilizador é retirado do Azure AD, que é . Assim, para os utilizadores na Ásia, `asia.contoso.com`selecione User Principal **Name**, e introduza . A UPN do `username@asia.contoso.com`utilizador torna-se, em vez de `username@contoso.com`.

  - **ID do dispositivo insintonizado**: Insinto automaticamente seleciona o ID do dispositivo intune.

    Por predefinição, as aplicações só precisam de utilizar o ID do dispositivo. No entanto, se a sua aplicação utilizar o âmbito e o ID do dispositivo, pode escrever o âmbito na caixa de texto **Âmbito**.

    > [!NOTE]
    > Por predefinição, mantenha o âmbito em branco se utilizar o ID do dispositivo.

  - **ID do dispositivo Azure AD**
  - Nome da **conta SAM**: Intune preenche o nome da conta Do Gestor de Contas de Segurança (SAM) no local.


- **Apps**: **Adicione** aplicações em dispositivos utilizadores que podem usar um único sinal.

  A `AppIdentifierMatches` matriz deve incluir cordas que correspondam a iDs de pacote de aplicativos. Estas cordas podem ser correspondências `com.contoso.myapp`exatas, tais como, ou introduzir \* uma correspondência de prefixo no id do pacote utilizando o caracteres wildcard. O carácter wildcard deve aparecer após um carácter de período (.), e pode `com.contoso.*`aparecer apenas uma vez, no final da corda, como . Quando um caráter universal é incluído, todas as aplicações cujo ID da coleção de pacotes começa com o prefixo têm acesso à conta.

  Utilize o **Nome da Aplicação** para introduzir um nome simples, para o ajudar a identificar o ID do pacote.

- **Prefixos de URL**: **Adicione** quaisquer URLs na sua organização que exijam a autenticação de inscrição única do utilizador.

  Por exemplo, quando um utilizador se conecta a qualquer um destes sites, o dispositivo iOS/iPadOS utiliza as credenciais de inscrição únicas. Os utilizadores não precisam de introduzir credenciais adicionais. Se a autenticação de vários fatores estiver ativada, então os utilizadores são obrigados a introduzir a segunda autenticação.

  > [!NOTE]
  > Estes URLs têm de ter um FQDN formatado adequadamente. A Apple exige que `http://<yourURL.domain>` estes estejam no formato.

  Os padrões de correspondências do URL têm de começar com `http://` ou `https://`. Uma simples combinação de cordas `http://www.contoso.com/` é executada, por `http://www.contoso.com:80/`isso o prefixo URL não corresponde a . Com iOS 10.0+ e iPadOS 13.0+, um único wildcard \* pode ser usado para introduzir todos os valores correspondentes. Por exemplo, `http://*.contoso.com/` `http://store.contoso.com/` corresponde `http://www.contoso.com`tanto a ambos como .

  Os `http://.com` `https://.com` padrões e padrões combinam com todos os URLs HTTP e HTTPS, respectivamente.

- **Certificado de renovação**: Se utilizar certificados para autenticação (não palavras-passe), selecione o certificado SCEP ou PFX existente como certificado de autenticação. Normalmente, este certificado é o mesmo certificado que é implantado para utilizadores para outros perfis, tais como VPN, Wi-Fi ou e-mail.

## <a name="web-content-filter"></a>Filtro de conteúdo web

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Tipo de filtro**: Escolha permitir web sites específicos. As opções são:

  - **Configure URLs**: Use o filtro web incorporado da Apple que procura termos para adultos, incluindo profanação e linguagem sexualmente explícita. Esta funcionalidade avalia cada página web à medida que é carregada, e identifica e bloqueia conteúdo inadequado. Também pode adicionar URLs que não quer verificados pelo filtro. Ou bloquear URLs específicos, independentemente das definições de filtro da Apple.

    - **URLs permitidos**: **Adicione** os URLs que pretende permitir. Estes URLs contornam o filtro web da Apple.

        > [!NOTE]
        > Os URLs que você insere são os URLs que você não quer evauluado pelo filtro web apple. Estes URLs não são uma lista de sites permitidos. Para criar uma lista de websites permitidos, detete o **Tipo de Filtro** para sites **específicos apenas.**

    - **URLs bloqueados**: **Adicione** os URLs que pretende parar de abrir, independentemente das definições do filtro web da Apple.

  - **Websites específicos apenas** (apenas para o navegador Web Safari): Estes URLs são adicionados aos marcadores do navegador Safari. Os utilizadores **só** podem visitar estes sites; nenhum outro sítio pode ser aberto. Utilize esta opção apenas se souber a lista exata de URLs aos quais os utilizadores podem aceder.

    - **URL**: Introduza o URL do site que pretende permitir. Por exemplo, introduza `https://www.contoso.com`.
    - **Bookmark Path**: A Apple alterou esta definição. Todos os marcadores vão para a pasta **Sites Aprovados.** Os marcadores não entram no caminho do marcador.
    - **Título**: Introduza um título descritivo para o marcador.

    Se não introduzir nenhum URLs, então os utilizadores não `microsoft.com`podem `microsoft.net`aceder `apple.com`a nenhum website exceto , e . Estes URLs são automaticamente permitidos pela Intune.

## <a name="single-sign-on-app-extension"></a>Extensão única da aplicação de inscrição

Esta funcionalidade aplica-se a:

- iOS 13.0 e mais tarde
- iPadOS 13.0 e mais tarde

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Tipo de extensão da aplicação SSO:** Escolha o tipo de extensão da aplicação SSO. As opções são:

  - **Não configurado**: Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA não utilizará extensões de aplicações. Para desativar uma extensão da aplicação, pode mudar o tipo de extensão da aplicação SSO para **Não configurado**.
  - **Microsoft Azure AD**: Utiliza o plug-in Microsoft Enterprise SSO, que é uma extensão de aplicação SSO do tipo redireccionador. Este plug-in fornece contas SSO para Diretório Ativo em todas as aplicações que suportam a funcionalidade [Enterprise Single Sign-On da Apple.](https://developer.apple.com/documentation/authenticationservices) Utilize este tipo de extensão de aplicações SSO para permitir o SSO em aplicações da Microsoft, aplicações de organização e websites que autenticam usando o Azure AD.

    O plug-in SSO funciona como um corretor de autenticação avançado que oferece melhorias na segurança e na experiência do utilizador. Todas as aplicações que usaram anteriormente a autenticação intermediada com a aplicação Microsoft Authenticator continuam a obter SSO com o [plug-in Microsoft Enterprise SSO para dispositivos Apple](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin).

    > [!IMPORTANT]
    > Para obter o SSO com o tipo de extensão da aplicação Microsoft Azure AD SSO, instale primeiro a aplicação iOS/iPadOS Microsoft Authenticator nos dispositivos. A aplicação Authenticator fornece o plug-in Microsoft Enterprise SSO aos dispositivos, e as definições de extensão da aplicação MDM SSO ativam o plug-in. Assim que o Autenticador e o perfil de extensão da aplicação SSO estiverem instalados nos dispositivos, os utilizadores devem introduzir as suas credenciais para iniciar sessão e estabelecer uma sessão nos seus dispositivos. Esta sessão é então utilizada em diferentes aplicações sem exigir que os utilizadores voltem a autenticar. Para mais informações sobre o Autenticador, consulte [o que é a aplicação Autenticadora Microsoft](https://docs.microsoft.com/azure/active-directory/user-help/user-help-auth-app-overview).

  - **Redirecionamento**: Utilize uma extensão de aplicação de redirecionamento genérica e personalizável para utilizar o SSO com fluxos de autenticação modernos. Certifique-se de que conhece o ID de extensão para a extensão da aplicação da sua organização.
  - **Credencial**: Utilize uma extensão de aplicação credencial genérica e personalizável para utilizar o SSO com fluxos de autenticação de desafio e resposta. Certifique-se de que conhece o ID de extensão para a extensão da aplicação da sua organização.
  - **Kerberos**: Use a extensão Kerberos incorporada da Apple, que está incluída no iOS 13.0+ e iPadOS 13.0+. Esta opção é uma versão específica da Extensão da aplicação **Credencial** da Kerberos.

  > [!TIP]
  > Com os tipos **Redirecionamento** e **Credenciais,** adicione os seus próprios valores de configuração para passar pela extensão. Se estiver a utilizar o **Credential,** considere utilizar as configurações de configuração incorporadas fornecidas pela Apple no tipo **Kerberos.**

- **Modo de dispositivo partilhado** (apenas Microsoft Azure AD): Escolha **o Enable** se estiver a implementar o plug-in Microsoft Enterprise SSO para dispositivos iOS/iPadOS configurados para a funcionalidade de modo de dispositivo partilhado da Azure AD. Os dispositivos em modo partilhado permitem que muitos utilizadores inscretem globalmente as aplicações que suportam o modo de dispositivo partilhado. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição. Por padrão, os dispositivos iOS/iPadOS não se destinam a ser partilhados entre vários utilizadores.

  Para obter mais informações sobre o modo de dispositivo partilhado e como o ativar, consulte a [visão geral do modo de dispositivo partilhado](https://docs.microsoft.com/azure/active-directory/develop/msal-shared-devices) e o modo de dispositivo partilhado para [dispositivos iOS](https://docs.microsoft.com/azure/active-directory/develop/msal-ios-shared-devices).  

- **ID de extensão** (Redirecionamento e Credencial): Introduza o identificador `com.apple.extensiblesso`de pacote que identifica a extensão da sua aplicação SSO, como .

- **ID da equipa** (Redirecionamento e Credencial): Introduza o identificador de equipa da extensão da sua aplicação SSO. Um identificador de equipa é uma cadeia alfanumérica de 10 caracteres `ABCDE12345`(números e letras) gerada pela Apple, como . A identificação da equipa não é necessária.

  [Localizar o seu Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (abre o site da Apple) tem mais informações.

- **Reino** (Credencial e Kerberos): Introduza o nome do seu reino de autenticação. O nome do reino deve ser `CONTOSO.COM`capitalizado, como. Tipicamente, o seu nome de reino é o mesmo que o seu nome de domínio DNS, mas em todas as maiúsculas.

- **Domínios** (Credential e Kerberos): Introduza o domínio ou nomes de anfitriões dos sites que podem autenticar através do SSO. Por exemplo, se `mysite.contoso.com`o `mysite` seu website é `contoso.com` , então é o nome do anfitrião, e é o nome de domínio. Quando os utilizadores se ligam a qualquer um destes sites, a extensão da aplicação trata do desafio de autenticação. Esta autenticação permite que os utilizadores utilizem o Face ID, touch ID ou Apple pincode/código de acesso para iniciar sessão.

  - Todos os domínios da sua única extensão de aplicação de início de sessão Os perfis Intune devem ser únicos. Não é possível repetir um domínio em qualquer perfil de extensão de aplicações de início de sessão, mesmo que esteja a utilizar diferentes tipos de extensões de aplicações SSO.
  - Estes domínios não são sensíveis a casos.

- **URLs** (apenas redirecionamento): Introduza os prefixos URL dos seus fornecedores de identidade em nome de quem a extensão da aplicação de redirecionamento utiliza SSO. Quando os utilizadores são redirecionados para estes URLs, a extensão da aplicação SSO intervém e solicita sSO.

  - Todos os URLs nos seus perfis de extensão de aplicações intune devem ser únicos. Não é possível repetir um domínio em qualquer perfil de extensão de aplicações SSO, mesmo que esteja a utilizar diferentes tipos de extensões de aplicações SSO.
  - Os URLs devem `http://` `https://`começar com ou .

- **Configuração adicional** (Microsoft Azure AD, Redirect e Credential): Introduza dados adicionais específicos de extensão para passar para a extensão da aplicação SSO:
  - **Chave**: Introduza o nome do item `user name`que pretende adicionar, como .
  - **Tipo**: Introduza o tipo de dados. As opções são:

    - String
    - Boolean: No valor `True` de `False` **configuração,** insira ou .
    - Integer: No valor de **configuração,** introduza um número.

  - **Valor**: Introduza os dados.

  - **Adicione**: Selecione para adicionar as suas chaves de configuração.

- **Utilização** em cadeia de chaves (apenas Kerberos): **O bloco** impede que as palavras-passe sejam guardadas e armazenadas no porta-chaves. Se bloqueados, os utilizadores não são solicitados a guardar a sua palavra-passe e precisam de reintroduzir a palavra-passe quando o bilhete Kerberos expirar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que as palavras-passe sejam guardadas e armazenadas no porta-chaves. Os utilizadores não são solicitados a reintroduzir a sua palavra-passe quando o bilhete expirar.
- **Id do rosto, Touch ID ou código de acesso** (apenas Kerberos): **Exigir** que os utilizadores introduzam o seu ID facial, touch ID ou código de acesso do dispositivo quando a credencial é necessária para refrescar o bilhete Kerberos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode não exigir que os utilizadores utilizem a biometria ou a senha do dispositivo para atualizar o bilhete Kerberos. Se o uso do **Keychain** estiver bloqueado, esta definição não se aplica.
- **Reino padrão** (apenas Kerberos): **Ativar** define o valor do **Reino** que introduziu como o reino padrão. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode não definir um reino padrão.

  > [!TIP]
  > - **Ative** esta definição se estiver a configurar várias extensões de aplicações Kerberos SSO na sua organização.
  > - **Ative** esta definição se estiver a utilizar vários reinos. Define o valor do **Reino** que introduziu como o reino padrão.
  > - Se tiver apenas um reino, deixe-o **não configurado** (predefinido).

- **Nome principal** (apenas Kerberos): Introduza o nome de utilizador do diretor kerberos. Não precisas de incluir o nome do reino. Por exemplo, `user@contoso.com` `user` em , é `contoso.com` o nome principal, e é o nome do reino.

  > [!TIP]
  > - Também pode utilizar variáveis no nome principal, entrando em suportes `{{ }}`encaracolados . Por exemplo, para mostrar o `Username: {{username}}`nome de utilizador, introduza . 
  > - No entanto, tenha cuidado com a substituição variável porque as variáveis não são validadas na UI e são sensíveis ao caso. Certifique-se de introduzir a informação correta.

- Código de **site de Diretório Ativo** (apenas Kerberos): Introduza o nome do site Ative Directory que a extensão Kerberos deve utilizar. Pode não precisar de alterar este valor, uma vez que a extensão Kerberos pode automaticamente encontrar o código do site do Ative Directory.
- **Nome cache** (apenas Kerberos): Introduza o nome genérico de serviços de segurança (GSS) da cache Kerberos. Provavelmente não precisa definir este valor.
- **IDs** de pacote de aplicativos (apenas Kerberos): **Adicione** os identificadores de pacote de aplicativos que devem usar um único sinal nos seus dispositivos. Estas aplicações têm acesso ao Bilhete de Concessão de Bilhetes Kerberos, ao bilhete de autenticação e autenticam os utilizadores aos serviços a que estão autorizados a aceder.
- **Mapeamento** do domínio (apenas Kerberos): **Adicione** os sufixos dNS de domínio que devem mapear para o seu reino. Use este cenário quando os nomes DNS dos anfitriões não corresponderem ao nome do reino. Provavelmente não precisa de criar este mapeamento personalizado domínio-realm.
- **Certificado PKINIT** (apenas Kerberos): **Selecione** o certificado de criptografia de chave pública para autenticação inicial (PKINIT) que pode ser usado para autenticação Kerberos. Pode escolher entre os certificados [PKCS](../protect/certficates-pfx-configure.md) ou [SCEP](../protect/certificates-scep-configure.md) que adicionou no Intune. Para obter mais informações sobre certificados, consulte [Utilize certificados para autenticação no Microsoft Intune](../protect/certificates-configure.md).

## <a name="wallpaper"></a>Padrão de Fundo

Pode experimentar um comportamento inesperado quando um perfil sem imagem é atribuído a dispositivos com uma imagem existente. Por exemplo, cria-se um perfil sem imagem. Este perfil é atribuído a dispositivos que já tenham uma imagem. Neste cenário, a imagem pode mudar para a predefinição do dispositivo, ou a imagem original pode permanecer no dispositivo. Este comportamento é controlado e limitado pela plataforma MDM da Apple.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Localização do ecrã do papel de parede**: Escolha uma localização nos dispositivos para mostrar a imagem. As opções são:
  - **Não configurado**: Intune não altera nem atualiza esta definição. Uma imagem personalizada não é adicionada aos dispositivos. Por padrão, o SISTEMA pode definir a sua própria imagem.
  - **Ecrã de bloqueio**: Adiciona a imagem ao ecrã de bloqueio.
  - **Ecrã principal**: Adiciona a imagem ao ecrã principal.
  - **Ecrã de bloqueio e ecrã principal**: Utiliza a mesma imagem no ecrã de bloqueio e no ecrã principal.
- **Imagem de papel de parede:** Faça upload de uma imagem .png, .jpg ou .jpeg existente que queira utilizar. Certifique-se de que o tamanho do ficheiro é inferior a 750 KB. Também pode **remover** uma imagem que acrescentou.

> [!TIP]
> Para exibir diferentes imagens no ecrã de bloqueio e no ecrã principal, crie um perfil com a imagem do ecrã de bloqueio. Crie outro perfil com a imagem do ecrã principal. Atribua ambos os perfis aos grupos de utilizadores ou dispositivos iOS/iPadOS.

## <a name="next-steps"></a>Passos seguintes

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode criar perfis de funcionalidades de dispositivos para dispositivos [macOS.](macos-device-features-settings.md)
