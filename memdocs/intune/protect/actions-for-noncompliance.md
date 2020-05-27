---
title: Mensagem de não conformidade e ações com o Microsoft Intune – Azure | Microsoft Docs
description: Crie um e-mail de notificação para enviar para os dispositivos não conformes. Adicione ações depois de um dispositivo ser marcado como não conforme, tais como adicionar um período de tolerância para obter conformidade, ou crie um agendamento para bloquear o acesso até o dispositivo ficar em conformidade. Faça isto com o Microsoft Intune no Azure.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fff21eac61f7b68e00989aefc1f9ea6dc3ad7c0a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989305"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>Configure ações para dispositivos não conformes em Intune

Para dispositivos que não cumpram as suas políticas ou regras de conformidade, pode adicionar **Ações por incumprimento.** Esta funcionalidade configura uma sequência de ações ordenada pelo tempo, como enviar e-mails ao utilizador final, e muito mais.

## <a name="overview"></a>Descrição geral

Por predefinição, cada política de conformidade inclui a ação de incumprimento do **dispositivo Mark, não conforme** com um horário de zero dias **(0**). O resultado desta falha é quando intune deteta que um dispositivo não está em conformidade, Intune marca imediatamente o dispositivo como incompatível. Em seguida, o [Acesso Condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) do Diretório Ativo Azure (AD) pode bloquear o dispositivo.

Ao configurar **Ações para incumprimento** ganha flexibilidade para decidir o que fazer em relação a dispositivos não conformes e quando fazê-lo. Por exemplo, pode optar por não bloquear o dispositivo imediatamente e dar ao utilizador um período de carência para se tornar compatível.

Para cada ação que pode definir, pode configurar um horário que determina quando essa ação entrar em vigor com base no número de dias após a marcação do dispositivo como incompatível. Também pode configurar várias instâncias de uma ação. Quando se define várias instâncias de uma ação numa política, a ação volta a ser operada na hora programada posterior se o dispositivo permanecer incompatível.

Nem todas as ações estão disponíveis para todas as plataformas.

## <a name="available-actions-for-noncompliance"></a>Ações disponíveis para o incumprimento

Seguem-se as ações disponíveis para o incumprimento. Salvo indicação em contrário, cada ação está disponível para todas as plataformas suportadas pela Intune:

- **Marque o dispositivo sem conformidade:** Por defeito, esta ação está definida para cada política de conformidade e tem um horário de zero (**0**) dias, marcando os dispositivos como não conformes imediatamente.

  Ao alterar o horário predefinido, proporciona um período de carência no qual um utilizador pode remediar problemas ou tornar-se conforme sem ser marcado como incompatível.

