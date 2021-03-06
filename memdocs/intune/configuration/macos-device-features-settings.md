---
title: as definições de funcionalidades do dispositivo macOS no Microsoft Intune - Azure / Microsoft Docs
description: Consulte as definições para configurar dispositivos macOS para AirPrint e personalize a janela de Login para mostrar ou ocultar botões de energia no Microsoft Intune. Consulte os passos para obter as definições de endereço IP, caminho e porta de um servidor AirPrint na sua rede. Utilize estas definições num perfil de configuração do dispositivo para configurar as funcionalidades do dispositivo macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d4bc2de9e16cfcf9322cf343badafe3c9a35c70
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428909"
---
# <a name="macos-device-feature-settings-in-intune"></a>funcionalidade do dispositivo macOS em Intune

Intune inclui configurações incorporadas para personalizar funcionalidades nos seus dispositivos macOS. Por exemplo, os administradores podem adicionar impressoras AirPrint, escolher como os utilizadores entram, configurar os controlos de energia, usar a autenticação de entrada única e muito mais.

Utilize estas funcionalidades para controlar dispositivos macOS como parte da sua solução de gestão de dispositivos móveis (MDM).

Este artigo lista estas definições e descreve o que cada definição faz. Também lista os passos para obter o endereço IP, caminho e impressoras porta de AirPrint usando a aplicação Terminal (emulador). Para obter mais informações sobre as funcionalidades do dispositivo, vá a adicionar definições de funcionalidades de [dispositivos iOS/iPadOS ou macOS](device-features-configure.md).

> [!NOTE]
> A interface do utilizador não pode corresponder aos tipos de inscrição deste artigo. A informação neste artigo está correta. A interface do utilizador está a ser atualizada num próximo lançamento.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de funcionalidades do [dispositivo macOS](device-features-configure.md).

> [!NOTE]
> Estas configurações aplicam-se a diferentes tipos de matrículas, com algumas definições aplicáveis a todas as opções de inscrição. Para obter mais informações sobre os diferentes tipos de matrículas, consulte a [inscrição do macOS.](../enrollment/macos-enroll.md)

