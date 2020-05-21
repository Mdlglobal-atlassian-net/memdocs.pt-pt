---
title: Definições dos dispositivos macOS no Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Adicionar, configurar ou criar definições em dispositivos macOS para restringir funcionalidades, incluindo a definição de requisitos de palavra-passe, controlar o ecrã bloqueado, utilizar aplicações incorporadas, adicionar aplicações restritas ou aprovadas, gerir dispositivos Bluetooth, ligar à cloud para cópia de segurança e armazenamento, ativar o modo de quiosque, adicionar domínios e controlar como os utilizadores interagem com o browser Safari no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e48ba131d97e68570f1d6cb85b285ddc3198971c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429753"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Definições dos dispositivos macOS para permitir ou restringir funcionalidades com o Intune

Este artigo apresenta e descreve as diferentes definições que pode controlar nos dispositivos macOS. Como parte da solução de gestão de dispositivos móveis (MDM), utilize estas definições para permitir ou desativar funcionalidades, definir regras de palavra-passe, permitir ou restringir aplicações específicas e muito mais.

Estas definições são adicionadas a um perfil de configuração do dispositivo no Intune e, em seguida, atribuídas ou implementadas nos dispositivos macOS.

> [!NOTE]
> A interface do utilizador não pode corresponder aos tipos de inscrição deste artigo. A informação neste artigo está correta. A interface do utilizador está a ser atualizada num próximo lançamento.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de configuração de restrições de [dispositivos macOS](device-restrictions-configure.md).

> [!NOTE]
> Estas definições aplicam-se a diferentes tipos de matrículas. Para obter mais informações sobre os diferentes tipos de matrículas, consulte a [inscrição do macOS.](../enrollment/macos-enroll.md)

## <a name="built-in-apps"></a>Aplicações Incorporadas

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Block Safari AutoFill**: **Sim** desativa a função de enchimento automático no Safari nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores alterem as definições autocompletas no navegador web.
- **Utilização por bloco da câmara**: **Sim** impede o acesso à câmara nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à câmara do dispositivo.

  Intune só consegue o acesso à câmara do dispositivo. Não tem acesso a fotografias ou vídeos.
  
- **Block Apple Music**: **Yes** reverte a aplicação Music para o modo clássico, e desativa o serviço Music. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização da aplicação Apple Music.
- **Bloqueie sugestões**de holofotes : **Sim** impede o Spotlight de devolver quaisquer resultados de uma pesquisa na Internet. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que a pesquisa de Holofotes se conectem à Internet e obtenha resultados de pesquisa.
- **Transferência de ficheiros por bloco utilizando finder ou iTunes**: **Sim** desativa os serviços de partilha de ficheiros de pedidos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir serviços de partilha de ficheiros de aplicação.

  Esta funcionalidade aplica-se a:  
  - macOS 10.13 e mais recente

## <a name="cloud-and-storage"></a>Cloud e armazenamento

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- Bloqueie a sincronização do **keychain iCloud:** **Sim** desativa as credenciais de sincronização armazenadas no Keychain para o iCloud. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores sincroniem estas credenciais.
- **Bloqueie o iCloud Desktop e o Document Sync:** **Sim** impede o iCloud de sincronizar documentos e dados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir sincronização de documentos e valor-chave para o seu espaço de armazenamento iCloud.
- **Block iCloud Mail Backup**: **Sim** impede o iCloud de sincronizar na aplicação macOS Mail. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização do Correio para o iCloud.
- **Block iCloud Contact Backup**: **Sim** impede o iCloud de sincronizar os contactos do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a sincronização de contacto utilizando o iCloud.
- **Block iCloud Calendar Backup**: **Sim** impede o iCloud de sincronizar na aplicação macOS Calendar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização do Calendário para o iCloud.
- **Block iCloud Reminder Backup**: **Sim** impede o iCloud de sincronizar na aplicação macOS Reminders. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização de Lembretes para o iCloud.
- **Block iCloud Bookmark Backup**: **Sim** impede o iCloud de sincronizar os Marcadores do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização do Bookmark no iCloud.
- **Block iCloud Notes Backup**: **Sim** impede o iCloud de sincronizar o dispositivo Notas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização de Notas para o iCloud.
- **Block iCloud Photos backup**: **Yes** desativa o iCloud Photo Library e impede o iCloud de sincronizar as fotos do dispositivo. Quaisquer fotos não totalmente descarregadas do iCloud Photo Library são removidas do armazenamento local em dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir sincronizar fotografias entre o dispositivo e a biblioteca de fotografias iCloud.
- **Block Handoff**: Esta funcionalidade permite que os utilizadores comecem a trabalhar num dispositivo macOS e, em seguida, continuem o trabalho que iniciaram noutro dispositivo iOS/iPadOS ou macOS. **Sim,** impede a função de entrega nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade nos dispositivos.

  Esta funcionalidade aplica-se a:  
  - macOS 10.15 e mais recente

