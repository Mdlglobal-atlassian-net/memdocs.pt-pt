---
title: Definições de dispositivos iOS/iPadOS no Microsoft Intune - Azure Microsoft Docs
titleSuffix: ''
description: Adicione, configure ou crie configurações em dispositivos iOS/iPadOS para restringir funcionalidades, incluindo definir requisitos de palavra-passe, controlar o ecrã bloqueado, usar aplicações incorporadas, adicionar aplicações restritas ou aprovadas, lidar com dispositivos Bluetooth, ligar à nuvem para backup e armazenamento, ativar o modo de quiosque, adicionar domínios e controlar como os utilizadores interagem com o navegador web Safari no Microsoft Intune.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 897366ba9b7bae15050c0aa5e392ba5255a90b24
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407823"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>Definições de dispositivos iOS e iPadOS para permitir ou restringir funcionalidades usando Intune

Este artigo lista e descreve as diferentes definições que pode controlar nos dispositivos iOS e iPadOS. Como parte da solução de gestão de dispositivos móveis (MDM), utilize estas definições para permitir ou desativar funcionalidades, definir regras de palavra-passe, permitir ou restringir aplicações específicas e muito mais.

Estas definições são adicionadas a um perfil de configuração do dispositivo em Intune e, em seguida, atribuídas ou implantadas para os seus dispositivos iOS/iPadOS.