## <a name="airprint"></a>Impressão Aérea

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Destinos AirPrint**: **Adicione** uma ou mais impressoras AirPrint que os utilizadores podem imprimir a partir dos seus dispositivos. Introduza também:
  - **Porta** (iOS 11.0+, iPadOS 13.0+): Introduza a porta de escuta do destino AirPrint. Se deixar esta propriedade em branco, o AirPrint utiliza a porta predefinida.
  - **Endereço IP**: Introduza o endereço IPv4 ou IPv6 da impressora. Por exemplo, introduza `10.0.0.1`. Se utilizar os nomes do anfitrião para identificar impressoras, pode obter o endereço IP através do pingping da impressora na aplicação Terminal. [Obtenha o endereço IP e o caminho](#get-the-ip-address-and-path) (neste artigo) tem mais detalhes.
  - **Caminho**: Introduza o caminho de recursos da impressora. O caminho é normalmente `ipp/print` para impressoras na sua rede. [Obtenha o endereço IP e o caminho](#get-the-ip-address-and-path) (neste artigo) tem mais detalhes.
  - **TLS** (iOS 11.0+, iPadOS 13.0+): As suas opções:
    - **Não** (padrão): A Segurança da Camada de Transporte (TLS) não é aplicada quando se conecta com impressoras AirPrint.
    - **Sim:** Assegura ligações AirPrint com segurança da camada de transporte (TLS).

- **Importar** um ficheiro separado de vírvias (.csv) que inclua uma lista de impressoras AirPrint. Além disso, depois de adicionar impressoras AirPrint em Intune, pode **exportar** esta lista.

### <a name="get-the-ip-address-and-path"></a>Obtenha o endereço IP e o caminho

Para adicionar servidores AirPrinter, precisa do endereço IP da impressora, do caminho dos recursos e da porta. Os seguintes passos mostram-lhe como obter esta informação.

1. Num Mac que esteja ligado à mesma rede local (subnet) que as impressoras AirPrint, **terminal** aberto (de **/Aplicações/Utilitários).**
2. Na aplicação Terminal, `ippfind` digite e selecione entrar.

    Repare na informação da impressora. Por exemplo, pode devolver algo semelhante a `ipp://myprinter.local.:631/ipp/port1` . A primeira parte é o nome da impressora. A última parte `ipp/port1` () é o caminho dos recursos.

3. No Terminal, `ping myprinter.local` digite e selecione entrar.

   Note o endereço IP. Por exemplo, pode devolver algo semelhante a `PING myprinter.local (10.50.25.21)` .

4. Utilize os valores do endereço IP e do caminho dos recursos. Neste exemplo, o endereço IP é `10.50.25.21` , e o caminho dos recursos é `/ipp/port1` .

## <a name="associated-domains"></a>Domínios associados

Em Intune, pode:

- Adicione muitas associações app-to-domain.
- Associe muitos domínios com a mesma app.

Esta funcionalidade aplica-se a:

- macOS 10.15 e mais recente

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>As definições aplicam-se a: Inscrição do dispositivo aprovado pelo utilizador e inscrição automática do dispositivo

- **Domínios associados**: **Adicione** uma associação entre o seu domínio e uma app. Esta funcionalidade partilha o sinal de credenciais entre uma app Contoso e um website Contoso. Introduza também:

  - Id da **aplicação**: Introduza o identificador de aplicações da app para se associar a um website. O identificador de aplicações inclui o ID da equipa e um id de pacote: `TeamID.BundleID` .

    O ID da equipa é uma cadeia alfanumérica de 10 caracteres (letras e números) gerada pela Apple para os desenvolvedores de aplicações, tais como `ABCDE12345` . [Localize o seu ID](https://help.apple.com/developer-account/#/dev55c3c710c)   da equipa (abre o site da Apple) tem mais informações.

    O id do pacote identifica exclusivamente a app, e tipicamente é formatado em notação de nome de domínio invertido. Por exemplo, o id de pacote do Finder é `com.apple.finder` . Para encontrar o ID do pacote, utilize o AppleScript no Terminal:

    `osascript -e 'id of app "ExampleApp"'`

  - **Domínio**: Insira o domínio do site para se associar a uma aplicação. O domínio inclui um tipo de serviço e um nome de anfitrião totalmente qualificado, como `webcredentials:www.contoso.com` .

    Pode combinar todos os subdomínios de um domínio associado introduzindo `*.` (um wildcard asterisco e um período) antes do início do domínio. O período é necessário. Os domínios exatos têm uma prioridade maior do que os domínios wildcard. Assim, os padrões dos domínios dos pais são combinados *se* uma correspondência não for encontrada no subdomínio totalmente qualificado.

    O tipo de serviço pode ser:

    - **authsrv**: Extensão única da aplicação de sinalização
    - **applink**: Ligação universal
    - **webcredenciais**: Autofill password

> [!TIP]
> Para resolver problemas, no seu **System Preferences**dispositivo macOS, abra perfis de  >  **preferências**do sistema . Confirme que o perfil que criou está na lista de perfis do dispositivo. Se estiver listado, certifique-se de que a Configuração de **Domínios Associados** está no perfil, e inclui o ID e domínios corretos da aplicação.

## <a name="login-items"></a>Itens de login

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Adicione os ficheiros, pastas e aplicações personalizadas que serão lançados no início**do início de sessão : **Adicione** o caminho de um ficheiro, pasta, aplicação personalizada ou aplicação do sistema que pretende abrir quando os utilizadores iniciarem o início dos seus dispositivos. Introduza também:

  - **Caminho do item**: Insira o caminho para o ficheiro, pasta ou app. Aplicações do sistema, ou aplicações construídas ou personalizadas para a sua organização estão tipicamente na `Applications` pasta, com um caminho semelhante a `/Applications/AppName.app` .

    Pode adicionar muitos ficheiros, pastas e aplicações. Por exemplo, introduza:   
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Ao adicionar qualquer aplicação, pasta ou ficheiro, certifique-se de que introduza o caminho correto. Nem todos os itens estão na `Applications` pasta. Se os utilizadores moverem um item de um local para outro, então o caminho muda. Este item movido não será aberto quando o utilizador entrar.

  - **Ocultar**: Escolha mostrar ou esconder a aplicação. As opções são:
    - **Não configurado**: Este é o padrão. Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA mostrará itens na lista de itens de login de Grupos de Utilizadores & com a opção de ocultação desmarcada.
    - **Sim:** Esconde a aplicação na lista de itens de login de Grupos de Utilizadores &.

## <a name="login-window"></a>Janela de login

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Mostre informações adicionais na barra de menus**: Quando a área de tempo na barra de menu sé selecionada, **Sim** mostra o nome do anfitrião e a versão macOS. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não mostrar esta informação na barra de menus.
- **Banner**: Introduza uma mensagem que é mostrada no sinal no ecrã nos dispositivos. Por exemplo, insira as informações da sua organização, uma mensagem de boas-vindas, informação perdida e encontrada, e assim por diante.
- **Requerer o nome**de utilizador e os campos de texto de palavra-passe : Escolha como os utilizadores acedem aos dispositivos. **Sim,** requer que os utilizadores introduzam um nome de utilizador e uma palavra-passe. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode exigir que os utilizadores selecionem o seu nome de utilizador a partir de uma lista e, em seguida, digitem a sua palavra-passe.

  Introduza também:

  - **Ocultar os utilizadores locais**: **Sim** não mostra as contas de utilizador locais na lista de utilizadores, o que pode incluir as contas padrão e de administração. Apenas são apresentadas as contas de utilizador da rede e do sistema. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode apresentar as contas de utilizador locais na lista de utilizadores.
  - **Ocultar contas móveis**: **Sim** não mostra contas móveis na lista de utilizadores. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode apresentar as contas móveis na lista de utilizadores. Algumas contas móveis podem mostrar como utilizadores da rede.
  - **Mostrar os utilizadores da rede**: Selecione **Sim** para listar os utilizadores da rede na lista de utilizadores. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não mostrar as contas de utilizador da rede na lista de utilizadores.
  - **Ocultar os administradores do computador**: **Sim** não mostra as contas de utilizador do administrador na lista de utilizadores. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode mostrar as contas de utilizador do administrador na lista de utilizadores.
  - **Mostrar a outros utilizadores**: Selecione **Sim** para **listar Outros...** utilizadores na lista de utilizadores. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não mostrar as outras contas de utilizador na lista de utilizadores.

- **Botão de desligar o esconda-se**: **Sim** não mostra o botão de paragem no sinal no ecrã. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode mostrar o botão de paragem.
- Ocultar o **botão**de reiniciar : **Sim** não mostra o botão de reiniciar o sinal no ecrã. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode mostrar o botão de reinício.
- **Esconda o botão de sono**: **Sim** não mostra o botão de sono no sinal no ecrã. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode mostrar o botão de sono.
- **Desative o login do utilizador a partir da Consola:** **Sim** esconde a linha de comando macOS utilizada para iniciar sessão. Para utilizadores típicos, defina esta definição para **Sim**. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores avançados assinem a utilização da linha de comando macOS. Para entrar no modo consola, os utilizadores entram `>console` no campo Username e devem autenticar na janela da consola.
- **Desative desligar durante o login**: **Sim** impede que os utilizadores selecionem a opção **Desligar** depois de iniciarem o seu login. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores selecionem o item do menu **'Desligar'** nos dispositivos.
- **Desative reiniciar durante o início de sessão**: **Sim** impede que os utilizadores selecionem a opção **Reiniciar** após o início de sessão. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores selecionem o item do menu **Restart** nos dispositivos.
- **Desativar o desativado durante o login**: **Sim** impede que os utilizadores selecionem a opção Desligar a **desligar** após o seu login. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores selecionem o item do menu **Desligar** em dispositivos.
- **Desative o Log out durante o início de sessão** (macOS 10.13 e posteriormente): **Sim** impede os utilizadores de selecionarem a opção **Log out** após o início de sessão. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores selecionem o item do menu **'Iniciar sessão'** nos dispositivos.
- **Desativar** o ecrã de bloqueio durante o login (macOS 10.13 e posteriormente): **Sim** impede os utilizadores de selecionarem a opção de **ecrã lock** após o seu login. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores selecionem o item do menu **'Bloquear'** nos dispositivos.

## <a name="single-sign-on-app-extension"></a>Extensão única da aplicação de inscrição

Esta funcionalidade aplica-se a:

- macOS 10.15 e mais recente

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>As definições aplicam-se a: Inscrição do dispositivo aprovado pelo utilizador e inscrição automática do dispositivo

- **Tipo de extensão da aplicação SSO**: Escolha o tipo de extensão da aplicação SSO credencial. As opções são:

  - **Não configurado**: As extensões de aplicações não são utilizadas. Para desativar uma extensão da aplicação, altere o tipo de extensão da aplicação SSO para **Não configurado**.
  - **Redirecionamento**: Utilize uma extensão de aplicação de redirecionamento genérica e personalizável para utilizar o SSO com fluxos de autenticação modernos. Certifique-se de que conhece a extensão e o ID da equipa para a extensão da aplicação da sua organização.
  - **Credencial**: Utilize uma extensão de aplicação credencial genérica e personalizável para utilizar o SSO com fluxos de autenticação de desafio e resposta. Certifique-se de que conhece o ID de extensão e o ID da equipa para a extensão da aplicação SSO da sua organização.  
  - **Kerberos**: Use a extensão Kerberos incorporada da Apple, que está incluída no macOS Catalina 10.15 e mais recente. Esta opção é uma versão específica da Extensão da aplicação **Credencial** da Kerberos.

  > [!TIP]
  > Com os tipos **Redirecionamento** e **Credenciais,** adicione os seus próprios valores de configuração para passar pela extensão. Se estiver a utilizar o **Credential,** considere utilizar as configurações de configuração incorporadas fornecidas pela Apple no tipo **Kerberos.**

- **ID de extensão** (Redirecionamento e Credencial): Introduza o identificador de pacote que identifica a extensão da sua aplicação SSO, como `com.apple.ssoexample` .
- **ID da equipa** (Redirecionamento e Credencial): Introduza o identificador de equipa da extensão da sua aplicação SSO. Um identificador de equipa é uma cadeia alfanumérica de 10 caracteres (números e letras) gerada pela Apple, como `ABCDE12345` . 

  [Localizar o seu Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (abre o site da Apple) tem mais informações.

- **Reino** (Credencial e Kerberos): Introduza o nome do seu reino de autenticação. O nome do reino deve ser capitalizado, `CONTOSO.COM` como. Tipicamente, o seu nome de reino é o mesmo que o seu nome de domínio DNS, mas em todas as maiúsculas.

- **Domínios** (Credential e Kerberos): Introduza o domínio ou nomes de anfitriões dos sites que podem autenticar através do SSO. Por exemplo, se o seu website é `mysite.contoso.com` , então `mysite` é o nome do anfitrião, e `contoso.com` é o nome de domínio. Quando os utilizadores se ligam a qualquer um destes sites, a extensão da aplicação trata do desafio de autenticação. Esta autenticação permite que os utilizadores utilizem o Face ID, touch ID ou Apple pincode/código de acesso para iniciar sessão.

  - Todos os domínios da sua única extensão de aplicação de início de sessão Os perfis Intune devem ser únicos. Não é possível repetir um domínio em qualquer perfil de extensão de aplicações de início de sessão, mesmo que esteja a utilizar diferentes tipos de extensões de aplicações SSO.
  - Estes domínios não são sensíveis a casos.

- **URLs** (apenas redirecionamento): Introduza os prefixos URL dos seus fornecedores de identidade em nome de quem a extensão da aplicação de redirecionamento utiliza SSO. Quando os utilizadores são redirecionados para estes URLs, a extensão da aplicação SSO intervém e solicita para SSO.

  - Todos os URLs nos seus perfis de extensão de aplicações intune devem ser únicos. Não é possível repetir um domínio em qualquer perfil de extensão de aplicações SSO, mesmo que esteja a utilizar diferentes tipos de extensões de aplicações SSO.
  - Os URLs devem começar com http:// ou https://.

- **Configuração adicional** (Redirecionamento e Credencial): Introduza dados adicionais específicos de extensão para passar para a extensão da aplicação SSO:
  - **Chave**: Introduza o nome do item que pretende adicionar, como `user name` .
  - **Tipo**: Introduza o tipo de dados. As opções são:

    - String
    - Boolean: No valor de **configuração,** insira `True` ou `False` .
    - Integer: No valor de **configuração,** introduza um número.

  - **Valor**: Introduza os dados.
  
  - **Adicione**: Selecione para adicionar as suas chaves de configuração.

- **Utilização** em cadeia de chaves (apenas Kerberos): Escolha **o Bloco** para evitar que as palavras-passe sejam guardadas e armazenadas no porta-chaves. Se bloqueados, os utilizadores não são solicitados a guardar a sua palavra-passe e precisam de reintroduzir a palavra-passe quando o bilhete Kerberos expirar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que as palavras-passe sejam guardadas e armazenadas no porta-chaves. Os utilizadores não são solicitados a reintroduzir a sua palavra-passe quando o bilhete expirar.
- **Id do rosto, Touch ID ou código de acesso** (apenas Kerberos): **Exigir** que os utilizadores introduzam o seu ID facial, touch ID ou código de acesso do dispositivo quando a credencial é necessária para refrescar o bilhete Kerberos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode não exigir que os utilizadores utilizem a biometria ou a senha do dispositivo para atualizar o bilhete Kerberos. Se o uso do **Keychain** estiver bloqueado, esta definição não se aplica.
- **Reino padrão** (apenas Kerberos): Escolha **ativar** para definir o valor real **que** introduziu como o reino padrão. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode não definir um reino padrão.

  > [!TIP]
  > - **Ative** esta definição se estiver a configurar várias extensões de aplicações Kerberos SSO na sua organização.
  > - **Ative** esta definição se estiver a utilizar vários reinos. Define o valor do **Reino** que introduziu como o reino padrão.
  > - Se tiver apenas um reino, deixe-o **não configurado** (predefinido).

- **Autodescubra** (apenas Kerberos): Quando definida para **bloquear,** a extensão Kerberos não utiliza automaticamente LDAP e DNS para determinar o seu nome de site ative diretório. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que a extensão encontre automaticamente o nome do site do Diretório Ativo.
- **Alterações de palavra-passe** (apenas Kerberos): **O bloco** impede que os utilizadores mudem as palavras-passe que utilizam para iniciar sessão nos domínios em que inseriu. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir alterações de palavra-passe.  
- **Sincronização de passwords** (apenas Kerberos): Escolha **ativar** para sincronizar as palavras-passe locais dos seus utilizadores para o Azure AD. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode desativar a sincronização de palavra-passe para o Azure AD. Utilize esta definição como alternativa ou cópia de segurança para o SSO. Esta definição não funciona se os utilizadores forem inscritos numa conta móvel da Apple.
- Complexidade da **palavra-passe do Diretório Ativo do Windows Server** (apenas Kerberos): Escolha **exigir** que as palavras-passe dos utilizadores cumpram os requisitos de complexidade da palavra-passe do Ative Directory. Para mais informações, consulte [a Palavra-passe deve satisfazer os requisitos](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)de complexidade . Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não exigir que os utilizadores cumpram o requisito de senha do Diretório Ativo.
- **Comprimento mínimo da palavra-passe** (apenas Kerberos): Introduza o número mínimo de caracteres que podem compor as palavras-passe dos utilizadores. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não impor um comprimento mínimo de senha aos utilizadores.
- Limite de **reutilização de palavra-passe** (apenas Kerberos): Introduza o número de novas senhas, de 1 a 24, que devem ser utilizadas até que uma palavra-passe anterior possa ser reutilizada no domínio. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não impor um limite de reutilização de palavra-passe.
- Idade mínima da **palavra-passe** (apenas Kerberos): Introduza o número de dias em que uma palavra-passe deve ser utilizada no domínio antes que os utilizadores possam alterá-la. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode não impor uma idade mínima de senhas antes de poderem ser alteradas.
- Notificação de expiração de **palavra-passe** (apenas Kerberos): Insira o número de dias antes de expirar uma palavra-passe para que os utilizadores sejam notificados de que a sua palavra-passe expirará. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode utilizar `15` dias.
- **Expiração da palavra-passe** (apenas Kerberos): Introduza o número de dias antes de a palavra-passe do dispositivo ser alterada. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode nunca expirar senhas.
- URL de **alteração de palavra-passe** (apenas Kerberos): Introduza o URL que se abre quando os utilizadores iniciarem uma alteração de senha kerberos.
- **Nome principal** (apenas Kerberos): Introduza o nome de utilizador do diretor kerberos. Não precisas de incluir o nome do reino. Por exemplo, em `user@contoso.com` , é o nome `user` principal, e é o nome do `contoso.com` reino.

  > [!TIP]
  > - Também pode utilizar variáveis no nome principal, entrando em suportes encaracolados `{{ }}` . Por exemplo, para mostrar o nome de utilizador, introduza `Username: {{username}}` . 
  > - No entanto, tenha cuidado com a substituição variável porque as variáveis não são validadas na UI e são sensíveis ao caso. Certifique-se de introduzir a informação correta.
  
- Código de **site de Diretório Ativo** (apenas Kerberos): Introduza o nome do site Ative Directory que a extensão Kerberos deve utilizar. Pode não precisar de alterar este valor, uma vez que a extensão Kerberos pode automaticamente encontrar o código do site do Ative Directory.
- **Nome cache** (apenas Kerberos): Introduza o nome genérico de serviços de segurança (GSS) da cache Kerberos. Provavelmente não precisa definir este valor.  
- **Mensagem de prescrição de palavra-passe** (apenas Kerberos): Introduza uma versão de texto dos requisitos de palavra-passe da sua organização que é mostrada aos utilizadores. A mensagem é mostrada se não necessitar dos requisitos de complexidade da palavra-passe do Ative Directory ou se não introduzir um comprimento mínimo de senha.  
- **IDs** de pacote de aplicativos (apenas Kerberos): **Adicione** os identificadores de pacote de aplicativos que devem usar um único sinal nos seus dispositivos. Estas aplicações têm acesso ao Bilhete de Concessão de Bilhetes Kerberos e ao bilhete de autenticação. As aplicações também autenticam os utilizadores aos serviços a que estão autorizados a aceder.
- **Mapeamento** do domínio (apenas Kerberos): **Adicione** os sufixos dNS de domínio que devem mapear para o seu reino. Use este cenário quando os nomes DNS dos anfitriões não corresponderem ao nome do reino. Provavelmente não precisa de criar este mapeamento personalizado domínio-realm.
- **Certificado PKINIT** (apenas Kerberos): **Selecione** o certificado de criptografia de chave pública para autenticação inicial (PKINIT) que pode ser usado para autenticação Kerberos. Pode escolher entre os certificados [PKCS](../protect/certficates-pfx-configure.md) ou [SCEP](../protect/certificates-scep-configure.md) que adicionou no Intune. Para obter mais informações sobre certificados, consulte [Utilize certificados para autenticação no Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode configurar as funcionalidades do dispositivo no [iOS/iPadOS](ios-device-features-settings.md).
