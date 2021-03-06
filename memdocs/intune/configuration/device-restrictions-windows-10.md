---
title: Definições de restrição de dispositivos para Windows 10 no Microsoft Intune – Azure | Microsoft Docs
description: Consulte uma lista de todas as definições e descrições para criar restrições de dispositivos no Windows 10 e dispositivos posteriores. Utilize estas definições num perfil de configuração para controlar imagens, requisitos de palavra-passe, configurações de quiosque, aplicações na loja, navegador Microsoft Edge, Microsoft Defender, acesso à nuvem, menu inicial e muito mais no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20c552ff879574edc0ed497b5c99b45b8092918a
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864904"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Definições do dispositivo Windows 10 (e mais recentes) para permitir ou restringir funcionalidades usando Intune

Este artigo lista e descreve todas as diferentes definições que pode controlar no Windows 10 e em dispositivos mais recentes. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para permitir ou desativar funcionalidades, definir regras de palavra-passe, personalizar o ecrã de bloqueio, utilizar o Microsoft Defender e muito mais.

Estas definições são adicionadas a um perfil de configuração do dispositivo em Intune e, em seguida, atribuídas ou implantadas para os seus dispositivos Windows 10.

> [!Note]
> Nem todas as opções estão disponíveis em todas as edições do Windows. Para ver as edições suportadas, consulte os [CSPs de política](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (abre outro web site da Microsoft).

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de restrições de [dispositivos Windows 10.](device-restrictions-configure.md#create-the-profile)

## <a name="app-store"></a>App Store

Estas definições utilizam a política de Gestão de [Aplicações CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement), que também lista as edições suportadas pelo Windows.

- **Loja de aplicações (apenas para dispositivos móveis)**: **O bloco** impede que os utilizadores acedam à loja de aplicações em dispositivos móveis. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir aos utilizadores o acesso à loja de aplicações.
- **Aplicações de atualização automática a partir da loja**: O **bloco** impede que as atualizações sejam instaladas automaticamente a partir da Microsoft Store. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que as aplicações instaladas a partir da Microsoft Store sejam automaticamente atualizadas.

  [Gestão de aplicações/PermitirAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Instalação de aplicativos fidedignos**: Escolha se as aplicações não Microsoft Store podem ser instaladas, também conhecidacomo sideloading. A sideloading está a instalar-se e, em seguida, a executar ou a testar uma aplicação que não é certificada pela Microsoft Store. Por exemplo, uma aplicação que é interna apenas para a sua empresa. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Bloco**: Evita a colocação lateral. As aplicações não microsoft Store não podem ser instaladas.
  - **Permitir**: Permite a sideloading. As aplicações não Microsoft Store podem ser instaladas.

- **Desbloqueio do desenvolvedor**: Permitir configurações de desenvolvedores do Windows, tais como permitir que as aplicações paradas sejam modificadas pelos utilizadores. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Bloco**: Previne o modo de desenvolvimento e as aplicações de carregamento lateral.
  - **Permitir**: Permite o modo de desenvolvimento e aplicações de carregamento lateral.

  [Ativar o seu dispositivo para desenvolvimento](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) tem mais informações sobre esta funcionalidade.
  
  [Gestão de aplicações/Permitir alltrustedapps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- Dados de **aplicações partilhadas do utilizador**: Escolha **permitir** partilhar dados de aplicações entre diferentes utilizadores no mesmo dispositivo e com outras instâncias dessa aplicação. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode impedir a partilha de dados com outros utilizadores e outros casos da mesma aplicação.

  [Gestão de aplicações/permitiruseruserappdata cSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Utilize apenas uma loja privada**: **Permitir apenas** permitir que as aplicações sejam descarregadas de uma loja privada e não descarregadas a partir da loja pública, incluindo um catálogo de retalho. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que as aplicações sejam descarregadas de uma loja privada e de uma loja pública.

  [Gestão de aplicações/RequerPrivateStore Only CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Lançamento de aplicações originadas**na loja : **O bloco** desativa todas as aplicações que foram pré-instaladas no dispositivo ou descarregadas a partir da Microsoft Store. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que estas aplicações se abram.

  [ApplicationManagement/DisableStoreOriginadoApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **Instale dados**de aplicações no volume do sistema : O **bloco** impede que as aplicações armazenem dados no volume do sistema do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que as aplicações armazenem dados no volume do disco do sistema.

  [Gestão de aplicações/restringir o volume de dados do sistema csp](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Instale aplicações na unidade do sistema**: O **bloco** impede que as aplicações se instalem na unidade do sistema no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que as aplicações se instalem na unidade do sistema.

  [Gestão de aplicações/restringir o volume de aplicações csp](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **DVR do jogo (apenas no ambiente de trabalho)**: **O bloco** desativa a gravação e a radiodifusão do Windows Game. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a gravação e transmissão de jogos.

  [Gestão de aplicações/permitirGameDVR CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Aplicações apartir da loja apenas**: Esta definição determina a experiência do utilizador quando os utilizadores instalam aplicações de outros lugares que não a Microsoft Store. Não impede a instalação de conteúdo de dispositivos USB, partilhas de rede ou outras fontes não internet. Utilize um navegador de confiança para ajudar a garantir que estas proteções funcionem como esperado.

  As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por padrão, o OS poderá permitir que os utilizadores instalem aplicações de outros locais que não a Microsoft Store, incluindo aplicações definidas noutras definições de política.  
  - **Qualquer lugar**: Desliga as recomendações da aplicação e permite que os utilizadores instalem aplicações a partir de qualquer local.  
  - **Armação Apenas**: A intenção é evitar que conteúdos maliciosos afetem os seus dispositivos de utilizador ao descarregar conteúdo executável a partir da internet. Quando os utilizadores tentam instalar aplicações a partir da internet, a instalação está bloqueada. Os utilizadores vêem uma mensagem recomendando que descarreguem aplicações a partir da Microsoft Store.
  - **Recomendações**: Ao instalar uma aplicação a partir da web que está disponível na Microsoft Store, os utilizadores vêem uma mensagem recomendando que a descarreguem da loja.  
  - **Prefer Store**: Avisa os utilizadores quando instalam aplicações em outros lugares que não a Microsoft Store.

  [SmartScreen/EnableAppInstallControl CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **Controlo do utilizador sobre instalações**: **O bloco** impede que os utilizadores mudem as opções de instalação normalmente reservadas aos administradores do sistema, tais como a introdução do diretório para instalar os ficheiros. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por defeito, o Instalador do Windows poderá impedir que os utilizadores mudem estas opções de instalação e algumas das funcionalidades de segurança do Instalador do Windows são ignoradas.

  [Gestão de aplicações/msiallowusercontroloverinstall CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Instale aplicações com privilégios elevados**: **O Block** direciona o Instalador do Windows para utilizar permissões elevadas quando instala qualquer programa no sistema. Estes privilégios são estendidos a todos os programas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o sistema pode aplicar as permissões do utilizador atual quando instala programas que um administrador do sistema não implementa ou oferece.

  [Gestão de Aplicações/MSIAlwaysInstallWithElevatedPrivileges CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Aplicações**de arranque : Insira uma lista de aplicações para abrir depois de um utilizador iniciar sintetização no dispositivo. Certifique-se de que utiliza uma lista semi-cólon denomes familiares (PFN) de aplicações Windows. Para que esta política funcione, o manifesto nas aplicações windows deve utilizar uma tarefa de arranque.

  [Gestão de Aplicações/LaunchAppafterlogon CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>Rede Móvel e Conectividade

Estas definições utilizam a política de [conectividade](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) e os CSPs da [política wi-fi,](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi) que também listam as edições suportadas do Windows.

- Canal de **dados celulares**: Escolha se os utilizadores podem usar dados, como navegar na web, quando ligados a uma rede celular. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. os utilizadores podem desligá-lo.
  - **Bloco**: Não permita o canal de dados celular. Os utilizadores não podem ligá-lo.
  - **Permitir (não editável)**: Permite o canal de dados celular. Os utilizadores não podem desligá-lo.

- **Roaming de dados**: **O bloco** impede o roaming de dados celulares no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, ao aceder a dados, pode ser permitido roaming entre redes.
- **VPN sobre a rede celular**: O **bloco** impede que o dispositivo aceda a ligações VPN quando ligado a uma rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o OS pode permitir que a VPN utilize qualquer ligação, incluindo celular.
- **VPN roaming sobre a rede celular**: O **bloco** impede que o dispositivo aceda a ligações VPN ao roaming numa rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o OS pode permitir ligações VPN durante o roaming.
- **Serviço de dispositivos conectados:** **O bloco** desativa o componente da Plataforma de Dispositivos Conectados (CDP). O CDP permite a descoberta e ligação a outros dispositivos (através de Bluetooth/LAN ou da nuvem) para suportar o lançamento de aplicações remotas, mensagens remotas, sessões de aplicações remotas e outras experiências de dispositivos cruzados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o serviço de dispositivos conectados, que permite a descoberta e ligação a outros dispositivos Bluetooth.
- **NFC**: **O bloco** previne as capacidades de comunicações de campo (NFC) próximas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por defeito, o SISTEMA pode permitir que os utilizadores ativem e configurem as funcionalidades nfc no dispositivo.
- **Wi-Fi**: **O bloco** impede os utilizadores de e ativar, configurar e utilizar ligações Wi-Fi no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir ligações Wi-Fi.
- **Ligue-se automaticamente aos hotspots Wi-Fi**: **O bloco** impede que os dispositivos se conectem automaticamente aos hotspots Wi-Fi. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os dispositivos se conectem automaticamente a hotspots Wi-Fi gratuitos e aceitem automaticamente quaisquer termos e condições para a ligação.
- **Configuração Wi-Fi manual**: **O bloco** impede que os dispositivos se conectem ao Wi-Fi fora das redes instaladas pelo servidor MDM. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores adicionem e configurem as suas próprias redes de ligações Wi-Fi SSIDs.
- **Intervalo de varredura Wi-Fi**: Introduza a frequência com que os dispositivos digitalizam para redes Wi-Fi. Introduza um valor de 1 (mais frequente) a 500 (menos frequente). O padrão é `0` (zero).

### <a name="bluetooth"></a>Bluetooth

Estas definições utilizam a [política Bluetooth CSP,](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth)que também lista as edições suportadas pelo Windows.

- **Bluetooth**: **O bloco** impede os utilizadores de ativarem bluetooth. **Não configurado** (predefinido) permite Bluetooth no dispositivo.
- **Descoberta Bluetooth**: **O bloco** impede que o dispositivo seja detetável por outros dispositivos ativados por Bluetooth. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que outros dispositivos ativados por Bluetooth, como um auricular, descubram o dispositivo.

  [Bluetooth/AllowDiscoverMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Pré-emparelhamento Bluetooth**: **O bloco** impede que dispositivos Bluetooth específicos emparelhem automaticamente com um dispositivo de acolhimento. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o emparelhamento automático com o dispositivo hospedeiro.

  [Bluetooth/Permitir O CSP de emparelhamento](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **Publicidade Bluetooth**: **O bloco** impede que o dispositivo envie anúncios Bluetooth. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que o dispositivo envie anúncios Bluetooth.

  [Bluetooth/Permitir Publicidade CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **Serviços bluetooth permitidos**: **Adicione** uma lista de serviços e perfis Bluetooth permitidos como cordas hexáxinas, tais como `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}` .

  [ServicesAllowedList guia](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) de utilização tem mais informações na lista de serviços.

  [Bluetooth/Serviços PermitidoLista CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## <a name="cloud-and-storage"></a>Cloud e Armazenamento

Estas definições utilizam a política de [contas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts), que também lista as edições suportadas pelo Windows.

> [!IMPORTANT]
> Bloquear ou desativar estas definições de conta da Microsoft pode ter impacto em cenários de inscrição que exigem que os utilizadores assinem no Azure AD. Por exemplo, está a usar [luva branca AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). Normalmente, os utilizadores são mostrados um sinal de Anúncio Azure na janela. Quando estas definições estiverem definidas para **bloquear** ou **desativar,** o sinal de AD Azure pode não aparecer. Em vez disso, pede-se aos utilizadores que aceitem o EULA e criem uma conta local, que pode não ser o que deseja.

- **Conta Microsoft**: **O bloco** impede os utilizadores de associarem uma conta Microsoft ao dispositivo. **O Bloco** também pode ter impacto em alguns cenários de inscrição que dependem dos utilizadores para completar o processo de inscrição. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir adicionar e utilizar uma conta Microsoft.
- **Conta não Microsoft**: **O bloco** impede que os utilizadores adicionem contas não Microsoft utilizando a interface do utilizador. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores adicionem contas de e-mail que não estejam associadas a uma conta Microsoft.
- **Definições de sincronização para a conta microsoft**: O **bloco** impede as definições de dispositivos e aplicações associadas a uma conta Microsoft para sincronizar entre dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir esta sincronização.
- **Assistente de sessão**da Conta Microsoft : Este serviço DE SO permite que os utilizadores insinuem na sua conta Microsoft. Por predefinição, o SISTEMA pode permitir que os utilizadores iniciem e parem o serviço de **Assistente de Início de Conta Microsoft** (wlidsvc).
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores iniciem e parem o serviço de **Assistente de Início de Conta Microsoft** (wlidsvc).
  - **Desativado**: Define o serviço de assistente de acesso da Microsoft (wlidsvc) para Desativado e impede que os utilizadores o iniciem manualmente.

      **O desativação** também pode ter impacto em alguns cenários de inscrição que dependem dos utilizadores para completar a inscrição. Por exemplo, está a usar [luva branca AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). Normalmente, os utilizadores são mostrados um sinal de Anúncio Azure na janela. Quando definido para **desativar,** o sinal de AD Azure pode não aparecer. Em vez disso, pede-se aos utilizadores que aceitem o EULA e criem uma conta local, que pode não ser o que deseja.

## <a name="cloud-printer"></a>Impressora em Cloud

Estas definições utilizam o [CSP da política EnterpriseCloudPrint,](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint)que também lista as edições suportadas pelo Windows.

- **URL de descoberta**da impressora : Introduza o URL para encontrar impressoras em nuvem. Por exemplo, introduza `https://cloudprinterdiscovery.contoso.com`.
- **URL**da autoridade de acesso à impressora : Introduza o URL final de autenticação para obter fichas OAuth. Por exemplo, introduza `https://azuretenant.contoso.com/adfs`.
- **Aplicação de clientes nativos azure GUID**: Insira o GUID de uma aplicação de cliente permitida para obter fichas OAuth da OAuthAuthority. Por exemplo, introduza `E1CF1107-FF90-4228-93BF-26052DD2C714`.
- **Imprimir recurso de serviço URI**: Introduza o recurso OAuth URI para o serviço de impressão configurado no portal Azure. Por exemplo, introduza `http://MicrosoftEnterpriseCloudPrint/CloudPrint`.
- **Impressoras máximas para consulta**: Introduza o número máximo de impressoras que pretende ser consultada. O valor predefinido é `20`.
- **Recurso**de serviço de descoberta de impressora URI : Introduza o recurso OAuth URI para o serviço de descoberta de impressoras configurado no portal Azure. Por exemplo, introduza `http://MopriaDiscoveryService/CloudPrint`.

> [!TIP]
> Depois de configurar uma [Impressão de Cloud Híbrida do Windows Server,](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview)pode configurar estas definições e, em seguida, implementar para os seus dispositivos Windows.

## <a name="control-panel-and-settings"></a>Painel de Controlo e Definições

- **Aplicação definições**: **O bloco** impede que os utilizadores acedam à aplicação de definições do Windows. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores abram a aplicação Definições no dispositivo.
  - **Sistema**: **O bloco** impede o acesso à área do Sistema da aplicação Definições. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
    - **Modificação das definições de alimentação e sono** (apenas no ambiente de trabalho): O **bloco** impede que os utilizadores mudem as definições de energia e de sono no dispositivo. **Não configurado** (predefinido) permite que os utilizadores alterem as definições de energia e de sono.
  - **Dispositivos**: **O bloco** impede o acesso à área de Dispositivos da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Internet da rede**: **O bloco** impede o acesso à rede & área de Internet da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Personalização**: **O bloco** impede o acesso à área de Personalização da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Apps**: **O bloco** impede o acesso à área de Apps da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Contas**: **O bloco** impede o acesso à área de Contas da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Tempo e Idioma**: **O bloco** impede o acesso à área de Idioma horário & da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
    - **Modificação do tempo**do sistema : **O bloco** impede que os utilizadores mudem as definições de data e hora no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Os utilizadores podem alterar estas definições.
    - **Modificação das definições** da região (apenas no ambiente de trabalho): **O bloco** impede que os utilizadores mudem as definições da região no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Os utilizadores podem alterar estas definições.
    - **Modificação das definições de idiomas (apenas no ambiente**de trabalho) : **O bloco** impede que os utilizadores mudem as definições de idioma no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Os utilizadores podem alterar estas definições.

      [Política de Definições CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings)

  - **Gaming**: **O bloco** impede o acesso à área de Jogos da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Facilidade de acesso**: **O bloco** impede o acesso à área de facilidade de acesso da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Privacidade**: **O bloco** impede o acesso à área de privacidade da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Atualização e Segurança**: **O bloco** impede o acesso à área de Atualização & Segurança da aplicação Definições no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="display"></a>Apresentar

Estas definições utilizam a política de [exibição CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-display), que também lista as edições suportadas pelo Windows.

A escala de DPI do DDI permite aplicações que não estão conscientes de DPI para se tornarem por monitorização consciente síPi.

- **Ligue a escala gDI para apps**: **Adicione** as aplicações antigas que deseja a escala de DPI GDI ligada. Por exemplo, introduza: `filename.exe` ou `%ProgramFiles%\Path\Filename.exe`.

  A escala de DPI da GDI está ligada para todas as aplicações antigas da sua lista.

- **Desligue a escala gDI para apps**: **Adicione** as aplicações antigas que deseja que o escalonamento DeDD desligado. Por exemplo, introduza: `filename.exe` ou `%ProgramFiles%\Path\Filename.exe`.

  A escala de DPI do GDI está desligada para todas as aplicações antigas da sua lista.

Também pode **importar** um ficheiro .csv com a lista de aplicações.

## <a name="general"></a>Geral

Estas definições utilizam a política de [experiência CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience), que também lista as edições suportadas pelo Windows. 

- **Captura de ecrã** (apenas móvel): **O bloco** impede que os utilizadores obtem imagens no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Cópia e pasta (apenas para dispositivos móveis)**: **O bloco** impede os utilizadores de utilizarem cópia e pasta entre aplicações no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Desinscrição manual**: **O bloco** impede que os utilizadores aleem a conta no local de trabalho utilizando o painel de controlo do local de trabalho no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  Esta definição de política não se aplica se o computador for Azure AD aderiu e a inscrição automática estiver ativada.

- **Instalação manual** do certificado de raiz (apenas móvel): **Bloco** impede os utilizadores de instalarmanualmente certificados de raiz e certificados intermédios DACAP. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Câmara**: **O bloco** impede que os utilizadores utilizem a câmara no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à câmara do dispositivo.

  Intune só consegue o acesso à câmara do dispositivo. Não tem acesso a fotografias ou vídeos.

  [Câmara CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-camera)

- **Sincronização de ficheiros OneDrive**: **O bloco** impede que os utilizadores sincronizem ficheiros para o OneDrive a partir do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Sistema/DesactivaçãoOneDriveFileSync CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **Armazenamento amovível**: **O bloco** impede os utilizadores de utilizarem dispositivos de armazenamento externos, como cartões SD com o dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Geolocalização**: **O bloco** impede que os utilizadores desligá-lo no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Sistema/Permitir localização CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **Partilha de Internet**: **O bloco** impede a partilha de ligações à Internet no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Reset do telefone**: **O bloco** impede que os utilizadores limpem ou façam uma reinstalação de fábrica no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Ligação USB**: **O bloco** impede o acesso a dispositivos de armazenamento externos através de uma ligação USB no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. O carregamento USB não é afetado por esta definição.

  [Conectividade/Permitir A Conexão CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **Modo AntiTheft** (apenas móvel): **O bloco** impede que os utilizadores selecionem a preferência do modo AntiTheft no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Cortana**: **Bloquear** desativar o assistente de voz Cortana no dispositivo. Quando cortana está desligado, os utilizadores ainda podem pesquisar para encontrar itens no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema Operativo pode permitir cortana.

  [Experiência/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

- **Gravação de voz** (apenas móvel): **O bloco** impede que os utilizadores utilizem o gravador de voz do dispositivo no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a gravação de voz para aplicações.
- **Modificação** do nome do dispositivo (apenas móvel): **O bloco** impede que os utilizadores mudem o nome do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Adicionar pacotes**de provisionamento : **O bloco** impede o agente de configuração do tempo de execução que instala pacotes de fornecimento no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Remova as embalagens**de fornecimento : **O bloco** impede o agente de configuração do tempo de execução que remove as embalagens de fornecimento do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Descoberta do dispositivo**: **O bloco** impede que o dispositivo seja descoberto por outros dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Experiência/Permitir A Descoberta de Dispositivos](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **Comutador de tarefas** (apenas para dispositivo): **O bloco** impede a ligação da tarefa no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- Diálogo de erro do **cartão SIM** (apenas para dispositivos móveis): **Bloqueie** as mensagens de erro de aparecer no dispositivo se não for detetada nenhuma placa SIM. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode mostrar as mensagens de erro.
- **Espaço de trabalho de tinta**: Escolha se e como o utilizador acede ao espaço de trabalho da tinta. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ligar o espaço de trabalho de tinta e os utilizadores podem usá-lo acima do ecrã de bloqueio.
  - **Desativado no ecrã de bloqueio**: O espaço de trabalho da tinta está ativado e a função é ativada. Mas os utilizadores não podem aceder-lhe acima do ecrã de bloqueio.
  - **Desativado:** O acesso ao espaço de trabalho de tinta é desativado. A característica está desligada.

  [Política de espaço WindowsInkWork CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Reset do Piloto Automático**: Escolha **permitir** que os utilizadores com direitos administrativos possam eliminar todos os dados e configurações do utilizador utilizando **CTRL + Win + R** no ecrã de bloqueio do dispositivo. O dispositivo é automaticamente reconfigurado e reinscrito na gestão. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir esta funcionalidade.
- **Exigir que os utilizadores se conectem à rede durante**a configuração do dispositivo : Escolha o **Require** si para que o dispositivo se conecte a uma rede antes de passar pela página da Rede durante a configuração do Windows. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores ultrapassem a página da Rede, mesmo que não esteja ligado a uma rede.

  A regulação torna-se eficaz da próxima vez que o dispositivo for limpo ou reposto. Como qualquer outra configuração Intune, o dispositivo deve ser matriculado e gerido por Intune para receber configurações de configuração. Mas uma vez matriculado, e recebendo políticas, então a reposição do dispositivo impõe a definição durante a próxima configuração do Windows.

  [InquilinoLockdown CSP](https://docs.microsoft.com/windows/client-management/mdm/tenantlockdown-csp)

- **Acesso direto à memória**: **O bloco** impede o acesso direto à memória (DMA) para todas as portas a jusante do PCI pluggable a quente até que um utilizador instem no Windows. **Ativado** (predefinido) permite o acesso ao DMA, mesmo quando um utilizador não está inscrito.

  [Proteção de Dados/Permitir Acesso de Memória Direta CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **Processos finais do Task Manager**: Esta definição determina se os não administradores podem usar o Task Manager para terminar tarefas. **O bloco** impede que os utilizadores padrão (não administradores) utilizem o Task Manager para pôr fim a um processo ou tarefa no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores padrão terminem um processo ou tarefa utilizando o Task Manager.

  [TaskManager/AllowEndTask CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## <a name="locked-screen-experience"></a>Experiência de ecrã bloqueado

- **Notificações do Centro de Ação (apenas para dispositivos)**: **Bloco** impede que as notificações do Action Center apareçam no ecrã de bloqueio do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores escolham quais as aplicações que mostram notificações no ecrã de bloqueio.

  [AboveLock/AllowActionCenterNotifications CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#AboveLock_AllowActionCenterNotifications)

- URL de imagem de **ecrã bloqueado (apenas para desktop)**: Introduza o URL numa imagem em formato JPG, JPEG ou PNG que seja usado como papel de parede de ecrã de bloqueio do Windows. Por exemplo, introduza `https://contoso.com/image.png`. Esta definição bloqueia a imagem, e não pode ser alterada depois.

  [Personalization/LockScreenImageUrl CSP](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)

- Tempo de tempo configurável do **utilizador (apenas para dispositivos móveis)**: **Permitir que** os utilizadores configurem o intervalo do ecrã. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não dar esta opção aos utilizadores.

  [DeviceLock/AllowScreenTimeoutWhileLockedUserConfig CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana no ecrã bloqueado** (apenas no ambiente de trabalho): **O bloco** impede que os utilizadores interajam com o Cortana quando o dispositivo está no ecrã de bloqueio. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a interação com cortana.

  [AboveLock/AllowCortanaAboveLock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Notificações de torradas no ecrã bloqueado**: **O bloco** impede que as notificações de torradas apareçam no ecrã de bloqueio do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir estas notificações.

  [AboveLock/AllowToasts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- Tempo de paragem do **ecrã (apenas para dispositivos móveis)**: Desbloqueie a duração (em segundos) do ecrã para o ecrã desligado. Os valores suportados são 11-1800. Por exemplo, introduza `300` para definir este intervalo de tempo para 5 minutos.

  [DeviceLock/ScreenTimeoutWhileLocked CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Mensagens

Estas definições utilizam a [política de mensagens CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-messaging), que também lista as edições suportadas pelo Windows.

- **Sincronização de mensagens (apenas para dispositivos móveis)**: **O bloco** desativa as mensagens de texto de serem apoiadas e restauradas e de sincronizar mensagens entre dispositivos Windows. A desativação ajuda a evitar que as informações sejam armazenadas em servidores fora do controlo da organização. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem estas definições e sincronizem as suas mensagens.
- **MMS (apenas móvel)**: **O bloco** desativa o envio de MMS e recebe a funcionalidade no dispositivo. Para as empresas, utilize esta política para desativar o MMS nos dispositivos como parte do requisito de auditoria ou gestão. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir o envio e receção de MMS.
- **RCS (apenas móvel)**: **Bloco** desativa Os Serviços de Comunicação Ricos (RCS) enviam e recebem funcionalidades no dispositivo. Para as empresas, utilize esta política para desativar o RCS nos dispositivos como parte do requisito de auditoria ou gestão. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o envio e receção de RCS.

## <a name="microsoft-edge-browser"></a>Browser Microsoft Edge

Estas definições utilizam a política do [navegador CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser), que também lista as edições suportadas pelo Windows.

### <a name="use-microsoft-edge-kiosk-mode"></a>Utilize o modo de quiosque Microsoft Edge

As definições disponíveis mudam dependendo do que escolher. As opções são:

- **Não** (predefinido): o Microsoft Edge não está a funcionar no modo quiosque. Todas as definições do Microsoft Edge estão disponíveis para que altere e configure.
- **Sinalização digital/interativa (quiosque de aplicações únicas)**: Filtra as definições do Microsoft Edge aplicáveis ao modo de quiosque de sinalização Digital/Interactive Microsoft Edge para utilização apenas em quiosques de aplicações únicas do Windows 10. Escolha esta definição para abrir um ecrã completo url e apenas mostrar o conteúdo nesse website. [Configurar sinais digitais](https://docs.microsoft.com/windows/configuration/setup-digital-signage) fornece mais informações sobre esta funcionalidade.
- **Navegação em Público Privado (quiosque de aplicações únicas)**: Filtra as definições do Microsoft Edge aplicáveis ao modo de quiosque de navegação pública inprivate do Microsoft Edge Para utilização em quiosques de aplicações únicas do Windows 10. Executa uma versão multi-tab do Microsoft Edge.
- **Modo normal (quiosque de várias aplicações)**: Filtra as definições do Microsoft Edge aplicáveis ao modo normal do Quiosque do Microsoft Edge. Executa uma versão completa do Microsoft Edge com todas as funcionalidades de navegação.
- **Navegação pública (quiosque de várias aplicações)**: Filtra as definições do Microsoft Edge aplicáveis à navegação pública num quiosque multi-app do Windows 10.  Executa uma versão multi-tab do Microsoft Edge InPrivate.

> [!TIP]
> Para obter mais informações sobre o que estas opções fazem, consulte os tipos de [configuração](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types)do modo de quiosque do Microsoft Edge .

Este perfil de restrições do dispositivo está diretamente relacionado com o perfil do quiosque que cria utilizando as [definições](kiosk-settings-windows.md)do quiosque windows . Em resumo:

1. Crie o perfil de [definições](kiosk-settings-windows.md) do quiosque windows para executar o dispositivo no modo quiosque. Selecione o Microsoft Edge como aplicação e coloque o modo de quiosque Microsoft Edge no perfil do Quiosque.
2. Crie o perfil de restrições do dispositivo descrito neste artigo e configure funcionalidades e configurações específicas permitidas no Microsoft Edge. Certifique-se de que escolhe o mesmo tipo de modo de quiosque do Microsoft Edge, selecionado no seu perfil de[quiosque (definições](kiosk-settings-windows.md)de quiosque windows). 

    [As definições](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) de modo de quiosque suportado são um ótimo recurso.

> [!IMPORTANT] 
> Certifique-se de atribuir este perfil microsoft Edge aos mesmos dispositivos que o seu perfil de quiosque[(definições](kiosk-settings-windows.md)de quiosque windows).

[ConfigureKioskMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>Iniciar experiência

- Inicie o **Microsoft Edge com:** Escolha quais as páginas abertas quando o Microsoft Edge começar. As opções são:
  - **Páginas de início personalizadas**: Introduza as páginas de início, tais como `http://www.contoso.com` . O Microsoft Edge carrega as páginas iniciais em que entra.
  - **Nova página do Separador**: Microsoft Edge carregue o que estiver introduzido na definição de URL do **Novo Separador.**
  - **Página da última sessão**: Microsoft Edge carrega a última página da sessão.
  - **Iniciar páginas nas definições de aplicações locais**: Microsoft Edge começa com a página de início predefinida definida pelo OS.

- **Permitir que o utilizador altere as páginas**de início : **Sim** (padrão) permite que os utilizadores alterem as páginas de início. Os administradores podem utilizar as `EdgeHomepageUrls` para introduzir as páginas iniciais que os utilizadores vêem por padrão quando abrem o Microsoft Edge. **Nenhum** bloqueio aos utilizadores de alterar as páginas de início.
- Permitir o **conteúdo web na nova página do separador**: Quando definido para **Sim** (predefinido), o Microsoft Edge abre o URL introduzido na definição de URL do **Novo Separador.** Se a definição de URL do **Novo Separador** estiver em branco, o Microsoft Edge abre a nova página do separador listada nas definições do Microsoft Edge. Os utilizadores podem mudá-lo. Quando definido para **Não,** o Microsoft Edge abre um novo separador com uma página em branco. Os utilizadores não podem mudá-lo.
- **Novo URL do separador**: Introduza o URL para abrir na página New Tab. Por exemplo, introduza: `https://www.bing.com` ou `https://www.contoso.com`.

- **Botão inicial**: Escolha o que acontece quando o botão inicial é selecionado. As opções são:
  - **Páginas de início**: Abre a opção que escolheu no **Start Microsoft Edge com** definição
  - **Nova página do Separador**: Abre o URL introduzido na definição de URL do **Novo Separador.**
  - **URL do botão inicial**: Introduza o URL para abrir. Por exemplo, introduza: `https://www.bing.com` ou `https://www.contoso.com`.
  - **Botão Hide Home**: Esconde o botão inicial
- **Permitir que os utilizadores alterem**o botão inicial : **Sim** permite que os utilizadores alterem o botão inicial. As alterações do utilizador sobrepõem-se a quaisquer definições de administrador para o botão inicial. **Nenhum** (padrão) impede os utilizadores de alterar a forma como o administrador configurava o botão inicial.
- **Mostrar primeira página de Experiência de Execução (apenas móvel)**: **Sim** (padrão) mostra a primeira página de introdução no Microsoft Edge. **Nenhum** impede que a página de introdução mostre a primeira vez que executa o Microsoft Edge. Esta funcionalidade permite que empresas, como organizações matriculadas em configurações de emissões zero, bloqueiem esta página.
- **Localização** da lista de URL first Run Experience (apenas Windows 10 Mobile): Introduza o URL que aponta para o ficheiro XML que contém o URL ou a primeira página de execução. Por exemplo, introduza `https://www.contoso.com/sites.xml`.

- **Atualizar o navegador após o tempo de inatividade**: Insira o número de minutos inativos até que o navegador seja atualizado, de 0-1440 minutos. Padrão são `5` minutos. Quando definido para `0` (zero), o navegador não atualização depois de estar inativo.

  Esta definição só está disponível quando se executa na [navegação do InPrivate Public (quiosque de aplicações únicas)](#use-microsoft-edge-kiosk-mode).

- **Permitir pop-ups** (apenas desktop): **Sim** (padrão) permite pop-ups no navegador web. **Não** impede que as janelas pop-up no navegador.
- **Envie tráfego intranet para o Internet Explorer** (apenas desktop): **Sim** permite que os utilizadores abram websites intranet no Internet Explorer em vez do Microsoft Edge. Esta definição é para retroceder. **Nenhum** (padrão) permite que os utilizadores utilizem o Microsoft Edge.
- **Localização** da lista de sites do modo enterprise (apenas desktop): Introduza o URL que aponta para o ficheiro XML contendo uma lista de web sites que se abrem no modo Enterprise. Os utilizadores não podem alterar esta lista. Por exemplo, introduza `https://www.contoso.com/sites.xml`.
- **Mensagem ao abrir sites no Internet Explorer**: Utilize esta definição para configurar o Microsoft Edge para mostrar uma notificação antes de um site abrir no Internet Explorer 11. As opções são:
  - **Não mostre mensagem**: O comportamento padrão do OS é usado, o que pode não mostrar uma mensagem.
  - **Mostre a mensagem de que**o site está aberto no Internet Explorer 11 : Mostrar a mensagem ao abrir sites no IE. Sites abertos no IE. 
  - **Mostrar mensagem com opção de abrir sites no Microsoft Edge**: Mostrar a mensagem ao abrir sites no Microsoft Edge. A mensagem inclui um **link Para continuar no Microsoft Edge** para que os utilizadores possam escolher o Microsoft Edge em vez do IE.

  > [!IMPORTANT]
  > Esta definição requer que utilize a definição de localização da lista do **modo Enterprise,** o **tráfego de intranet enviar para** a definição do Internet Explorer ou ambas as definições.

- **Permitir a lista**de compatibilidade da Microsoft : **Sim** (padrão) permite utilizar uma lista de compatibilidade da Microsoft. **Não** impede a lista de compatibilidade da Microsoft no Microsoft Edge. Esta lista da Microsoft ajuda o Microsoft Edge a exibir corretamente sites com problemas de compatibilidade conhecidos.
- **Pré-carregar as páginas de início e a página New Tab:** **Sim** (padrão) utiliza o comportamento padrão do OS, que pode ser pré-carregar estas páginas. A pré-carga minimiza o tempo para iniciar o Microsoft Edge e carregar novos separadores. **Não** impede o Microsoft Edge de pré-carregar as páginas de início e a nova página do separador.
- **Pré-lançamento As páginas de início e a página New Tab**: **Sim** (padrão) usam o comportamento padrão do OS, que pode ser pré-lançamento destas páginas. O pré-lançamento ajuda o desempenho do Microsoft Edge e minimiza o tempo necessário para iniciar o Microsoft Edge. **Não** impede o Microsoft Edge de pré-lançar as páginas de início e a nova página de separadores.

### <a name="favorites-and-search"></a>Favoritos e pesquisa

- **Show Favorites bar**: Escolha o que acontece com o bar favorito em qualquer página do Microsoft Edge. As opções são:
  - **No Início e nas novas páginas do Separador**: Mostra a barra favorita quando o Microsoft Edge começa, e em todas as páginas do Tab. Os utilizadores podem alterar esta definição.
  - **Em todas as páginas**: Mostra o bar favorito em todas as páginas. Os utilizadores não podem alterar esta definição.
  - **Escondido**: Esconde o bar favorito em todas as páginas. Os utilizadores não podem alterar esta definição.
- **Permitir alterações aos favoritos**: **Sim** (padrão) utiliza o padrão DE SO, que permite aos utilizadores alterarem a lista. **Nenhum** impede que os utilizadores adicionem, importem, sequem ou editem a lista dos Favoritos.
  - **Lista de favoritos**: Adicione uma lista de URLs ao ficheiro favorito. Por exemplo, adicione `http://contoso.com/favorites.html`.
- **Sincronizar os favoritos entre os navegadores** da Microsoft (apenas desktop): **Sim** obriga o Windows a sincronizar os favoritos entre o Internet Explorer e o Microsoft Edge. Adições, supressões, modificações e alterações de encomendas aos favoritos são partilhadas entre navegadores.  **Nenhum** (padrão) utiliza o padrão DO, o que pode dar aos utilizadores a opção de sincronizar os favoritos entre os navegadores.
- **Motor de busca predefinido**: Escolha o motor de busca predefinido no dispositivo. Os utilizadores podem alterar este valor a qualquer momento. As opções são:
  - Motor de pesquisa nas definições do Microsoft Edge do cliente
  - Bing
  - Google
  - Yahoo
  - Valor personalizado: No **URL OpenSearch Xml,** introduza um URL HTTPS com o ficheiro XML que inclui o nome curto e o URL para o motor de busca, no mínimo. Por exemplo, introduza `https://www.contoso.com/opensearch.xml`.
- **Mostrar sugestões**de pesquisa : **Sim** (padrão) permite que o seu motor de busca sugira sites à medida que escreve frases de pesquisa na barra de endereços. **Nenhum previne** esta funcionalidade.
- **Permitir alterações no motor**de busca : **Sim** (padrão) permite que os utilizadores adicionem novos motores de busca ou alterem o motor de busca predefinido no Microsoft Edge. Escolha **Não** para evitar que os utilizadores personalizem o motor de busca.

  Esta definição só está disponível quando estiver em [modo Normal (quiosque multi-aplicações)](#use-microsoft-edge-kiosk-mode).

### <a name="privacy-and-security"></a>Privacidade e segurança

- **Permitir a navegação inprivada**: **Sim** (padrão) permite a navegação inPrivate no Microsoft Edge. Depois de fechar todos os separadores InPrivate, o Microsoft Edge elimina os dados de navegação do dispositivo. **Nenhum** impede que os utilizadores abram sessões de navegação InPrivate.
- **Guarde**o histórico de navegação : **Sim** (padrão) permite salvar o histórico de navegação no Microsoft Edge. **Não** impede que se guarde o histórico de navegação.
- **Limpar os dados de navegação na saída** (apenas no ambiente de trabalho): **Sim,** limpa o histórico e navega os dados quando os utilizadores saem do Microsoft Edge. **Nenhum** (padrão) utiliza o padrão DE Os, que pode cache os dados de navegação.
- **Sincronizar as definições do navegador entre os dispositivos do utilizador**: Escolha como pretende sincronizar as definições do navegador entre dispositivos. As opções são:
  - **Permitir**: Permitir sincronizar as definições do navegador Microsoft Edge entre os dispositivos do utilizador
  - **Bloquear e ativar**a sobreposição do utilizador : Sincronização do bloco das definições do navegador Microsoft Edge entre os dispositivos do utilizador. Os utilizadores podem anular esta definição.
  - **Bloco**: Sincronização do bloco da definição do navegador Microsoft Edge entre os dispositivos dos utilizadores. Os utilizadores não podem anular esta definição.

Quando é selecionado "bloquear e ativar a sobreposição do utilizador", o utilizador pode substituir a designação de administração.

- **Permitir o Gestor de Passwords**: **Sim** (predefinido) permite que o Microsoft Edge utilize automaticamente o Password Manager, o que permite aos utilizadores guardar e gerir palavras-passe no dispositivo. **Nenhum** impede o Microsoft Edge de utilizar o Password Manager.
- **Cookies**: Escolha como os cookies são tratados no navegador web. As opções são:
  - **Permitir**: Os cookies são armazenados no dispositivo.
  - **Bloqueie todos os cookies**: Os cookies não são armazenados no dispositivo.
  - **Bloqueie apenas cookies**de terceiros : Os cookies de terceiros ou parceiros não são armazenados no dispositivo.
- **Permitir o auto-enchimento nos formulários**: **Sim** (predefinido) permite que os utilizadores alterem as definições autocompletas no navegador e povoem automaticamente os campos de formulários. **Nenhum** desativa a função de auto-enchimento no Microsoft Edge.
- **Envie cabeçalhos de não-rastreio**: **Sim** envia cabeçalhos de não-rastre para sites que solicitam informações de rastreio (recomendado). **Nenhum** (padrão) não envia cabeçalhos que permitam que os websites rastreiem o utilizador. Os utilizadores podem configurar esta definição.
- Mostrar o endereço IP local **do WebRTC**: **Sim** (padrão) permite que o endereço IP local dos utilizadores seja mostrado ao fazer chamadas telefónicas usando este protocolo. **Não** impede que o endereço IP local dos utilizadores seja mostrado. 
- Permitir a **recolha de dados em azulejoao vivo**: **Sim** (padrão) permite ao Microsoft Edge recolher informações de Live Tiles fixados no menu inicial. **Não** impede a recolha desta informação, o que pode proporcionar aos utilizadores uma experiência limitada.
- **O utilizador pode substituir erros**de certificado : **Sim** (predefinido) permite que os utilizadores acedam a websites que tenham erros de segurança de camadas de camada de tomadas seguras (SSL/TLS). **Nenhum** (recomendado para maior segurança) impede os utilizadores de aceder em sites com erros SSL ou TLS.

### <a name="additional"></a>Adicionais

- **Permitir** o navegador Microsoft Edge (apenas para dispositivos móveis): **Sim** (padrão) permite utilizar o navegador Web Microsoft Edge no dispositivo móvel. **Não** impede a utilização do Microsoft Edge nos dispositivos. Se escolher **Não,** as outras definições individuais aplicam-se apenas ao ambiente de trabalho.
- Permitir a **queda da barra**de endereços : **Sim** (predefinido) permite ao Microsoft Edge mostrar a queda da barra de endereço com uma lista de sugestões. **Nenhum** impede o Microsoft Edge de apresentar uma lista de sugestões numa lista de drop-down quando escreve. Quando definido para **Não,** você:
  - Ajude a minimizar a largura de banda da rede entre os serviços microsoft Edge e Microsoft.
  - Desative as sugestões de **pesquisa e site do Show à medida que escrevo** no Microsoft Edge > Definições.
- **Permita**o modo de ecrã completo : **Sim** (predefinido) permite ao Microsoft Edge utilizar o modo fullscreen, que mostra apenas o conteúdo web e esconde o Microsoft Edge UI. **Não** impede o modo de ecrã completo no Microsoft Edge.
- **Permitir sobre a página das bandeiras**: **Sim** (predefinido) utiliza o padrão S, que pode permitir aceder à `about:flags` página. A `about:flags` página permite que os utilizadores alterem as definições do desenvolvedor e permitam funcionalidades experimentais. **Nenhum** impede que os utilizadores acedam à `about:flags` página no Microsoft Edge.
- **Permitir ferramentas**de desenvolvimento : **Sim** (padrão) permite que os utilizadores utilizem as ferramentas de desenvolvimento F12 para construir e depurar páginas web por padrão. **Nenhum** impede que os utilizadores utilizem as ferramentas de desenvolvimento F12.
- **Permitir que o JavaScript**: **Sim** (padrão) permita que scripts, como o JavaScript, possam ser executados no navegador Microsoft Edge. **Nenhum** impede que os scripts java no navegador funcionassem.
- **O utilizador pode instalar extensões**: **Sim** (predefinido) permite que os utilizadores instalem extensões do Microsoft Edge nos dispositivos. **Nenhum** impede a instalação.
- **Permitir a colocação lateral das extensões do desenvolvedor:** **Sim** (predefinido) utiliza a predefinição do SISTEMA, o que pode permitir a colocação lateral. A sideloading instala e executa extensões não verificadas. **Não** impede o Microsoft Edge de ser utilizado utilizando a função de **extensões de carga.** Não impede que as extensões de sideloading utilizem outras formas, como o PowerShell.
- **Extensões necessárias**: Escolha quais as extensões que não podem ser desligadas pelos utilizadores no Microsoft Edge. Introduza os nomes da família do pacote e selecione **Adicionar**. Encontre um nome de [família de pacote (PFN) para por app VPN](https://docs.microsoft.com/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) fornece alguma orientação.

  Também pode **importar** um ficheiro CSV que inclua os nomes da família do pacote. Ou **exportar** os nomes da família do pacote que você entrar.

## <a name="network-proxy"></a>Proxy de rede

Estas definições utilizam a [política NetworkProxy CSP,](https://docs.microsoft.com/windows/client-management/mdm/networkproxy-csp)que também lista as edições suportadas pelo Windows.

- **Detete automaticamente as definições de procuração:** **Bloquear** desativa os dispositivos ao detetar automaticamente um script proxy auto config (PAC). Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ativar esta funcionalidade e os dispositivos tentam encontrar o caminho para um script PAC.
- **Utilize o script proxy**: Escolha **permitir** introduzir um caminho para o seu script PAC para configurar o servidor proxy. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não permitir que introduza o URL num script PAC.
  - **Configurar**o URL do endereço do script : Introduza o URL de um script PAC que pretende utilizar para configurar o servidor proxy.
- **Utilize o servidor de procuração manual**: Escolha **permitir** introduzir manualmente o nome ou endereço IP e o número de porta TCP de um servidor proxy. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não permitir que introduza manualmente detalhes de um servidor proxy.
  - **Endereço**: Introduza o nome ou endereço IP do servidor proxy.
  - **Número**da porta : Introduza o número de porta do seu servidor proxy.
  - **Exceções proxy**: Introduza quaisquer URLs que não devem utilizar o servidor proxy. Utilize um ponto e vírgula `;` para separar cada item.
  - **Bypass proxy server para endereço local**: **Permitir** não utilizar o servidor proxy para endereços intranet locais. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode utilizar um servidor proxy para endereços locais na sua intranet.

## <a name="password"></a>Palavra-passe

Estas definições utilizam a política de Bloqueio de [Dispositivos CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock), que também lista as edições suportadas pelo Windows.

- **Palavra-passe**: **Exigir** que os utilizadores introduzam uma palavra-passe para aceder ao dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso a dispositivos sem senha. Aplica-se apenas às contas locais. As palavras-passe da conta de domínio permanecem configuradas por Ative Directory (AD) e Azure AD.

  [DeviceLock/DevicePassword-PasswordEnabled CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - Tipo de **palavra-passe necessário:** Escolha o tipo de senha. As opções são:
    - **Não configurado**: Intune não altera nem atualiza esta definição. Por predefinição, o SO pode permitir que a palavra-passe inclua números e letras.
    - **Alfanumérico:** A palavra-passe deve ser uma mistura de números e letras.
    - **Numérico:** A palavra-passe só deve ser números.

    [DeviceLock/AlphanumericDevicePasswordSRequired CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - Comprimento mínimo da **palavra-passe**: Introduza o número mínimo de caracteres necessários, de 4 a 16. Por exemplo, introduza `6` para exigir pelo menos seis caracteres no comprimento da palavra-passe. Por padrão, o SISTEMA pode defini-lo para `4` .
  
    [DeviceLock/MinDevicePasswordLength CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > Quando o requisito da palavra-passe é alterado num ambiente de trabalho do Windows, os utilizadores são impactados da próxima vez que iniciarem o seu inatividade, pois é aí que os dispositivos vão de ocioso para ativo. Os utilizadores com senhas que cumpram o requisito ainda são solicitados a alterar as suas palavras-passe.

  - **Número de falhas de entrada antes de limpar o dispositivo**: Introduza o número de senhas erradas permitidas antes de o dispositivo ser limpo, até 11. O número válido em que entra depende da edição. [DispositivoLock/MaxDevicePasswordFalhade tentativas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) lista os valores suportados. `0`(zero) pode desativar a funcionalidade de limpeza do dispositivo.

    Este cenário também tem um impacto diferente dependendo da edição. Para obter detalhes específicos sobre esta definição, consulte o [DeviceLock/MaxDevicePasswordFailedAttempts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts).

  - **Minutos máximos de inatividade até que o ecrã bloqueie**: Introduza o tempo de tempo em que um dispositivo deve ficar inativo antes de o ecrã estar bloqueado. Por exemplo, introduza os dispositivos de `5` bloqueio após 5 minutos de inatividade. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode defini-lo para `0` (zero), o que não é um intervalo de tempo.

    [DeviceLock/MaxInactivityTimeDeviceLock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **Expiração da palavra-passe (dias)**: Introduza o tempo de tempo nos dias em que a palavra-passe do dispositivo deve ser alterada, de 1 a 365. Por exemplo, `90` introduza para expirar a palavra-passe após 90 dias. Quando o valor está em branco, o Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode defini-lo para `0` (zero), o que não é expiração.

    [DeviceLock/DevicePasswordPasswordExpiration CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **Evite a reutilização de senhas anteriores**: Introduza o número de senhas anteriormente utilizadas que não podem ser utilizadas, de 1 a 24. Por exemplo, introduza para que `5` os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.

    [DeviceLock/DevicePasswordHistory CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **Exija uma palavra-passe quando o dispositivo regressar do estado inativo** (Mobile e Holographic): **Exija que** os utilizadores introduzam uma palavra-passe para desbloquear o dispositivo depois de estarem inativos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não necessitar de um PIN ou palavra-passe depois de estar inativo.

    [DeviceLock/AllowIdleReturnWithoutPassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **Palavras-passe simples**: **O bloco** impede os utilizadores de criarem senhas simples, tais como `1234` ou `1111` . Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores criem senhas simples. Esta definição também bloqueia a utilização de palavras-passe de imagem.

    [DeviceLock/AllowSimpleDevicePassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **Encriptação automática durante o AADJ**: **O bloco** impede a encriptação automática do dispositivo BitLocker quando os dispositivos são preparados para a primeira utilização, e quando os dispositivos são Azure AD unidos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode ativar a encriptação.

  Mais sobre encriptação do [dispositivo BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [Segurança/Prevenir Dispositivos AutomáticosEncriptaçãoForAzureADDispositivos Unidos CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- Política federal de **processamento de informação (FIPS)**: **Permitir** utiliza a política federal de processamento de informação (FIPS), que é um padrão do governo dos EUA para encriptação, hashing e assinatura. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não permitir FIPS.

  [Criptografia/AllowFipsAlgorithmPolicy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Autenticação**do dispositivo Windows Hello : **Permitir que** os utilizadores utilizem um dispositivo de companhia Do Windows Hello, como telefone, banda de fitness ou dispositivo IoT, para iniciar sessão num computador Windows 10. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir que os dispositivos companheiros do Windows Hello se atentiquem.

  [Autenticação/Permitir Autenticação Secundária Dispositivo CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Domínio de inquilino ad-ad-ad preferido**: Introduza um nome de domínio existente na sua organização Azure AD. Quando os utilizadores deste domínio fazem login, não têm de escrever o nome de domínio. Por exemplo, introduza `contoso.com`. Os utilizadores do domínio podem iniciar sessão utilizando o seu nome de `contoso.com` utilizador, `abby` como, em vez de `abby@contoso.com` .

  [Autenticação/PreferredAadTenantDomainName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>Exceções de privacidade por aplicação

**Adicione** aplicações que devem ter um comportamento de privacidade diferente do que define em "Privacidade Padrão".

- **Nome do pacote**: Nome familiar de pacote de aplicativos.
- Nome da **aplicação**: O nome da aplicação.

### <a name="exceptions"></a>Exceções

- **Informações sobre a conta**: Defina se esta aplicação pode aceder ao nome do utilizador, imagem e outras informações de contacto.
- **Aplicativos de fundo**: Defina se esta aplicação pode ser executada em segundo plano.
- **Calendário**: Defina se esta aplicação pode aceder ao calendário.
- **Histórico de chamadas**: Defina se esta aplicação pode aceder ao meu histórico de chamadas.
- **Câmara**: Defina se esta aplicação pode aceder à câmara.
- **Contactos**: Defina se esta aplicação pode aceder a contactos.
- **Email**: Defina se esta aplicação pode aceder e enviar e-mail.
- **Localização**: Defina se esta aplicação pode aceder a informações de localização.
- **Mensagens**: Defina se esta aplicação pode ler ou enviar mensagens de texto ou MMS.
- **Microfone**: Defina se esta aplicação pode utilizar o microfone.
- **Movimento**: Defina se esta aplicação pode aceder a informações de movimento do dispositivo.
- **Notificações**: Defina se esta aplicação pode aceder a notificações.
- **Telefone**: Defina se esta aplicação pode aceder ao telefone.
- **Rádios**: Algumas aplicações utilizam rádios (por exemplo, Bluetooth) no seu dispositivo para enviar e receber dados e precisam de ligar ou desligar estes rádios. Defina se esta aplicação pode controlar estes rádios.
- **Tarefas**: Defina se esta aplicação pode aceder às suas tarefas.
- **Dispositivos fidedignos**: Escolha se esta aplicação pode utilizar dispositivos fidedignos. Os dispositivos fidedignos são hardware que já ligou, ou hardware que vem com o dispositivo. Por exemplo, utilize televisões, projetores, e assim por diante, como dispositivos fidedignos.
- **Feedback e diagnósticos**: Defina se esta aplicação pode aceder a informações de diagnóstico.
- **Sincronizar com dispositivos**: Escolha se esta aplicação pode partilhar e sincronizar automaticamente informações com dispositivos sem fios que não emparelhem explicitamente com o dispositivo.

## <a name="personalization"></a>Personalização

Estas definições utilizam a política de [personalização CSP,](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)que também lista as edições suportadas pelo Windows.

- URL de imagem de fundo de ambiente de **trabalho (apenas desktop)**: Introduza o URL numa imagem em .jpg, .jpeg ou .png que pretende utilizar como papel de parede do Windows. Os utilizadores não podem alterar a imagem. Por exemplo, introduza `https://contoso.com/logo.png`.

  Quando deixada em branco, intune não altera nem atualiza esta definição.

## <a name="printer"></a>Impressora

- **Impressoras**: Adicione impressoras utilizando os nomes dos anfitriões da rede (nome DNS). O Sistema operativo procura e instala controladores de impressora correspondentes para cada impressora do dispositivo. Se não introduzir um valor, a Intune não altera nem atualiza esta definição.

  [Educação/ImpressoraNomes CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-printernames)

- **Impressora predefinida**: Introduza o nome do anfitrião da rede (nome DNS) de uma impressora instalada para utilizar como impressora predefinida. Se não introduzir um valor, a Intune não altera nem atualiza esta definição.

  [Educação/DefaultprinterName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **Adicione novas impressoras**: **O bloco** impede os utilizadores de adicionarem novas impressoras. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a adição de novas impressoras.

  [Educação/Prevenção De Novos Velocistas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## <a name="privacy"></a>Privacidade

Estas definições utilizam a política de [privacidade CSP,](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy)que também lista as edições suportadas pelo Windows.

- **Experiência de privacidade**: **O bloco** impede que a experiência de privacidade abra quando os utilizadores iniciarem o seu insessão e de abrir em utilizadores novos e atualizados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Privacidade/DesativaçãoExperiência](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **Personalização de entrada**: **O bloco** impede o uso da voz para ditado e para falar com cortana e outras aplicações que usam o reconhecimento de voz baseado na nuvem da Microsoft. É desativado e os utilizadores não podem permitir o reconhecimento de voz online usando configurações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores escolham. Se permitir estes serviços, a Microsoft recolherá os dados de voz para melhorar o serviço.

  [Privacidade/Permitir Personalização CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **Aceitação automática dos pedidos de consentimento do utilizador de emparelhamento e privacidade**: Escolha **permitir** para que o Windows possa aceitar automaticamente mensagens de emparelhamento e consentimento de privacidade ao executar aplicações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir a aceitação automática.

  [Privacidade/PermitirAutoAcceptPairingAndPrivacyConsentPrompts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **Publicar atividades de utilizador**: **O bloco** impede que as aplicações e o SO publiquem atividades de utilizador. Também impede experiências partilhadas e descoberta de recursos recentemente utilizados no feed de atividade. As Atividades do Utilizador acompanham o estado das tarefas de um utilizador numa aplicação ou no SISTEMA. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode ativar esta funcionalidade para que as aplicações possam publicar as atividades dos utilizadores.

  [Atividades de privacidade/publicação CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **Atividades locais apenas**: **O Bloco** impede experiências partilhadas e a descoberta de recursos recentemente utilizados no comutador de tarefas, baseados apenas na atividade local. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

Pode configurar informações que todas as aplicações do dispositivo podem aceder. Além disso, defina exceções numa base por app utilizando **exceções de privacidade per-app.**

### <a name="exceptions"></a>Exceções

- **Informações sobre a conta**: Defina se esta aplicação pode aceder ao nome do utilizador, imagem e outras informações de contacto.
- **Aplicativos de fundo**: Defina se esta aplicação pode ser executada em segundo plano.
- **Calendário**: Defina se esta aplicação pode aceder ao calendário.
- **Histórico de chamadas**: Defina se esta aplicação pode aceder ao meu histórico de chamadas.
- **Câmara**: Defina se esta aplicação pode aceder à câmara.
- **Contactos**: Defina se esta aplicação pode aceder a contactos.
- **Email**: Defina se esta aplicação pode aceder e enviar e-mail.
- **Localização**: Defina se esta aplicação pode aceder a informações de localização.
- **Mensagens**: Defina se esta aplicação pode ler ou enviar mensagens de texto ou MMS.
- **Microfone**: Defina se esta aplicação pode utilizar o microfone.
- **Movimento**: Defina se esta aplicação pode aceder a informações de movimento do dispositivo.
- **Notificações**: Defina se esta aplicação pode aceder a notificações.
- **Telefone**: Defina se esta aplicação pode aceder ao telefone.
- **Rádios**: Algumas aplicações utilizam rádios (por exemplo, Bluetooth) no seu dispositivo para enviar e receber dados e precisam de ligar ou desligar estes rádios. Defina se esta aplicação pode controlar estes rádios.
- **Tarefas**: Defina se esta aplicação pode aceder às suas tarefas.
- **Dispositivos fidedignos**: Escolha se esta aplicação pode utilizar dispositivos fidedignos. Os dispositivos fidedignos são hardware que já ligou, ou hardware que vem com o dispositivo. Por exemplo, utilize televisões, projetores, e assim por diante, como dispositivos fidedignos.
- **Feedback e diagnósticos**: Escolha se esta aplicação pode aceder a informações de diagnóstico.
- **Sincronização com dispositivos** – defina se esta aplicação pode partilhar e sincronizar automaticamente informações com dispositivos sem fios que não sejam emparelhados especificamente com o PC, tablet ou telefone.

## <a name="projection"></a>Projeção

Estas definições utilizam o [CSP da política WirelessDisplay,](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay)que também lista as edições suportadas pelo Windows.

- **Entrada do utilizador dos recetores de visualização sem fios**: **O bloco** impede a entrada do utilizador dos recetores de visualização sem fios. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que um ecrã sem fios envie teclado, rato, caneta e entrada no dispositivo de origem.

  [WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **Projeção para este PC**: **O bloco** impede que outros dispositivos encontrem o dispositivo para projeção e impeça a projeção de outros dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os dispositivos sejam detetáveis e pode projetar para o dispositivo acima do ecrã de bloqueio.

  [WirelessDisplay/AllowProjectionFromPC CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **Exigir PIN para emparelhamento**: **Exija** sempre indicações para um PIN quando ligar a um dispositivo de projeção. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não necessitar de um PIN para emparelhar o dispositivo.

  [WirelessDisplay/RequirePinForPairing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## <a name="reporting-and-telemetry"></a>Relatórios e telemetria

- **Partilhar dados de utilização**: Escolha o nível de dados de diagnóstico que são submetidos. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores escolhem o nível que é submetido. Por padrão, o SO pode não partilhar quaisquer dados.
  - **Segurança**: Informações necessárias para ajudar a manter o Windows mais seguro, incluindo dados sobre as definições de experiência de utilizador conectado e de componentes de telemetria, a Ferramenta de Remoção de Software Malicioso e o Microsoft Defender
  - **Básico**: Informações básicas do dispositivo, incluindo dados relacionados com a qualidade, compatibilidade de aplicações, dados de utilização de aplicações e dados do nível de Segurança
  - **Enhanced**: Insights adicionais, incluindo como windows, Windows Server, System Center e apps são usados, como eles executam, dados avançados de fiabilidade, e dados tanto dos níveis básico si e dos níveis de Segurança
  - **Completo**: Todos os dados necessários para identificar e ajudar a corrigir problemas, além de dados do nível de Segurança, Básico e Melhorado.

  [Sistema/Permitir Telemetria CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- Envie os dados de navegação do **Microsoft Edge para o Microsoft 365 Analytics**: Para utilizar esta funcionalidade, detete as definições de dados de **utilização** do Share para **'Enhanced'** ou **Full**. Esta funcionalidade controla os dados que o Microsoft Edge envia para o Microsoft 365 Analytics para dispositivos empresariais com um ID comercial configurado. As opções são:
  - **Não configurado**: Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não recolher ou enviar quaisquer dados do histórico de navegação.
  - **Enviar apenas dados intranet**: Permite ao administrador enviar histórico de dados intranet.
  - **Enviar apenas dados**da Internet : Permite ao administrador enviar o histórico de dados da Internet.
  - **Enviar dados intranet e internet**: Permite ao administrador enviar histórico de dados intranet e internet.

  [Browser/ConfigureTelemettryForMicrosoft365Analytics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Servidor proxy de telemetria**: Introduza o nome de domínio totalmente qualificado (FQDN) ou endereço IP de um servidor proxy para retransmitir experiências de utilizador conectadas e pedidos de telemetria, utilizando uma ligação Secure Sockets Layer (SSL). O formato para esta definição é *servidor*:*porta*. Se o representante nomeado falhar, ou se não for introduzido um representante, os dados connected User Experiences e Telemettry não são enviados. Fica no dispositivo local.

  Se não introduzir um valor, a Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode enviar os dados connected user experiences e telemetria para a Microsoft utilizando a configuração de proxy predefinido.

  Formatos de exemplo:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [Sistema/TelemettryProxy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

## <a name="search"></a>Pesquisa

Estas definições utilizam a política de [pesquisa CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search), que também lista as edições suportadas pelo Windows.

- **Pesquisa Segura (apenas móvel)**: Controle como a Cortana filtra o conteúdo adulto nos resultados da pesquisa. As opções são:
  - **Utilizador definido**: Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores escolhem as suas próprias definições.
  - **Estrita:** Filtragem mais elevada contra conteúdo adulto
  - **Moderado**: Filtragem moderada contra conteúdo adulto. Os resultados de pesquisa válidos não são filtrados.
- **Mostrar resultados web em pesquisa**: **O Bloco** impede que os utilizadores utilizem o Windows Search para pesquisar a internet e os resultados da web não são mostrados na Pesquisa. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores procurem na web e os resultados são mostrados no dispositivo.
- **Diacritics**: **O bloco** impede que os diacríticos sejam mostrados na Pesquisa do Windows. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SO pode mostrar diacritics.

  [Pesquisa/Permitir UsarDiacritics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **Deteção automática de idiomas**: **O bloco** impede que o Windows Search detete automaticamente o idioma ao indexar conteúdo ou propriedades. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.

  [Pesquisa/AlwaysUseAutoLangDetection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **Local**de pesquisa : **O bloco** impede que o Windows Search utilize a localização. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.

  [Pesquisa/Permitir Pesquisa/Permitir Pesquisa de Utilização CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **Recuo do indexante:** **O bloco** desativa a função de backoff do indexante de pesquisa. A indexação continua a toda velocidade, mesmo que a atividade do sistema seja elevada. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode usar a lógica de backoff para acelerar a atividade de indexação quando a atividade do sistema é elevada.

  [Pesquisa/DisableBackoff CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **Indexação de unidades amovíveis**: **O bloco** impede que as localizações em unidades amovíveis sejam adicionadas às bibliotecas e sejam indexadas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.

  [CSP de pesquisa/desativação de DriveIndexing](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **Indexação de espaço**de disco baixo: **Ativar** permite a indexação automática, mesmo quando o espaço do disco é baixo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode desligar a indexação automática quando o espaço do disco rígido é de 600 MB ou menos. Se os dispositivos da sua organização tiverem um espaço limitado de disco rígido, então deite-o para **Não configurado**.

  [Pesquisa/PrevençãoDeIndexingLowDiskSpaceMB CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **Consultas remotas**: **Ativar** permite consultas remotas do índice do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir que os utilizadores questionem o índice do dispositivo remotamente.

  [Pesquisa/Prevenção de Remotos CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## <a name="start"></a>Iniciar

Estas definições utilizam a política de [início CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start), que também lista as edições suportadas pelo Windows.  

- **Configurar o menu**: Faça upload de um ficheiro XML que inclui as suas personalizações, incluindo a encomenda que as aplicações estão listadas, e muito mais. O ficheiro XML substitui o layout de início predefinido. Os utilizadores não podem alterar o layout do menu inicial em que entra.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Início/StartLayout CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **Pin websites para azulejos no menu Iniciar**: Importar imagens do Microsoft Edge. Estas imagens são mostradas como links no menu Windows Start para dispositivos de ambiente de trabalho. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Start/ImportEdgeAssets CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **Despin apps da barra de tarefas**: **O bloco** impede que os utilizadores desinfem as aplicações da barra de tarefas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores desfixem as aplicações a partir da barra de tarefas.

  [Iniciar/NopinningToTaskbar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **Troca rápida do utilizador**: **O bloco** evita alternar entre os utilizadores que estão ligados simultaneamente sem o desligamento. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode mostrar o **utilizador da Switch** no azulejo do utilizador.

  [Iniciar/Ocultar Conta CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Aplicativos mais utilizados**: **Bloco** esconde as aplicações mais usadas de mostrar no menu inicial. Também desativa o seletor correspondente na aplicação Definições. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode mostrar as aplicações mais utilizadas.

  [Iniciar/Ocultar Apps Frequentemente Utilizados CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **Aplicações recentemente adicionadas**: **Block** hides recentemente adicionadoapps no menu inicial. Também desativa o seletor correspondente na aplicação Definições. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode mostrar as aplicações recentemente adicionadas no menu inicial.

  [Início/HideRecentlyAddedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **Modo de arranque**: Escolha o tamanho do ecrã inicial. As opções são:
  - **Utilizador definido**: Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores podem definir o tamanho.
  - **Ecrã completo**: Força um tamanho completo do Arranque.
  - **Ecrã não completo**: Force um tamanho de arranque não completo.

  [Início/Força StartSize CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **Itens recentemente abertos em Listas**de Salto : **Bloco** esconde listas de salto recentes de serem mostradas no menu inicial e na barra de tarefas. Também desativa o seletor correspondente na aplicação Definições. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode mostrar itens recentemente abertos nas listas de jumplists.

  [Iniciar/OcultarRecentesJumplists CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **Lista de aplicações**: Escolha como são mostradas as listas de todas as aplicações. As opções são:
  - **Utilizador definido**: Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores escolhem como é mostrada a lista de aplicações.
  - **Colapso**: Esconde a lista de todas as aplicações.
  - **Colapso e desativar a aplicação Definições**: Oculta a lista de todas as aplicações e desativa a lista de **aplicações do Show no menu Iniciar** na aplicação Definições.
  - **Remove e desativa a aplicação Definições**: Oculta a lista de todas as aplicações, remove todos os botões de aplicações e desativa a lista de **aplicações do Show no menu Iniciar** na aplicação Definições.

  [CSP de início/hideapplist](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **Botão de alimentação**: **Bloquear** esconde o botão de alimentação no menu inicial. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode mostrar o botão de alimentação.

  [Arranque/HidepowerButton CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **Tile do utilizador**: **Bloquear** esconde o azulejo do utilizador no menu inicial. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode mostrar o azulejo do utilizador. Configure as seguintes definições:
  - **Bloqueio**: **Bloquear** esconde a opção **Lock** no azulejo do utilizador no menu inicial.  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode mostrar a opção **Lock.**
  - **Sinal de saída**: **O bloco** esconde a opção **Sign out** no azulejo do utilizador no menu inicial. **Não configurado** (predefinido) mostra a opção **'Sair'** de sinal.

  [Iniciar/Ocultar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **Desligar**: **Bloquear** esconde a **Atualização e desliga** e **desliga** as opções no botão de alimentação no menu inicial. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Início/HideshutDown CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **Sleep**: **Bloco** esconde a opção **Sleep** no botão de alimentação no menu inicial. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Início/Hidesleep CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **Hibernar**: **Bloco** esconde a opção **Hibernate** no botão de alimentação no menu inicial. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Iniciar/Ocultar Hibernar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **Conta Switch**: **Bloquear** esconde a **conta Switch** no azulejo do utilizador no menu inicial. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Iniciar/Ocultar Conta CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Opções**de reiniciar : **Bloquear** esconde as opções **de Atualização e reiniciar** e **reiniciar** no botão de alimentação no menu inicial. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  [Início/HideRestart CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **Documentos no Início:** Ocultar ou mostrar a pasta Documentos no menu Início do Windows. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/Permitir Documentos de Pastas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **Downloads on Start:** Hide or show the Downloads folder in the Windows Start menu. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/PermitirTransferências de Pastas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **Explorador de ficheiros no início**: Ocultar ou mostrar o File Explorer no menu Windows Iniciar. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/PermitirOFileExplorer CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **HomeGroup on Start**: Esconda ou mostre o atalho homeGroup no menu Windows Iniciar. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/PermitirOHomeGroup CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **Música no Início**: Ocultar ou mostrar a pasta Música no menu Windows Iniciar. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/PermitirPastaMusic CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **Rede no Início**: Ocultar ou mostrar rede no menu Windows Iniciar. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/Permitir A Rede de Pastas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **Pasta pessoal no Início**: Ocultar ou mostrar pasta pessoal no menu Windows Iniciar. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/PermitirPasta Pessoal CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **Imagens no Início**: Ocultar ou mostrar a pasta para imagens no menu Windows Iniciar. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/PermitirPastasDeS CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **Definições no início**: Ocultar ou mostrar o atalho de Definições no menu Início do Windows. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/Permitir Definições de Pastas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **Vídeos no Início**: Ocultar ou mostrar a pasta para vídeos no menu Windows Iniciar. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores optam por mostrar ou esconder o atalho.
  - **Ocultar**: O atalho está escondido e a definição é desativada na aplicação Definições.
  - **Mostra**: O atalho é mostrado e a definição é desativada na aplicação Definições.

  [Iniciar/Permitir Vídeos de Pastas De Pastas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen para o Microsoft Edge**: **Exija** ligações no Microsoft Defender SmartScreen e impede que os utilizadores o desliguem. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ligar o SmartScreen e permitir que os utilizadores o liguem e desliguem.

  O Microsoft Edge utiliza o Microsoft Defender SmartScreen (ligado) para proteger os utilizadores de potenciais esquemas de phishing e software malicioso.

  [Browser/AllowSmartScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Acesso malicioso ao site**: **O Bloco** impede os utilizadores de ignorarem os avisos do Filtro SmartScreen do Microsoft Defender e bloqueia-os de irem para o site. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores ignorem os avisos e continuem no site.

  [Browser/PreventSmartScreenPromptOverride CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- Download de **ficheiros não verificados**: **O Bloco** impede os utilizadores de ignorarem os avisos do Filtro SmartScreen do Microsoft Defender e impede-os de descarregar ficheiros não verificados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores ignorem os avisos e continuem a descarregar os ficheiros não verificados.

  [Navegador/PreventSmartScreenPromptoveroverforFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Destaque do Windows

Estas definições utilizam a política de [experiência CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience), que também lista as edições suportadas pelo Windows.

- **Windows Spotlight**: **O bloco** desliga os holofotes do Windows no ecrã de bloqueio, no Windows Tips, nas funcionalidades do consumidor da Microsoft e noutras funcionalidades relacionadas. Se o seu objetivo é minimizar o tráfego de rede a partir de dispositivos, então selecione **Sim**. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir funcionalidades de destaque do Windows e pode ser controlado pelos utilizadores.

  [Experiência/permitirwindowsspotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  Quando definido para **Não configurado,** também pode permitir ou bloquear as seguintes definições:

  - **Windows Spotlight no ecrã de bloqueio**: O **bloco** impede o Windows Spotlight de mostrar informações no ecrã de bloqueio do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode mostrar informações sobre os holofotes do Windows no ecrã de bloqueio.

    [Experiência/ConfigureWindowsSpotlightOnLockScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Sugestões de terceiros no Windows Spotlight**: **Block** impede o Windows Spotlight de sugerir conteúdo que não seja publicado pela Microsoft. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS pode permitir sugestões de apps e conteúdos de parceiros, e mostrar aplicações sugeridas no menu Iniciar e dicas do Windows.

    [Experiência/PermitirSugestões ThirdPartyInWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **Características**do Consumidor : **O bloco** desliga experiências que são normalmente para os consumidores, tais como sugestões de início, notificações de adesão, instalação de aplicações pós-off-out de box experience e azulejos redirecionados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

    [Experiência/permitirjanelasCaracterísticas de consumo cSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Dicas do Windows**: **Bloquear** desativa dicas de janela pop-up. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que as Dicas do Windows apareçam.

    [Experiência/permitirjanelas CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **Windows Spotlight no centro**de ação : **Bloco** impede que as notificações do Windows sejam vistas no Centro de Ação. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS poderá apresentar notificações no Action Center que sugerem aplicações ou funcionalidades para ajudar os utilizadores a serem mais produtivos no Windows.

    [Experiência/permitirwindowsspotlightonActioncenter cSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Personalização do Windows Spotlight**: **O bloco** impede que o Windows utilize dados de diagnóstico para fornecer experiências personalizadas aos utilizadores. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que a Microsoft utilize dados de diagnóstico para fornecer recomendações personalizadas, dicas e ofertas para adaptar o Windows às necessidades do utilizador.

    [Experiência/Experiências Personalizadas Com DiagnosticData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Experiência de boas-vindas do Windows**: **O bloco** desliga a funcionalidade de boas-vindas do Windows Windows. A experiência de boas-vindas do Windows não vai aparecer quando existem atualizações e alterações no Windows e nas suas aplicações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS pode permitir ao Windows uma experiência de boas-vindas que mostra aos utilizadores informações sobre funcionalidades novas ou atualizadas.

    [Experiência/permitirwindowsSpotlightWindowsWelcomeExperience CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## <a name="microsoft-defender-antivirus"></a>Antivírus Do Microsoft Defender

Estas definições utilizam a [política de defensores CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender), que também lista as edições suportadas do Windows.

- **Monitorização em tempo real**: **Ativar** a verificação em tempo real de malware, spyware e outros softwares indesejados. Os utilizadores não podem desligá-lo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA liga esta funcionalidade e permite que os utilizadores a alterem.

  Se ativar esta definição e, em seguida, mudá-la para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/Permitir Monitorização Real](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Monitorização do comportamento**: **Ativar** a monitorização do comportamento e verificar certos padrões conhecidos de atividade suspeita em dispositivos. Os utilizadores não podem desligar a monitorização do comportamento. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ligar a Monitorização de Comportamento e permitir que os utilizadores o alterem.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/Permitir Comportamentos Monitores CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Sistema de Inspeção de Rede (NIS)**: O NIS ajuda a proteger os dispositivos contra explorações baseadas em rede. Utiliza as assinaturas de vulnerabilidades conhecidas do Microsoft Endpoint Protection Center para ajudar a detetar e bloquear tráfego malicioso.

  - **Ativar**: Liga a proteção da rede e o bloqueio da rede. Os utilizadores não podem desligá-lo. Quando ativados, os utilizadores estão impedidos de se ligarem a vulnerabilidades conhecidas.

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA liga o NIS e permite que os utilizadores o alterem.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/EnableNetworkProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Scaneie todos os downloads**: **Enable** liga esta definição e o Defender verifica todos os ficheiros descarregados a partir da Internet. Os utilizadores não podem desligar esta definição. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ligar esta definição e permitir que os utilizadores a alterem.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/AllowIOAVProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Scanscripts carregados nos navegadores web**da Microsoft : **Enable** permite ao Defender digitalizar scripts que são usados no Internet Explorer. Os utilizadores não podem desligar esta definição. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ligar esta definição e permitir que os utilizadores a alterem.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/PermitirScriptScantil CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Acesso final ao utilizador ao Defender**: **Bloquear** esconde a interface de utilizador do Microsoft Defender dos utilizadores. Todas as notificações do Microsoft Defender também são suprimidas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso do utilizador ao Microsoft Defender UI e permitir que os utilizadores o alterem.

  Se bloquear a definição e, em seguida, mudá-la para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  Quando esta definição é alterada, entra em vigor da próxima vez que o dispositivo for reiniciado.

  [Defender/permitir useruiaccess cSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- Intervalo de atualização da inteligência de **segurança (em horas)**: Introduza o intervalo que o Defender verifica por novas informações de segurança, de 0 a 24. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. A predefinição do sistema operativo pode verificar se há atualizações a cada 8 horas.
  - **Não verifique:** O Defender não verifica novas atualizações de informações de segurança.
  - **1-24:** `1` verifica de hora a hora, verifica de duas em duas `2` horas, verifica todos os `24` dias, e assim por diante.
  
  [CSP de intervalo de intervalo de atualização de defender/assinatura](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- Monitorizar a atividade de **ficheiros e programas:** Permite ao Defender monitorizar a atividade de ficheiros e programas nos dispositivos. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. A predefinição do sistema operativo pode monitorizar todos os ficheiros.
  - **Monitorização desativadas**
  - **Monitorizar todos os ficheiros**
  - **Monitorizar apenas os ficheiros de entrada**
  - **Monitorizar apenas ficheiros de saída**

  [Defender/RealTimeScanDirection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Dias antes**de apagar malware em quarentena : Continue a rastrear malware resolvido durante o número de dias em que entra para poder verificar manualmente dispositivos anteriormente afetados. 

  Se não configurar esta definição, ou defini-la para `0` dias, o malware permanece na pasta quarentena e não é automaticamente removido. Quando definidopara , os itens de `90` quarentena são armazenados durante 90 dias no sistema e, em seguida, removidos.

  [Defender/DaysToReterMalware Limpo CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- Limite de utilização do **CPU durante uma varredura:** Limite a quantidade de CPU que os exames são autorizados a usar, de `0` para por `100` cento. Por padrão, o SISTEMA pode fixá-lo em 50%.
- **Ficheiros**de arquivo de digitalização : **Ativar** as ligações do Defender para que digitale ficheiros de arquivo, tais como ficheiros Zip ou Cab. Os utilizadores não podem desligar esta definição. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ligar esta digitalização e permitir que os utilizadores a alterem.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/PermitirArchiveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Digitalizar mensagens de correio de entrada**: **Enable** permite ao Defender digitalizar mensagens de correio eletrónico à medida que chegam aos dispositivos. Quando ativado, o motor analisa a caixa de correio e os ficheiros de correio para analisar o corpo de correio e os anexos. Pode digitalizar os formatos .pst (Outlook), .dbx, .mbx, MIME (Outlook Express) e BinHex (Mac).

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA desliga esta digitalização e permite que os utilizadores a alterem.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/PermitirEmailScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Passe a varredura durante uma varredura completa**: **Ative** as ligações das unidades amovíveis do Defender durante uma varredura completa. Os utilizadores não podem desligar esta definição. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que o Defender possa digitalizar unidades amovíveis, como as pen USB, e permitir que os utilizadores alterem esta definição.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Durante uma varredura rápida, as unidades amovíveis podem ainda ser digitalizadas.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/PermitirFullScanRemovableDriveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Scan estão mapeadas durante uma varredura completa**: **Enable** tem ficheiros de digitalização Defender em unidades de rede mapeadas. Se os ficheiros da unidade forem apenas de leitura, o Defender não pode remover qualquer malware encontrado neles. Os utilizadores não podem desligar esta definição.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA liga esta funcionalidade e permite que os utilizadores a alterem.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado. 

  Durante uma varredura rápida, as unidades de rede mapeadas podem ainda ser digitalizadas.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/AllowFullScanOnMappedNetworkDrives CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Ficheiros de digitalização abertos**a partir de pastas de rede : **Enable** tem ficheiros de scans Do Defender abertos a partir de pastas de rede ou unidades de rede partilhadas, tais como ficheiros acedidos a partir de um caminho UNC. Os utilizadores não podem desligar esta definição. Se os ficheiros da unidade forem apenas de leitura, o Defender não pode remover qualquer malware encontrado neles.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA digitaliza ficheiros abertos a partir de pastas de rede e permite que os utilizadores os alterem.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/Permitir a digitalização DeNetworkFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Proteção da nuvem**: **Ative** activao serviço de proteção ativa da Microsoft para receber informações sobre a atividade de malware a partir de dispositivos que gere. Os utilizadores não podem alterar esta definição. 

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA permite que o Serviço de Proteção Ativa da Microsoft receba informações e permite que os utilizadores alterem esta definição.

  Se ativar a definição e, em seguida, troque-a novamente para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado.

  Intune não desliga esta característica. Para desativá-lo, utilize um URI personalizado.

  [Defender/Permitir CloudProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Solicitação aos utilizadores antes**da submissão da amostra : Controla se ficheiros potencialmente maliciosos que possam necessitar de análises adicionais são automaticamente enviados para a Microsoft. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. A predefinição do sistema operativo pode enviar automaticamente amostras seguras.
  - **Sempre rápido**
  - **Solicitação antes de enviar dados pessoais**
  - **Nunca envie dados**
  - **Envie todos os dados sem aviso:** Os dados são enviados automaticamente.

  [Defender/Submeter AmostrasConsent CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Hora de efetuar uma varredura rápida diária:** Escolha a hora para fazer uma varredura rápida diária. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SO pode executar esta varredura às 2 da manhã.

  Se quiser mais personalização, configure o **tipo de digitalização do sistema para executar a** definição.

  [Defender/AgendaQuickScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Tipo de verificação do sistema para realizar:** Agende uma verificação do sistema, incluindo o nível de digitalização, e o dia e a hora para executar a verificação. As opções são:
  - **Não configurado**: Intune não altera nem atualiza esta definição. Nenhuma definição é forçada. Os utilizadores podem executar manualmente as digitalizações conforme necessário ou desejado nos seus dispositivos.
  - **Desativação**: Desativa qualquer digitalização do sistema nos dispositivos. Escolha esta opção se estiver a utilizar uma solução antivírus parceira que digitaliza dispositivos.
  - **Sondagem rápida**: Olha para locais comuns onde pode haver malware registado, como chaves de registo e pastas de arranque conhecidas do Windows.
    - **Dia agendado**: Escolha o dia para executar a varredura.
    - **Horário programado**: Escolha a hora para executar a varredura.
  - **Varredura completa**: Olha para locais comuns onde pode haver malware registado, e também digitaliza todos os ficheiros e pastas do dispositivo.
    - **Dia agendado**: Escolha o dia para executar a varredura.
    - **Horário programado**: Escolha a hora para executar a varredura.

  > [!TIP]
  > Esta definição pode entrar em conflito com o Tempo para realizar uma configuração diária de **digitalização rápida.** Algumas recomendações:  
  >
  > - Se quiser agendar uma sondagem rápida diária e uma varredura semanal completa, então:
  >   1. Configure o tempo para realizar uma configuração diária de **digitalização rápida.**
  >   2. Configure o **tipo de digitalização do sistema para realizar** uma varredura completa.
  > 
  > - Se só quiser uma digitalização rápida diariamente (sem digitalização completa), utilize qualquer uma das definições: **Tempo para efetuar uma varredura rápida diária** ou tipo de sistema para **realizar**. Por exemplo, para fazer uma sondagem rápida todas as terças-feiras às 6 da manhã, configurar o **tipo de digitalização do sistema para executar a** definição.
  > 
  > - Não configure o **Tempo para efetuar uma configuração diária** de digitalização rápida simultaneamente com o tipo de **digitalização do sistema para executar** o conjunto para uma varredura **rápida**. Estas configurações podem entrar em conflito, e uma varredura pode não ser executada.

  [Defender/ScanParameter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [Defender/AgendaScanDay CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [Defender/AgendaScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **Detete aplicações potencialmente indesejadas**: Esta funcionalidade identifica e bloqueia aplicações potencialmente indesejadas (PUA) de descarregar e instalar na sua rede. Estas aplicações não são consideradas vírus, malware ou outros tipos de ameaças. Mas podem executar ações em pontos finais que podem afetar o seu desempenho ou uso. Escolha o nível de proteção quando o Windows detetar ApIs. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o Microsoft Defender poderá desativar esta funcionalidade.
  - **Bloco**: O Microsoft Defender deteta APIs e os itens detetados estão bloqueados. Estes itens aparecem na história juntamente com outras ameaças.
  - **Auditoria**: Microsoft Defender deteta APIs, mas não toma medidas. Pode rever informações sobre as aplicações contra as que o Microsoft Defender iria tomar medidas. Por exemplo, procure eventos criados pelo Microsoft Defender no Observador de Eventos.

  Para obter mais informações sobre aplicações potencialmente [indesejadas, consulte Detect e bloqueie aplicações potencialmente indesejadas.](https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/detect-block-potentially-unwanted-apps-windows-defender-antivirus)

  [Defender/PUAProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Submeta consentimento de amostras**: Atualmente, esta definição não tem impacto. Não use esta definição. Pode ser removido numa futura libertação.

- **Na Proteção de Acesso**: **O bloco** impede a digitalização de ficheiros que tenham sido acedidos ou descarregados. Os utilizadores não podem ligá-lo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ativar esta funcionalidade e permite que os utilizadores a alterem.

  Se bloquear a definição e, em seguida, mudá-la para **Não configurada,** então Intune deixa a definição no seu estado previamente configurado para o OS.

  Intune não liga esta característica. Para o ativar, utilize um URI personalizado.

  [Defender/PermitiracessosProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- Ações sobre ameaças de **malware detetadas**: Select **Enable** para escolher as ações que deseja que o Defender tome para cada nível de ameaça que deteta: baixa, moderada, alta e severa. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que o Microsoft Defender escolha a melhor opção.

  Quando programado para **ativar,** selecione a ação:
  
  - **Limpar**
  - **Quarentena**
  - **Remover**
  - **Permitir**
  - **Utilizador definido**
  - **Bloco**

  Se a sua ação não for possível, então o Microsoft Defender escolhe a melhor opção para garantir que a ameaça seja remediada.

  [Defender/AmeaçaSeverityDefaultAction CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Exclusões antivírus do Microsoft Defender

Pode excluir certos ficheiros dos exames Antivírus do Microsoft Defender modificando listas de exclusão. **Geralmente, não deve aplicar exclusões.** O Microsoft Defender Antivirus inclui uma série de exclusões automáticas baseadas em comportamentos conhecidos do SO e ficheiros típicos de gestão, tais como os utilizados na gestão de empresas, gestão de bases de dados e outros cenários e situações empresariais.

> [!WARNING]
> **A definição de exclusões reduz a proteção oferecida pelo Microsoft Defender Antivírus**. Avalie sempre os riscos associados à implementação de exclusões. Só exclua ficheiros que sabe que não são maliciosos.

- **Ficheiros e pastas para excluir de digitalizações e proteção em tempo real**: Adiciona um ou mais ficheiros e pastas como **C:\Path** ou **%ProgramFiles%\Path\filename.exe** à lista de exclusões. Estes ficheiros e pastas não são incluídos em análises em tempo real ou agendadas.
- **Extensões de ficheiros para excluir de digitalizações e proteção em tempo real**: Adicione uma ou mais extensões de ficheiros como **jpg** ou **txt** à lista de exclusões. Quaisquer ficheiros com estas extensões não estão incluídos em nenhum scans em tempo real ou programado.
- **Processos a excluir de digitalizações e proteção em tempo real**: Adicione um ou mais processos do tipo **.exe,** **.com**ou **.scr** à lista de exclusões. Estes processos não estão incluídos em nenhum tempo real, ou exames programados.

## <a name="power-settings"></a>Definições de energia

Estas definições utilizam a política de [energia CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power), que também lista as edições suportadas pelo Windows.

### <a name="battery"></a>Bateria

- **Nível da bateria para ligar o Energy Saver**: Quando o dispositivo estiver a utilizar a bateria, introduza o nível de carga da bateria para ligar o Energy Saver, de 0 a 100. Introduza um valor percentual que indique o nível de carga da bateria. Por exemplo, quando definido para `80` , Energy Saver liga quando a bateria tem 80% de carga ou menos disponível.

  Se não introduzir um valor, a Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode fixá-lo em 70%.

  [Potência/EnergySaverBatteryThresholdonBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Tampa fechada (apenas móvel)**: Quando o dispositivo estiver a utilizar energia da bateria, escolha o que acontece quando a tampa está fechada. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores controlem esta definição.
  - **Sem ação**: O dispositivo permanece ligado e continua a utilizar a bateria.
  - **Sono**: O aparelho entra em modo de sono e utiliza uma pequena quantidade de carga da bateria. O computador ainda está ligado e as aplicações e ficheiros abertos são armazenados em memória de acesso aleatório (RAM).
  - **Hibernar:** O dispositivo entra em modo de hibernação. As aplicações e ficheiros abertos são armazenados no disco rígido e o dispositivo desliga-se.
  - **Paragem**: O dispositivo desliga-se. As aplicações e ficheiros abertos estão fechados sem poupar.

  [Power/SelectLidCloseActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Botão de alimentação**: Quando o dispositivo estiver a utilizar a bateria, escolha o que acontece quando o botão Power é selecionado. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores controlem esta definição.
  - **Sem ação**: O dispositivo permanece ligado e continua a utilizar a bateria.
  - **Sono**: O aparelho entra em modo de sono e utiliza uma pequena quantidade de carga da bateria. O computador ainda está ligado e as aplicações e ficheiros abertos são armazenados em memória de acesso aleatório (RAM).
  - **Hibernar:** O dispositivo entra em modo de hibernação. As aplicações e ficheiros abertos são armazenados no disco rígido e o dispositivo desliga-se.
  - **Paragem**: O dispositivo desliga-se. As aplicações e ficheiros abertos estão fechados sem poupar.

  [Power/SelectPowerButtonActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Botão de sono**: Quando o dispositivo estiver a utilizar energia da bateria, escolha o que acontece quando o botão Sleep é selecionado. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores controlem esta definição.
  - **Sem ação**: O dispositivo permanece ligado e continua a utilizar a bateria.
  - **Sono**: O aparelho entra em modo de sono e utiliza uma pequena quantidade de carga da bateria. O computador ainda está ligado e as aplicações e ficheiros abertos são armazenados em memória de acesso aleatório (RAM).
  - **Hibernar:** O dispositivo entra em modo de hibernação. As aplicações e ficheiros abertos são armazenados no disco rígido e o dispositivo desliga-se.
  - **Paragem**: O dispositivo desliga-se. As aplicações e ficheiros abertos estão fechados sem poupar.

  [Potência/SelectSleepButtonActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Sono híbrido**: Quando o dispositivo estiver a utilizar energia da bateria, opte por permitir ou desativar o modo de sono híbrido.

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores controlem esta definição.
  - **Ativar**: Os dispositivos podem entrar em modo de sono híbrido. As aplicações e ficheiros abertos são armazenados na memória de acesso aleatório (RAM) e no disco rígido. Usa uma pequena quantidade de carga de bateria.
  - **Desativação**: Impede que os dispositivos entrem em modo de sono híbrido.

  [Power/OffHybridSleepOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>Pluggedin

- **Nível da bateria para ligar o Energy Saver**: Quando o dispositivo estiver ligado, introduza o nível de carga da bateria para ligar o Energy Saver de 0-100. Introduza um valor percentual que indique o nível de carga da bateria. Por exemplo, quando definido para `80` , Energy Saver liga quando a bateria tem 80% de carga ou menos disponível.

  Se não introduzir um valor, a Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode fixá-lo em 70%.

  [Potência/EnergySaverBatteryThresholdpluggedin CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Tampa fechada (apenas móvel)**: Quando o aparelho estiver ligado, escolha o que acontece quando a tampa está fechada. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Sem ação**: O dispositivo permanece ligado.
  - **Sono**: O aparelho entra em modo de sono. O computador ainda está ligado e as aplicações e ficheiros abertos são armazenados em memória de acesso aleatório (RAM).
  - **Hibernar:** O dispositivo entra em modo de hibernação. As aplicações e ficheiros abertos são armazenados no disco rígido e o dispositivo desliga-se.
  - **Paragem**: O dispositivo desliga-se. As aplicações e ficheiros abertos estão fechados sem poupar.
  
    [Power/SelectLidCloseActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Botão de alimentação**: Quando o dispositivo estiver ligado, escolha o que acontece quando o botão Power é selecionado. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Sem ação**: O dispositivo permanece ligado.
  - **Sono**: O aparelho entra em modo de sono. O computador ainda está ligado e as aplicações e ficheiros abertos são armazenados em memória de acesso aleatório (RAM).
  - **Hibernar:** O dispositivo entra em modo de hibernação. As aplicações e ficheiros abertos são armazenados no disco rígido e o dispositivo desliga-se.
  - **Paragem**: O dispositivo desliga-se. As aplicações e ficheiros abertos estão fechados sem poupar.

  [Power/SelectPowerButtonActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Botão de sono**: Quando o aparelho estiver ligado, escolha o que acontece quando o botão Dessono é selecionado. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Sem ação**: O dispositivo permanece ligado.
  - **Sono**: O aparelho entra em modo de sono. O computador ainda está ligado e as aplicações e ficheiros abertos são armazenados em memória de acesso aleatório (RAM).
  - **Hibernar:** O dispositivo entra em modo de hibernação. As aplicações e ficheiros abertos são armazenados no disco rígido e o dispositivo desliga-se.
  - **Paragem**: O dispositivo desliga-se. As aplicações e ficheiros abertos estão fechados sem poupar.

  [Potência/SelectSleepButtonActionPluggedin CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Sono híbrido**: Quando o aparelho estiver ligado, opte por permitir ou desativar o modo de sono híbrido.

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores controlem esta definição.
  - **Ativar**: Os dispositivos podem entrar em modo de sono híbrido. As aplicações e ficheiros abertos são armazenados na memória de acesso aleatório (RAM) e no disco rígido.
  - **Desativação**: Impede que os dispositivos entrem em modo de sono híbrido.

  [Power/TurnOffHybridSleepPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Passos seguintes

Para obter os detalhes técnicos adicionais de cada definição e quais as edições do Windows suportadas, veja [Windows 10 Policy CSP Reference](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (Referência de CSP de Políticas do Windows 10)

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).
