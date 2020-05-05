---
title: Configurações de dispositivos Android Enterprise no Microsoft Intune - Azure Microsoft Docs
description: Nos dispositivos Android Enterprise ou Android for Work, restringe as definições do dispositivo, incluindo cópia e pasta, notificações de exibição, permissões de aplicações, partilha de dados, comprimento da palavra-passe, registo de falhas, utilização de impressões digitais para desbloquear, reutilizar palavras-passe e permitir a partilha de bluetooth dos contactos de trabalho. Configure os dispositivos como um quiosque dedicado para executar uma aplicação, ou várias aplicações.
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
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38598e0245b0cfe15be4b9303620aea1724933d1
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166575"
---
# <a name="android-enterprise-device-settings-to-allow-or-restrict-features-using-intune"></a>Configurações do dispositivo Android Enterprise para permitir ou restringir funcionalidades usando Intune

Este artigo lista e descreve as diferentes configurações que pode controlar nos dispositivos Android Enterprise. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para permitir ou desativar funcionalidades, executar aplicações em dispositivos dedicados, segurança de controlo e muito mais.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [configuração do dispositivo](device-restrictions-configure.md).

## <a name="device-owner-only"></a>Proprietário do dispositivo apenas

Estas definições aplicam-se aos tipos de inscrição do Android Enterprise onde o Intune controla todo o dispositivo, como dispositivos Android Enterprise Totalmente Geridos ou Dedicados.

### <a name="general"></a>Geral

- **Captura do ecrã**: **O bloco** evita imagens ou capturas de ecrã no dispositivo. Também impede que os conteúdos presentes sejam apresentados em dispositivos de visualização que não tenham uma saída de vídeo segura. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores capturem o conteúdo do ecrã como uma imagem.
- **Câmara**: **Bloco** impede o acesso à câmara no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à câmara.

  Intune só consegue o acesso à câmara do dispositivo. Não tem acesso a fotografias ou vídeos.

- **Política de permissões predefinida**: esta definição configura a política de permissões predefinida para pedidos de permissões de runtime. As suas opções
  - **Predefinição do dispositivo**: Utilize a definição predefinida do dispositivo.
  - **Solicitação**: Os utilizadores são solicitados a aprovar a permissão.
  - **Conceder automaticamente**: as permissões são concedidas automaticamente.
  - **Negar automaticamente**: as permissões são negadas automaticamente.
- **Alterações de data e hora**: O **bloco** impede os utilizadores de definir manualmente a data e a hora. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores possam obter a data e hora definidas no dispositivo.
- **Alterações de volume**: **O bloco** impede que os utilizadores mudem o volume do dispositivo e também silencia o volume principal. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização das definições de volume no dispositivo.
- **Reset de fábrica**: **O bloco** impede que os utilizadores utilizem a opção de reset da fábrica nas definições do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem esta definição no dispositivo.
- **Bota segura**: **O bloco** impede que os utilizadores reiniciem o dispositivo em modo de segurança. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores reiniciem o dispositivo em modo de segurança.
- **Barra de estado**: **O bloco** impede o acesso à barra de estado, incluindo notificações e configurações rápidas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir aos utilizadores o acesso à barra de estado.
- **Serviços**de dados de roaming : **O bloco** impede que os dados circulam pela rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o roaming de dados quando o dispositivo está numa rede celular.
- Alterações de definição de **Wi-Fi**: **O bloco** impede que os utilizadores mudem as definições de Wi-Fi criadas pelo proprietário do dispositivo. Os utilizadores podem criar as suas próprias configurações wi-fi. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem as definições de Wi-Fi no dispositivo.
- **Configuração do ponto de acesso Wi-Fi**: O **bloco** impede os utilizadores de criar ou alterar quaisquer configurações wi-fi. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem as definições de Wi-Fi no dispositivo.
- **Configuração Bluetooth**: **O bloco** impede os utilizadores de configurar bluetooth no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização de Bluetooth no dispositivo.
- **Amarração e acesso a hotspots**: **O bloco** impede a amarração e o acesso a hotspots portáteis. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a amarração e o acesso a hotspots portáteis.
- **Armazenamento USB**: Escolha **permitir** aceder ao armazenamento USB no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode impedir o acesso ao armazenamento USB.
- **Transferência de ficheiros USB**: **O bloco** impede a transferência de ficheiros para USB. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a transferência de ficheiros.
- **Meios externos**: **O bloco** impede a utilização ou ligação de quaisquer meios externos no aparelho. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir meios externos no dispositivo.
- Dados de **feixes utilizando NFC**: **O bloco** impede a utilização da tecnologia Near Field Communication (NFC) para obter dados de aplicações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que o NFC partilhe dados entre dispositivos.
- **Funcionalidades de depuração**: Escolha **permitir** que os utilizadores utilizem funcionalidades de depuração no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir que os utilizadores utilizem as funcionalidades de depuração do dispositivo.
- **Regulação do microfone**: **O bloco** impede que os utilizadores desloquem o microfone e ajustem o volume do microfone. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem e ajustem o volume do microfone no dispositivo.
- **E-mails**de proteção de reset de fábrica : Escolha endereços de **e-mail da conta google**. Introduza os endereços de e-mail dos administradores do dispositivo que podem desbloquear o dispositivo depois de limpo. Certifique-se de separar os endereços de e-mail com um ponto evíbis, como `admin1@gmail.com;admin2@gmail.com`. Se um e-mail não for introduzido, qualquer pessoa pode desbloquear o dispositivo depois de restaurado nas definições da fábrica. Estes e-mails só se aplicam quando uma fábrica não utilizadora é executada, como executar uma reposição de fábrica usando o menu de recuperação.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

