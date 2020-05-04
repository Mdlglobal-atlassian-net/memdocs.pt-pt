---
title: Definições de dispositivos partilhados do Windows 10 - Microsoft Intune - Azure [ Microsoft Docs
description: Adicione e utilize o Windows 10 para configurar dispositivos partilhados ou utilizados por vários utilizadores no Microsoft Intune. Consulte uma lista de todas as definições e o que fazem nos dispositivos, incluindo o Microsoft Surface. Controle as contas dos hóspedes, gere as contas e elimine contas inativas, permita ou previna a poupança para o armazenamento local, delineie opções de energia e sono, escolha quando as atualizações são instaladas e utilize dispositivos em ambientes de educação num perfil de configuração do dispositivo.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/10/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: c76045413324deef395f546033d37ec47405a28f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79332249"
---
# <a name="windows-10-and-later-settings-to-manage-shared-devices-using-intune"></a>Windows 10 e configurações posteriores para gerir dispositivos partilhados usando Intune

O Windows 10 e dispositivos posteriores, como o Microsoft Surface, podem ser utilizados por muitos utilizadores. Os dispositivos que têm vários utilizadores são chamados dispositivos partilhados, e fazem parte das soluções de gestão de dispositivos móveis (MDM).

Utilizando o Microsoft Intune, os utilizadores finais podem iniciar sessão nestes dispositivos partilhados com uma conta de hóspedes. À medida que utilizam o dispositivo, só têm acesso às funcionalidades que permite. Como administrador intune, configura o acesso, escolhe quando as contas são eliminadas, as definições de gestão de energia de controlo e muito mais para os dispositivos windows 10 partilhados.

Este artigo lista e descreve as definições que utiliza num perfil de configuração do dispositivo Windows 10 (e posteriormente). Quando o perfil é criado em Intune, implementa ou atribui o perfil a grupos de dispositivos na sua organização. Também pode atribuir este perfil a grupos de dispositivos com tipos de dispositivos mistos e versões DE SM.

Para obter mais informações sobre esta funcionalidade em Intune, consulte o acesso ao [Controlo, contas e funcionalidades de energia em dispositivos de PC ou multiutilizadores partilhados](shared-user-device-settings.md). Para obter mais informações sobre o CSP do Windows, consulte [O CSP PartilhouPC](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

## <a name="before-your-begin"></a>Antes do seu início

[Criar o perfil.](shared-user-device-settings.md)

## <a name="shared-multi-user-device-settings"></a>Definições partilhadas de dispositivos multiutilizadores

Estas definições utilizam o [CSP SharedPC](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

- **Modo para PC partilhado**: Escolha **ativar** o modo PC partilhado. Neste modo, apenas um utilizador entra no dispositivo de cada vez. Outro utilizador não pode iniciar sessão até que o primeiro utilizador se inscreva. **Não configurado** (predefinido) deixa esta definição desgerida por Intune, e não pressiona nenhuma política para controlar esta definição num dispositivo.
- **Conta de hóspedes**: Escolha criar uma opção de Hóspede no ecrã de iniciar sessão. As contas dos hóspedes não requerem credenciais de utilizador ou autenticação. Esta definição cria uma nova conta local cada vez que é usada. As opções são:
  - **Hóspede**: Cria uma conta de hóspedes localmente no dispositivo.
  - **Domínio**: Cria uma conta de hóspedes no Diretório Ativo Azure (AD).
  - **Hóspede e domínio**: Cria uma conta de hóspedes localmente no dispositivo, e no Diretório Ativo Azure (AD).
- **Gestão de conta**: Definir para **permitir** a eliminação automática de contas locais criadas pelos hóspedes e contas em AD e Azure AD. Quando um utilizador assina fora do dispositivo, ou quando a manutenção do sistema é executado, estas contas são eliminadas. Quando ativado, também definido:
  - **Eliminação da conta**: Escolha quando as contas são eliminadas: **No limiar**do espaço de armazenamento , no limiar do espaço de armazenamento e no **limiar inativo,** ou imediatamente após o **log-out**. Também insira:
    - **Comece a eliminar o limiar(%)**: Introduza uma percentagem (0-100) de espaço em disco. Quando o espaço total de disco/armazenamento cai abaixo do valor que introduz, as contas em cache são eliminadas. Elimina continuamente as contas para recuperar o espaço do disco. As contas que estão inativas há mais tempo são eliminadas primeiro.
    - **Parar de eliminar limiar(%)**: Insira uma percentagem (0-100) do espaço do disco. Quando o espaço total de disco/armazenamento corresponde ao valor que introduz, a apagar para.

  Configurado para **Desativar** para manter as contas ad locais, AD e Azure criadas pelos hóspedes.

- **Armazenamento Local**: Escolha **ativado** para evitar que os utilizadores guardem e visualizam ficheiros no disco rígido do dispositivo. Escolha **o Desativado** para permitir que os utilizadores vejam e guardem ficheiros localmente utilizando o File Explorer. **Não configurado** (predefinido) deixa esta definição desgerida por Intune, e não pressiona nenhuma política para controlar esta definição num dispositivo.
- **Políticas de potência**: Quando definido para **Ativado,** os utilizadores não podem desligar a hibernação, não podem anular todas as ações de sono (como fechar a tampa), e não podem alterar as definições de energia. Quando programado para **Desativar,** os utilizadores podem hibernar o dispositivo, podem fechar a tampa para dormir o dispositivo e alterar as definições de energia. **Não configurado** (predefinido) deixa esta definição desgerida por Intune, e não pressiona nenhuma política para controlar esta definição num dispositivo.
- Tempo de **sono (em segundos)**: Introduza o número de segundos inativos (0-18000) antes de o dispositivo entrar em modo de sono. `0`significa que o dispositivo nunca dorme. Se não fixar um tempo, o aparelho dorme após 3600 segundos (60 minutos).
- **Iniciar sessão quando o PC acordar**: Ajuste para o **Ativado** para exigir que os utilizadores insinuem com uma palavra-passe quando o dispositivo sair do modo de sono. Escolha **O Desativado** para que os utilizadores não tenham de introduzir o seu nome de utilizador e palavra-passe. **Não configurado** (predefinido) deixa esta definição desgerida por Intune, e não pressiona nenhuma política para controlar esta definição num dispositivo.
- Tempo de **início de manutenção (em minutos a partir da meia-noite)**: Introduza o tempo em minutos (0-1440) quando as tarefas de manutenção automática, como o Windows Update, funcionarem. A hora de início padrão`0`é meia-noite, ou zero () minutos. Mude a hora de início entrando na hora de início em minutos a partir da meia-noite. Por exemplo, se quiser que a manutenção `120`comece às 2 da manhã, introduza . Se quiser que a manutenção comece `1200`às 20h, entre .
- Políticas de **educação**: Escolha **habilitado** a utilizar as definições recomendadas para dispositivos utilizados nas escolas, que são mais restritivas. Escolha **deficientes** para que as políticas de educação padrão e recomendada não sejam usadas. **Não configurado** (predefinido) deixa esta definição desgerida por Intune, e não pressiona nenhuma política para controlar esta definição num dispositivo.

  Para obter mais informações sobre o que as políticas de educação fazem, consulte as recomendações de [configuração do Windows 10 para os clientes de educação.](https://docs.microsoft.com/education/windows/configure-windows-for-education)

- **Início rápido de início de sessão** (depreciado): Escolha **Ativado para** que os utilizadores tenham uma experiência rápida de primeiro início de sessão. Quando **ativado,** o dispositivo liga automaticamente novas contas adinárias não-admin a contas locais pré-configuradas. Escolha **Desativado** para evitar a experiência rápida de primeiro início de sessão. **Não configurado** (predefinido) deixa esta definição desgerida por Intune, e não pressiona nenhuma política para controlar esta definição num dispositivo.

  Esta definição é removida numa próxima versão. Não utilize esta definição.

  [Autenticação/EnableFastFirstSignIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-enablefastfirstsignin)

> [!TIP]
> [Criar um PC partilhado ou convidado](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (abre outro site docs) é um grande recurso nesta funcionalidade do Windows 10, incluindo conceitos e políticas de grupo que podem ser definidas em modo partilhado.

## <a name="next-steps"></a>Passos seguintes

- [Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
- Consulte as definições para [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
