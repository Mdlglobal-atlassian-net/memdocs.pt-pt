---
title: Definições dos dispositivos macOS no Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Adicionar, configurar ou criar definições em dispositivos macOS para restringir funcionalidades, incluindo a definição de requisitos de palavra-passe, controlar o ecrã bloqueado, utilizar aplicações incorporadas, adicionar aplicações restritas ou aprovadas, gerir dispositivos Bluetooth, ligar à cloud para cópia de segurança e armazenamento, ativar o modo de quiosque, adicionar domínios e controlar como os utilizadores interagem com o browser Safari no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7054cb658314d00c3e10388c50c2309038c8a15b
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359124"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Definições dos dispositivos macOS para permitir ou restringir funcionalidades com o Intune

Este artigo apresenta e descreve as diferentes definições que pode controlar nos dispositivos macOS. Como parte da solução de gestão de dispositivos móveis (MDM), utilize estas definições para permitir ou desativar funcionalidades, definir regras de palavra-passe, permitir ou restringir aplicações específicas e muito mais.

Estas definições são adicionadas a um perfil de configuração do dispositivo no Intune e, em seguida, atribuídas ou implementadas nos dispositivos macOS.

## <a name="before-you-begin"></a>Antes de começar

[Crie um perfil de configuração de restrições do dispositivo](device-restrictions-configure.md).

> [!NOTE]
> Estas definições aplicam-se a diferentes tipos de matrículas. Para obter mais informações sobre os diferentes tipos de matrículas, consulte a [inscrição do macOS.](../enrollment/macos-enroll.md)

## <a name="general"></a>Geral

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo e inscrição automática de dispositivos

