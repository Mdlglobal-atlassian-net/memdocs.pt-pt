---
title: Definições de dispositivos partilhados do Windows 10 - Microsoft Intune - Azure [ Microsoft Docs
description: Adicione e utilize o Windows 10 para configurar dispositivos partilhados ou utilizados por vários utilizadores no Microsoft Intune. Consulte uma lista de todas as definições e o que fazem nos dispositivos, incluindo o Microsoft Surface. Controle as contas dos hóspedes, gere as contas e elimine contas inativas, permita ou previna a poupança para o armazenamento local, delineie opções de energia e sono, escolha quando as atualizações são instaladas e utilize dispositivos em ambientes de educação num perfil de configuração do dispositivo.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
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
ms.openlocfilehash: f013074ac67b7622b509d8b9781de3ab5f4041e0
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429494"
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

- **Modo para PC partilhado**: **Ativar** as ligações no modo PC partilhado. Neste modo, apenas um utilizador entra no dispositivo de cada vez. Outro utilizador não pode iniciar sessão até que o primeiro utilizador se inscreva. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Conta de hóspedes**: Escolha criar uma opção de Hóspede no ecrã de iniciar sessão. As contas dos hóspedes não requerem credenciais de utilizador ou autenticação. Esta definição cria uma nova conta local cada vez que é usada. As opções são:
  - **Hóspede**: Cria uma conta de hóspedes localmente no dispositivo.
  - **Domínio**: Cria uma conta de hóspedes no Diretório Ativo Azure (AD).
  - **Hóspede e domínio**: Cria uma conta de hóspedes localmente no dispositivo, e no Diretório Ativo Azure (AD).
- **Gestão da conta**: Escolha se as contas são automaticamente eliminadas. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Ativado**: As contas criadas pelos hóspedes e as contas em AD e Azure AD são automaticamente eliminadas. Quando um utilizador assina fora do dispositivo, ou quando a manutenção do sistema é executado, estas contas são eliminadas.

    Introduza também:

    - **Eliminação da conta**: Escolha quando as contas são eliminadas:
      - **No limiar do espaço de armazenamento**
      - **No limiar do espaço de armazenamento e limiar inativo**
      - **Imediatamente após o log-out**

    Introduza também:

    - **Comece a eliminar o limiar(%)**: Introduza uma percentagem (0-100) de espaço em disco. Quando o espaço total de disco/armazenamento cai abaixo do valor que introduz, as contas em cache são eliminadas. Elimina continuamente as contas para recuperar o espaço do disco. As contas que estão inativas há mais tempo são eliminadas primeiro.
    - **Parar de eliminar limiar(%)**: Insira uma percentagem (0-100) do espaço do disco. Quando o espaço total de disco/armazenamento corresponde ao valor que introduz, a apagar para.
    - Limiar de **conta inativa**: Insira o número de dias consecutivos antes de apagar a conta que não assinou, de 0 a 60 dias.

  - **Desativado**: As contas ad locais, AD e Azure criadas pelos hóspedes permanecem no dispositivo e não são eliminadas.

- **Armazenamento local**: Com o armazenamento local, os utilizadores podem guardar e ver ficheiros no disco rígido do dispositivo. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Ativado**: Impede que os utilizadores guardem e visualizam ficheiros no disco rígido do dispositivo.
  - **Desativado**: Permite que os utilizadores vejam e guardem ficheiros localmente utilizando o File Explorer.

- **Políticas de alimentação**: Permitir ou impedir que os utilizadores mudem as definições de energia. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Ativado**: Os utilizadores não podem desligar a hibernação, não podem anular todas as ações de sono (como fechar a tampa) e não podem alterar as definições de energia.
  - **Desativado:** Os utilizadores podem hibernar o dispositivo, podem fechar a tampa para dormir o dispositivo e alterar as definições de energia.

- Tempo de **sono (em segundos)**: Introduza o número de segundos inativos (0-18000) antes de o dispositivo entrar em modo de sono. `0`significa que o dispositivo nunca dorme. Se não fixar um tempo, o aparelho dorme após 3600 segundos (60 minutos).

- **Iniciar sessão quando o PC acordar**: Escolha se os utilizadores devem iniciar sessão após o dispositivo sair do modo de sono. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Ativado**: Requer que os utilizadores insinuem com uma palavra-passe quando o dispositivo sai do modo de sono.
  - **Desativado**: Os utilizadores não têm de introduzir o seu nome de utilizador e palavra-passe.

- Tempo de **início de manutenção (em minutos a partir da meia-noite)**: Introduza o tempo em minutos (0-1440) quando as tarefas de manutenção automática, como o Windows Update, funcionarem. A hora de início padrão é meia-noite, ou zero `0` () minutos. Mude a hora de início entrando na hora de início em minutos a partir da meia-noite. Por exemplo, se quiser que a manutenção comece às 2 da manhã, introduza `120` . Se quiser que a manutenção comece às 20h, entre `1200` .

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

- **Políticas de educação**: Escolha se as políticas para o ambiente educativo estão habilitadas. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Ativado**: Utiliza as definições recomendadas para dispositivos utilizados nas escolas, que são mais restritivos.
  - **Deficientes**: As políticas de educação por defeito e recomendadas não são utilizadas.

  Para obter mais informações sobre o que as políticas de educação fazem, consulte as recomendações de [configuração do Windows 10 para os clientes de educação.](https://docs.microsoft.com/education/windows/configure-windows-for-education)

> [!TIP]
> [Criar um PC partilhado ou convidado](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (abre outro site docs) é um grande recurso nesta funcionalidade do Windows 10, incluindo conceitos e políticas de grupo que podem ser definidas em modo partilhado.

## <a name="next-steps"></a>Próximos passos

- [Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
- Consulte as definições para [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
