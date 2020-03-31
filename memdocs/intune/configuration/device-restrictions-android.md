---
title: Definições de restrição de dispositivos para Android no Microsoft Intune – Azure | Microsoft Docs
description: Consulte uma lista de todas as definições de administrador de dispositivos Android que pode controlar e restringir no Microsoft Intune. Utilize estas definições para controlar a palavra-passe, aceder ao Google Play, permitir ou proibir aplicações, controlar as definições do browser, bloquear aplicações, criar cópias de segurança na cloud do Google e controlar as opções de mensagens, voz, roaming de dados, Wi-Fi e ligação Bluetooth.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4afc27680c464f67756340ebcb0958887ae6f795
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407877"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Listas de configurações de restrições de dispositivos Android e Samsung Knox Standard em Intune

Este artigo mostra-lhe todas as definições de restrições de dispositivos do Microsoft Intune que pode configurar para dispositivos a executar o Android.

>[!TIP]
>Se as definições que pretende não estiverem disponíveis, poderá conseguir configurá-las nos seus dispositivos através de um [perfil personalizado](custom-settings-android.md).

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [configuração do dispositivo](device-restrictions-configure.md).

## <a name="general"></a>Geral

- **Câmara**: **Bloco** impede o acesso à câmara do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à câmara do dispositivo.

  Intune só consegue o acesso à câmara do dispositivo. Não tem acesso a fotografias ou vídeos.

- **Cópia e pasta (apenas Samsung Knox)** : **Bloco** impede a cópia e a pasta. **Não configurado** permite funções de cópia e pasta nos dispositivos.
- **Partilha de clipboard entre apps (apenas Samsung Knox)** : **O bloco** impede a utilização da pasta para copiar e colar entre apps. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir funções de cópia e pasta nos dispositivos.
- **Submissão de dados de diagnóstico (apenas Samsung Knox)** : **O bloco** impede os utilizadores de enviarem relatórios de bugs a partir de dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores enviem os dados.
- **Wipe (apenas Samsung Knox)** : Permite que os utilizadores executem uma ação de [limpeza](../remote-actions/devices-wipe.md) nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Geolocalização (apenas Samsung Knox)** : **Bloquear** desativa dispositivos de utilização de informações de localização. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os dispositivos utilizem as informações de localização.
- **Desligar (apenas Samsung Knox)** : **O bloco** impede que os utilizadores desliguem o dispositivo. Também impede que o **número de falhas de inscrição antes** de limpar a configuração do dispositivo seja configurado e de funcionar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores desliguem os dispositivos.
- **Captura de ecrã (apenas Samsung Knox)** : **Bloco** evita imagens. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores capturem o conteúdo do ecrã como uma imagem.
- **Assistente de voz (apenas Samsung Knox)** : **O bloco** desativa o serviço S Voice. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização do serviço S Voice e da aplicação em dispositivos. Esta definição não se aplica a Bixby ou ao assistente de voz para acessibilidade que lê o conteúdo do ecrã em voz alta.
- **YouTube (apenas Samsung Knox)** : **O bloco** impede os utilizadores de usarem a aplicação do YouTube. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização da aplicação do YouTube nos dispositivos.
- **Dispositivos partilhados (apenas Samsung Knox)** : Configure um dispositivo Samsung Knox Standard gerido como partilhado. **Permitir que** os utilizadores insinem e saem dos dispositivos com as suas credenciais De AD Azure. Os dispositivos mantêm-se geridos, quer estejam a ser utilizados ou não.

  Quando utilizada com um perfil de certificado SCEP, esta funcionalidade permite que os utilizadores partilhem um dispositivo com as mesmas aplicações para todos os utilizadores. Mas cada utilizador tem o seu próprio certificado de utilizador SCEP. Quando os utilizadores terminam sessão, todos os dados das aplicações são limpos. Esta funcionalidade é limitada a aplicações LOB.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode impedir vários utilizadores de iniciars sessão na aplicação Portal da Empresa em dispositivos que utilizem as suas credenciais De AD Azure.
- **Alterações na data e hora do bloco (Samsung Knox)** : O **bloco** impede que os utilizadores mudem as definições de data e hora nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem as definições de data e hora.

## <a name="password"></a>Palavra-passe

- **Palavra-passe**: **Exija que** os utilizadores introduzam uma palavra-passe para aceder aos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores acedam aos dispositivos sem introduzir uma palavra-passe.

    > [!NOTE]
    > Os dispositivos Samsung Knox exigem automaticamente um PIN de 4 dígitos durante a inscrição na MDM. Os dispositivos Android nativos podem exigir automaticamente que um PIN se torne compatível com o Acesso Condicional.

