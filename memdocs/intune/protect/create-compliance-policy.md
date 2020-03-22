---
title: Criar políticas de conformidade de dispositivos no Microsoft Intune - Azure  Microsoft Docs
description: Criar políticas de conformidade com dispositivos, visão geral dos níveis de estado e gravidade, utilizando o estatuto InGracePeriod, trabalhando com acesso condicional, manuseamento de dispositivos sem uma política atribuída, e as diferenças de conformidade no portal Azure e portal clássico em Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f84df30204f866e5498e97b8d64ed3fc6fd4ba28
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084915"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Criar uma política de conformidade no Microsoft Intune

As políticas de conformidade de dispositivos são um elemento fundamental ao utilizar o Intune para proteger os recursos da sua organização. No Intune, pode criar regras e definições que os dispositivos têm de cumprir para serem considerados como estando em conformidade, como a versão mínima do SO. Se o dispositivo não estiver em conformidade, pode bloquear o acesso a dados e recursos utilizando o [Acesso Condicional](conditional-access.md).

Também pode tomar medidas quanto à não conformidade, tais como enviar um e-mail de notificação ao utilizador. Para obter uma descrição geral do que fazem e como são utilizadas as políticas de conformidade, veja [introdução à conformidade de dispositivos](device-compliance-get-started.md).

Este artigo:

- Apresenta os pré-requisitos e os passos para criar uma política de conformidade.
- Mostra como atribuir a política aos grupos de utilizadores e dispositivos.
- Descreve funcionalidades adicionais, incluindo etiquetas de âmbito para “filtrar” as políticas, e os passos que pode efetuar nos dispositivos que não estão em conformidade.
- Apresenta os tempos de ciclos de atualização de entrada quando os dispositivos recebem as atualizações de política.

## <a name="before-you-begin"></a>Antes de começar

Para utilizar as políticas de conformidade de dispositivos:

- Utilize as seguintes subscrições:

  - Intune
  - Se utilizar o Acesso Condicional, precisa da edição Premium do Diretório Ativo Azure (AD). A página [Preços do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) descreve as funcionalidades das diferentes edições. A conformidade no Intune não exige o Microsoft Azure AD.

- Utilize uma plataforma suportada:

  - Administrador de dispositivos Android
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Wnodows Phone 8.1

- Inscreva os dispositivos no Intune (necessário para ver o estado de conformidade).

- Inscreva os dispositivos para um utilizador ou inscreva sem um utilizador primário. Os dispositivos inscritos para vários utilizadores não são suportados.

## <a name="create-the-policy"></a>Criar a política

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **Dispositivos** > **políticas** de conformidade > **políticas** > **criar políticas**.

3. Selecione uma **Plataforma** para esta política a partir das seguintes opções:
   - *Administrador de dispositivos Android*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows Phone 8.1*
   - *Windows 8.1 e posterior*
   - *Windows 10 e posterior*

    Para *Android Enterprise,* também selecione um tipo de **Política:**
     - *Política de conformidade do proprietário do dispositivo Android*
     - *Política de conformidade do perfil de trabalho android*

    Em seguida, selecione **Criar** para abrir a janela de configuração da **política Criar.**

4. No separador **Basics,** especifique um **Nome** que o ajude a identificá-los mais tarde. Por exemplo, um bom nome de política é **Mark iOS/iPadOS jailbroken devices como não conformes**.

   Também pode optar por especificar uma **Descrição**.
  
5. No separador definições de **conformidade,** expanda as categorias disponíveis e configure as definições para a sua apólice.  Os seguintes artigos descrevem as definições para cada plataforma:
   - [Administrador de dispositivos Android](compliance-policy-create-android.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows Phone 8.1, Windows 8.1 e posterior](compliance-policy-create-windows-8-1.md)
   - [Windows 10 e posterior](compliance-policy-create-windows.md)  

6. No separador **Localizações,** pode forçar a conformidade com base na localização do dispositivo. Escolha uma das localizações existentes. Se ainda não tiver uma localização disponível, consulte locais de [utilização (cerca de rede)](use-network-locations.md) para obter orientação.
   > [!TIP]
   > **As localizações** estão disponíveis apenas para a plataforma de administrador de *dispositivos Android.*

