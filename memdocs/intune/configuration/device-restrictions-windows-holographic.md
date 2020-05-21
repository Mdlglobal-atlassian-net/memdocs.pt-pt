---
title: Definições de dispositivos Holográficos do Windows Business - Microsoft Intune - Azure [ Microsoft Docs
description: Leia e configure as definições de restrição do dispositivo no Microsoft Intune para Windows Holographic for Business. Controle a não inscrição, geolocalização, palavras-passe, instale aplicações a partir de lojas de aplicações, cookies e pop-ups no Microsoft Edge, Microsoft Defender, pesquisa, nuvem e armazenamento, conectividade bluetooth, tempo do sistema e dados de utilização.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 301cdd9403b0bb3e2d64c8707782ecbc639dc044
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556053"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Windows Holographic for Business device definições para permitir ou restringir funcionalidades usando Intune

Este artigo lista e descreve as diferentes definições que pode controlar no Windows Holographic para dispositivos Empresariais, como o Microsoft Hololens. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para permitir ou desativar funcionalidades, segurança de controlo e muito mais.

Como administrador intune, pode criar e atribuir estas definições aos seus dispositivos.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de configuração de restrições de [dispositivos Windows 10](device-restrictions-configure.md#create-the-profile).

Quando cria um perfil de configuração de configuração de restrições de dispositivos Windows 10, existem mais configurações do que as listadas neste artigo. As definições deste artigo são suportadas no Windows Holographic para dispositivos Empresariais.

## <a name="app-store"></a>App Store

- **Aplicações de atualização automática a partir da loja**: O **bloco** impede que as atualizações sejam instaladas automaticamente a partir da Microsoft Store. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que as aplicações instaladas a partir da Microsoft Store sejam automaticamente atualizadas.

  [Gestão de aplicações/PermitirAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Instalação de aplicativos fidedignos**: Escolha se as aplicações não Microsoft Store podem ser instaladas, também conhecidacomo sideloading. A sideloading está a instalar-se e, em seguida, a executar ou a testar uma aplicação que não é certificada pela Microsoft Store. Por exemplo, uma aplicação que é interna apenas para a sua empresa. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Bloco**: Evita a colocação lateral. As aplicações não microsoft Store não podem ser instaladas.
  - **Permitir**: Permite a sideloading. As aplicações não Microsoft Store podem ser instaladas.

  [Gestão de aplicações/Permitir alltrustedapps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Desbloqueio do desenvolvedor**: Permitir configurações de desenvolvedores do Windows, tais como permitir que as aplicações paradas sejam modificadas pelos utilizadores. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Bloco**: Previne o modo de desenvolvimento e as aplicações de carregamento lateral.
  - **Permitir**: Permite o modo de desenvolvimento e aplicações de carregamento lateral.

  [Gestão de aplicações/permitirdeveloperunlock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Rede Móvel e Conectividade

- **Bluetooth**: **O bloco** impede os utilizadores de ativarem bluetooth. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir bluetooth no dispositivo.

  [Conectividade/Permitir CSP Bluetooth](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Descoberta Bluetooth**: **O bloco** impede que o dispositivo seja detetável por outros dispositivos ativados por Bluetooth. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que outros dispositivos ativados por Bluetooth, como um auricular, descubram o dispositivo.

  [Bluetooth/AllowDiscoverMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Publicidade Bluetooth**: **O bloco** impede que o dispositivo envie anúncios Bluetooth. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que o dispositivo envie anúncios Bluetooth.

  [Bluetooth/Permitir Publicidade CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Cloud e Armazenamento

- **Conta Microsoft**: **O bloco** impede os utilizadores de associarem uma conta Microsoft ao dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir adicionar e utilizar uma conta Microsoft.

  [Contas/Permitir MicrosoftAccountConnection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Painel de Controlo e Definições

- **Modificação do tempo**do sistema : **O bloco** impede que os utilizadores mudem as definições de data e hora no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem estas definições.

  [Definições/Permitir Data Data CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>Geral

- **Desinscrição manual**: **O bloco** impede que os utilizadores aleem a conta no local de trabalho utilizando o painel de controlo do local de trabalho no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Experiência/PermitirManualMDMUninscriç CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Geolocalização**: **O bloco** impede que os utilizadores desligá-lo no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Experiência/permitirFindmydevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: **O bloco** desativa o assistente de voz Cortana no dispositivo. Quando cortana está desligado, os utilizadores ainda podem pesquisar para encontrar itens no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema Operativo pode permitir cortana.

  [Experiência/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Browser Microsoft Edge

- **Iniciar experiência**  >  **Permitir pop-ups**: **Sim** (padrão) permite pop-ups no navegador web. **Não** impede que as janelas pop-up no navegador.

  [Browser/AllowPopups CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Favoritos e pesquisa**  >  **Mostrar sugestões**de pesquisa : **Sim** (padrão) permite que o seu motor de busca sugira sites à medida que escreve frases de pesquisa na barra de endereços. **Nenhum previne** esta funcionalidade.

  [Browser/AllowSearchSuggestionsinAddressBar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Privacidade e segurança**  >  **Permitir o Gestor de Passwords**: **Sim** (predefinido) permite que o Microsoft Edge utilize automaticamente o Password Manager, o que permite aos utilizadores guardar e gerir palavras-passe no dispositivo. **Nenhum** impede o Microsoft Edge de utilizar o Password Manager.

  [Browser/AllowPasswordManager CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Privacidade e segurança**  >  **Cookies**: Escolha como os cookies são tratados no navegador web. As opções são:
  - **Permitir**: Os cookies são armazenados no dispositivo.
  - **Bloqueie todos os cookies**: Os cookies não são armazenados no dispositivo.
  - **Bloqueie apenas cookies**de terceiros : Os cookies de terceiros ou parceiros não são armazenados no dispositivo.

  [Browser/AllowCookies CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Privacidade e segurança**  >  **Envie cabeçalhos de não-rastreio**: **Sim** envia cabeçalhos de não-rastre para sites que solicitam informações de rastreio (recomendado). **Nenhum** (padrão) não envia cabeçalhos que permitam que os websites rastreiem o utilizador. Os utilizadores podem configurar esta definição.

  [Browser/AllowDoNotTrack CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen para o Microsoft Edge**: **Exija** ligações no Microsoft Defender SmartScreen e impede que os utilizadores o desliguem. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ligar o SmartScreen e permitir que os utilizadores o liguem e desliguem.

  [Browser/AllowSmartScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>Palavra-passe

- **Palavra-passe**: **Exigir** que os utilizadores introduzam uma palavra-passe para aceder ao dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso a dispositivos sem senha. Aplica-se apenas às contas locais. As palavras-passe da conta de domínio permanecem configuradas por Ative Directory (AD) e Azure AD.

  [DeviceLock/DevicePassword-PasswordEnabled CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Requerer uma palavra-passe quando o dispositivo regressar do estado de marcha lenta**: Exija **que** os utilizadores introduzam uma palavra-passe para desbloquear o dispositivo depois de estarem inativos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não necessitar de um PIN ou palavra-passe depois de estar inativo.

  [DeviceLock/AllowIdleReturnWithoutPassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Relatórios e Telemetria

- **Partilhar dados de utilização**: Escolha o nível de dados de diagnóstico que são submetidos. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores escolhem o nível que é submetido. Por padrão, o SO pode não partilhar quaisquer dados.
  - **Segurança**: Informações necessárias para ajudar a manter o Windows mais seguro, incluindo dados sobre as definições de experiência de utilizador conectado e de componentes de telemetria, a Ferramenta de Remoção de Software Malicioso e o Microsoft Defender
  - **Básico**: Informações básicas do dispositivo, incluindo dados relacionados com a qualidade, compatibilidade de aplicações, dados de utilização de aplicações e dados do nível de Segurança
  - **Enhanced**: Insights adicionais, incluindo como windows, Windows Server, System Center e apps são usados, como eles executam, dados avançados de fiabilidade, e dados tanto dos níveis básico si e dos níveis de Segurança
  - **Completo**: Todos os dados necessários para identificar e ajudar a corrigir problemas, além de dados do nível de Segurança, Básico e Melhorado.

  [Sistema/Permitir Telemetria CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>Pesquisa

- **Local**de pesquisa : **O bloco** impede que o Windows Search utilize a localização. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.

  [Pesquisa/Permitir Pesquisa/Permitir Pesquisa de Utilização CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Próximos passos

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).