- Comprimento mínimo da **palavra-passe**: Introduza o número mínimo de caracteres necessários, de 4 a 16. Por exemplo, insira `6` para exigir pelo menos seis números ou caracteres no comprimento da palavra-passe.
- **Minutos máximos de inatividade até que o ecrã bloqueie**: Introduza o tempo de tempo em que um dispositivo deve ficar inativo antes de o ecrã estar automaticamente bloqueado. Por exemplo, introduza `5` para bloquear dispositivos após 5 minutos de inatividade. Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.

  Num dispositivo, os utilizadores não podem definir um valor de tempo superior ao tempo configurado no perfil. Os utilizadores podem definir um valor de tempo mais baixo. Por exemplo, se o perfil for definido para `15` minutos, os utilizadores podem definir o valor para 5 minutos. Os utilizadores não podem definir o valor para 30 minutos.

- **Número de falhas de entrada antes de limpar o dispositivo**: Introduza o número de senhas erradas permitidas antes de os dispositivos serem limpos, de 4 a 11. `0` (zero) pode desativar a funcionalidade de limpeza do dispositivo. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Expiração da palavra-passe (dias)** : Introduza o número de dias, até que a palavra-passe do dispositivo seja alterada, de 1 a 365. Por exemplo, insira `90` para expirar a senha após 90 dias. Quando a palavra-passe expirar, será pedido aos utilizadores para criar uma nova. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- Tipo de **palavra-passe necessário**: Introduza o nível de complexidade da palavra-passe exigido e se podem ser utilizados dispositivos biométricos. As opções são:
  - **Predefinição do dispositivo**
  - **Biometria de baixa segurança**: [Biometria forte vs. biométrico fraco](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (abre o site do Android)
  - **Pelo menos numérico:** Inclui caracteres numéricos, como `123456789`.
  - **Complexo numérico**: Números repetidos ou consecutivos, como "1111" ou "1234", não são permitidos. Antes de atribuir esta definição aos dispositivos, certifique-se de atualizar a aplicação Portal da Empresa para a versão mais recente desses dispositivos.

    Quando definido para **complexo numérico**, e você atribui a configuração a dispositivos que executam uma versão Android antes de 5.0, então o seguinte comportamento se aplica:

    - Se a aplicação Do Portal da Empresa estiver a executar uma versão antes de 1704, nenhuma política PIN se aplica aos dispositivos, e um erro mostra no centro de administração do Microsoft Endpoint Manager.
    - Se a aplicação Portal da Empresa executar a versão 1704 ou posterior, apenas pode ser aplicado um PIN simples. A versão Android anterior a 5.0 não suporta esta configuração. Não é mostrado nenhum erro no centro de administração do Microsoft Endpoint Manager.

  - **Pelo menos alfabético:** Inclui letras no alfabeto. Não são obrigatórios números nem símbolos.
  - **Pelo menos alfanumérico:** Inclui letras maiúsculas, letras minúsculas e caracteres numéricos.
  - **Pelo menos alfanumérico com símbolos**: Inclui letras maiúsculas, letras minúsculas, caracteres numéricos, marcas de pontuação e símbolos.

- **Evite a reutilização de senhas anteriores**: Utilize esta definição para restringir os utilizadores a criarem senhas usadas anteriormente. Introduza o número de senhas usadas anteriormente que não podem ser usadas, de 1 a 24. Por exemplo, introduza `5` para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Desbloqueio de impressões digitais (apenas Samsung Knox)** : **Bloco** impede o uso de uma impressão digital para desbloquear dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores desbloqueiem dispositivos utilizando uma impressão digital.
- **Smart Lock e outros agentes fidedignos:** **O Bloco** impede que o Smart Lock ou outros agentes fidedignos ajustem as definições do ecrã de bloqueio. Se o dispositivo estiver num local de confiança, então esta funcionalidade, também conhecida como agente fiduciário, permite-lhe desativar ou contornar a palavra-passe do ecrã de bloqueio do dispositivo. Por exemplo, utilize esta funcionalidade quando os dispositivos estiverem ligados a um dispositivo Bluetooth específico, ou quando os dispositivos estiverem perto de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores configurem o Smart Lock.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  Esta definição aplica-se a:

  - Samsung KNOX Standard 5.0+

- **Encriptação**: Escolha **Exigir para** que os ficheiros do dispositivo sejam encriptados. Nem todos os dispositivos suportam encriptação. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Para configurar esta definição e reportar corretamente a conformidade, configurar também:
  1. **Palavra-passe**: Definir para **exigir**.
  2. **Tipo de palavra-passe requerida**: Definir para **pelo menos numérico**.
  3. **Comprimento mínimo da palavra-passe**: Definir para pelo menos `4`.

  > [!NOTE]
  > Se for imposta uma política de encriptação, os dispositivos Samsung Knox exigem que os utilizadores definam uma palavra-passe complexa de 6 carateres como o código de acesso do dispositivo.

## <a name="google-play-store"></a>Google Play Store

- **Google Play store (apenas Samsung Knox)** : **O bloco** impede os utilizadores de utilizarem a loja Google Play. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir aos utilizadores acederem à loja Google Play nos dispositivos.

## <a name="restricted-apps"></a>Aplicações restritas

Utilize estas definições para permitir ou prevenir aplicações específicas em dispositivos. Esta funcionalidade é suportada em dispositivos Android e Samsung Knox Standard.

- **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
- **Aplicações proibidas**: Lista rita as aplicações (não geridas pela Intune) que os utilizadores não estão autorizados a instalar e executar. Se um utilizador instalar uma aplicação desta lista, receberá uma notificação do Intune.
- **Aplicações aprovadas**: Lista as aplicações que os utilizadores estão autorizados a instalar. Para permanecerem compatíveis, os utilizadores não podem instalar outras aplicações.  As aplicações que são geridas pela Intune são automaticamente permitidas, incluindo a aplicação Portal da Empresa.
- **Lista de aplicações**: **Adicionar-lhe** aplicação :
  - Id do **pacote de aplicativos**: Introduza o pacote de aplicações ID.
  - URL da loja de **aplicações**: Introduza o URL da Google Play Store da aplicação que deseja. Por exemplo, para adicionar a aplicação Microsoft Remote Desktop para Android, introduza `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`.

    Para encontrar o URL de uma aplicação, abra a [loja Google Play](https://play.google.com/store/apps)e procure a app. Por exemplo, procure `Microsoft Remote Desktop Play Store` ou `Microsoft Planner`. Selecione a aplicação e copie o URL.
  
  - Nome da **aplicação**: Introduza o nome que deseja. Este nome é mostrado aos utilizadores.
  - **Editor** (opcional): Insira o editor da app, como `Microsoft`.

Também pode **importar** um ficheiro CSV com detalhes sobre a aplicação, incluindo o URL. Use o url de*aplicativo*<, < nome de*app*>, <*app publisher*> formato. Ou, **Exportar** uma lista existente que inclui a lista de aplicações restritas no mesmo formato.

> [!IMPORTANT]
> Os perfis do dispositivo que utilizam as definições restritas da aplicação devem ser atribuídos a grupos de utilizadores e não a grupos de dispositivos.

## <a name="browser"></a>Browser

- **Navegador web (apenas Samsung Knox)** : **O bloco** impede que o navegador predefinido seja utilizado em dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a aplicação do navegador predefinido do dispositivo.
- **Autofill (apenas Samsung Knox)** : **O bloco** impede que o navegador preencha automaticamente o texto. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a auto-enchimento.
- **Cookies (apenas Samsung Knox)** : Escolha como lidar com cookies a partir de websites em dispositivos. As opções são:
  - Permitir
  - Bloquear todos os cookies
  - Permitir cookies dos sites visitados
  - Permitir cookies do site atual
- **JavaScript (apenas Samsung Knox)** : **O bloco** impede que o JavaScript esteja a funcionar no navegador. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir estes scripts.
- **Pop-ups (apenas Samsung Knox)** : **Block** liga o Pop-up Blocker para evitar pop-ups no navegador web. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode permitir pop-ups.

## <a name="allow-or-block-apps"></a>Permitir ou Bloquear aplicações

Utilize estas definições para permitir, bloquear ou ocultar aplicações específicas em dispositivos Samsung Knox Standard. As aplicações ocultas não podem ser abertas ou ser percorreu os utilizadores.

As opções são:

- **Apps autorizadas a serem instaladas (apenas Samsung Knox Standard)** : Adicione aplicações que os utilizadores possam instalar. Os utilizadores não podem instalar aplicações que não estejam na lista.
- **Apps bloqueadas de lançamento (apenas Samsung Knox Standard)** : Introduza as aplicações que os utilizadores não podem executar no seu dispositivo.
- **Aplicações ocultas do utilizador (apenas Samsung Knox Standard)** : Introduza as aplicações escondidas nos dispositivos. Os utilizadores não podem descobrir ou executar estas aplicações.

Para cada definição, adicione as suas aplicações:

- **Adicione aplicativos por nome**de pacote : Insira o nome da aplicação e o nome do pacote de aplicações. Usado principalmente para aplicações de linha de negócio. 
- **Adicione aplicativos por URL**: Introduza o nome da aplicação e o seu URL na loja Google Play.
- **Adicionar aplicativo de loja**: Selecione uma aplicação da lista existente de aplicações que gere no Intune.

## <a name="cloud-and-storage"></a>Cloud e Armazenamento

- **Backup da Google (apenas Samsung Knox)** : **O bloco** impede que os dispositivos se sincroniem à cópia de segurança da Google. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização de backup do Google.
- **Sincronização automática da conta google (apenas Samsung Knox)** : **O bloco** impede a funcionalidade de sincronização automática da conta da Google nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que as definições da conta da Google sejam automaticamente sincronizadas.
- **Armazenamento amovível (apenas Samsung Knox)** : **O bloco** impede que os dispositivos utilizem armazenamento amovível. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os dispositivos utilizem armazenamento amovível, como um cartão SD.
- **Encriptação em cartões de armazenamento (apenas Samsung Knox)** : **Exigir** que os cartões de armazenamento sejam encriptados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a sua aplicação de cartões de armazenamento não encriptados. Nem todos os dispositivos suportam encriptação de cartões de armazenamento. Para confirmar, consulte o fabricante do dispositivo.

## <a name="cellular-and-connectivity"></a>Rede Móvel e Conectividade

- **Roaming de dados (apenas Samsung Knox)** : **Bloco** impede que os dados perversem a rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir o roaming de dados.
- **Mensagens SMS/MMS (apenas Samsung Knox)** : **O bloco** impede a mensagem de texto nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização de mensagens SMS e MMS.
- **Marcação por voz (apenas Samsung Knox)** : **O bloco** impede que os utilizadores utilizem a funcionalidade de marcação de voz nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode permitir a marcação de voz.
- **Roaming de voz (apenas Samsung Knox)** : **Bloco** impede que a voz vagueie pela rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o roaming de voz.
- **Bluetooth (apenas Samsung Knox)** : **Bloco** evita a utilização de Bluetooth nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização de Bluetooth.
- **NFC (apenas Samsung Knox)** : **Bloquear** desativa operações que utilizam perto da comunicação de campo (NFC) em dispositivos que o suportam. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode permitir operações NFC.
- **Wi-Fi (apenas Samsung Knox)** : **O bloco** impede a utilização de Wi-Fi nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode permitir a utilização de Wi-Fi.
- **Wi-Fi tethering (apenas Samsung Knox)** : **O bloco** impede a utilização de wi-fi nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização de tetering Wi-Fi.

## <a name="kiosk"></a>Modo de Local Público

As definições de modo de local público aplicam-se apenas a dispositivos Samsung Knox Standard e apenas a aplicações que gere com o Intune.

- Adicione aplicações que pretende executar quando o dispositivo estiver no modo quiosque. No modo quiosque, apenas as aplicações que adiciona executar; apps não adicionadas não executar. Os navegadores pré-instalados não funcionam como uma aplicação quando o dispositivo está em modo quiosque. Se for necessário utilizar um browser, considere a utilização do [Managed Browser](../apps/app-configuration-managed-browser.md).

  As opções das suas aplicações:

  - **Adicione aplicativos por nome de pacote**: Usado principalmente para aplicações de linha de negócio. Introduza o nome da aplicação e o nome do pacote de aplicação.
  - **Adicione aplicativos por URL**: Introduza o nome da aplicação e o seu URL na loja Google Play.
  - **Adicionar aplicativo de loja**: Selecione uma aplicação da lista existente de aplicações que gere no Intune.

- **Botão de sono de tela**: **Bloqueie** ou esconda o botão de sono do ecrã. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o botão de despertar do sono do ecrã nos dispositivos.
- **Botões de volume**: **O bloco** impede os utilizadores de ajustarem o volume desativando os botões de volume. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização dos botões de volume nos dispositivos.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode criar perfis de quiosque para dispositivos [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) e [Windows 10.](kiosk-settings.md)
