---
title: Mensagem de não conformidade e ações com o Microsoft Intune – Azure | Microsoft Docs
description: Crie um e-mail de notificação para enviar para os dispositivos não conformes. Adicione ações depois de um dispositivo ser marcado como não conforme, tais como adicionar um período de tolerância para obter conformidade, ou crie um agendamento para bloquear o acesso até o dispositivo ficar em conformidade. Faça isto com o Microsoft Intune no Azure.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/08/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17a3a3b38b28eda0e4bde9c353482d0234fa3329
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330013"
---
# <a name="automate-email-and-add-actions-for-noncompliant-devices-in-intune"></a>Automatizar e-mail e adicionar ações para dispositivos não conformes em Intune

Para dispositivos que não cumpram as suas políticas ou regras de conformidade, pode adicionar **Ações por incumprimento.** Esta funcionalidade configura uma sequência de ações ordenada pelo tempo, como enviar e-mails ao utilizador final, e muito mais.

## <a name="overview"></a>Descrição geral

Por predefinição, quando o Intune deteta um dispositivo não conforme, este marca imediatamente o dispositivo como não conforme. [Acesso Condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) do Diretório Ativo Azure (AD) bloqueia o dispositivo. Quando um dispositivo não é compatível, **a ação por incumprimento** também lhe dá flexibilidade para decidir o que fazer. Por exemplo, não bloqueie o dispositivo de imediato e dê ao utilizador um período de tolerância para ficar conforme.

Existem vários tipos de ação:

- **Enviar um e-mail para o utilizador final**: personalize uma notificação por e-mail antes de a enviar para o utilizador final. Pode personalizar os destinatários, o assunto e o corpo da mensagem, incluindo o logótipo da empresa e as informações de contacto.

    Além disso, o Intune inclui detalhes sobre o dispositivo não conforme na notificação por e-mail.

- **Bloquear remotamente o dispositivo em não conformidade**: para dispositivos que não estão em conformidade, pode emitir um bloqueio remoto. Em seguida, é pedido ao utilizador um PIN ou palavra-passe para desbloquear o dispositivo. Saiba mais sobre a funcionalidade [Bloqueio Remoto](../remote-actions/device-remote-lock.md).

- **Marcar dispositivos como não conformes**: crie um agendamento (ao nível do número de dias) após o dispositivo ser marcado como não conforme. Pode configurar a ação para entrar em vigor imediatamente ou dar ao utilizador um período de tolerância para este ficar em conformidade.

Este artigo mostra-lhe como:

- Criar um modelo de notificação por mensagem
- Criar uma ação de não conformidade, como enviar um e-mail ou bloquear um dispositivo remotamente


## <a name="before-you-begin"></a>Antes de começar

- Para configurar as ações de não conformidade, tem de ter pelo menos uma política de conformidade de dispositivos. Para criar uma política de conformidade de dispositivos, veja as seguintes plataformas:

  - [Android](compliance-policy-create-android.md)
  - [Perfis de trabalho do Android](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows](compliance-policy-create-windows.md)

- Ao utilizar as políticas de conformidade do dispositivo para bloquear dispositivos a partir de recursos corporativos, o Azure AD Conditional Access deve ser configurado. Consulte o [Acesso Condicional no Diretório Ativo Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) ou [formas comuns](conditional-access-intune-common-ways-use.md) de utilizar o Acesso Condicional com Intune para obter orientação.

## <a name="create-a-notification-message-template"></a>Criar um modelo de mensagem de notificação

Para enviar um e-mail aos seus utilizadores, crie um modelo de mensagem de notificação. Quando um dispositivo não estiver em conformidade, os detalhes que introduzir no modelo são apresentados no e-mail enviado aos utilizadores.

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Políticas de **conformidade** > **Notificações** > **Criar notificação**.
3. Em princípio, especifique as *seguintes*informações:

   - **Nome**
   - **Assunto**
   - **Mensagem**