> [!TIP]
> Estas definições utilizam as definições de MDM da Apple. Para obter mais informações sobre estas definições, consulte [as definições de gestão de dispositivos móveis da Apple](https://support.apple.com/guide/mdm/welcome/web) (abre o site da Apple).

## <a name="before-you-begin"></a>Antes de começar

[Crie um perfil de configuração de restrições do dispositivo](device-restrictions-configure.md).

> [!NOTE]
> Estas configurações aplicam-se a diferentes tipos de matrículas, com algumas definições aplicáveis a todas as opções de inscrição. Para obter mais informações sobre os diferentes tipos de matrículas, consulte a [inscrição do iOS/iPadOS.](../enrollment/ios-enroll.md)

## <a name="general"></a>Geral

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Partilhar dados de utilização**: **O bloco** impede que os dispositivos enviem dados de diagnóstico e utilização para a Apple. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que estes dados sejam enviados.

- **Captura do ecrã**: **O bloco** impede imagens ou capturas de ecrã nos dispositivos. No iOS/iPadOS 9.0 e mais recente, também bloqueia as gravações de ecrã. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores capturem o conteúdo do ecrã como uma imagem ou como um vídeo.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Certificados TLS não fidedignos**: **Bloco** impede certificados de segurança de camadas de transporte não confiáveis (TLS) em dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir certificados TLS.
- **Bloqueie atualizações PKI over-the-air**: **O bloco** impede que os seus utilizadores recebem atualizações de software a menos que os dispositivos estejam ligados a um computador. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que um dispositivo receba atualizações de software sem estar ligado a um computador.
- **Limitar o rastreio de anúncios:** **Limitar** desativa o identificador de publicidade do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode mantê-lo ativado.
- **Enterprise app trust**: **Block** remove o botão Trust **Enterprise Developer** em Definições > General > Perfis & Gestão de Dispositivos nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores optem por confiar em aplicações que não são descarregadas a partir da loja de aplicações.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Modificação das definições de submissão**de diagnósticos : **O bloco** impede que os utilizadores mudem as definições de submissão de diagnóstico e análise de aplicações em **Diagnósticos e Utilizações** (Definições do dispositivo). Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem estas definições do dispositivo.

  Para utilizar esta definição, defina a definição de dados de **utilização do Share** para **bloquear**.

  Esta funcionalidade aplica-se a:  
  - iOS 9.3.2 e mais recente
  - iPadOS 13.0 e mais recente

- **Observação de ecrã remoto por app classroom**: O **bloco** impede que a aplicação de sala de aula veja remotamente o ecrã nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que a aplicação Apple Classroom veja o ecrã.

  Para utilizar esta definição, defina a definição de captura do **ecrã** para **bloquear**.

  Esta funcionalidade aplica-se a:  
  - iOS 9.3 e mais recente
  - iPadOS 13.0 e mais recente

- **Observação não solicitada por ecrã por app classroom**: Permitir **permite** que os professores observem silenciosamente o ecrã dos dispositivos iOS/iPadOS dos alunos utilizando a app Classroom sem o conhecimento dos alunos. Os dispositivos estudantis matriculados numa aula utilizando a app Classroom dão automaticamente permissão ao professor desse curso. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir esta funcionalidade.

  Para utilizar esta definição, defina a definição de captura do **ecrã** para **bloquear**.

- **Modificação da conta**: **O bloco** impede os utilizadores de atualizarem as definições específicas do dispositivo a partir da aplicação de definições iOS/iPadOS. Por exemplo, os utilizadores não podem criar novas contas de dispositivos ou alterar o nome de utilizador ou palavra-passe. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem estas definições.

  Esta funcionalidade aplica-se também a definições acessíveis a partir da aplicação de definições iOS/iPadOS, tais como Correio, Contactos, Calendário, Twitter e muito mais. Esta funcionalidade não se aplica a apps com configurações de conta que não sejam configuráveis a partir da aplicação de definições iOS/iPadOS, como é o caso da aplicação Microsoft Outlook.

- **Tempo**de ecrã : **O bloco** impede que os utilizadores estabeleçam as suas próprias restrições no Tempo do Ecrã (definições do dispositivo). Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores configurem as restrições do dispositivo (tais como controlos parentais ou conteúdo, e restrições de privacidade) em dispositivos.

  O nome desta definição foi mudado em **Ativar restrições nas definições do dispositivo**. Impacto desta alteração:  
  
  - iOS 11.4.1 ou mais: **O bloco** impede que os utilizadores estabeleçam as suas próprias restrições nas definições do dispositivo. O comportamento é o mesmo; e não há alterações para os utilizadores.
  - iOS 12.0 e mais recente: **O bloco** impede que os utilizadores definam o seu próprio Tempo de **Ecrã** nas definições do dispositivo (Definições > General > Tempo de ecrã), incluindo restrições de conteúdo e privacidade. Os dispositivos atualizados para o iOS 12.0 deixam apresentar o separador de restrições nas definições do dispositivo (Definições > Geral > Gestão de Dispositivos > Perfil de Gestão > Restrições). Estas definições estão em **Tempo do Ecrã**.
  
- **Utilização da opção**de apagar todos os conteúdos e definições no dispositivo : **O bloco** impede a utilização de todos os conteúdos e definições dos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode dar aos utilizadores acesso a estas definições.
- **Modificação do nome**do dispositivo : **O bloco** evita alterar o nome do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem o nome dos dispositivos.
- **Modificação das definições de notificação**: **O bloco** evita alterar as definições de notificação. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem as definições de notificação do dispositivo.
- **Modificação do papel de parede**: O **bloco** impede que o papel de parede seja alterado. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem o papel de parede nos dispositivos.
- **Alterações no perfil de configuração**: **O bloco** evita alterações no perfil de configuração nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores instalem perfis de configuração.
- **Bloqueio de ativação**: **Permitir ativa** o bloqueio de ativação em dispositivos iOS/iPadOS supervisionados. O Bloqueio de Ativação dificulta que um dispositivo perdido ou roubado seja reativado. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Remoção de aplicativos de blocos**: **Bloco** impede a remoção de aplicações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores removam as aplicações dos dispositivos.
- **Permitir acessórios USB enquanto o dispositivo estiver bloqueado:** **Permitir que** os acessórios USB troquem dados com dispositivos que estejam bloqueados durante mais de uma hora. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não atualizar o modo RESTRITO USB nos dispositivos, e os acessórios USB estão bloqueados da transferência de dados dos dispositivos se estiverem bloqueados durante mais de uma hora.
- **Forçar a data e a hora automáticas**: **Exigir** forças com controlo de dispositivos para definir automaticamente a Data e a Hora. O fuso horário do dispositivo é atualizado quando o dispositivo está ligado à rede móvel ou ao Wi-Fi com os serviços de localização ativados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Exigir que os alunos solicitem autorização para deixar**o curso de sala de aula : **Exigir** que os alunos matriculados num curso não gerido utilizem a app sala de aula para solicitar autorização ao professor para deixar o curso. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por defeito, o SO pode não forçar o aluno a pedir permissão.

  Esta funcionalidade aplica-se a:  
  - iOS 11.3 e mais recente
  - iPadOS 13.0 e mais recente

- Permitir que a **sala de aula bloqueie uma aplicação e bloqueie o dispositivo sem aviso:** **Ativar** permite que o professor bloqueie aplicações ou bloqueie dispositivos usando a aplicação Sala de aula sem avisar o aluno. Bloquear aplicações significa que os dispositivos só podem aceder a aplicações específicas do professor. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode impedir os professores de bloquear aplicações ou dispositivos usando a aplicação Sala de aula sem avisar o aluno.

  Esta funcionalidade aplica-se a:  
  - iOS 11.0 e mais recente
  - iPadOS 13.0 e mais recente

- **Junte-se automaticamente às aulas de sala**de aula sem pedir : **Ativar** automaticamente permite que os alunos entrem numa aula que esteja na app de sala de aula sem pedir ao professor. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SO pode levar o professor a querer aderir a uma aula que está na app da sala de aula.

  Esta funcionalidade aplica-se a:  
  - iOS 11.0 e mais recente
  - iPadOS 13.0 e mais recente

- **Criação VPN do bloco**: **O bloco** impede os utilizadores de criar configurações de configuração VPN. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores criem VPNs nos dispositivos.
- **Modificação das definições de eSIM**: **O bloco** impede a remoção ou adição de um plano celular ao eSIM nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem estas definições.

  Esta funcionalidade aplica-se a:  
  - iOS 12.1 e mais recente
  - iPadOS 13.0 e mais recente

- **Atualizações de software Defer**: **Enable** permite-lhe atrasar quando as atualizações de software são mostradas nos dispositivos, a partir de 0-90 dias. Esta definição não controla quando as atualizações são ou não instaladas.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS poderá apresentar atualizações de software em dispositivos à medida que a Apple os lança. Por exemplo, se uma atualização iOS/iPadOS for lançada pela Apple numa data específica, então essa atualização aparece naturalmente nos dispositivos em torno da data de lançamento.  

  - **Adiar a visibilidade das atualizações de software**: Introduza um valor de 0-90 dias. Quando o atraso expira, os utilizadores são notificados para atualizarem para a versão osso mais antiga disponível quando o atraso é desencadeado.

    Por exemplo, se o iOS 12.a estiver disponível a **1 de janeiro**, e a visibilidade do **Atraso** for fixada para **5 dias,** então o iOS 12.a não é apresentado como uma atualização disponível nos dispositivos do utilizador. No **sexto dia** seguinte ao lançamento, esta atualização está disponível e os utilizadores podem instalá-la.

    Esta definição aplica-se a:  
    - iOS 11.3 e mais recente
    - iPadOS 13.0 e mais recente

## <a name="password"></a>Palavra-passe

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Palavra-passe**: **Exija que** os utilizadores introduzam uma palavra-passe para aceder aos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores acedam aos dispositivos sem introduzir uma palavra-passe.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

> [!IMPORTANT]
> Nos dispositivos inscritos pelo utilizador, se configurar qualquer definição de palavra-passe, as definições **de palavras-passe Simples** são automaticamente definidas para **Bloquear**, e um PIN de 6 dígitos é aplicado.
>
> Por exemplo, configura a definição de validade da **Palavra-passe** e empurra esta política para dispositivos inscritos pelo utilizador. Nos dispositivos, acontece o seguinte:
>
> - A definição de expiração da **palavra-passe** é ignorada.
> - Não são permitidas senhas simples, como `1111` ou `1234`.
> - Um pino de 6 dígitos é imposto.

- **Palavras-passe simples**: **O bloco** requer senhas mais complexas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir senhas simples, como `0000` e `1234`.

- Tipo de **palavra-passe necessário**: Introduza o nível de complexidade de senha exigido que a sua organização necessita. As opções são:
  - **Predefinição do dispositivo**
  - **Numérico:** A palavra-passe deve ser apenas números, como o 123456789.
  - **Alfanumérico:** Inclui letras maiúsculas, letras minúsculas e caracteres numéricos.
- **Número de caracteres não alfanuméricos na palavra-passe**: Introduza o número de caracteres de símbolo, como `#` ou `@`, que devem ser incluídos na palavra-passe, de 1 a 4. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

- Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, de 4 a 16 caracteres. Nos dispositivos inscritos no utilizador, introduza um comprimento entre 4 e 6 caracteres.
  
  > [!NOTE]
  > Para dispositivos inscritos no utilizador, os utilizadores podem definir um PIN superior a 6 dígitos. Mas, não são aplicados mais de 6 dígitos nos dispositivos. Por exemplo, um administrador define o comprimento mínimo para `8`. Nos dispositivos inscritos no utilizador, os utilizadores só são obrigados a definir um PIN de 6 dígitos. Intune não força um PIN superior a 6 dígitos em dispositivos matriculados pelo utilizador.

- **Número de falhas de entrada antes de limpar o dispositivo**: Introduza o número de inscrições falhadas antes de o dispositivo ser limpo, de 4 a 11.
  
  O iOS/iPadOS tem uma segurança incorporada que pode afetar esta definição. Por exemplo, o iOS/iPadOS pode atrasar o desencadear da apólice dependendo do número de sinais em falhas. Também pode considerar introduzir repetidamente a mesma senha que uma tentativa. O guia de [segurança iOS/iPadOS](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) da Apple (abre o site da Apple) é um bom recurso e fornece detalhes mais específicos sobre códigos de acesso.
  
- **Minutos máximos após**o bloqueio do ecrã antes de ser necessária a palavra-passe<sup>1</sup>: Introduza o tempo de permanência dos dispositivos antes de os utilizadores reintroduzirem a sua palavra-passe. Se o tempo introduzido for maior do que o valor definido no dispositivo, o dispositivo ignorará o tempo introduzido.

  Esta definição aplica-se a:  
  - iOS 8.0+
  - iPadOS 13.0+

- **Minutos máximos de inatividade até que o ecrã bloqueie**<sup>1</sup>: Introduza o número máximo de minutos de inatividade permitidos nos dispositivos até que o ecrã bloqueie.

  **Opções iOS/iPadOS:**  

  - **Não configurado** (Predefinido): Intune não altera nem atualiza esta definição.
  - **Imediatamente**: Bloqueios de ecrã após 30 segundos de inatividade.
  - **1**: Bloqueios de ecrã após 1 minuto de inatividade.
  - **2**: Bloqueios de ecrã após 2 minutos de inatividade.
  - **3**: Bloqueios de ecrã após 3 minutos de inatividade.
  - **4**: Bloqueios de ecrã após 4 minutos de inatividade.
  - **5**: Bloqueios de ecrã após 5 minutos de inatividade.

  **opções para iPadOS:**  

  - **Não configurado** (Predefinido): Intune não altera nem atualiza esta definição.
  - **Imediatamente**: Bloqueios de ecrã após 2 minutos de inatividade.
  - **2**: Bloqueios de ecrã após 2 minutos de inatividade.
  - **5**: Bloqueios de ecrã após 5 minutos de inatividade.
  - **10**: Bloqueios de ecrã após 10 minutos de inatividade.
  - **15**: Bloqueios de ecrã após 15 minutos de inatividade.

  Se um valor não se aplica ao iOS e iPadOS, então a Apple utiliza o valor *mais baixo* mais próximo. Por exemplo, se introduzir `4` minutos, os dispositivos iPadOS usam `2` minutos. Se entrar `10` minutos, os dispositivos iOS utilizam `5` minutos. Esta é uma limitação da Apple.
  
  > [!NOTE]
  > O Intune UI para esta definição não separa os valores suportados pelo iOS e iPadOS. A UI pode ser atualizada num futuro lançamento.

- **Expiração da palavra-passe (dias)** : Introduza o número de dias antes de a palavra-passe do dispositivo ser alterada, de 1-65535.
- **Evite a reutilização de senhas anteriores**: Utilize esta definição para restringir os utilizadores a criarem senhas usadas anteriormente. Introduza o número de senhas usadas anteriormente que não podem ser usadas, de 1 a 24. Por exemplo, insira 5 para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Touch ID e Face ID desbloqueia:** **O bloco** evita a utilização de uma impressão digital ou rosto para desbloquear dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores desbloqueiem dispositivos utilizando biometria.

  Bloquear esta definição também impede a utilização da autenticação FaceID para desbloquear dispositivos.

  O ID do rosto aplica-se a:  
  - iOS 11.0 e mais recente
  - iPadOS 13.0 e mais recente

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Modificação da senha**: **O bloco** impede que a senha seja alterada, adicionada ou removida. Depois de bloquear esta funcionalidade, as alterações às restrições de código de acesso são ignoradas em dispositivos supervisionados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode permitir que as códigos de acesso sejam adicionadas, alteradas ou removidas.

  - **Modificação do ID do toque e do Face ID:** **O bloco** impede que os utilizadores mudem, acrescentem ou removam as impressões digitais touchID e o Face ID. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir aos utilizadores atualizaras impressões digitais TouchID e Face ID nos dispositivos.

    Bloquear esta definição também impede que os utilizadores mudem, acrescentem ou removam a autenticação FaceID.

    O ID do rosto aplica-se a:  
    - iOS 11.0 e mais recente
    - iPadOS 13.0 e mais recente

- **Bloquear palavra-passe AutoFill**: **Bloquear** a utilização da função de palavras-passe automáticas no iOS/iPadOS. A escolha de **Bloquear** também tem o seguinte impacto:

  - Não é pedido aos utilizadores que utilizem uma palavra-passe guardada no Safari nem noutras aplicações.
  - As Palavras-passe Seguras automáticas estão desativadas, pelo que não são sugeridas aos utilizadores.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir estas funcionalidades.

- Bloquear pedidos de proximidade de **palavras-passe**: **O bloco** impede que os dispositivos solicitem senhas de dispositivos próximos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir estes pedidos de senha.
- **Partilha de palavras-passe**bloqueada : **O bloco** impede a partilha de palavras-passe entre dispositivos que utilizam o AirDrop. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a partilha de palavras-passe.
- **Requerer a autenticação do Touch ID ou face ID para informações de palavra-passe ou cartão**de crédito AutoFill : **Exija que** os utilizadores autentiquem usando touchID ou FaceID antes que as palavras-passe ou informações do cartão de crédito possam ser preenchidas automaticamente no Safari e outras aplicações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores controlem esta funcionalidade nas definições do dispositivo.

  Esta funcionalidade aplica-se a:  
  - iOS 11.0 e mais recente
  - iPadOS 13.0 e mais recente
  
<sup>1</sup> Quando configurar os **minutos máximos de inatividade até que** o ecrã bloqueie e **os minutos máximos após** o bloqueio do ecrã antes de ser necessária uma definição de senha, são aplicados em sequência. Por exemplo, se definir o valor para ambas as definições para **5** minutos, o ecrã desliga-se automaticamente após cinco minutos e os dispositivos ficam bloqueados após mais cinco minutos. No entanto, se os utilizadores desligarem o ecrã manualmente, a segunda definição é imediatamente aplicada. No mesmo exemplo, depois de os utilizadores desligarem o ecrã, o dispositivo bloqueia cinco minutos depois.

## <a name="locked-screen-experience"></a>Experiência de Ecrã Bloqueado

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Acesso do Centro de Controlo enquanto está bloqueado**pelo dispositivo : **O bloco** impede o acesso à aplicação Do Centro de Controlo enquanto o dispositivo está bloqueado. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à aplicação Control Center quando os dispositivos estão bloqueados.
- **Notificações enquanto o dispositivo está bloqueado**: O **bloco** impede o acesso a notificações quando os dispositivos estão bloqueados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso a notificações sem desbloquear dispositivos.
- **Hoje vista enquanto o dispositivo está bloqueado**: O **bloco** impede o acesso à vista De hoje quando os dispositivos estão bloqueados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores vejam a visualização De hoje quando os dispositivos estão bloqueados.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Notificações de carteira enquanto o dispositivo está bloqueado**: O **bloco** impede o acesso à aplicação Wallet quando os dispositivos estão bloqueados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à aplicação Wallet enquanto os dispositivos estão bloqueados.

## <a name="app-store-doc-viewing-gaming"></a>App Store, Visualização de Documentos, Jogos

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Visualizar documentos corporativos em aplicações não geridas**: **O Bloco** impede a visualização de documentos corporativos em aplicações não geridas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que documentos corporativos sejam visualizados em qualquer aplicação.

  Por exemplo, quer impedir que os utilizadores guardem os ficheiros da aplicação OneDrive na Dropbox. Configure esta definição como **Bloquear**. Depois de os dispositivos receberem a apólice (por exemplo, após um reinício), já não permite a poupança.

  > [!NOTE]
  > Quando esta definição está bloqueada, os teclados de terceiros instalados na App Store também estão bloqueados.

  - **Permitir que as aplicações não geridas leiam**a partir de contas de contactos geridas : **Permitir** que as aplicações não geridas, como a aplicação incorporada iOS/iPadOS Contacts, leiam e acedam a informações de contacto de aplicações geridas, incluindo a aplicação móvel Outlook. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir a leitura, incluindo a remoção de duplicados, da aplicação Contactos incorporados nos dispositivos.  
  
    Esta definição permite ou impede a leitura de informações de contacto. Não controla sincronizar contactos entre as aplicações.
  
    Para utilizar esta definição, configure **Ver documentos empresariais em aplicações não geridas** como **Bloquear**.

  Para obter mais informações sobre estas duas definições e o seu impacto no Outlook para a sincronização de exportação de contactos iOS/iPadOS, consulte [a Dica de Suporte: Utilize as definições de perfil personalizado intune com a aplicação iOS/iPadOS Native Contacts.](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453)

- **Trate o AirDrop como um destino não gerido**: **Exigir** que o AirDrop seja considerado um alvo de queda não gerido. Impede que as aplicações geridas enviem dados através do Airdrop. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Visualizar documentos não corporativos em aplicações corporativas**: **O Bloco** impede a visualização de documentos não corporativos em aplicações corporativas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que qualquer documento seja visualizado em aplicações geridas por empresas.

  **O Bloco** também impede o contacto com a sincronização de exportação no Outlook para iOS/iPadOS. Para mais informações, consulte [A dica de suporte: Ativar o Outlook iOS/iPadOS Contact Sync com os controlos do MDM iOS12](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Requerer a senha do iTunes Store para todas as compras**: Exija **que** os utilizadores introduzam a palavra-passe apple ID para cada compra na aplicação ou iTunes. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir compras sem pedir sempre uma senha.
- **Compras in-app**: **O bloco** impede as compras in-app da loja. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir compras de loja dentro de uma aplicação de execução.
- **Descarregue os conteúdos da loja iBook sinalizadas como 'Erotica'** : **O Bloco** impede os utilizadores de descarregarem os meios de comunicação da loja iBook que está marcada como erótica. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores descarreguem livros com a categoria "Erotica".
- **Permitir que as aplicações geridas escrevam contactos para contas**de contactos não geridas : **Permitir** que as aplicações geridas, como a aplicação móvel Outlook, guardem ou sincronizam informações de contacto, incluindo contactos empresariais e corporativos, para a aplicação incorporada iOS/iPadOS Contacts. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS poderá impedir que as aplicações geridas guardem ou sincronizem informações de contacto para a aplicação de contactos iOS/iPadOS incorporados nos dispositivos.
  
  Para utilizar esta definição, configure **Ver documentos empresariais em aplicações não geridas** como **Bloquear**.

- **Região**de classificações : Selecione a região de classificações que pretende utilizar para downloads permitidos. E, em seguida, selecione as classificações permitidas para **Filmes,** **TV Shows**e **Apps**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Loja de aplicações**: **O bloco** impede o acesso à loja de aplicações em dispositivos supervisionados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode permitir o acesso.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

  - **Instalar aplicações a partir da App Store**: O **Block** não mostra a loja de aplicações no ecrã principal do dispositivo. Os utilizadores podem continuar a utilizar o iTunes ou o Configurator Apple para instalar aplicações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a loja de aplicações no ecrã principal.
  - **Downloads automáticos de aplicações**: **O Bloco** impede o descarregamento automático de aplicações compradas noutros dispositivos. Não afeta a atualização das aplicações existentes. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS poderá permitir que as aplicações compradas em outros dispositivos iOS/iPadOS descarreguem no dispositivo.

- Conteúdo explícito da **música, podcast ou notícias**do iTunes : **Block** previne conteúdos explícitos de música, podcast ou notícias do iTunes. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que o dispositivo aceda a conteúdos classificados como adultos a partir da loja.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

- **Adicionar amigos do Game Center**: O **Bloco** impede os utilizadores de adicionarem amigos do Game Center. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores adicionem amigos no Game Center.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

- **Game Center**: **Bloqueie** a utilização da aplicação Game Center. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização da aplicação Game Center nos dispositivos.
- **Jogos multijogador**: **Bloco** evita jogos multijogador. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores joguem jogos multijogador em dispositivos.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

- **Acesso à unidade de rede na aplicação Ficheiros**: Utilizando o protocolo do Bloco de Mensagens do Servidor (SMB), os dispositivos podem aceder a ficheiros ou outros recursos num servidor de rede. **Desativar** impede o acesso a ficheiros numa unidade SMB de rede. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode permitir o acesso.

  Esta funcionalidade aplica-se a:  
  - iOS 13.0 e mais recente
  - iPadOS 13.0 e mais recente

## <a name="built-in-apps"></a>Aplicações Incorporadas

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Siri**: **Bloco** impede acesso à Siri. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização do assistente de voz Siri nos dispositivos.
  - **Siri enquanto o dispositivo está bloqueado:** **O bloco** impede o acesso à Siri quando os dispositivos estão bloqueados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização do assistente de voz Siri nos dispositivos quando estão bloqueados.

- **Avisos de fraude safari**: **Exija que** os avisos de fraude sejam mostrados no navegador web em dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode desativar esta funcionalidade.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Pesquisa de holofotes para devolver resultados da internet**: **O Bloco** impede o Spotlight de devolver quaisquer resultados de uma pesquisa na Internet. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que a pesquisa de Holofotes se conectem à Internet para fornecer resultados de pesquisa.

- **Cookies de Safari**: Selecione como os cookies são tratados em dispositivos. As opções são:
  - Permitir
  - Bloquear todos os cookies
  - Permitir cookies dos sites visitados
  - Permitir cookies do site atual

- **Safari JavaScript**: **Bloco** impede que scripts Java no navegador sejam recorridos em dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir scripts Java.

- **Safari Pop-ups**: **O bloco** desativa o bloqueador pop-up no navegador web. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o bloqueador pop-up.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Câmara**: **Bloco** impede o acesso à câmara no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à câmara do dispositivo.

  Intune só consegue o acesso à câmara do dispositivo. Não tem acesso a fotografias ou vídeos.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

  - **FaceTime**: **O bloco** impede o acesso à aplicação FaceTime. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à aplicação FaceTime nos dispositivos.

    A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

- **Filtro de profanação Siri**: **Exigir** impede a Siri de ditar ou falar linguagem profana. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  Para utilizar esta definição, defina a definição **Siri** para **bloquear**.

  Esta funcionalidade aplica-se a:  
  - iOS 11.0 e mais recente

- **Siri para consultar conteúdo gerado pelo utilizador a partir da internet**: O **Bloco** impede a Siri de aceder a websites para responder a perguntas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir à Siri aceder a conteúdos gerados pelo utilizador a partir da internet.

  Para utilizar esta definição, defina a definição **Siri** para **bloquear**.

- **Apple News**: **Block** impede o acesso à aplicação Apple News nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização da aplicação Apple News.
- **loja iBooks**: **Bloco** impede o acesso à loja de iBooks. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores naveguem e comprem livros na loja iBooks.
- **Aplicação de mensagens no dispositivo**: **O Bloco** impede os utilizadores de utilizarem a aplicação Mensagens para iMessage. Se os dispositivos suportarem mensagens de texto, os utilizadores podem ainda enviar e receber mensagens de texto usando SMS. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que a utilização da aplicação Mensagens envie e leia mensagens através da internet.
- **Podcasts**: **O bloco** impede os utilizadores de utilizarem a aplicação Podcasts. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização da aplicação Podcasts.
- **Serviço de música**: **O bloco** reverte a aplicação Music para o modo clássico e desativa o serviço De Música. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização da aplicação Apple Music.
- **serviço de rádio iTunes**: **Bloquear** impede a utilização da aplicação iTunes Radio. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização da aplicação iTunes Radio.
- **loja iTunes**: **Bloquear** evita a utilização do iTunes nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir o iTunes.

  Esta funcionalidade aplica-se a:  
  - iOS 4.0 e mais recente
  - iPadOS 13.0 e mais recente

- **Encontre o meu iPhone**: **O Bloco** impede esta funcionalidade na aplicação Find My. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização desta funcionalidade Find My para obter a localização aproximada do dispositivo.

  Esta funcionalidade aplica-se a:  
  - iOS 13.0 e mais recente
  - iPadOS 13.0 e mais recente

- **Find my Friends**: **Block** evita esta funcionalidade na aplicação Find My. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização desta funcionalidade Find My para encontrar familiares e amigos de um dispositivo apple ou iCloud.com.

  Esta funcionalidade aplica-se a:  
  - iOS 13.0 e mais recente
  - iPadOS 13.0 e mais recente

- **Alterações nas definições da aplicação Find My Friends**: **Block** evita alterações nas definições da aplicação Find My Friends. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores alterem as definições para a aplicação Find My Friends.

- **Pesquisa de holofotes para devolver resultados da internet**: **O Bloco** impede o Spotlight de devolver quaisquer resultados de uma pesquisa na Internet. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que a pesquisa de Holofotes se conectem à Internet para fornecer resultados de pesquisa.

- **Remoção de blocos de aplicações do sistema a partir do dispositivo**: O **bloco** desativa a capacidade de remover aplicações do sistema dos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores removam as aplicações do sistema.

- **Safari**: **Bloqueie** a utilização do navegador Safari em dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores utilizem o navegador Safari.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

- **Safari Autofill**: **O bloco** desativa a função de enchimento automático no Safari nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores alterem as definições autocompletas no navegador web.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

## <a name="restricted-apps"></a>Aplicações restritas

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Tipo de lista de aplicações restritas**: Criar uma lista de aplicações que os utilizadores não estão autorizados a instalar ou usar. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir o acesso a apps que atribui e aplicações incorporadas.
  - **Aplicações proibidas**: Lista rita as aplicações (não geridas pela Intune) que os utilizadores não estão autorizados a instalar e executar. Os utilizadores não estão impedidos de instalar uma aplicação proibida. Se um utilizador instalar uma aplicação a partir desta lista, é reportado no Intune.
  - **Aplicações aprovadas**: Lista as aplicações que os utilizadores estão autorizados a instalar. Para permanecerem compatíveis, os utilizadores não podem instalar outras aplicações. As aplicações que são geridas pela Intune são automaticamente permitidas, incluindo a aplicação Portal da Empresa. Os utilizadores não são impedidos de instalar uma aplicação que não esteja na lista aprovada. Mas se o fizerem, é relatado em Intune.

Para adicionar aplicações a estas listas, pode:

- **Adicionar** o URL do iTunes App Store da aplicação desejada. Por exemplo, para adicionar a aplicação Microsoft Work Folders, insira `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` ou `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`.

  Para localizar o URL de uma aplicação, abra o iTunes App Store e procure a aplicação. Por exemplo, procure `Microsoft Remote Desktop` ou `Microsoft Word`. Selecione a aplicação e copie o URL.

  Também pode utilizar o iTunes para localizar a aplicação e, em seguida, utilizar a tarefa **Copiar Ligação** para obter o URL da aplicação.

- **Importe** um ficheiro CSV com detalhes sobre a aplicação, incluindo o URL. Utilize o formato `<app url>, <app name>, <app publisher>`. Ou, **Exportar** uma lista existente que inclui a lista de aplicações restritas no mesmo formato.

> [!IMPORTANT]
> Os perfis de dispositivo que utilizam as definições de aplicações restritas têm de ser atribuídos a grupos de utilizadores.

## <a name="show-or-hide-apps"></a>Mostrar ou ocultar aplicações

Esta funcionalidade aplica-se a:

- iOS 9.3 e mais recente
- iPadOS 13.0 e mais recente

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Tipo de lista de aplicações**: Criar uma lista de aplicações para mostrar ou ocultar. Você pode mostrar ou esconder aplicativos incorporados e aplicativos de linha de negócio. O site da Apple tem uma lista de [aplicações incorporadas](https://support.apple.com/HT208094)da Apple. As opções são:

  - **Aplicações ocultas**: Insira uma lista de aplicações ocultas dos utilizadores. Os utilizadores não podem ver nem abrir estas aplicações.
  
    A Apple evita esconder algumas aplicações nativas. Por exemplo, não é possível ocultar a aplicação **Definições** no dispositivo. [Eliminar aplicações incorporadas](https://support.apple.com/HT208094) da Apple lista as aplicações que podem ser ocultadas.
  
  - **Aplicativos visíveis**: Insira uma lista de aplicações que os utilizadores possam visualizar e lançar. Mais nenhuma outra aplicação pode ser vista ou lançada.

- **URL da aplicação**: Introduza o URL da aplicação da loja da app que pretende mostrar ou ocultar. Por exemplo:

  - Para adicionar a aplicação Microsoft Work Folders, introduza `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` ou `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`. 

  - Para adicionar a aplicação Microsoft Word, introduza `https://itunes.apple.com/de/app/microsoft-word/id586447913` ou `https://apps.apple.com/de/app/microsoft-word/id586447913`.

  Para localizar o URL de uma aplicação, abra o iTunes App Store e procure a aplicação. Por exemplo, procure `Microsoft Remote Desktop` ou `Microsoft Word`. Selecione a aplicação e copie o URL.

  Também pode utilizar o iTunes para localizar a aplicação e, em seguida, utilizar a tarefa **Copiar Ligação** para obter o URL da aplicação.

- Id do **pacote de aplicativos**: Introduza o pacote de aplicações [ID](bundle-ids-built-in-ios-apps.md) da app que deseja. Você pode mostrar ou esconder aplicativos incorporados e aplicativos de linha de negócio. O site da Apple tem uma lista de [aplicações incorporadas](https://support.apple.com/HT208094)da Apple.
- Nome da **aplicação**: Introduza o nome da aplicação que deseja. Você pode mostrar ou esconder aplicativos incorporados e aplicativos de linha de negócio. O site da Apple tem uma lista de [aplicações incorporadas](https://support.apple.com/HT208094)da Apple.
- **Editor**: Insira o editor da app que deseja.

Para adicionar aplicações, pode:

- **Adicionar**: Selecione para criar a sua lista de aplicações.
- **Importe** um ficheiro CSV com detalhes sobre a aplicação, incluindo o URL. Utilize o formato `<app url>, <app name>, <app publisher>`. Ou, **Exportar** para criar uma lista das aplicações restritas que adicionou, no mesmo formato.

## <a name="wireless"></a>Sem fios

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Roaming de dados**: **O bloco** impede que os dados perversem a rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o roaming de dados quando o dispositivo está numa rede celular.

  > [!IMPORTANT]
  > Esta definição é tratada como uma ação remota do dispositivo. Portanto, esta definição não é mostrada no perfil de gestão dos dispositivos. Sempre que o estado de roaming de dados muda no dispositivo, o **roaming de dados** é bloqueado pelo serviço Intune. Em Intune, se o estado de reporte mostrar um sucesso, então saiba que está a funcionar, mesmo que a configuração não seja mostrada no perfil de gestão do dispositivo.

- **Busca**global de fundo durante o roaming : O **bloco** impede a utilização da funcionalidade global de busca de fundo ao roaming através da rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os dispositivos recolham dados, como e-mail, quando está a roaming numa rede celular.
- **Marcação por voz**: **O bloco** impede a utilização da função de marcação por voz nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode permitir a marcação de voz nos dispositivos.
- **Roaming de voz**: **O bloco** impede que a voz vagueie pela rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o roaming de voz quando os dispositivos estão numa rede celular.
- **Hotspot pessoal**: **O bloco** desliga o hotspot pessoal em dispositivos com cada sincronização do dispositivo. Esta definição pode não ser compatível com algumas transportadoras. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode manter a configuração de hotspot pessoal como o padrão definido pelos utilizadores.

  > [!IMPORTANT]
  > Esta definição é tratada como uma ação remota do dispositivo. Portanto, esta definição não é mostrada no perfil de gestão dos dispositivos. Sempre que o estado do hotspot pessoal muda no dispositivo, o **Hotspot Pessoal** é bloqueado pelo serviço Intune. Em Intune, se o estado de reporte mostrar um sucesso, então saiba que está a funcionar, mesmo que a configuração não seja mostrada no perfil de gestão do dispositivo.

- **Regras de utilização celular (apenas aplicações geridas)** : **Permitir definir** os tipos de dados que as aplicações geridas podem usar quando em redes celulares. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. As opções são:
  - **Bloquear a utilização de dados celulares**: Bloquear a utilização de dados celulares para **todas as aplicações geridas** ou **escolher aplicações específicas**.
  - **Bloquear a utilização de dados celulares durante o roaming**: Bloquear a utilização de dados celulares ao roaming para **todas as aplicações geridas** ou **escolher aplicações específicas**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Alterações nas definições de utilização de dados celulares**da aplicação : **O bloco** evita alterações nas definições de utilização de dados celulares da aplicação. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores controlem quais as aplicações que podem utilizar dados celulares.
- **Alterações nas definições**do plano celular : **O bloco** evita alterar quaisquer definições no plano celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores façam alterações.

  Esta funcionalidade aplica-se a:  
  - iOS 11.0 e mais recente
  - iPadOS 13.0 e mais recente

- **Modificação do utilizador do Hotspot Pessoal**: O **bloco** evita alterar a definição de hotspot pessoal. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores ativem ou desativem o seu hotspot pessoal.

  Se bloquear esta definição e bloquear a definição **de Hotspot Pessoal,** o hotspot pessoal está desligado.

  Esta funcionalidade aplica-se a:  
  - iOS 12.2 e mais recente
  - iPadOS 13.0 e mais recente

- **Junte-se às redes Wi-Fi apenas utilizando perfis**de configuração : **Exija** que os dispositivos utilizem apenas redes Wi-Fi configuradas através de perfis de configuração Intune. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os dispositivos utilizem outras redes Wi-Fi.

  Quando estiver definido para **exigir,** certifique-se de que o dispositivo tem um perfil Wi-Fi. Se não atribuir um perfil Wi-Fi, esta definição poderá impedir que os dispositivos se conectem à internet. Por outras palavras, se este perfil de restrições do dispositivo for atribuído antes de um perfil Wi-Fi, o dispositivo poderá ser bloqueado da ligação à internet.
  
  Se não conseguir ligar, desinscreva o dispositivo e reinscreva-se com um perfil Wi-Fi. Em seguida, defina esta definição para **exigir** num perfil de restrições do dispositivo e atribua o perfil ao dispositivo.

- **Wi-Fi sempre ligado**: **Requiret** mantém wi-fi ligado na aplicação Definições. Não pode ser desligado em Definições ou no Centro de Controlo, mesmo quando o dispositivo está em modo avião. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores liguem ou desliguem o Wi-Fi.

  Configurar esta definição não impede que os utilizadores selecionem uma rede Wi-Fi.

  Esta funcionalidade aplica-se a:  
  - iOS 13.0 e mais recente
  - iPadOS 13.0 e mais recente

## <a name="connected-devices"></a>Dispositivos Ligados

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Deteção de pulso para relógio Apple emparelhado**: **Exigir** força um relógio Apple emparelhado para usar a deteção do pulso. Quando exigido, o Apple Watch não apresenta notificações quando não estiver a ser utilizado. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Requerer pedidos de saída do AirPlay a emparelhar palavra-passe**: **Exija** uma palavra-passe de emparelhamento ao utilizar o AirPlay para transmitir conteúdo para outros dispositivos da Apple. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores transmitam conteúdo utilizando o AirPlay sem introduzir uma palavra-passe.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **AirDrop**: **O bloco** evita a utilização do AirDrop nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que a utilização da função AirDrop troque conteúdos com dispositivos próximos.
- **Emparelhamento Apple Watch**: **Bloco** impede o emparelhamento com um Apple Watch. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os dispositivos emparelhem com um Apple Watch.
- **Modificação Bluetooth**: **O bloco** impede os utilizadores de alterar em dispositivos as definições Bluetooth. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores alterem estas definições.
- **Emparelhamento de hospedeiros para controlar os dispositivos um dispositivo iOS/iPadOS pode emparelhar com**: **O bloco** impede o emparelhamento do hospedeiro. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o OS pode permitir que o emparelhamento do anfitrião deixe o administrador controlar quais os dispositivos com que um dispositivo iOS/iPadOS pode emparelhar.
- **Block AirPrint**: **O bloco** impede a utilização da função AirPrint nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem o AirPrint.
  - **Armazenamento em bloco de credenciais AirPrint no Keychain**: **Bloquear** impede a utilização do armazenamento em keychain para o nome de utilizador e palavra-passe nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir armazenar o nome de utilizador e a palavra-passe do AirPrint na aplicação Keychain.
  - **Requerer um certificado TLS fidedigno para airPrint**: **Exigir** que os dispositivos utilizem certificados fidedignos para a comunicação de impressão TLS. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - Bloquear a **descoberta do iBeacon das impressoras AirPrint**: **Bloco** impede que balizas Bluetooth maliciosas do AirPrint sejam phishing para tráfego de rede. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a publicidade de impressoras AirPrint em dispositivos.
- **Bloquear a instalação de novos dispositivos próximos:** **Bloquear** desativa a solicitação para configurar novos dispositivos que se encontram nas proximidades. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores se conectem a outros dispositivos da Apple nas proximidades.

  Esta funcionalidade aplica-se a:  
  - iOS 11.0 e mais recente
  - iPadOS 13.0 e mais recente

- **Acesso a ficheiros na unidade USB:** Os dispositivos podem ligar e abrir ficheiros numa unidade USB. **Desativar** impede o acesso do dispositivo à unidade USB na aplicação Ficheiros quando uma USB está ligada ao dispositivo. Desativar esta funcionalidade também impede os utilizadores de transferirficheiros para uma unidade USB ligada a um iPad. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso a uma unidade USB na aplicação Ficheiros.

  Esta funcionalidade aplica-se a:  
  - iOS 13.0 e mais recente
  - iPadOS 13.0 e mais recente

## <a name="keyboard-and-dictionary"></a>Teclado e Dicionário

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Olhar de definição**de palavras : **O bloco** impede realçar uma palavra e, em seguida, olhar para a sua definição. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à funcionalidade de procura de definição.
- **Teclados preditivos**: **O bloco** impede a utilização de teclados preditivos para sugerir palavras que os utilizadores possam querer. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.
- **Correção automática**: **O bloco** evita a correção automática. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os dispositivos corrijam automaticamente palavras mal escritas.
- **Verificação ortográfica do teclado**: **O bloco** previne o verificador de feitiços. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode permitir a utilização de um verificador ortográfico.
- **Atalhos de teclado**: **O bloco** impede os utilizadores de utilizarem atalhos de teclado. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização de atalhos de teclado nos dispositivos.
- **Ditado**: **O bloco** impede que os utilizadores utilizem a entrada de voz para introduzir texto. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem a entrada de ditados.
- **QuickPath**: **O bloco** impede que os utilizadores utilizem quickPath. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem quickPath, o que permite uma entrada contínua no teclado do dispositivo. Os utilizadores podem escrever deslizando através das teclas para criar palavras.

  Esta funcionalidade aplica-se a:  
  - iOS 13.0 e mais recente
  - iPadOS 13.0 e mais recente

## <a name="cloud-and-storage"></a>Cloud e Armazenamento

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Backup encriptado**: **Exija** para que as cópias de segurança do dispositivo sejam encriptadas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Apps geridas sincronizam-se na nuvem**: **O Bloco** impede que as aplicações geridas por Intune sincronizem dados na conta iCloud do utilizador. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que este sincronizado de dados seja sincronizado no iCloud.
- **Block Enterprise Book Backup**: **Block** impede o backup de livros empresariais. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores reerquem estes livros.
- **Sincronização de metadados de livros empresariais de blocos (notas e destaques)** : **Bloco** impede a sincronização de notas e destaques nos livros empresariais. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a sincronização.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Sincronização**de fluxo de fotografia para iCloud : **Bloco** impede sincronização de fluxo de fotos no iCloud. Bloquear esta funcionalidade pode causar perda de dados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o OS pode permitir que os utilizadores ativem o **My Photo Stream** no seu dispositivo para sincronizar em iCloud, e ter fotos disponíveis em todos os dispositivos do utilizador.
- **iCloud Photo Library**: **Block** desativa utilizando biblioteca fotográfica iCloud para armazenar fotos e vídeos na nuvem. Quaisquer fotos não totalmente descarregadas do iCloud Photo Library para dispositivos são removidas do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a utilização da biblioteca fotográfica iCloud.
- **Fluxo de fotografiapartilhada**: **Bloco** desativa a partilha de **fotos do iCloud** nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir o streaming de fotografias partilhadas.
- **Handoff**: **O bloco** impede que os utilizadores comecem a trabalhar num dispositivo iOS/iPadOS e, em seguida, continue a trabalhar noutro dispositivo iOS/iPadOS ou macOS. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode permitir esta entrega.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Backup para iCloud**: **O bloco** impede os utilizadores de fazer backup de dispositivos para o iCloud. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores reporem os dispositivos para o iCloud.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

- **Sincronização de documentos do iCloud**: **O bloco** impede o iCloud de sincronizar documentos e dados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir sincronização de documentos e valor-chave para o seu espaço de armazenamento iCloud.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

- **Sincronização de keychain do iCloud:** **O bloco** desativa as credenciais de sincronização armazenadas no Keychain para o iCloud. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores sincroniem estas credenciais.

  A partir do iOS/iPadOS 13.0, esta definição requer dispositivos supervisionados.

## <a name="autonomous-single-app-mode"></a>Modo de aplicação single autónomo

Utilize estas definições para configurar dispositivos iOS/iPadOS para executar aplicações específicas no modo de aplicação single autónomo. Quando este modo está configurado e os utilizadores iniciam uma das aplicações configuradas, o dispositivo está bloqueado a essa aplicação. A comutação de aplicações/tarefas é desativada até que os utilizadores saiam da aplicação permitida.

Por exemplo, em ambiente escolar ou universitário, adicione uma aplicação que permite que os utilizadores possam fazer um teste no dispositivo. Ou, bloqueie o dispositivo na aplicação Portal da Empresa até que o utilizador autentique. Quando as ações das aplicações são concluídas pelos utilizadores, ou se remove esta política, o dispositivo regressa ao seu estado normal.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- Nome da **aplicação**: Introduza o nome da app que deseja.
- Id do **pacote de aplicativos**: Introduza o [pacote de identificação](bundle-ids-built-in-ios-apps.md) da app que deseja.
- **Adicionar**: Selecione para criar a sua lista de aplicações.

Também pode **importar** um ficheiro CSV com a lista de nomes de aplicações e as suas iDs de pacote. Ou **Exportar** uma lista existente que inclua as aplicações.

## <a name="kiosk"></a>Modo de Local Público

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **App para funcionar no modo quiosque**: Selecione o tipo de aplicações que pretende executar no modo quiosque. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não aplicar as definições do quiosque. O dispositivo não é executado no modo de quiosque.
  - **App de loja**: Introduza o URL numa aplicação na loja de aplicações do iTunes.
  - **App gerida**: Selecione uma aplicação que adicionou anteriormente ao Intune.
  - **App incorporada**: Introduza o [pacote ID](bundle-ids-built-in-ios-apps.md) da aplicação incorporada.

- **Toque de assistência**: **Exija** que a definição de acessibilidade do Toque de Assistência esteja nos dispositivos. Esta funcionalidade ajuda os utilizadores com os gestos no ecrã que podem ser difíceis para eles. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não executar ou ativar esta funcionalidade no modo quiosque.
- **Cores invertas**: **Exija** a definição de acessibilidade invert Colors para que os utilizadores com deficiências visuais possam alterar o ecrã de exibição. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não executar ou ativar esta funcionalidade no modo quiosque.
- **Mono audio**: **Exija** que a definição de acessibilidade áudio Mono esteja nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não executar ou ativar esta funcionalidade no modo quiosque.
- **Controlo de voz**: **A necessidade** permite o controlo de voz nos dispositivos e permite que os utilizadores controlem totalmente o SISTEMA utilizando comandos Siri. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode desativar o controlo de voz.

  Esta definição aplica-se a:  
  - iOS 13.0 e mais recente
  - iPadOS 13.0 e mais recente
  
  > [!TIP]
  > Se tiver aplicações LOB disponíveis para a sua organização, e **não** estiverem prontas no dia 0 quando o iOS 13.0 for lançado, recomendamos que deixe esta definição como **Não configurada**.

- **VoiceOver**: **Exija** que a definição de acessibilidade VoiceOver leia o texto no ecrã em voz alta. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não executar ou ativar esta funcionalidade no modo quiosque.
- **Zoom**: **Exija** a definição de Zoom para que os utilizadores possam tocar para ampliar no ecrã. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não executar ou ativar esta funcionalidade no modo quiosque.
- **Bloqueio automático**: **Bloqueio** evita bloqueio automático de dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.
- **Interruptor de toque**: **Bloqueie** o interruptor de toque (mudo) dos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.
- **Rotação do ecrã**: **O bloco** evita alterar a orientação do ecrã quando os utilizadores giram o dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.
- **Botão de sono de ecrã**: **Bloqueie** o botão de despertar do sono do ecrã nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade.
- **Toque**: **O bloco** desativa o ecrã tátil nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem o ecrã tátil.
- **Botões de volume**: **Bloquear** evita a utilização dos botões de volume nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir os botões de volume.
- **Controlo do toque assistida**: **Permitir que** os utilizadores utilizem a função de toque assistida. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode desativar esta funcionalidade.
- **Controlo de cores invertais**: **Permita** alterações de cor inversas para que os utilizadores ajustem a função de cores inversas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode desativar esta funcionalidade.
- **Falar sobre texto selecionado**: **Permita que** as definições de acessibilidade da Seleção de Fala estejam nos dispositivos. Esta funcionalidade lê texto em voz alta que os utilizadores selecionam. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode desativar esta funcionalidade.
- **Modificação**do controlo de voz : **Permitir que** os utilizadores alterem o estado de controlo de voz nos seus dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir os utilizadores de alterar o estado de controlo de voz nos seus dispositivos.

  Esta definição aplica-se a:  
  - iOS 13.0 e mais recente
  - iPadOS 13.0 e mais recente

- **Controlo VoiceOver**: **Permitir** alterações de voiceover para permitir que os utilizadores atualizem a função VoiceOver, como a rapidez com que o texto no ecrã é lido em voz alta. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode evitar alterações de voiceover.
- **Controlo de zoom**: **Permitir** alterações de zoom por parte dos utilizadores. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode evitar alterações de zoom.

> [!NOTE]
> Antes de configurar um dispositivo iOS/iPadOS para o modo de quiosque, tem de utilizar a ferramenta Configurator apple ou o Programa de Inscrição de Dispositivos apple para colocar os dispositivos em modo supervisionado. Consulte o guia da Apple sobre a utilização da ferramenta Apple Configurator.
> Se a aplicação iOS/iPadOS que introduz estiver instalada depois de atribuir o perfil, o dispositivo não entra no modo quiosque até que o dispositivo seja reiniciado.

## <a name="domains"></a>Domínios

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição do dispositivo, inscrição automática de dispositivos (supervisionado)

- **Domínios de e-mail não marcados** > URL de domínio de **e-mail**: Adicione um ou mais URLs à lista. Quando os utilizadores recebem um e-mail de um domínio diferente dos domínios em que introduz, o e-mail é marcado como não confiável na aplicação iOS/iPadOS Mail.

- **Domínios Web geridos** > **URL do Domínio Web**: adicione um ou mais URLs à lista. Quando forem transferidos documentos dos domínios introduzidos, estes serão considerados geridos. Esta definição só se aplica a documentos transferidos através do browser Safari.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Definições aplicam-se a: Inscrição automática de dispositivos (supervisionado)

- **Domínios de auto-enchimento de palavra-passe safari** > URL de **domínio:** Adicione um ou mais URLs à lista. Os utilizadores só podem guardar as palavras-passe Web de URLs nesta lista. Esta definição aplica-se apenas ao navegador Safari e aos dispositivos em modo supervisionado. Se não introduzir urLs, as palavras-passe podem ser guardadas em todos os web sites.

  Esta definição aplica-se a:  
  - iOS 9.3 e mais recente
  - iPadOS 13.0 e mais recente

## <a name="settings-that-require-supervised-mode"></a>Definições que exigem o modo supervisionado

O modo supervisionado iOS/iPadOS só pode ser ativado durante a configuração inicial do dispositivo através do Programa de Inscrição de Dispositivos da Apple, ou utilizando o Configurador Apple. Depois de ativar o modo supervisionado, o Intune pode configurar um dispositivo com a seguinte funcionalidade:

- Bloqueio de Aplicação (Modo de Aplicação Única) 
- Proxy HTTP Global 
- Desativar o Bloqueio de Ativação 
- Modo de Aplicação Única Autónomo 
- Filtro de Conteúdo Web 
- Definição de fundo e ecrã de bloqueio 
- Push da Aplicação Silencioso 
- VPN Sempre Ativada 
- Permitir exclusivamente a instalação de aplicações geridas 
- iBookstore 
- iMessages 
- Centro de Jogos 
- AirDrop 
- AirPlay 
- Emparelhamento de anfitrião 
- Sincronização de Nuvem 
- Pesquisa Spotlight 
- Handoff 
- Apagar dispositivo 
- Restrições da IU 
- Instalação dos perfis de configuração pela IU 
- Notícias 
- Atalhos de teclado 
- Modificações do código de acesso 
- Alterações do nome do dispositivo 
- Transferências automáticas de aplicações 
- Apple Music 
- Mail Drop 
- Emparelhar com o Apple Watch 

> [!NOTE]
> A Apple confirmou que determinadas definições serão mudadas para o modo apenas supervisionado em 2019. Recomendamos que tenha isto em consideração ao utilizar estas definições em vez de aguardar que a Apple efetue a migração para o modo apenas supervisionado:
>
> - Instalação da aplicação por utilizadores finais
> - Remoção de aplicações
> - FaceTime
> - Safari
> - iTunes
> - Conteúdos explícitos
> - Documentos e dados do iCloud
> - Jogos de vários jogadores
> - Adicionar amigos do Game Center
> - Siri

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode restringir as funcionalidades e as definições dos dispositivos nos dispositivos [macOS](device-restrictions-macos.md).
