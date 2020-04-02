---
title: Crie o perfil do iOS/iPadOS ou do dispositivo macOS com o Microsoft Intune - Azure  Microsoft Docs
description: Adicione ou crie um perfil de dispositivo iOS, iPadOS ou macOS e, em seguida, configure as definições para o AirPrint, layout do ecrã principal, notificações de aplicações, dispositivo partilhado, definição de inscrição única e filtro de conteúdo web no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb8d5b53e136ea22d1edbad7755e198fd4155285
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551393"
---
# <a name="add-ios-ipados-or-macos-device-feature-settings-in-intune"></a>Adicione as definições de funcionalidades do iOS, iPadOS ou macOS em Intune

Intune inclui muitas funcionalidades e configurações que ajudam os administradores a controlar os dispositivos iOS, iPadOS e macOS. Por exemplo, os administradores podem:

- Permitir aos utilizadores o acesso a impressoras AirPrint na sua rede
- Adicione aplicativos e pastas ao ecrã principal, incluindo a adição de novas páginas
- Escolha se e como as notificações de aplicações são mostradas
- Configure o ecrã de bloqueio para mostrar uma mensagem ou a etiqueta de ativo, especialmente para dispositivos partilhados
- Dar aos utilizadores uma experiência de inscrição única segura para partilhar credenciais entre apps
- Filtrar web sites que usam linguagem adulta e permitir ou bloquear sites específicos

Intune usa "perfis de configuração" para criar e personalizar estas configurações para as necessidades da sua organização. Depois de adicionar estas funcionalidades num perfil, empurre ou implemente o perfil para dispositivos iOS/iPadOS e macOS na sua organização.

Este artigo descreve as diferentes funcionalidades que pode configurar e mostra-lhe como criar um perfil de configuração do dispositivo. Também pode ver todas as definições disponíveis para [dispositivos iOS/iPadOS](ios-device-features-settings.md) e [macOS.](macos-device-features-settings.md)

> [!NOTE]
> A interface de utilizador Intune (UI) está a atualizar-se para uma experiência completa de ecrã, podendo demorar várias semanas. Até que o seu inquilino receba esta atualização, terá um fluxo de trabalho ligeiramente diferente quando criar ou editar configurações descritas neste artigo.

## <a name="airprint"></a>Impressão aérea

Airprint é uma funcionalidade da Apple que permite que os dispositivos imprimam para ficheiros numa rede sem fios. Em Intune, pode adicionar informações airPrint aos dispositivos.