4. Também no *Basics,* configure as seguintes opções para a notificação, quais todas as predefinições para *Ativado:*

   - **Cabeçalho do e-mail – incluir o logótipo da empresa**
   - **Rodapé do e-mail – incluir o nome da empresa**
   - **Rodapé do e-mail – incluir informações de contacto**

   O logótipo que envia como parte da marca Portal da Empresa é usado para modelos de e-mail. Para obter mais informações sobre a imagem corporativa do Portal da Empresa, veja [Personalização da imagem corporativa da empresa](../apps/company-portal-app.md#company-identity-branding-customization).

   ![Exemplo de uma mensagem de notificação de conformidade no Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Selecione **Next** para continuar.

5. Em **Review + criar,** reveja as suas configurações para garantir que o modelo de mensagem de notificação está pronto a ser utilizado. Selecione **Criar** para completar a criação da notificação.

> [!NOTE]
> Também pode selecionar um modelo de notificação existente que criou anteriormente e **editar** as suas informações para atualizar o modelo.

## <a name="add-actions-for-noncompliance"></a>Adicionar ações de não conformidade

Quando cria uma política de conformidade do dispositivo, o Intune cria automaticamente uma ação de não conformidade. Se um dispositivo não estiver a cumprir a sua política de conformidade, esta ação marca o dispositivo como não conforme. Pode personalizar o intervalo de tempo durante o qual o dispositivo está marcado como não conforme. Esta ação não pode ser removida.

Além da ação padrão para marcar dispositivos como não conformes, pode adicionar ações opcionais quando criar uma política de conformidade ou atualizar uma política existente.

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **Dispositivos** > Políticas de **conformidade** > **Políticas,** selecione uma das suas políticas e, em seguida, selecione **Propriedades**.

   Ainda não tem uma política? Crie uma política para [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) ou para outra plataforma.

   > [!NOTE]
   > Os dispositivos JAMF e dispositivos visados com grupos de dispositivos não conseguem receber ações de conformidade neste momento.

3. Selecione **Ações para não conformidade** > **Adicionar**.

4. Selecione a sua **Ação**:

   - **Enviar um email para os utilizadores finais**: quando o dispositivo não está em conformidade, opte por enviar um e-mail ao utilizador. Além disso:
     - Selecione o **Modelo de mensagem** que criou anteriormente
     - Introduza **Destinatários adicionais** ao selecionar grupos

   - **Bloquear remotamente o dispositivo em não conformidade**: quando o dispositivo não estiver em conformidade, bloqueie-o. Esta ação obriga o utilizador a introduzir um PIN ou uma senha para desbloquear o dispositivo.

5. Configurar um **Horário**: Insira o número de dias (0 a 365) após o incumprimento para desencadear a ação nos dispositivos dos utilizadores. Após este período de carência, pode impor uma política de [acesso condicional.](conditional-access-intune-common-ways-use.md) Se introduzir o número de **dias 0** (zero) e ntão o acesso condicional entra em vigor **imediatamente**. Por exemplo, se um dispositivo não for conforme, utilize o acesso condicional para bloquear o acesso a e-mail, SharePoint e outros recursos da organização imediatamente.

   Quando cria uma política de conformidade, a ação não conforme do **dispositivo Mark** é automaticamente criada e configura-se automaticamente para **0** dias (imediatamente). Com esta ação, quando o dispositivo faz o check-in, o dispositivo é avaliado como não conforme imediatamente. Se também utilizar acesso condicional, o acesso condicional começa imediatamente. Se pretender permitir um período de carência, altere a **Agenda** da ação não conforme do **dispositivo Mark.**

   Na sua política de conformidade, por exemplo, também pretende notificar o utilizador. Pode adicionar o **e-mail enviar para terminar** a ação do utilizador. Neste enviar ação **por e-mail,** você definir o **Horário** para 2 dias. Se o dispositivo ou utilizador final ainda for avaliado como incompatível no dia 2, então o seu e-mail é enviado no dia 2. Se quiser enviar novamente um e-mail ao utilizador no dia 5 de incumprimento, adicione outra ação e marque o **Horário** para 5 dias.

   Para obter mais informações sobre o cumprimento e as ações incorporadas, consulte a visão geral da [conformidade.](device-compliance-get-started.md)

6. Quando terminar, selecione **Adicionar** > **OK** para guardar as alterações.

## <a name="next-steps"></a>Próximos passos

[Monitorizar as políticas](compliance-policy-monitor.md).