- **Saída de rede**: **Ativar** permite que os utilizadores liguem a função de saída da rede. Se uma ligação de rede não for feita quando o dispositivo arranca, então a escotilha de fuga pede para ligar temporariamente a uma rede e refrescar a política do dispositivo. Depois da aplicação da política, a rede temporária é esquecida e o dispositivo continua o arranque. Esta função liga os dispositivos a uma rede se:
  - Não há uma rede adequada na última apólice.
  - O dispositivo entra numa aplicação em modo de tarefa de bloqueio.
  - Os utilizadores não conseguem alcançar as definições do dispositivo.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir que os utilizadores ligassem a função de saída da rede no dispositivo.

- **Atualização do sistema**: Escolha uma opção para definir como o dispositivo lida com atualizações over-the-air. As suas opções
  - **Predefinição do Dispositivo**: utiliza a predefinição do dispositivo.
  - **Automático**: as atualizações são instaladas automaticamente sem interação do utilizador. Definir esta política imediatamente instala todas as atualizações pendentes.
  - **Adiado**: as atualizações são adiadas por 30 dias. No final dos 30 dias, o Android leva os utilizadores a instalarem a atualização. É possível os fabricantes de dispositivos ou operadoras impedirem (isentarem) o adiamento de atualizações de segurança importantes. Uma atualização isenta mostra uma notificação do sistema aos utilizadores no dispositivo.
  - **Janela de manutenção**: as atualizações são instaladas automaticamente durante uma janela de manutenção diária definida no Intune. A instalação tenta diariamente durante 30 dias, podendo falhar se não houver espaço ou níveis de bateria insuficientes. Após 30 dias, o Android leva os utilizadores a instalarem-se. Esta janela também é utilizada para instalar atualizações para aplicações do Play. Utilize esta opção para dispositivos dedicados, como quiosques, uma vez que as aplicações de primeiro plano dedicadas a dispositivos únicos podem ser atualizadas.

- **Janelas de notificação**: Quando definido para **Desativar,** notificações de janelas, incluindo torradas, chamadas recebidas, chamadas de saída, alertas de sistema e erros do sistema não são mostrados no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode apresentar notificações.
- **Ignore as dicas de utilização inicial**: **Ative** ocultar ou ignora sugestões de apps que passem por tutoriais ou sugestões quando a aplicação começa. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode mostrar estas sugestões quando a aplicação começar.

### <a name="system-security"></a>Segurança do sistema

- **A varredura de ameaças em apps**: **Require** (padrão) permite ao Google Play Protect digitalizar aplicações antes e depois de serem instaladas. Caso detete uma ameaça, poderá alertar os utilizadores para a remoção da aplicação do dispositivo. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição. Por padrão, o OS pode não ativar ou executar o Google Play Protect para digitalizar aplicações.

### <a name="dedicated-devices"></a>Dispositivos dedicados

Utilize estas definições para configurar uma experiência de estilo quiosque nos seus dispositivos dedicados. Pode configurar dispositivos para executar uma aplicação ou executar muitas aplicações. Quando um dispositivo é definido com o modo de quiosque, apenas as aplicações que adiciona estão disponíveis. Estas definições aplicam-se a dispositivos dedicados ao Android Enterprise. Não se aplicam a dispositivos geridos pela Android Enterprise.

**Modo quiosque**: Escolha se o dispositivo executa uma aplicação ou executa várias aplicações.

- **Não configurado**: Intune não altera nem atualiza esta definição.
- **Aplicação única**: Os utilizadores só podem aceder a uma única aplicação no dispositivo. Quando o dispositivo começa, apenas começa a aplicação específica. Os utilizadores não podem abrir novas aplicações ou mudar a aplicação em execução.

  - **Selecione uma aplicação gerida**: Selecione a aplicação gerida do Google Play na lista.

    Se não tiver nenhuma aplicação listada, [adicione algumas aplicações Android](../apps/apps-add-android-for-work.md) ao dispositivo. Certifique-se de [atribuir a app ao grupo de dispositivos criado para os seus dispositivos dedicados](../apps/apps-deploy.md).

  > [!IMPORTANT]
  > Ao utilizar o modo de quiosque de aplicações únicas, as aplicações dialerador/telefone podem não funcionar corretamente.
  