## <a name="connected-devices"></a>Dispositivos ligados

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Block AirDrop**: **Sim** evita a utilização do AirDrop nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que a utilização da função AirDrop troque conteúdos com dispositivos próximos.
- Bloqueio de **desbloqueio automático**do Apple Watch : **Sim** impede os utilizadores de desbloquearem o seu dispositivo macOS com o apple Watch. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o OS poderá permitir que os utilizadores desbloqueiem o seu dispositivo macOS com o apple Watch.

## <a name="domains"></a>Domínios

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Domínios de e-mail não marcados**: Introduza um ou mais URLs de domínio de **e-mail** na lista. Quando os utilizadores enviam ou recebem um e-mail de um domínio diferente dos domínios que adicionou, o e-mail é marcado como não confiável na aplicação macOS Mail.

## <a name="general"></a>Geral

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Bloqueio de espera**: **Sim** impede o utilizador de realçar uma palavra e, em seguida, procurar a sua definição no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a funcionalidade de procura de definição.
- **Ditado do bloco**: **Sim** impede os utilizadores de utilizarem a entrada de voz para introduzir texto. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem a entrada de ditados.
- **Bloqueio**de cache de conteúdo : **Sim** evita o cache de conteúdo. Os dados das aplicações das lojas de conteúdo, os dados do navegador web, os downloads e mais localmente nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ativar o cache de conteúdo.

  Para obter mais informações sobre a colocação de conteúdos em cache no macOS, veja [Gerir a cache de conteúdo no Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (abre outro site).

  Esta funcionalidade aplica-se a:  
  - macOS 10.13 e mais recente

- **Defer atualizações de software**: **Sim** permite-lhe atrasar quando as atualizações de software são mostradas nos dispositivos, de 0 a 90 dias. Esta definição não controla quando as atualizações são ou não instaladas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode apresentar atualizações nos dispositivos à medida que a Apple os lança. Por exemplo, se uma atualização do macOS for lançada pela Apple numa data específica, então essa atualização aparece naturalmente nos dispositivos em torno da data de lançamento. São permitidas atualizações de compilações de seed sem atraso.  

  - **Adiar a visibilidade das atualizações de software**: Introduza um valor de 0-90 dias. Quando o adiamento expirar, os utilizadores recebem uma notificação para atualizar para a versão mais antiga do SO disponível quando o adiamento foi acionado.

    Por exemplo, se uma atualização do macOS estiver disponível a **1 de janeiro**, e a visibilidade do **Atraso** for definida para **5 dias,** então a atualização não é mostrada como uma atualização disponível. No **sexto dia** seguinte ao lançamento, esta atualização está disponível e os utilizadores podem instalá-la.

    Esta funcionalidade aplica-se a:  
    - macOS 10.13.4 e mais recente

- **Imagens de blocos e gravação**de ecrã : O dispositivo deve ser matriculado na Inscrição automática de dispositivos da Apple (DEP). **Sim,** impede que os utilizadores guardem imagens do ecrã. Também impede que a aplicação classroom observe ecrãs remotos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores capturem imagens e permita que a aplicação classroom veja ecrãs remotos.

  - **Desative o AirPlay, veja o ecrã por app classroom e partilhe o ecrã:** **Sim** bloqueia o AirPlay e impede a partilha de ecrãs para outros dispositivos. Também impede os professores de usarem a app Classroom para verem os ecrãs dos seus alunos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode permitir que os professores vejam os ecrãs dos seus alunos.

    Para utilizar esta definição, defina as **imagens** do Bloco e a definição de gravação do ecrã para **Não configurada** (são permitidas imagens).

  - **Permitir que a aplicação de sala**de aula execute o AirPlay e veja o ecrã sem pedir : **Sim** permite que os professores vejam os ecrãs dos seus alunos sem exigir que os alunos concordem. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode exigir que os alunos concordem antes que os professores possam ver os ecrãs.

    Para utilizar esta definição, defina as **imagens** do Bloco e a definição de gravação do ecrã para **Não configurada** (são permitidas imagens).

- **Exigir autorização dos professores para deixar a app de sala**de aula não gerida : **Sim** obriga os alunos matriculados num curso de sala de aula não gerido a obter a aprovação dos professores para deixarem o curso. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os alunos abandonem o curso sempre que o aluno quiser.

- **Permitir que a sala de aula bloqueie o dispositivo sem pedir:** **Sim** permite que os professores bloqueiem o dispositivo ou app de um aluno sem a aprovação do aluno. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode exigir que os alunos concordem antes que os professores possam bloquear o dispositivo ou a aplicação.

- **Os alunos podem automaticamente ingressar na aula**de aula sem pedir : **Sim** permite que os alunos entrem numa aula sem pedir ao professor. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SO pode exigir a aprovação dos professores para se juntar a uma aula.

## <a name="password"></a>Palavra-passe

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Requerer a palavra-passe**: **Sim** requer que os utilizadores introduzam uma palavra-passe para aceder aos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não necessitar de uma senha. Também não força quaisquer restrições, tais como bloquear senhas simples ou definir um comprimento mínimo.
  - Tipo de **palavra-passe necessário**: Introduza o nível de complexidade de senha exigido que a sua organização necessita. Quando deixada em branco, intune não altera nem atualiza esta definição. As opções são:
    - **Não configurado:** Utiliza a predefinição do dispositivo.
    - **Alfanumérico:** Inclui letras maiúsculas, letras minúsculas e caracteres numéricos.
    - **Numérico:** A palavra-passe deve ser apenas números, como o 123456789.

    Esta funcionalidade aplica-se a:  
    - macOS 10.10.3 e mais recente

  - **Número de caracteres não alfanuméricos na palavra-passe**: Introduza o número de caracteres complexos exigidos na palavra-passe, de 0-4. Um caráter complexo é um símbolo, `?` como. Quando deixado em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.
  - Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, de 4 a 16 caracteres. Quando deixada em branco, intune não altera nem atualiza esta definição.
  - **Bloqueie palavras-passe simples**: **Sim** impede a utilização de senhas simples, tais como `0000` ou `1234` . Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir senhas simples.
  - **Minutos máximos de inatividade até que o ecrã bloqueie**: Introduza o comprimento do tempo que os dispositivos devem ficar inativos antes de o ecrã estar automaticamente bloqueado. Por exemplo, introduza os dispositivos de `5` bloqueio após 5 minutos de inatividade. Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.
  - **Minutos máximos após**o bloqueio do ecrã antes da necessidade da palavra-passe : Introduza o comprimento do tempo que os dispositivos devem estar inativos antes de ser necessária uma palavra-passe para desbloqueá-la. Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.
  - **Expiração da palavra-passe (dias)**: Introduza o número de dias até que a palavra-passe do dispositivo seja alterada, de 1-65535. Por exemplo, `90` introduza para expirar a palavra-passe após 90 dias. Quando a palavra-passe expirar, será pedido aos utilizadores para criar uma nova. Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.
  - **Evite a reutilização de senhas anteriores**: Restrinja os utilizadores de criarem senhas previamente utilizadas. Introduza o número de senhas usadas anteriormente que não podem ser usadas, de 1 a 24. Por exemplo, insira 5 para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.

- **Bloqueie o utilizador de modificar a senha**: **Sim** impede que a senha seja alterada, adicionada ou removida. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode permitir que as códigos de acesso sejam adicionadas, alteradas ou removidas.

- **Block Touch ID para desbloquear dispositivo**: **Sim** impede a utilização de impressões digitais para desbloquear dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores desbloqueiem o dispositivo utilizando uma impressão digital.

- **Bloquear palavra-passe AutoFill**: **Sim** impede a utilização da função de palavras-passe automática no macOS. Escolher **Sim** também tem o seguinte impacto:

  - Não é pedido aos utilizadores que utilizem uma palavra-passe guardada no Safari nem noutras aplicações.
  - As Palavras-passe Seguras automáticas estão desativadas, pelo que não são sugeridas aos utilizadores.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir estas funcionalidades.

- Bloquear pedidos de proximidade de **palavras-passe**: **Sim** impede que os dispositivos solicitem senhas de dispositivos próximos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir estes pedidos de senha.

- **Partilha de palavras-passe**bloqueada : **Sim** impede a partilha de palavras-passe entre dispositivos que utilizam o AirDrop. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a partilha de palavras-passe.

## <a name="privacy-preferences"></a>Preferências de privacidade

Em dispositivos macOS, apps e processos muitas vezes levam os utilizadores a permitir ou negar o acesso a funcionalidades do dispositivo, como a câmara, microfone, calendário, pasta de documentos e muito mais. Estas definições permitem aos administradores pré-aprovar ou pré-negar o acesso a estas funcionalidades do dispositivo. Ao configurar estas definições, gere o consentimento de acesso de dados em nome dos seus utilizadores. As suas definições anulam as decisões anteriores.

O objetivo destas configurações é reduzir o número de solicitações por apps e processos.

Esta funcionalidade aplica-se a:

- macOS 10.14 e mais recente
- Algumas definições aplicam-se ao macOS 10.15 e mais recentes.
- Estas definições aplicam-se apenas em dispositivos que tenham o perfil de preferências de privacidade instalado antes de serem atualizados.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo aprovado pelo utilizador, inscrição automática do dispositivo

- **Apps e processos**: **Adicione** apps ou processos para configurar o acesso. Introduza também:
  - **Nome**: Insira um nome para a sua aplicação ou processo. Por exemplo, introduza: `Microsoft Remote Desktop` ou `Microsoft Office 365`.
  
  - **Tipo de identificador**: As suas opções:
    - **Id do pacote**: Selecione esta opção para apps.
    - **Caminho**: Selecione esta opção para binários não agregados, que é um processo ou executável.

    As ferramentas auxiliares incorporadas num pacote de aplicações herdam automaticamente as permissões do seu pacote de aplicações de encerramento.

  - **Identificador**: Introduza o pacote de identificação da aplicação ou o caminho de ficheiro de instalação do processo ou executável. Por exemplo, introduza `com.contoso.appname`.

    Para obter o pacote de aplicações ID, abra a aplicação Terminal e execute o `codesign` comando. Este comando identifica a assinatura do código. Para que possa obter a identificação do pacote e a assinatura de código simultaneamente.

  - **Requisito de código**: Introduza a assinatura do código para a aplicação ou processo.

    Uma assinatura de código é criada quando uma aplicação ou binário é assinado por um certificado de desenvolvimento. Para encontrar a designação, execute o `codesign` comando manualmente na aplicação Terminal: `codesign --display -r -/path/to/app/binary` . A assinatura de código é tudo o que aparece `=>` depois.

  - **Ativar a validação de código estático**: Escolha **Sim** para a app ou processe para validar estáticamente o requisito do código. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição.

    Ativar esta definição apenas se o processo invalidar a sua assinatura de código dinâmico. Caso contrário, utilize **não configurado**.  

  - **Câmara de bloqueio**: **Sim** impede que a aplicação aceda à câmara do sistema. Não pode permitir o acesso à câmara. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição.

  - **Microfone do bloco**: **Sim** impede que a aplicação aceda ao microfone do sistema. Não pode permitir o acesso ao microfone. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição.

  - **Gravação do ecrã**do bloco : **Sim** bloqueia a aplicação de capturar o conteúdo do ecrã do sistema. Não é possível permitir o acesso à gravação de ecrã e à captura de ecrãs. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição.

    Requer macOS 10.15 e mais recente.

  - **Monitorização de entrada**por blocos : **Sim** bloqueia a aplicação de usar CoreGraphics e HID APIs para ouvir eventos CGEvents e HID de todos os processos. **Sim** também nega apps e processos de ouvir e recolher dados de dispositivos de entrada, como um rato, teclado ou trackpad. Não é possível permitir o acesso aos CoreGraphics e HID APIs.

    Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição.

    Requer macOS 10.15 e mais recente.

  - **Reconhecimento da fala**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a app aceda ao reconhecimento de voz do sistema e permita o envio de dados de fala para a Apple.
    - **Bloco**: Impede que a aplicação aceda ao reconhecimento da fala do sistema e impeça o envio de dados de fala para a Apple.

    Requer macOS 10.15 e mais recente.

  - **Acessibilidade**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda à aplicação de acessibilidade do sistema. Esta aplicação inclui legendas fechadas, texto sonoro e controlo de voz.
    - **Bloco**: Impede que a aplicação aceda à aplicação de acessibilidade do sistema.

  - **Contactos**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a informações de contacto geridas pela aplicação Contactos do sistema.  
    - **Bloco**: Impede que a aplicação aceda a estas informações de contacto.

  - **Calendário**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a informações de calendário geridas pela aplicação calendário do sistema.
    - **Bloco**: Impede que a aplicação aceda a esta informação do calendário.

  - **Lembretes**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a informações de lembrete geridas pela aplicação Lembretes do sistema.
    - **Bloco**: Impede que a aplicação aceda a esta informação de lembrete.

  - **Fotos**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda às imagens geridas pela aplicação fotos do sistema `~/Pictures/.photoslibrary` em .
    - **Bloco**: Impede que a aplicação aceda a estas imagens.

  - **Biblioteca de mídia**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda à atividade apple music, música e vídeo, e à biblioteca de mídia.  
    - **Bloco**: Impede que a aplicação aceda a este meio de comunicação.

    Requer macOS 10.15 e mais recente.

  - Presença do **fornecedor de ficheiros**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda à aplicação Do Fornecedor de Ficheiros e saiba quando os utilizadores estão a utilizar ficheiros geridos pelo Fornecedor de Ficheiros. Uma aplicação do Fornecedor de Ficheiros permite que outras aplicações do Fornecedor de Ficheiros acedam aos documentos e diretórios armazenados e geridos pela aplicação contendo.
    - **Bloco**: Impede que a aplicação aceda à aplicação Do Fornecedor de Ficheiros.

    Requer macOS 10.15 e mais recente.

  - **Acesso completo ao disco**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a todos os ficheiros protegidos, incluindo ficheiros de administração do sistema. Aplique esta definição com cuidado.
    - **Bloco**: Impede que a aplicação aceda a estes ficheiros protegidos.

  - **Ficheiros de administração**do sistema : As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a alguns ficheiros utilizados na administração do sistema.
    - **Bloco**: Impede que a aplicação aceda a estes ficheiros.

  - **Pasta de ambiente de trabalho**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a ficheiros na pasta desktop do utilizador.
    - **Bloco**: Impede que a aplicação aceda a estes ficheiros.

    Requer macOS 10.15 e mais recente.

  - **Pasta de documentos**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a ficheiros na pasta documentos do utilizador.
    - **Bloco**: Impede que a aplicação aceda a estes ficheiros.

    Requer macOS 10.15 e mais recente.

  - **Pasta de downloads**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a ficheiros na pasta de Downloads do utilizador.
    - **Bloco**: Impede que a aplicação aceda a estes ficheiros.

    Requer macOS 10.15 e mais recente.

  - **Volumes de rede**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a ficheiros em volumes de rede.
    - **Bloco**: Impede que a aplicação aceda a estes ficheiros.

    Requer macOS 10.15 e mais recente.

  - **Volumes amovíveis**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação aceda a ficheiros em volumes amovíveis, como um disco rígido.
    - **Bloco**: Impede que a aplicação aceda a estes ficheiros.

    Requer macOS 10.15 e mais recente.

  - **Eventos do sistema**: As suas opções:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Permitir**: Permite que a aplicação utilize APIs CoreGraphics para enviar CGEvents para o fluxo de eventos do sistema.
    - **Bloco**: Impede que a aplicação utilize APIs CoreGraphics para enviar CGEvents para o fluxo de eventos do sistema.

  - **Eventos apple**: Esta definição permite que as aplicações enviem um evento restrito da Apple para outra aplicação ou processo. Selecione **Adicionar** para adicionar uma aplicação ou processo de receção. Introduza as seguintes informações da app ou processo recetor:

    - **Tipo de identificador**: Selecione **O ID do pacote** se o identificador recetor for uma aplicação. Selecione **Caminho** se o identificador recetor for um processo ou executável.
    
    - **Identificador**: Introduza o pacote de identificação da aplicação ou o caminho de instalação do processo que recebe um evento da Apple.  

    - **Requisito de código**: Introduza a assinatura do código para a aplicação ou processo recetor.

      Uma assinatura de código é criada quando uma aplicação ou binário é assinado por um certificado de desenvolvimento. Para encontrar a designação, execute o `codesign` comando manualmente na aplicação Terminal: `codesign --display -r -/path/to/app/binary` . A assinatura de código é tudo o que aparece `=>` depois.

    - **Acesso**: Permitir que um macOS Apple Event seja enviado para a app ou processo recetor. As opções são:
      - **Não configurado**: Intune não altera nem atualiza esta definição.
      - **Permitir**: Permite que a aplicação ou processo envie o evento restrito da Apple para a app ou processo recetor.
      - **Bloco**: Impede que a aplicação ou processo envie um evento restrito da Apple para a app ou processo recetor.

  - **Guarde** as suas alterações.

## <a name="restricted-apps"></a>Aplicações restritas

### <a name="settings-apply-to-all-enrollment-types"></a>Definições aplicam-se a: Todos os tipos de inscrição

- **Tipo de lista de aplicações restritas**: Criar uma lista de aplicações que os utilizadores não estão autorizados a instalar ou usar. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por padrão, os utilizadores podem ter acesso a apps que atribuem e aplicações incorporadas.
  - **Aplicações aprovadas**: Lista as aplicações que os utilizadores estão autorizados a instalar. Para permanecerem compatíveis, os utilizadores não podem instalar outras aplicações. As aplicações que são geridas pela Intune são automaticamente permitidas, incluindo a aplicação Portal da Empresa. Os utilizadores não são impedidos de instalar uma aplicação que não esteja na lista aprovada. Mas se o fizerem, é relatado em Intune.
  - **Aplicações proibidas**: Lista rita as aplicações (não geridas pela Intune) que os utilizadores não estão autorizados a instalar e executar. Os utilizadores não estão impedidos de instalar uma aplicação proibida. Se um utilizador instalar uma aplicação a partir desta lista, é reportado no Intune.

- Lista de **aplicações**: **Adicione** aplicativos à sua lista:
  - Id do **pacote de aplicativos**: Introduza o id do [pacote](bundle-ids-built-in-ios-apps.md) da aplicação. Pode adicionar aplicações incorporadas e aplicações de linha de negócio. O site da Apple tem uma lista de [aplicações incorporadas](https://support.apple.com/HT208094)da Apple.

    Para localizar o URL de uma aplicação, abra o iTunes App Store e procure a aplicação. Por exemplo, procure `Microsoft Remote Desktop` ou `Microsoft Word`. Selecione a aplicação e copie o URL. Também pode utilizar o iTunes para localizar a aplicação e, em seguida, utilizar a tarefa **Copiar Ligação** para obter o URL da aplicação.

  - **Nome da aplicação**: introduza um nome simples para o ajudar a identificar o ID do pacote. Por exemplo, introduza `Intune Company Portal app`.
  - **Editor**: Insira o editor da app.

- **Importe** um ficheiro CSV com detalhes sobre a aplicação, incluindo o URL. Utilize o formato `<app bundle ID>, <app name>, <app publisher>`. Ou, **Exportar** para criar uma lista de aplicações que adicionou, no mesmo formato.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode restringir as funcionalidades e definições do dispositivo nos dispositivos [iOS/iPadOS.](device-restrictions-ios.md)