7. No separador **Ações para o incumprimento,** especifique uma sequência de ações para aplicar automaticamente a dispositivos que não cumpram esta política de conformidade.

   Pode adicionar múltiplas ações e configurar horários e detalhes adicionais para algumas ações. Por exemplo, pode alterar o horário da ação predefinida *O dispositivo Mark não está em conformidade* com o facto de ocorrer após um dia. Em seguida, pode adicionar uma ação para enviar um e-mail ao utilizador quando o dispositivo não estiver em conformidade para os avisar desse estado. Também pode adicionar ações que bloqueiem ou retirem dispositivos que permanecem incompatíveis.

   Para obter informações sobre as ações que pode configurar, consulte [Adicionar ações para dispositivos não conformes](actions-for-noncompliance.md), incluindo como criar e-mails de notificação para enviar aos seus utilizadores.

   Outro exemplo inclui a utilização de Locais onde se adiciona pelo menos um local a uma política de conformidade. Neste caso, a ação por incumprimento aplica-se quando seleciona pelo menos um local. Se o dispositivo não estiver ligado a nenhum dos locais selecionados, considera-se que não está em conformidade. Pode configurar a programação para dar aos seus utilizadores um período de carência, como um dia.

8. No separador **'Etiquetas Scope',** selecione etiquetas para ajudar a filtrar políticas para grupos específicos, como `US-NC IT Team` ou `JohnGlenn_ITDepartment`. Depois de adicionar as definições, também pode adicionar uma etiqueta de âmbito às políticas de conformidade. 

   Para obter informações sobre a utilização de etiquetas de âmbito, consulte [Utilize etiquetas de mira para filtrar as políticas](../fundamentals/scope-tags.md).

9. No separador **Atribuição,** atribua a apólice aos seus grupos.  

   Selecione **+ Selecione grupos para incluir** e, em seguida, atribuir a apólice a um ou mais grupos. A política aplicar-se-á a estes grupos quando salvar a política após o próximo passo. 

10. No **separador Review + criar,** reveja as definições e selecione **Criar** quando estiver pronto para salvar a política de conformidade.  

    Os utilizadores ou dispositivos visados pela sua apólice são avaliados para o cumprimento quando fazem o check-in com o Intune.

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>Tempos de ciclos de atualização

Intune usa diferentes ciclos de atualização para verificar se há atualizações às políticas de conformidade. Se o dispositivo se matriculou recentemente, o check-in funciona com mais frequência. Os ciclos de atualização de políticas e perfis listam os [tempos estimados](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) de atualização.

A qualquer momento, os utilizadores podem abrir a aplicação Portal da Empresa e sincronizar o dispositivo para verificar imediatamente as atualizações de políticas.

### <a name="assign-an-ingraceperiod-status"></a>Atribuir um estado InGracePeriod

O estado InGracePeriod de uma política de conformidade é um valor. Este valor é determinado pela combinação do período de carência de um dispositivo e pelo estado real de um dispositivo para essa política de conformidade.

Mais concretamente, se um dispositivo tiver um estado NonCompliant para uma política de conformidade atribuída e:

- O dispositivo não tem um período de carência atribuído, então o valor atribuído para a política de conformidade é NonCompliant
- O dispositivo tem um período de carência que expirou, então o valor atribuído para a política de conformidade é NonCompliant
- O dispositivo tem um período de carência que está no futuro, então o valor atribuído para a política de conformidade é InGracePeriod

A tabela seguinte apresenta um resumo destas opções:

|Estado de conformidade real|Valor do período de tolerância atribuído|Estado de conformidade em vigor|
|---------|---------|---------|
|NonCompliant |Sem período de tolerância atribuído |NonCompliant |
|NonCompliant |A data de ontem.|NonCompliant|
|NonCompliant |A data de amanhã|InGracePeriod|

Para obter mais informações sobre a monitorização de políticas de conformidade do dispositivo, veja [Monitorizar as Políticas de conformidade do dispositivo do Intune](compliance-policy-monitor.md).

### <a name="assign-a-resulting-compliance-policy-status"></a>Atribuir um resultado de estado das políticas de conformidade

Se um dispositivo tiver múltiplas políticas de conformidade e estados de conformidade diferentes para duas ou mais políticas de conformidade atribuídas, isso significa que está atribuído um único resultado de estado de conformidade. Esta atribuição baseia-se num nível de gravidade concetual atribuído a cada estado de conformidade. Cada estado de conformidade tem o seguinte nível de gravidade:

|Estado  |Gravidade  |
|---------|---------|
|Desconhecido     |1|
|NotApplicable     |2|
|Compatível|3|
|InGracePeriod|4|
|NonCompliant|5|
|Error|6|

Quando um dispositivo tem múltiplas políticas de conformidade, é atribuído o nível de gravidade mais elevado de todas as políticas a esse dispositivo.

Por exemplo, um dispositivo tem três políticas de conformidade atribuídas: uma com o estado Desconhecido (gravidade = 1), outra com o estado Conforme (gravidade = 3) e uma com o estado Em Período de Tolerância (gravidade = 4). O estado Em Período de Tolerância tem o nível de gravidade mais elevado. Por isso, todas as três políticas têm o estado de conformidade Em Período de Tolerância.

## <a name="next-steps"></a>Próximos passos

[Monitorizar as políticas](compliance-policy-monitor.md).