- **Multi-aplicações:** Os utilizadores podem aceder a um conjunto limitado de aplicações no dispositivo. Quando o dispositivo começa, apenas as aplicações que adiciona saem. Também pode adicionar alguns links web que os utilizadores podem abrir. Quando a política é aplicada, os utilizadores vêem ícones para as aplicações permitidas no ecrã principal.

  > [!IMPORTANT]
  > Para dispositivos dedicados a várias aplicações, a [aplicação Managed Home Screen](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) do Google Play **deve ser:**
  >   - [Adicionado como uma aplicação de cliente](../apps/apps-add-android-for-work.md) em Intune
  >   - [Atribuído ao grupo de dispositivos](../apps/apps-deploy.md) criado para os seus dispositivos dedicados
  >
  > A aplicação **Managed Home Screen** não é necessária para estar no perfil de configuração, mas é necessário ser adicionada como uma aplicação de cliente. Quando a aplicação **Managed Home Screen** é adicionada como uma aplicação para clientes, quaisquer outras aplicações que adicione no perfil de configuração são mostradas como ícones na aplicação **Managed Home Screen.**
  >
  > Ao utilizar o modo de quiosque multi-aplicações, as aplicações de dialer/telefone podem não funcionar corretamente. 

  - **Adicione:** Selecione as suas aplicações da lista.

    Se a aplicação **Managed Home Screen** não estiver listada, [adicione-a a partir do Google Play](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). Certifique-se de [atribuir a app](../apps/apps-deploy.md) ao grupo de dispositivos criado para os seus dispositivos dedicados.

    Também pode adicionar [outras aplicações Android](../apps/apps-add-android-for-work.md) e [aplicações web](../apps/web-app.md) criadas pela sua organização ao dispositivo. Certifique-se de [atribuir a app ao grupo de dispositivos criado para os seus dispositivos dedicados](../apps/apps-deploy.md).

  - **Botão doméstico virtual**: Um botão soft-key que devolve os utilizadores ao Ecrã Home Gerido para que os utilizadores possam alternar entre apps. As opções são:

    - **Não configurado** (predefinido): Não é mostrado um botão inicial. Os utilizadores devem usar o botão traseiro para alternar entre aplicações.
    - **Swipe up**: Um botão doméstico mostra quando um utilizador passa para cima no dispositivo.
    - **Flutuação**: Mostra um botão doméstico persistente e flutuante no dispositivo.

  - **Modo de saída do quiosque**: **Ativar** permite que os administradores interrompam temporariamente o modo de quiosque para atualizar o dispositivo. Para utilizar esta funcionalidade, o administrador:
  
    1. Continua a selecionar o botão traseiro até que seja mostrado o botão do **quiosque de saída.** 
    2. Seleciona o botão **de quiosque de saída** e introduz o código pin do modo de quiosque **Leave.**
    3. Quando terminar, selecione a aplicação **Managed Home Screen.** Este passo rebloqueia o dispositivo em modo quiosque multi-aplicações.

      Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir os administradores de pararem o modo de quiosque. Se o administrador continuar a selecionar o botão de trás e selecionar o botão de **quiosque de saída,** então uma mensagem indica que é necessária uma senha.

    - **Deixe**o código do modo quiosque : Introduza um PIN numérico de 4-6 dígitos. O administrador utiliza este PIN para interromper temporariamente o modo de quiosque.

  - **Definir o fundo de URL personalizado**: Introduza um URL para personalizar o ecrã de fundo no dispositivo dedicado. Por exemplo, introduza `http://contoso.com/backgroundimage.jpg`.

    > [!NOTE]
    > Para a maioria dos casos, recomendamos começar com imagens de pelo menos os seguintes tamanhos:
    >
    > - Telefone: 1080x1920 px
    > - Tablet: 1920x1080 px
    >
    > Para a melhor experiência e detalhes nítidos, sugere-se que os ativos de imagem por dispositivo sejam criados de acordo com as especificações de exibição.
    >
    > Os ecrãs modernos têm densidades de pixels mais elevadas e podem exibir imagens de definição equivalentes de 2K/4K.

  - **Configuração Wi-Fi**: **Ativar** mostra o controlo Wi-Fi no Ecrã Home Gerido e permite que os utilizadores conectem o dispositivo a diferentes redes Wi-Fi. Ativar esta funcionalidade também liga a localização do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não mostrar o controlo Wi-Fi no Ecrã Home Gerido. Impede que os utilizadores se conectem às redes Wi-Fi enquanto utilizam o Ecrã Home Gerido.

  - **Configuração Bluetooth**: **Ativar** mostra o controlo Bluetooth no Ecrã Home Gerido e permite que os utilizadores emparelhem dispositivos em vez de Bluetooth. Ativar esta funcionalidade também liga a localização do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não mostrar o controlo Bluetooth no Ecrã Home Gerido. Impede os utilizadores de configurar em dispositivos Bluetooth e emparelhamento durante a utilização do Ecrã Home Gerido.

  - **Acesso à lanterna**: **Ativar** mostra o controlo da lanterna no Ecrã Home Gerido e permite que os utilizadores liguem ou desliguem a lanterna. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não mostrar o controlo da lanterna no Ecrã Home Gerido. Impede que os utilizadores utilizem a lanterna durante a utilização do Ecrã Home Gerido.

  - **Controlo de volume**de mídia : **Ativar** mostra o controlo de volume de mídia no Ecrã Home Gerido e permite que os utilizadores ajustem o volume de suporte do dispositivo utilizando um slider. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não mostrar o controlo de volume de mídia no Ecrã Home Gerido. Impede que os utilizadores ajustem o volume de suporte do dispositivo enquanto utilizam o Ecrã Home Gerido, a menos que os seus botões de hardware o suportem.

  - **Modo**de poupança de ecrã : **Ativar** mostra um protetor de ecrã no Ecrã Home Gerido quando o dispositivo está bloqueado ou que está fora. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não mostrar um protetor de ecrã no Ecrã Home Gerido.

    Quando ativado, configure também:

    - **Definir imagem de poupança**de ecrã personalizada : Introduza o URL num PNG personalizado, JPG, JPEG, GIF, BMP, WebP ou ICOimage. Por exemplo, introduza: 

      - `http://www.contoso.com/image.jpg`
      - `www.contoso.com/image.bmp`
      - `https://www.contoso.com/image.webp`

      Se não introduzir um URL, então a imagem padrão do dispositivo é usada, se houver uma imagem padrão.

      > [!TIP]
      > Qualquer URL de recurso de ficheiro que possa ser transformado num bitmap é suportado.

    - **Número de segundos o dispositivo mostra o protetor de ecrã antes**de desligar o ecrã : Escolha quanto tempo o dispositivo mostra o protetor de ecrã. Introduza um valor entre 0-9999999 segundos. Padrão `0` são segundos. Quando deixada em branco,`0`ou definida a zero , o protetor de ecrã está ativo até que um utilizador interaja com o dispositivo.
    - **Número de segundos em**que o dispositivo está inativo antes de mostrar o protetor de ecrã : Escolha o tempo que o dispositivo está inativo antes de mostrar o protetor de ecrã. Introduza um valor entre 1-9999999 segundos. Padrão `30` são segundos. Deve introduzir um número superior`0`a zero ( ).
    - **Detete os meios de comunicação antes**de iniciar o protetor de ecrã : **Ativar** (predefinido) não mostra o protetor de ecrã se o áudio ou o vídeo estiverem a reproduzir-se no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode mostrar o protetor de ecrã, mesmo que o áudio ou o vídeo esteja a ser reproduzido.