- **Definição Lookup**: **O bloco** impede o utilizador de realçar uma palavra e, em seguida, procurar a sua definição no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a funcionalidade de procura de definição.
- **Ditado**: **O bloco** impede que os utilizadores utilizem a entrada de voz para introduzir texto. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores utilizem a entrada de ditados.
- **Cache de conteúdo**: **O bloco** evita o cache de conteúdo. Os dados das aplicações das lojas de conteúdo, os dados do navegador web, os downloads e mais localmente nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ativar o cache de conteúdo.

  Para obter mais informações sobre a colocação de conteúdos em cache no macOS, veja [Gerir a cache de conteúdo no Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (abre outro site).

  Esta funcionalidade aplica-se a:  
  - macOS 10.13 e mais recente

- **Atualizações de software Defer**: **Enable** permite-lhe atrasar quando as atualizações de software são mostradas nos dispositivos, a partir de 0-90 dias. Esta definição não controla quando as atualizações são ou não instaladas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode apresentar atualizações nos dispositivos à medida que a Apple os lança. Por exemplo, se uma atualização do macOS for lançada pela Apple numa data específica, então essa atualização aparece naturalmente nos dispositivos em torno da data de lançamento. São permitidas atualizações de compilações de seed sem atraso.  

  - **Adiar a visibilidade das atualizações de software**: Introduza um valor de 0-90 dias. Quando o adiamento expirar, os utilizadores recebem uma notificação para atualizar para a versão mais antiga do SO disponível quando o adiamento foi acionado.

    Por exemplo, se uma atualização do macOS estiver disponível a **1 de janeiro**, e a visibilidade do **Atraso** for definida para **5 dias,** então a atualização não é mostrada como uma atualização disponível. No **sexto dia** seguinte ao lançamento, esta atualização está disponível e os utilizadores podem instalá-la.

    Esta funcionalidade aplica-se a:  
    - macOS 10.13.4 e mais recente

- **Screenshots**: O dispositivo deve ser matriculado na Inscrição automática de Dispositivos da Apple (DEP). **O bloco** impede que os utilizadores guardem imagens do ecrã. Também impede que a aplicação classroom observe ecrãs remotos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores capturem imagens e permita que a aplicação classroom veja ecrãs remotos.

### <a name="settings-apply-to-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição automática de dispositivos

- **Observação de ecrã remoto através**da aplicação Classroom : **Disable** impede os professores de usar a app Classroom para ver os ecrãs dos seus alunos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode permitir que os professores vejam os ecrãs dos seus alunos.

  Para utilizar esta definição, defina a definição **de Screenshots** para **Não configurada** (são permitidas imagens).

- **Observação não solicitada por app classroom**: Permitir **que** os professores vejam os ecrãs dos seus alunos sem exigir que os alunos concordem. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o Sistema operativo pode exigir que os alunos concordem antes que os professores possam ver os ecrãs.

  Para utilizar esta definição, defina a definição **de Screenshots** para **Não configurada** (são permitidas imagens).

- **Os alunos devem pedir autorização para deixar a aula**de aula : **Exigir** que os alunos matriculados num curso de sala de aula não gerido saiam do curso de sala de aula para obter a aprovação dos professores para abandonar o curso. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os alunos abandonem o curso sempre que o aluno quiser.

- **Os professores podem bloquear automaticamente dispositivos ou aplicações na aplicação Classroom**: **Permitir** que os professores bloqueiem o dispositivo ou app de um aluno sem a aprovação do aluno. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode exigir que os alunos concordem antes que os professores possam bloquear o dispositivo ou a aplicação.

- **Os alunos podem automaticamente aderir à aula**de aula : **Permitir** permite que os alunos entrem numa aula sem pedir ao professor. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SO pode exigir a aprovação dos professores para se juntar a uma aula.

## <a name="password"></a>Palavra-passe

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo e inscrição automática de dispositivos

- **Palavra-passe**: **Exija que** os utilizadores introduzam uma palavra-passe para aceder aos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode não necessitar de uma senha. Também não força quaisquer restrições, tais como bloquear senhas simples ou definir um comprimento mínimo.
  - Tipo de **palavra-passe necessário**: Introduza o nível de complexidade de senha exigido que a sua organização necessita. As opções são:
    - **Não configurado**: Intune não altera nem atualiza esta definição.
    - **Numérico:** A palavra-passe deve ser apenas números, como o 123456789.
    - **Alfanumérico:** Inclui letras maiúsculas, letras minúsculas e caracteres numéricos.

    Esta funcionalidade aplica-se a:  
    - macOS 10.10.3 e mais recente

  - **Número de caracteres não alfanuméricos na palavra-passe**: Introduza o número de caracteres complexos exigidos na palavra-passe, de 0-4. Um caráter complexo é um símbolo, como `?`
  - Comprimento mínimo da **palavra-passe**: Introduza o comprimento mínimo que a palavra-passe deve ter, de 4 a 16 caracteres.
  - **Palavras-passe simples**: Permitir a utilização de senhas simples, tais como `0000` ou `1234`.
  - **Minutos máximos após**o bloqueio do ecrã antes da necessidade da palavra-passe : Introduza o comprimento do tempo que os dispositivos devem estar inativos antes de ser necessária uma palavra-passe para desbloqueá-la. Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.
  - **Minutos máximos de inatividade até que o ecrã bloqueie**: Introduza o comprimento do tempo que os dispositivos devem ficar inativos antes de o ecrã estar automaticamente bloqueado. Por exemplo, introduza 5 dispositivos de bloqueio após 5 minutos de inativo. Quando o valor está em branco ou definido para **Não configurado**, Intune não altera nem atualiza esta definição.
  - **Expiração da palavra-passe (dias)** : Introduza o número de dias até que a palavra-passe do dispositivo seja alterada, de 1-65535. Por exemplo, insira `90` para expirar a senha após 90 dias. Quando a palavra-passe expirar, será pedido aos utilizadores para criar uma nova. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
  - **Evite a reutilização de senhas anteriores**: Utilize esta definição para restringir os utilizadores a criarem senhas usadas anteriormente. Introduza o número de senhas usadas anteriormente que não podem ser usadas, de 1 a 24. Por exemplo, insira 5 para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.

- **Bloquear o utilizador de modificar a senha**: O **bloco** impede que a senha seja alterada, adicionada ou removida. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o Sistema operativo pode permitir que as códigos de acesso sejam adicionadas, alteradas ou removidas.
- **Bloqueio de impressões digitais**: **Bloquear** impede a utilização de impressões digitais para desbloquear dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores desbloqueiem o dispositivo utilizando uma impressão digital.

- **Bloquear palavra-passe AutoFill**: **Bloquear** a utilização da função de palavras-passe automáticas no macOS. A escolha de **Bloquear** também tem o seguinte impacto:

  - Não é pedido aos utilizadores que utilizem uma palavra-passe guardada no Safari nem noutras aplicações.
  - As Palavras-passe Seguras automáticas estão desativadas, pelo que não são sugeridas aos utilizadores.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir estas funcionalidades.

- Bloquear pedidos de proximidade de **palavras-passe**: **O bloco** impede que os dispositivos solicitem senhas de dispositivos próximos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir estes pedidos de senha.

- **Partilha de palavras-passe**bloqueada : **O bloco** impede a partilha de palavras-passe entre dispositivos que utilizam o AirDrop. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a partilha de palavras-passe.

## <a name="built-in-apps"></a>Aplicações Incorporadas

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo e inscrição automática de dispositivos

- **Block Safari AutoFill**: **Bloquear** desativa a função de enchimento automático no Safari nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores alterem as definições autocompletas no navegador web.
- **Câmara de bloqueio**: **O bloco** impede o acesso à câmara nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir o acesso à câmara do dispositivo.
- **Block Apple Music**: **Block** reverte a aplicação Music para o modo clássico e desativa o serviço Music. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a utilização da aplicação Apple Music.
- **Bloquear resultados**de pesquisa na Internet : **Bloquear** impede o Spotlight de devolver quaisquer resultados de uma pesquisa na Internet. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que a pesquisa de Holofotes se conectem à Internet e obtenha resultados de pesquisa.
- **Transferência de ficheiros de bloco utilizando o iTunes**: **Bloquear** desativa serviços de partilha de ficheiros de aplicações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir serviços de partilha de ficheiros de aplicação.

  Esta funcionalidade aplica-se a:  
  - macOS 10.13 e mais recente

## <a name="restricted-apps"></a>Aplicações restritas

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo e inscrição automática de dispositivos

- **Tipo de lista de aplicações restritas**: Criar uma lista de aplicações que os utilizadores não estão autorizados a instalar ou usar. As opções são:

  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. Por padrão, os utilizadores podem ter acesso a apps que atribuem e aplicações incorporadas.
  - **Aplicações proibidas**: Lista rita as aplicações (não geridas pela Intune) que os utilizadores não estão autorizados a instalar e executar. Os utilizadores não estão impedidos de instalar uma aplicação proibida. Se um utilizador instalar uma aplicação a partir desta lista, é reportado no Intune.
  - **Aplicações aprovadas**: Lista as aplicações que os utilizadores estão autorizados a instalar. Para permanecerem compatíveis, os utilizadores não podem instalar outras aplicações. As aplicações que são geridas pela Intune são automaticamente permitidas, incluindo a aplicação Portal da Empresa. Os utilizadores não são impedidos de instalar uma aplicação que não esteja na lista aprovada. Mas se o fizerem, é relatado em Intune.

- Id do **pacote de aplicativos**: Introduza o pacote de aplicações [ID](bundle-ids-built-in-ios-apps.md) da app que deseja. Você pode mostrar ou esconder aplicativos incorporados e aplicativos de linha de negócio. O site da Apple tem uma lista de [aplicações incorporadas](https://support.apple.com/HT208094)da Apple.
- Nome da **aplicação**: Introduza o nome da aplicação que deseja. Você pode mostrar ou esconder aplicativos incorporados e aplicativos de linha de negócio. O site da Apple tem uma lista de [aplicações incorporadas](https://support.apple.com/HT208094)da Apple.
- **Editor**: Insira o editor da app.

Para adicionar aplicações a estas listas, pode:

- **Adicionar**: Selecione para criar a sua lista de aplicações.
- **Importe** um ficheiro CSV com detalhes sobre a aplicação, incluindo o URL. Utilize o formato `<app bundle ID>, <app name>, <app publisher>`. Ou, **Exportar** para criar uma lista de aplicações que adicionou, no mesmo formato.

## <a name="connected-devices"></a>Dispositivos ligados

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo e inscrição automática de dispositivos

- **Block AirDrop**: **Bloco** evita a utilização do AirDrop nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que a utilização da função AirDrop troque conteúdos com dispositivos próximos.
- **Bloqueio Apple Watch Auto Unlock**: O **bloco** impede os utilizadores de desbloquearem o seu dispositivo macOS com o apple Watch. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o OS poderá permitir que os utilizadores desbloqueiem o seu dispositivo macOS com o apple Watch.

## <a name="cloud-and-storage"></a>Cloud e armazenamento

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo e inscrição automática de dispositivos

- **Sincronização de keychain do iCloud:** **O bloco** desativa as credenciais de sincronização armazenadas no Keychain para o iCloud. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os utilizadores sincroniem estas credenciais.
- **Bloquear o iCloud Document Sync**: **O bloco** impede o iCloud de sincronizar documentos e dados. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir sincronização de documentos e valor-chave para o seu espaço de armazenamento iCloud.
- **Block iCloud Mail Backup**: **O bloco** impede que o iCloud se sincronize com a aplicação macOS Mail. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização do Correio para o iCloud.
- **Block iCloud Contact Backup**: **O bloco** impede o iCloud de sincronizar os contactos do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a sincronização de contacto utilizando o iCloud.
- **Block iCloud Calendar Backup**: **O bloco** impede que o iCloud se sincronize com a aplicação do calendário macOS. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização do Calendário para o iCloud.
- **Block iCloud Reminder Backup**: **O bloco** impede que o iCloud se sincronize com a aplicação de lembretes macOS. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização de Lembretes para o iCloud.
- **Block iCloud Bookmark Backup**: **O bloco** impede o iCloud de sincronizar os Marcadores do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização do Bookmark no iCloud.
- **Block iCloud Notes Backup**: **Bloco** impede o iCloud de sincronizar o dispositivo Notas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir a sincronização de Notas para o iCloud.
- **Bloqueie a biblioteca de fotos do iCloud**: **O bloco** desativa a biblioteca de fotos do iCloud e impede o iCloud de sincronizar as fotos do dispositivo. Quaisquer fotos não totalmente descarregadas do iCloud Photo Library são removidas do armazenamento local em dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir sincronizar fotografias entre o dispositivo e a biblioteca de fotografias iCloud.
- **Entrega**: Esta funcionalidade permite que os utilizadores comecem a trabalhar num dispositivo macOS e, em seguida, continuem o trabalho que iniciaram noutro dispositivo iOS/iPadOS ou macOS. **O bloco** impede a função Desminante nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir esta funcionalidade nos dispositivos.

  Esta funcionalidade aplica-se a:  
  - macOS 10.15 e mais recente

## <a name="domains"></a>Domínios

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo e inscrição automática de dispositivos

- URL de domínio de **e-mail**: **Adicione** um ou mais URLs na lista. Quando os utilizadores recebem um e-mail de um domínio diferente daquele configurado, o e-mail é marcado como não confiável na aplicação macOS Mail.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode restringir as funcionalidades e definições do dispositivo nos dispositivos [iOS/iPadOS.](device-restrictions-ios.md)