Para obter uma lista das definições que pode configurar em Intune, consulte [AirPrint no iOS/iPadOS](ios-device-features-settings.md#airprint) e [AirPrint no macOS](macos-device-features-settings.md#airprint).

Para obter mais informações sobre o AirPrint, consulte sobre o [AirPrint](https://support.apple.com/HT201311) no site da Apple.

Aplica-se a:

- iOS 7.0 e mais recente
- iPadOS 13.0 e mais recente
- macOS 10.10 e mais recente

## <a name="app-notifications"></a>Notificações de aplicativos

Escolha como as aplicações dos seus dispositivos iOS e iPadOS recebem notificações. Por exemplo, a partir de Intune, envie notificações de aplicativos para que apareçam no centro de notificação, mostrem no ecrã de bloqueio ou reproduzissem um som.

Para obter uma lista das definições que pode configurar em Intune, consulte notificações da [App no iOS/iPadOS](ios-device-features-settings.md#app-notifications).

Para obter mais informações sobre esta funcionalidade, consulte [notificações](https://developer.apple.com/notifications/) no site da Apple.

Aplica-se a:

- iOS 9.3 e mais recente
- iPadOS 13.0 e mais recente

## <a name="associated-domains"></a>Domínios associados

Os domínios associados permitem criar uma relação entre os seus domínios, como `contoso.com`e as suas apps. Esta funcionalidade permite-lhe:

- Partilhe dados e assine credenciais entre apps e websites da sua organização.
- Utilize funcionalidades de aplicações baseadas no seu website, tais como extensão de aplicação de entrada única, links universais e preenchimento automático de palavra-passe.

  Por exemplo, crie um domínio associado para permitir o auto-enchimento de palavras-passe para recomendar credenciais, como uma palavra-passe, para websites associados à sua aplicação.

Para obter uma lista das definições que pode configurar em Intune, consulte [domínios associados no macOS](macos-device-features-settings.md#associated-domains).

Para obter mais informações sobre esta funcionalidade, consulte [a Configuração de domínios associados de uma aplicação](https://developer.apple.com/documentation/security/password_autofill/setting_up_an_app_s_associated_domains) no site da Apple.

Aplica-se a:

- macOS 10.15 e mais recente

## <a name="home-screen-layout"></a>Esquema do ecrã principal

Estas configurações configuram o layout da aplicação e as pastas na doca e ecrãs domésticos nos dispositivos iOS e iPadOS. É possível:

- Utilize as definições **da Doca** para adicionar aplicações ou pastas ao ecrã. Por exemplo, mostre o Safari e a aplicação Mail na doca do dispositivo.
- Adicione **páginas** que deseja mostradas no ecrã principal e as aplicações que pretende mostrar em cada página. Por exemplo, adicione uma página **de Contoso** e adicione a aplicação Definições nesta página.

Para obter uma lista das definições que pode configurar em Intune, consulte o layout do [ecrã Principal no iOS/iPadOS](ios-device-features-settings.md#home-screen-layout).

Aplica-se a:

- iOS 9.3 e mais recente
- iPadOS 13.0 e mais recente

## <a name="lock-screen-message"></a>Mensagem de tela de bloqueio

Utilize estas definições para mostrar uma mensagem ou texto personalizado no sinal na janela e no ecrã de bloqueio. Por exemplo, pode introduzir um "Se estiver perdido, volte a..." mensagem, e mostrar informações de etiqueta de ativo.

Para obter uma lista das definições que pode configurar em Intune, consulte as definições de mensagem de [ecrã de bloqueio no iOS/iPadOS](ios-device-features-settings.md#lock-screen-message).

Para obter mais informações sobre a Mensagem de Ecrã de Bloqueio, consulte [o LockScreenMessage](https://developer.apple.com/documentation/devicemanagement/lockscreenmessage) no site da Apple.

Aplica-se a:

- iOS 9.3 e mais recente
- iPadOS 13.0 e mais recente

## <a name="login-items"></a>Itens de login

Utilize esta funcionalidade para escolher as aplicações, aplicações personalizadas, ficheiros e pastas que se abrem quando os utilizadores iniciam sessão nos dispositivos.

Para obter uma lista das definições que pode configurar em Intune, consulte [itens de Login no macOS](macos-device-features-settings.md#login-items).

Aplica-se a:

- macOS 10.13 e mais recente

## <a name="login-window"></a>Janela de login

Controle o aparecimento do ecrã de login e as funções disponíveis para os utilizadores antes de iniciar o seu login. Por exemplo, adicione um banner com uma mensagem personalizada, escolha se o botão de sono é mostrado, e muito mais.

Para obter uma lista das definições que pode configurar em Intune, consulte [a janela De Login no macOS](macos-device-features-settings.md#login-window).

Aplica-se a:

- macOS 10.7 e mais recente

## <a name="single-sign-on"></a>Início de sessão único

A maioria das aplicações de Linha de Negócio (LOB) exige algum nível de autenticação do utilizador para suportar a segurança. Em muitos casos, a autenticação requer que o utilizador introduza repetidamente as mesmas credenciais. Para melhorar a experiência do utilizador, os desenvolvedores podem criar aplicações que utilizem um único sign-on (SSO). A utilização de um único sinal reduz o número de vezes que um utilizador deve introduzir credenciais.

Para utilizar um único sinal, certifique-se de que tem:

- Uma aplicação codificada para procurar a loja credencial do utilizador em um único sinal no dispositivo.
- Insintonizado configurado para iOS/iPadOS único sinal de inscrição.

![Painel Início de Sessão Único](./media/device-features-configure/sso-blade.png)

Para obter uma lista das definições que pode configurar em Intune, consulte [o único sinal no iOS/iPadOS](ios-device-features-settings.md#single-sign-on).

Aplica-se a:

- iOS 7.0 e mais recente
- iPadOS 13.0 e mais recente

## <a name="single-sign-on-app-extension"></a>Extensão única da aplicação de inscrição

Estas configurações configuram uma extensão de aplicação que permite um único sinal (SSO) para os seus dispositivos iOS, iPadOS e macOS. A maioria das aplicações e websites da organização da Linha de Negócios (LOB) requerem algum nível de autenticação segura do utilizador. Em muitos casos, a autenticação requer que os utilizadores introduzam repetidamente as mesmas credenciais. O SSO dá aos utilizadores acesso a apps e websites depois de terem entrado nas suas credenciais uma vez. O SSO também fornece uma melhor experiência de autenticação para os utilizadores, e reduz o número de pedidos repetidos para credenciais.

No Intune, utilize estas definições para configurar uma extensão de aplicação SSO criada pela sua organização, pelo seu fornecedor de identidade, Microsoft ou Apple. A extensão da aplicação SSO trata da autenticação para os seus utilizadores. Estas configurações configuram extensões de aplicações SSO tipo redirecionamento e credenciais.

- O tipo redireccional foi concebido para protocolos de autenticação modernos, tais como OAuth e SAML2. A Microsoft tem uma extensão de aplicação SSO do tipo IOS/iPadOS Azure que pode ser ativada com as definições de extensão de aplicações de início de sinal único.
- O tipo credencial foi concebido para fluxos de autenticação de desafio e resposta. Pode escolher entre uma extensão de credencial específica da Kerberos fornecida pela Apple, ou uma extensão de credencial genérica.

Para obter uma lista das definições que pode configurar em Intune, consulte a extensão da [aplicação iOS/iPadOS SSO](ios-device-features-settings.md#single-sign-on-app-extension) e a extensão da [aplicação macOS SSO](macos-device-features-settings.md#single-sign-on-app-extension).

Para obter mais informações sobre o desenvolvimento de uma extensão de aplicações SSO, assista a [Extensible Enterprise SSO](https://developer.apple.com/videos/play/tech-talks/301) no site da Apple. Para ler a descrição da funcionalidade da Apple, visite as definições de carga de carga de [extensões de sinais simples](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web). 

> [!NOTE]
> A funcionalidade de extensão da **aplicação de assinatura única** é diferente da funcionalidade de **inscrição única:**
>
> - As definições de extensão de aplicações de **assinatura única aplicam-se** ao iPadOS 13.0 (e mais recente), iOS 13.0 (e mais recente) e macOS 10.15 (e mais recente). As definições **de inscrição única aplicam-se** ao iPadOS 13.0 (e mais recente) e iOS 7.0 e mais recentes.
>
> - As definições **de extensão de aplicações** de assinatura única definem extensões para utilização por fornecedores de identidade ou organizações para oferecer uma experiência de inscrição de empresa sem emenda. As definições **de inscrição única** definem as informações da conta Kerberos para quando os utilizadores acedem a servidores ou aplicações.
>
> - A extensão da **aplicação de início de sessão Single** utiliza o sistema operativo Apple para autenticar. Portanto, pode proporcionar uma experiência de utilizador final que é melhor do que o **único sinal.**
>
> - Do ponto de vista do desenvolvimento, com a extensão da **aplicação de inscrição única,** pode utilizar qualquer tipo de autenticação SSO redirecionária ou credencial SSO. Com **um único sinal,** só pode utilizar a autenticação Kerberos SSO.
>
> - A extensão de aplicação de **sign-on Kerberos Single** foi desenvolvida pela Apple e está integrada nas plataformas iOS/iPadOS 13.0+ e macOS 10.15+. A extensão kerberos incorporada pode ser usada para registar utilizadores em aplicações nativas e websites que suportam a autenticação Kerberos. **A única inscrição** não é uma implementação da Apple de Kerberos.
>
> - A extensão de aplicação de **sinalização Kerberos Single** incorporada lida com os desafios kerberos para páginas web e aplicações tal como **o single sign-on**. No entanto, a extensão kerberos incorporada suporta alterações de password e comporta-se melhor nas redes empresariais. Ao decidir entre a extensão de uma aplicação de **sinalização Kerberos Single** e o único **sinal,** recomendamos a utilização da extensão devido a um melhor desempenho e capacidades.

Aplica-se a:

- iOS 13.0 e mais recente
- iPadOS 13.0 e mais recente
- macOS 10.15 e mais recente

## <a name="wallpaper"></a>Papel de parede

Adicione uma imagem personalizada .png, .jpg ou .jpeg aos seus dispositivos iOS/iPadOS supervisionados. Por exemplo, utilize o Intune para adicionar um logótipo da empresa ao ecrã de bloqueio dos seus dispositivos.

Para obter uma lista das definições que pode configurar em Intune, consulte [wallpaper no iOS/iPadOS](ios-device-features-settings.md#wallpaper).

Aplica-se a:

- iOS
- iPadOS 13.0 e mais recente

## <a name="web-content-filter"></a>Filtro de conteúdo web

Estas definições usam o algoritmo autofilter incorporado da Apple para avaliar páginas web e bloquear conteúdo adulto e linguagem adulta. Também pode criar uma lista de links web permitidos e links web restritos. Por exemplo, só pode permitir que `contoso` web sites se abram.

Para obter uma lista das definições que pode configurar em Intune, consulte o filtro de [conteúdo web no iOS/iPadOS](ios-device-features-settings.md#web-content-filter).

Aplica-se a:

- iOS 7.0 e mais recente
- iPadOS 13.0 e mais recente

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Escolha a plataforma dos seus dispositivos. As opções são:  

        - **iOS/iPadOS**
        - **macOS**

    - **Perfil**: Selecione **as funcionalidades do dispositivo**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política é **macOS: Configures login screen**.
    - **Descrição**: Insira uma descrição para a apólice. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Nas definições de **Configuração**, dependendo da plataforma que escolheu, as definições que pode configurar são diferentes. Escolha a sua plataforma para configurações detalhadas:

    - [iOS/iPadOS](ios-device-features-settings.md)
    - [macOS](macos-device-features-settings.md)

8. Selecione **Seguinte**.
9. Nas **etiquetas scope** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como `US-NC IT Team` ou `JohnGlenn_ITDepartment`. Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="next-steps"></a>Próximos passos

O perfil é criado, mas pode ainda não estar a fazer nada. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Ver todas as definições de funcionalidades do dispositivo para [dispositivos iOS/iPadOS](ios-device-features-settings.md) e [macOS.](macos-device-features-settings.md)