### <a name="password"></a>Palavra-passe

- **Desativar o ecrã**de bloqueio : Escolha **desativar** para evitar que os utilizadores utilizem a função de bloqueio do Keyguard no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem as funcionalidades Keyguard.
- **Características do ecrã de bloqueio desativado**: Quando o teclado estiver ativado no dispositivo, escolha quais as funcionalidades a desativar. Por exemplo, quando a **câmara Segura** é verificada, a função da câmara é desativada no dispositivo. Quaisquer funcionalidades não verificadas estão ativadas no dispositivo.

  Estas funcionalidades estão disponíveis para os utilizadores quando o dispositivo está bloqueado. Os utilizadores não verão ou acederão a funcionalidades que sejam verificadas.

- Tipo de **palavra-passe necessário**: Introduza o nível de complexidade da palavra-passe exigido e se podem ser utilizados dispositivos biométricos. As opções são:
  - **Predefinição do dispositivo**
  - **Palavra-passe obrigatória, sem restrições**
  - **Biométrico fraco**: [Biometria forte vs. biométrico fraco](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (abre o site do Android)
  - **Numérico:** A palavra-passe `123456789`só deve ser números, tais como . Introduza também:
    - Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, entre 4 e 16 caracteres.
  - **Complexo numérico**: Números repetidos ou consecutivos, como "1111" ou "1234", não são permitidos. Introduza também:
    - Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, entre 4 e 16 caracteres.
  - **Alfabética:** São necessárias letras no alfabeto. Não são obrigatórios números nem símbolos. Introduza também:
    - Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, entre 4 e 16 caracteres.
  - **Alfanumérico:** Inclui letras maiúsculas, letras minúsculas e caracteres numéricos. Introduza também:
    - Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, entre 4 e 16 caracteres.
  - **Alfanumérico com símbolos**: Inclui letras maiúsculas, letras minúsculas, caracteres numéricos, marcas de pontuação e símbolos. Introduza também:

    - Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, entre 4 e 16 caracteres.
    - **Número de caracteres necessários**: Introduza o número de caracteres que a palavra-passe deve ter, entre 0 e 16 caracteres.
    - **Número de caracteres minúsculos necessários**: Introduza o número de caracteres minúsculos que a palavra-passe deve ter, entre 0 e 16 caracteres.
    - **Número de caracteres maiúsculos necessários**: Introduza o número de caracteres maiúsculos que a palavra-passe deve ter, entre 0 e 16 caracteres.
    - **Número de caracteres não-letra necessários**: Introduza o número de não-letras (qualquer outra coisa que não seja letras no alfabeto) a palavra-passe deve ter, entre 0 e 16 caracteres.
    - **Número de caracteres numéricos necessários:** Introduza`1` `2`o `3`número de caracteres numéricos ( , , , e assim por diante) a palavra-passe deve ter, entre 0 e 16 caracteres.
    - **Número de caracteres de símbolo necessários**:`&` `#`Introduza o número de caracteres de símbolo ( , , `%`, e assim por diante) a palavra-passe deve ter, entre 0 e 16 caracteres.

- Número de dias até que a **palavra-passe expire**: Introduza o número de dias, até que a palavra-passe do dispositivo seja alterada, de 1 a 365. Por exemplo, `90` introduza para expirar a palavra-passe após 90 dias. Quando a palavra-passe expirar, será pedido aos utilizadores para criar uma nova. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Número de palavras-passe necessárias antes de o utilizador poder reutilizar uma palavra-passe**: Utilize esta definição para restringir os utilizadores de criarem senhas usadas anteriormente. Introduza o número de senhas usadas anteriormente que não podem ser usadas, de 1 a 24. Por exemplo, `5` introduza para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Número de falhas de entrada antes de limpar o dispositivo**: Introduza o número de senhas erradas permitidas antes de o dispositivo ser limpo, de 4 a 11. `0`(zero) pode desativar a funcionalidade de limpeza do dispositivo. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.

  > [!NOTE]
  > Dispositivo Os dispositivos proprietário do dispositivo não serão solicitados a definir uma palavra-passe. As definições serão aplicadas e terá de definir a palavra-passe manualmente. A aplicação da política será como falhada até definir a palavra-passe que satisfaz os seus requisitos.

### <a name="power-settings"></a>Definições de energia

- **Tempo para bloquear o ecrã**: Introduza o tempo máximo que um utilizador pode definir até que o dispositivo bloqueie. Por exemplo, se definir `10 minutes`esta definição para , então os utilizadores podem definir o tempo de 15 segundos até 10 minutos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

- **Ecrã ligado enquanto o dispositivo está ligado**: selecione que fontes de energia fazem com que o ecrã do dispositivo permaneça ligado enquanto o dispositivo está ligado.

### <a name="users-and-accounts"></a>Utilizadores e Contas

- **Adicionar novos utilizadores**: **O Bloco** impede os utilizadores de adicionarem novos utilizadores. Cada utilizador tem um espaço pessoal no dispositivo para ecrãs, contas, apps e configurações personalizadas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores adicionem outros utilizadores ao dispositivo.
- **Remoção do utilizador**: **O bloco** impede que os utilizadores removam os utilizadores. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores removam outros utilizadores do dispositivo.
- **Alterações na conta** (apenas dispositivos dedicados): **O bloco** impede os utilizadores de modificar contas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir aos utilizadores atualizarem as contas dos utilizadores no dispositivo.

  > [!NOTE]
  > Esta definição não é honrada em dispositivos proprietários de dispositivos (totalmente geridos). Se configurar esta definição, a definição é ignorada e não tem impacto.

- **O utilizador pode configurar credenciais**: **O Bloco** impede os utilizadores de configurar em dispositivos os certificados, mesmo dispositivos que não estejam associados a uma conta de utilizador. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir aos utilizadores configurar ou alterar as suas credenciais quando as acederem à loja de chaves.
- **Contas pessoais**do Google : **O Bloco** impede os utilizadores de adicionarem a sua conta pessoal da Google ao dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores adicionem a sua conta pessoal do Google.

### <a name="applications"></a>Aplicações

- **Permitir a instalação a partir de fontes desconhecidas**: **Permitir que** os utilizadores liguem **fontes desconhecidas**. Esta definição permite que as aplicações se instalem a partir de fontes desconhecidas, incluindo outras fontes que não a Google Play Store. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir que os utilizadores se ligarem a **fontes desconhecidas**.
- **Permitir o acesso a todas as aplicações na loja Google Play**: Quando definido para **permitir,** os utilizadores têm acesso a todas as aplicações na loja Google Play. Não têm acesso às aplicações que o administrador bloqueia nas [Aplicações de Clientes.](../apps/apps-add-android-for-work.md) Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS pode forçar os utilizadores a aceder apenas às aplicações que o administrador disponibiliza na loja Google Play, ou aplicações necessárias nas [Aplicações do Cliente.](../apps/apps-add-android-for-work.md)
- **Atualizações automáticas**da aplicação : Os dispositivos verificam diariamente as atualizações das aplicações. Escolha quando as atualizações automáticas forem instaladas. As opções são:
  - **Não configurado**: Intune não altera nem atualiza esta definição.
  - **Escolha do utilizador**: O SISTEMA pode não estar em defeito com esta opção. Os utilizadores podem definir as suas preferências na aplicação gerida do Google Play.
  - **Nunca:** As atualizações nunca são instaladas. Esta opção não é recomendada.
  - **Apenas Wi-Fi**: As atualizações só são instaladas quando o dispositivo está ligado a uma rede Wi-Fi.
  - **Sempre:** As atualizações são instaladas quando estão disponíveis.

### <a name="connectivity"></a>Conectividade

- **VPN sempre ligado**: **Ativar** define o cliente VPN para ligar e voltar a ligar-se automaticamente à VPN. As ligações VPN sempre ligadas permanecem ligadas. Ou, ligue imediatamente quando os utilizadores bloqueiam o seu dispositivo, o dispositivo reinicia ou a rede sem fios muda.

  Selecione **Não configurado** para desativar a VPN sempre ativada para todos os clientes VPN.

  > [!IMPORTANT]
  > Certifique-se de que implementa apenas uma política de VPN sempre on para um único dispositivo. A implementação de múltiplas políticas de VPN sempre on para um único dispositivo não é suportada.

- **Cliente VPN**: selecione um cliente VPN que suporte a funcionalidade Always On. As opções são:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Personalizado
    - **ID de Pacote**: introduza o ID do pacote da aplicação na Google Play Store. Por exemplo, se o URL da aplicação na Play Store for `https://play.google.com/store/details?id=com.contosovpn.android.prod`, o ID de pacote é `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - O cliente VPN que escolher tem de estar instalado no dispositivo e deve suportar a VPN por aplicação em perfis de trabalho. Caso contrário, ocorrerá um erro. 
  > - Tem de aprovar a aplicação cliente VPN na **Managed Google Play Store**, sincronizar a aplicação com o Intune e implementar a aplicação no dispositivo. Depois de o fazer, a aplicação é instalada no perfil de trabalho do utilizador.
  > - Ainda precisa de configurar o cliente VPN com um [perfil VPN](vpn-settings-android-enterprise.md), ou através de um perfil de configuração de [aplicações](../apps/app-configuration-policies-use-android.md).
  > - Pode haver problemas conhecidos ao utilizar VPN por app com Acesso F5 para Android 3.0.4. Para mais informações, consulte as notas de lançamento do F5 para o [Acesso F5 para Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Modo de bloqueio**: **Ativar** todo o tráfego de rede para utilizar o túnel VPN. Se não for estabelecida uma ligação à VPN, o dispositivo não terá acesso à rede. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que o tráfego flua através do túnel VPN ou através da rede móvel.

- **Proxy global recomendado**: **Enable** adiciona um proxy global aos dispositivos. Quando ativado, o tráfego HTTP e HTTPS, incluindo algumas aplicações no dispositivo, utilize o proxy em que entra. Este representante é apenas uma recomendação. É possível que algumas aplicações não usem o proxy. **Não configurado** (padrão) não adiciona um proxy global recomendado.

  Para obter mais informações sobre esta funcionalidade, consulte [o setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (abre um site Android).

  Quando ativado, introduza também o **tipo** de procuração. As opções são:

  - **Direto**: Introduza manualmente os dados do servidor proxy, incluindo:
    - **Anfitrião**: Introduza o nome de anfitrião ou endereço IP do seu servidor proxy. Por exemplo, introduza: `proxy.contoso.com` ou `127.0.0.1`.
    - **Número**da porta : Introduza o número da porta TCP utilizado pelo servidor proxy. Por exemplo, introduza `8080`.
    - **Anfitriões excluídos**: Introduza uma lista de nomes de anfitriões ou endereços IP que não utilizem o proxy. Esta lista pode incluir um`*`wildcard asterisco e vários`;`anfitriões separados por pontos evímetros ( ) sem espaços. Por exemplo, introduza `127.0.0.1;web.contoso.com;*.microsoft.com`.

  - **Proxy Auto-Config**: Introduza o **URL PAC** num script de configuração automática proxy. Por exemplo, introduza `https://proxy.contoso.com/proxy.pac`.

    Para obter mais informações sobre ficheiros PAC, consulte o [ficheiro Proxy Auto-Configuration (PAC)](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (abre um site não Microsoft).

  Para obter mais informações sobre esta funcionalidade, consulte [o setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (abre um site Android).

## <a name="work-profile-only"></a>Apenas perfil de trabalho

Estas definições aplicam-se aos tipos de inscrição do Android Enterprise onde o Intune controla apenas o Perfil de Trabalho, como a inscrição do perfil android Enterprise Work num dispositivo pessoal ou de trazer o seu próprio dispositivo (BYOD).

### <a name="work-profile-settings"></a>Definições de perfil de trabalho

- **Copiar e colar entre trabalho e perfis pessoais**: **Bloco** impede cópia e pasta entre trabalho e aplicações pessoais. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores partilhem dados usando cópia e pasta com aplicações no perfil pessoal.
- **Partilha de dados entre trabalho e perfis pessoais**: Escolha se as aplicações no perfil de trabalho podem partilhar com aplicações no perfil pessoal. Por exemplo, pode controlar ações de partilha dentro de aplicações, como a **Partilha...** na aplicação do browser Chrome. Esta definição não se aplica ao comportamento da área de transferência de copiar/colar. As opções são:
  - **Padrão do dispositivo**: O comportamento de partilha padrão do dispositivo, que varia consoante a versão Android. Por predefinição, é permitida a partilha do perfil pessoal com o perfil de trabalho. Também por predefinição, é bloqueada a partilha do perfil de trabalho para o perfil pessoal. Esta definição impede a partilha de dados do perfil de trabalho para o perfil pessoal. Em dispositivos com a versão 6.0 e versões posteriores, a Google não bloqueia a partilha do perfil pessoal para o perfil de trabalho.
  - **Evite qualquer partilha além-fronteiras**: Impede a partilha entre trabalho e perfis pessoais.
  - **As aplicações no perfil de trabalho podem processar o pedido de partilha do perfil pessoal**: ativa a funcionalidade do Android incorporada que permite a partilha do perfil pessoal para o perfil de trabalho. Quando ativada, um pedido de partilha de uma aplicação no perfil pessoal pode partilhar com aplicações no perfil de trabalho. Esta definição é o comportamento predefinido para dispositivos Android com versões anteriores à 6.0.
  - **Sem restrições à partilha**: Permite a partilha através do limite do perfil de trabalho em ambas as direções. Quando seleciona esta definição, as aplicações no perfil de trabalho podem partilhar dados com aplicações sem destaque no perfil pessoal. Esta definição permite que aplicações geridas no perfil de trabalho partilhem com aplicações no lado não gerido do dispositivo. Por isso, utilize esta definição com cuidado.

- **Notificações**de perfil de trabalho enquanto o dispositivo está bloqueado : O **bloco** impede que as notificações das janelas, incluindo torradas, chamadas recebidas, chamadas de saída, alertas de sistema e erros do sistema apareçam em dispositivos bloqueados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode apresentar notificações.
- **Permissões de aplicações predefinidas**: define a política de permissões predefinida para todas as aplicações do perfil de trabalho. A partir do Android 6, os utilizadores são solicitados a conceder determinadas permissões exigidas pelas aplicações quando a aplicação é lançada. Esta definição de política permite-lhe decidir se é pedido aos utilizadores a concessão de permissões para todas as aplicações no perfil de trabalho. Por exemplo, poderá atribuir uma aplicação ao perfil de trabalho que precisa de acesso de localização. Normalmente, essa aplicação leva os utilizadores a aprovarou ou negar o acesso à localização da aplicação. Utilize esta política para conceder automaticamente permissões sem um aviso prévio, negar automaticamente permissões sem um aviso prévio ou deixar os utilizadores decidirem. As opções são:
  - **Predefinição do dispositivo**
  - **Mensagem**
  - **Concessão de automóveis**
  - **Negar automaticamente**

  Também pode utilizar uma política de configuração de aplicações para conceder permissões para aplicações individuais (políticas de configuração de > **aplicações****de aplicações de clientes).**

- **Adicionar e remover contas**: **O bloco** impede os utilizadores de adicionar ou remover manualmente contas no perfil de trabalho. Por exemplo, quando implementa a aplicação do Gmail num perfil de trabalho Android, pode impedir que os utilizadores adicionem ou removam contas neste perfil de trabalho. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir adicionar contas no perfil de trabalho.  

  > [!NOTE]
  > As contas do Google não podem ser adicionadas a um perfil de trabalho.

- **Partilha de contato através de Bluetooth**: **Ativar** permite a partilha e acesso aos contactos de perfil de trabalho de outro dispositivo, incluindo um carro, que é emparelhado com Bluetooth. Ativar esta definição pode permitir que determinados dispositivos Bluetooth coloquem os contactos de trabalho na cache após a primeira ligação. A desativação desta política após um emparelhamento/sincronização inicial pode não remover os contactos de trabalho dos dispositivos Bluetooth.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode não partilhar contactos de trabalho.

  Esta definição aplica-se a:

  - Dispositivos de perfil de trabalho Android que executam o Android OS v6.0 e mais recentes

- **Captura do ecrã**: **O bloco** impede imagens ou capturas de ecrã no dispositivo no perfil de trabalho. Também impede que os conteúdos presentes sejam apresentados em dispositivos de visualização que não tenham uma saída de vídeo segura. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode permitir obter imagens.

- **Mostrar**o contacto do trabalho no perfil pessoal : **O bloco** não mostra o número de contacto de trabalho no perfil pessoal. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode mostrar detalhes de contacto de trabalho.

  Esta definição aplica-se a:

  - Android OS v6.0 e versões mais recentes

- **Pesquisar contactos de trabalho a partir de perfil pessoal**: O **Bloco** impede os utilizadores de procurar contactos de trabalho em aplicações no perfil pessoal. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir procurar contactos de trabalho no perfil pessoal.

- **Câmara**: **Bloco** impede o acesso à câmara no dispositivo no perfil de trabalho. A câmara na parte pessoal não é afetada por esta definição. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à câmara.

- **Permitir widgets a partir de aplicações de perfil de trabalho**: **Enable** permite que os utilizadores coloquem widgets expostos por aplicações no ecrã principal. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode desativar esta funcionalidade.

  Por exemplo, o Outlook está instalado nos perfis de trabalho dos seus utilizadores. Quando definido para **Ativar,** os utilizadores podem colocar o widget da agenda no ecrã principal do dispositivo.

- **Requerer a palavra-passe do perfil**de trabalho : **Exigir** forças uma política de código de acesso que se aplica apenas a aplicações no perfil de trabalho. Por predefinição, os utilizadores podem utilizar os dois PINs definidos separadamente. Ou, os utilizadores podem combinar os PINs no mais forte dos dois PINs. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores utilizem aplicações de trabalho sem introduzir uma palavra-passe.

  Esta definição aplica-se a:

  - Android 7.0 e mais recente com o perfil de trabalho ativado

- Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, entre 4 e 16 caracteres.
- **Minutos máximos de inatividade até que o perfil**de trabalho bloqueie : Introduza o comprimento do tempo que os dispositivos devem ficar inativos antes de o ecrã estar automaticamente bloqueado. Os utilizadores devem introduzir as suas credenciais para recuperar o acesso. Por exemplo, `5` introduza para bloquear o dispositivo após 5 minutos de inativo. Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.

  Nos dispositivos, os utilizadores não podem definir um valor de tempo superior ao tempo configurado no perfil. Os utilizadores podem definir um valor de tempo mais baixo. Por exemplo, se o `15` perfil for definido para minutos, os utilizadores podem definir o valor para 5 minutos. Os utilizadores não podem definir o valor para 30 minutos.

- **Número de falhas de entrada antes de limpar o dispositivo**: Introduza o número de senhas erradas permitidas antes de o dispositivo ser limpo, de 4 a 11. `0`(zero) pode desativar a funcionalidade de limpeza do dispositivo. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.

- **Expiração da palavra-passe (dias)**: Introduza o número de dias até que as palavras-passe do utilizador sejam alteradas (a partir de **1**-**365**).
- Tipo de **palavra-passe necessário**: Introduza o nível de complexidade da palavra-passe exigido e se podem ser utilizados dispositivos biométricos. As opções são:
  - **Predefinição do dispositivo**
  - **Biometria de baixa segurança**: [Biometria forte vs. biométrico fraco](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (abre o site do Android)
  - **Necessário**
  - **Pelo menos numérico:** Inclui caracteres `123456789`numéricos, tais como .
  - **Complexo numérico**: Números `1111` repetidos ou consecutivos, tais como ou, `1234`não são permitidos.
  - **Pelo menos alfabético:** Inclui letras no alfabeto. Não são obrigatórios números nem símbolos.
  - **Pelo menos alfanumérico:** Inclui letras maiúsculas, letras minúsculas e caracteres numéricos.
  - **Pelo menos alfanumérico com símbolos**: Inclui letras maiúsculas, letras minúsculas, caracteres numéricos, marcas de pontuação e símbolos.

- **Evite a reutilização de senhas anteriores**: Utilize esta definição para restringir os utilizadores a criarem senhas usadas anteriormente. Introduza o número de senhas usadas anteriormente que não podem ser usadas, de 1 a 24. Por exemplo, `5` introduza para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Desbloqueio de impressões digitais**: **O bloco** impede que os utilizadores utilizem o scanner de impressões digitais do dispositivo para desbloquear o dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores desbloqueiem o dispositivo utilizando uma impressão digital.
- **Smart Lock e outros agentes fidedignos:** **O Bloco** impede que o Smart Lock ou outros agentes fiduciários ajustem as definições do ecrã de bloqueio em dispositivos compatíveis. Se os dispositivos estiverem num local de confiança, então esta funcionalidade, também conhecida como agente fiduciário, permite-lhe desativar ou contornar a palavra-passe do ecrã de bloqueio do dispositivo. Por exemplo, ignore a palavra-passe do perfil de trabalho quando os dispositivos estiverem ligados a um dispositivo Bluetooth específico, ou quando os dispositivos estiverem perto de uma etiqueta NFC. Utilize esta definição para impedir que os utilizadores configurem o Smart Lock.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

### <a name="password"></a>Palavra-passe

Estas definições de palavra-passe aplicam-se a perfis pessoais em dispositivos que utilizam um perfil de trabalho.

- Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, entre 4 e 16 caracteres.
- **Minutos máximos de inatividade até que o ecrã bloqueie**: Introduza o comprimento do tempo que os dispositivos devem ficar inativos antes de o ecrã estar automaticamente bloqueado. Os utilizadores devem introduzir as suas credenciais para recuperar o acesso. Por exemplo, `5` introduza para bloquear o dispositivo após 5 minutos de inativo. Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.

  Nos dispositivos, os utilizadores não podem definir um valor de tempo superior ao tempo configurado no perfil. Os utilizadores podem definir um valor de tempo mais baixo. Por exemplo, se o `15` perfil for definido para minutos, os utilizadores podem definir o valor para 5 minutos. Os utilizadores não podem definir o valor para 30 minutos.

- **Número de falhas de entrada antes de limpar o dispositivo**: Introduza o número de senhas erradas permitidas antes de o dispositivo ser limpo, de 4 a 11. `0`(zero) pode desativar a funcionalidade de limpeza do dispositivo. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Expiração da palavra-passe (dias)**: Introduza o número de dias, até que a palavra-passe do dispositivo seja alterada, de 1 a 365. Por exemplo, `90` introduza para expirar a palavra-passe após 90 dias. Quando a palavra-passe expirar, será pedido aos utilizadores para criar uma nova. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- Tipo de **palavra-passe necessário**: Introduza o nível de complexidade da palavra-passe exigido e se podem ser utilizados dispositivos biométricos. As opções são:
  - **Predefinição do dispositivo**
  - **Biometria de baixa segurança**: [Biometria forte vs. biométrico fraco](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (abre o site do Android)
  - **Necessário**
  - **Pelo menos numérico:** Inclui caracteres `123456789`numéricos, tais como .
  - **Complexo numérico**: Números `1111` repetidos ou consecutivos, tais como ou, `1234`não são permitidos.
  - **Pelo menos alfabético:** Inclui letras no alfabeto. Não são obrigatórios números nem símbolos.
  - **Pelo menos alfanumérico:** Inclui letras maiúsculas, letras minúsculas e caracteres numéricos.
  - **Pelo menos alfanumérico com símbolos**: Inclui letras maiúsculas, letras minúsculas, caracteres numéricos, marcas de pontuação e símbolos.

- **Evite a reutilização de senhas anteriores**: Utilize esta definição para restringir os utilizadores a criarem senhas usadas anteriormente. Introduza o número de senhas usadas anteriormente que não podem ser usadas, de 1 a 24. Por exemplo, `5` introduza para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Desbloqueio de impressões digitais**: **O bloco** impede que os utilizadores utilizem o scanner de impressões digitais do dispositivo para desbloquear o dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores desbloqueiem o dispositivo utilizando uma impressão digital.
- **Smart Lock e outros agentes fidedignos:** **O Bloco** impede que o Smart Lock ou outros agentes fiduciários ajustem as definições do ecrã de bloqueio em dispositivos compatíveis. Se os dispositivos estiverem num local de confiança, então esta funcionalidade, também conhecida como agente fiduciário, permite-lhe desativar ou contornar a palavra-passe do ecrã de bloqueio do dispositivo. Por exemplo, ignore a palavra-passe do perfil de trabalho quando os dispositivos estiverem ligados a um dispositivo Bluetooth específico, ou quando os dispositivos estiverem perto de uma etiqueta NFC. Utilize esta definição para impedir que os utilizadores configurem o Smart Lock.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

### <a name="system-security"></a>Segurança do sistema

- **Verificação de ameaças em apps**: **Exigir** aplicações que a definição de Apps **de Verificação** está ativada para trabalho e perfis pessoais. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  Esta definição aplica-se a:

  - Android 8 (Oreo) e acima

- **Evite instalações de aplicações de fontes desconhecidas no perfil pessoal**: Por design, os dispositivos de perfil de trabalho android Enterprise não podem instalar aplicações de outras fontes que não a Play Store. Esta definição permite aos administradores um maior controlo das instalações de aplicações de fontes desconhecidas. **O Bloco** impede instalações de aplicações de outras fontes que não a Google Play Store no perfil pessoal. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir instalações de aplicações de fontes desconhecidas no perfil pessoal. Por natureza, os dispositivos de perfil de trabalho destinam-se a ter duplo perfil:

  - Um perfil de trabalho gerido usando MDM.
  - Um perfil pessoal isolado da gestão do MDM.

### <a name="connectivity"></a>Conectividade

- **VPN sempre ligado**: **Ativar** configura um cliente VPN para ligar e voltar a ligar-se automaticamente à VPN. As ligações VPN sempre ligadas permanecem ligadas. Ou, ligue imediatamente quando os utilizadores bloqueiam o seu dispositivo, o dispositivo reinicia ou a rede sem fios muda.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS pode desativar vpn sempre on para todos os clientes VPN.

  > [!IMPORTANT]
  > Certifique-se de que implementa apenas uma política de VPN Sempre Ativada num único dispositivo. Não é suportado implementar várias políticas de VPN Sempre Ativada num único dispositivo.

- **Cliente VPN**: selecione um cliente VPN que suporte a funcionalidade Always On. As opções são:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Personalizado
    - **ID de Pacote**: introduza o ID do pacote da aplicação na Google Play Store. Por exemplo, se o URL da aplicação na Play Store for `https://play.google.com/store/details?id=com.contosovpn.android.prod`, o ID de pacote é `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - O cliente VPN que escolher tem de estar instalado no dispositivo e deve suportar a VPN por aplicação em perfis de trabalho. Caso contrário, ocorrerá um erro.
  > - Tem de aprovar a aplicação cliente VPN na **Managed Google Play Store**, sincronizar a aplicação com o Intune e implementar a aplicação no dispositivo. Depois de o fazer, a aplicação é instalada no perfil de trabalho do utilizador.
  > - Pode haver problemas conhecidos ao utilizar VPN por app com Acesso F5 para Android 3.0.4. Consulte [as notas de lançamento do F5 para o Acesso F5 para Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android) para obter mais informações.

- **Modo de bloqueio**: **Ativar** todo o tráfego de rede para utilizar o túnel VPN. Se não for estabelecida uma ligação à VPN, o dispositivo não terá acesso à rede.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que o tráfego flua através do túnel VPN ou através da rede móvel.

## <a name="next-steps"></a>Passos seguintes

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode criar perfis de quiosque de dispositivos dedicados para dispositivos [Android](device-restrictions-android.md#kiosk) e [Windows 10.](kiosk-settings.md)

[Configure e desaponte os dispositivos empresariais Android no Microsoft Intune](https://support.microsoft.com/help/4476974).