- **Enviar e-mail para utilizador final**: Esta ação envia uma notificação por e-mail ao utilizador.
Quando ativar esta ação:

  - Selecione um modelo de *mensagem de notificação* que esta ação envia. Deve [criar um modelo](#create-a-notification-message-template) de mensagem de notificação antes de poder atribuir um a esta ação. Ao criar a notificação personalizada, personaliza o assunto, o corpo da mensagem e pode incluir o logótipo da empresa, o nome da empresa e informações adicionais de contacto.
  - Opte por enviar a mensagem a destinatários adicionais selecionando um ou mais dos seus Grupos AD Azure.

Quando o e-mail é enviado, intune inclui detalhes sobre o dispositivo não conforme na notificação de e-mail.

- **Bloqueie remotamente o dispositivo não conforme**: Utilize esta ação para emitir um bloqueio remoto de um dispositivo. Em seguida, é pedido ao utilizador um PIN ou palavra-passe para desbloquear o dispositivo. Saiba mais sobre a funcionalidade [Bloqueio Remoto](../remote-actions/device-remote-lock.md).

  As seguintes plataformas apoiam esta ação:
  - Android:
    - Android device administrator (Administrador de dispositivos Android)
    - Proprietário de dispositivo seleto de empresa android
    - Perfil de trabalho da empresa android
    - Dispositivos de quiosque Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 e posterior

- **Retire o dispositivo não conforme**: Esta ação remove todos os dados da empresa do dispositivo e remove o dispositivo da gestão intune. Para evitar a limpeza acidental de um dispositivo, esta ação suporta um horário mínimo de **30** dias.

  As seguintes plataformas apoiam esta ação:
  - Android:
    - Android device administrator (Administrador de dispositivos Android)
    - Proprietário de dispositivo seleto de empresa android
    - Perfil de trabalho da empresa android
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 e posterior

  Saiba mais sobre [dispositivos de aposentadoria.](../remote-actions/devices-wipe.md#retire)

- **Envie notificação push ao utilizador final**: Configure esta ação para enviar uma notificação push sobre o incumprimento de um dispositivo através da aplicação Portal da Empresa ou da App Intune no dispositivo.

  As seguintes plataformas apoiam esta ação:
  - Android:
    - Android device administrator (Administrador de dispositivos Android)
    - Proprietário de dispositivo seleto de empresa android
    - Perfil de trabalho da empresa android
  - iOS/iPadOS

  A notificação push é enviada na primeira vez que um dispositivo faz check-in com Intune e é considerado incompatível com a política de conformidade. Quando um utilizador seleciona a notificação, a aplicação 'Portal da Empresa' ou a aplicação Intune abre e exibe informações sobre o motivo pelo qual não são compatíveis. O utilizador pode então tomar medidas para resolver o problema. Os detalhes da mensagem sobre o incumprimento são gerados pela Intune e não podem ser personalizados.

  > [!IMPORTANT]
  > Intune, a aplicação Portal da Empresa e a aplicação Microsoft Intune não podem garantir a entrega de uma notificação push. As notificações podem aparecer após várias horas de atraso, se é que existem. Isto inclui quando os utilizadores desativam as notificações push.
  >
  > Não confie neste método de notificação para mensagens urgentes.

  Cada instância da ação envia uma notificação uma única vez. Para enviar novamente a mesma notificação de uma política, configure casos adicionais da ação nessa política, cada uma com um calendário diferente.
  
  Por exemplo, pode agendar a primeira ação por zero dias e, em seguida, adicionar uma segunda instância da ação definida para três dias. Este atraso antes da segunda notificação dá ao utilizador alguns dias para resolver o problema e evitar a segunda notificação.

  Para evitar spam ming utilizadores com demasiadas mensagens duplicadas, reveja e agilize quais as políticas de conformidade que incluem uma notificação push por incumprimento, e reveja os horários para evitar que as notificações repetidas para o mesmo problema sejam enviadas com demasiada frequência.

  Considere:
  - Para uma única política que inclua múltiplos casos de notificação push definida para o mesmo dia, apenas é enviada uma notificação única para esse dia.

  - Quando várias políticas de conformidade incluem as mesmas condições de conformidade, e incluem a ação de notificação push com o mesmo horário, várias notificações são enviadas para o mesmo dispositivo no mesmo dia.

## <a name="before-you-begin"></a>Antes de começar

Pode [adicionar ações de incumprimento](#add-actions-for-noncompliance) quando configura r'se a política de conformidade do dispositivo, ou posteriormente editando a política. Pode adicionar ações adicionais a cada política para atender às suas necessidades. Tenha em mente que cada política de conformidade inclui automaticamente a ação predefinida por incumprimento que marca os dispositivos como não conformes, com um horário definido para zero dias.

Para utilizar as políticas de conformidade do dispositivo para bloquear dispositivos a partir de recursos corporativos, o Azure AD Conditional Access deve ser configurado. Consulte o [Acesso Condicional no Diretório Ativo Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) ou [formas comuns](conditional-access-intune-common-ways-use.md) de utilizar o Acesso Condicional com Intune para obter orientação.

Para criar uma política de conformidade com o dispositivo, consulte as seguintes orientações específicas da plataforma:

- [Android](compliance-policy-create-android.md)
- [Perfis de trabalho do Android](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>Criar um modelo de mensagem de notificação

Para enviar um e-mail aos seus utilizadores, crie um modelo de mensagem de notificação. Quando um dispositivo não estiver em conformidade, os detalhes que introduzir no modelo são apresentados no e-mail enviado aos utilizadores.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Políticas de**conformidade de  >  **Compliance policies**  >  **dispositivos**  >  **Notificações Criar notificação**.
3. Em princípio, especifique as *seguintes*informações:

   - **Nome**
   - **Assunto**
   - **Mensagem**

4. Também no *Basics,* configure as seguintes opções para a notificação, quais todas as predefinições para *Ativado:*

   - **Cabeçalho de e-mail - Incluir logotipo da empresa**
   - **E-mail footer - Incluir nome da empresa**
   - **E-mail footer - Incluir informações de contacto**

   O logótipo que envia como parte da marca Portal da Empresa é usado para modelos de e-mail. Para obter mais informações sobre a imagem corporativa do Portal da Empresa, veja [Personalização da imagem corporativa da empresa](../apps/company-portal-app.md#customizing-the-user-experience).

   ![Exemplo de uma mensagem de notificação de conformidade no Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Selecione **Seguinte** para continuar.

5. Em **Review + criar,** reveja as suas configurações para garantir que o modelo de mensagem de notificação está pronto a ser utilizado. Selecione **Criar** para completar a criação da notificação.

> [!NOTE]
> Também pode selecionar um modelo de notificação existente que criou anteriormente e **editar** as suas informações para atualizar o modelo.

## <a name="add-actions-for-noncompliance"></a>Adicionar ações de não conformidade

Quando cria uma política de conformidade do dispositivo, o Intune cria automaticamente uma ação de não conformidade. Se um dispositivo não estiver a cumprir a sua política de conformidade, esta ação marca o dispositivo como não conforme. Pode personalizar o intervalo de tempo durante o qual o dispositivo está marcado como não conforme. Esta ação não pode ser removida.

Pode adicionar ações opcionais quando criar uma política de conformidade, ou atualizar uma política existente.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione Políticas de conformidade de **dispositivos,**  >  **Compliance policies**  >  **Policies**selecione uma das suas políticas e, em seguida, selecione **Propriedades**.

   Ainda não tem uma política? Crie uma política para [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) ou para outra plataforma.

   > [!NOTE]
   > Os dispositivos JAMF e dispositivos visados com grupos de dispositivos não conseguem receber ações de conformidade neste momento.

3. Selecione **Ações para não conformidade**  >  **Adicionar**.

4. Selecione a sua **Ação**:

   - **Enviar um email para os utilizadores finais**: quando o dispositivo não está em conformidade, opte por enviar um e-mail ao utilizador. Além disso:
     - Selecione o **Modelo de mensagem** que criou anteriormente
     - Introduza **Destinatários adicionais** ao selecionar grupos

   - **Bloquear remotamente o dispositivo em não conformidade**: quando o dispositivo não estiver em conformidade, bloqueie-o. Esta ação obriga o utilizador a introduzir um PIN ou uma senha para desbloquear o dispositivo.

   - **Retire o dispositivo não conforme**: Quando o dispositivo não estiver em conformidade, retire todos os dados da empresa do dispositivo e retire o dispositivo da gestão intune.

   - **Envie notificação push ao utilizador final**: Configure esta ação para enviar uma notificação push sobre o incumprimento de um dispositivo através da aplicação Portal da Empresa ou da App Intune no dispositivo.

5. Configurar um **Horário**: Insira o número de dias (0 a 365) após o incumprimento para desencadear a ação nos dispositivos dos utilizadores. (Reformar*o dispositivo não conforme* suporta um mínimo de 30 dias.) Após este período de carência, pode impor uma política de [acesso condicional.](conditional-access-intune-common-ways-use.md) Se introduzir o número de **dias 0** (zero) e ntão o acesso condicional entra em vigor **imediatamente**. Por exemplo, se um dispositivo não for conforme, utilize o acesso condicional para bloquear o acesso a e-mail, SharePoint e outros recursos da organização imediatamente.

   Quando cria uma política de conformidade, a ação não conforme do **dispositivo Mark** é automaticamente criada e configura-se automaticamente para **0** dias (imediatamente). Com esta ação, quando o dispositivo faz o check-in, o dispositivo é avaliado como não conforme imediatamente. Se também utilizar acesso condicional, o acesso condicional começa imediatamente. Se pretender permitir um período de carência, altere a **Agenda** da ação não conforme do **dispositivo Mark.**

   Na sua política de conformidade, por exemplo, também pretende notificar o utilizador. Pode adicionar o **e-mail enviar para terminar** a ação do utilizador. Neste enviar ação **por e-mail,** você definir o **Horário** para dois dias. Se o dispositivo ou utilizador final ainda for avaliado como incompatível no segundo dia, então o seu e-mail é enviado no segundo dia. Se quiser enviar novamente um e-mail ao utilizador no quinto dia de incumprimento, adicione outra ação e marque o **Horário** para cinco dias.

  Para obter mais informações sobre o cumprimento e as ações incorporadas, consulte a visão geral da [conformidade.](device-compliance-get-started.md)

6. Quando terminar, selecione **Adicionar**  >  **OK** para guardar as suas alterações.

## <a name="next-steps"></a>Passos seguintes

[Monitorizar as políticas](compliance-policy-monitor.md).
