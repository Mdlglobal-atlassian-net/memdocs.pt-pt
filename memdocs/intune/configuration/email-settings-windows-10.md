---
title: Definições de e-mail para dispositivos com o Windows 10 no Microsoft Intune – Azure | Microsoft Docs
description: Crie um perfil de e-mail de configuração de dispositivos que utiliza os servidores Exchange e obtém atributos do Azure Active Directory. Também pode ativar o SSL e sincronizar e-mails e agendas em dispositivos com o Windows 10 através do Microsoft Intune.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0cd3505d0a0067adfe9082d7aa3882f3421a2183
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429607"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>Definições de perfil de e-mail para dispositivos que executam o Windows 10 no Microsoft Intune

Utilize as definições de perfil de e-mail para configurar a aplicação Mail nos seus dispositivos que executam o Windows 10 e mais recentes.

## <a name="before-you-begin"></a>Antes de começar

[Criar o perfil.](email-settings-configure.md)

## <a name="email-settings"></a>Definições de e-mail

- **Servidor de e-mail**: introduza o nome de anfitrião do seu servidor Exchange. Por exemplo, introduza `outlook.office365.com`.
- **Nome da conta**: introduza o nome a apresentar da conta de e-mail. Este nome será apresentado nos dispositivos dos utilizadores.
- **Atributo de nome de utilizador do AAD**: este nome é o atributo que o Intune obtém do Azure Active Directory (AAD). O Intune gera de forma dinâmica o nome de utilizador utilizado por este perfil. As opções são:
  - **Nome principal do utilizador**: Obtém o nome, como `user1` ou `user1@contoso.com` .
  - **Endereço Principal SMTP**: Obtém o nome no formato de endereço de e-mail, como `user1@contoso.com` .
  - **Nome da Conta SAM**: precisa do domínio, como `domain\user1`. Introduza também:  
    - **Fonte**de nome do utilizador : Selecione **AAD** (Diretório Ativo Azure) ou **Personalizado**.

      Ao obter os atributos da **AAD,** também introduza:
      - **Atributo de nome de domínio do utilizador a partir de AAD**: Opte por obter o **nome de domínio completo** ou o atributo de **nome NetBIOS** do utilizador.

      Ao utilizar atributos **personalizados,** introduza também:
      - **Nome de domínio personalizado a utilizar**: Introduza um valor que Intune utiliza para o nome de domínio, como ou `contoso.com` `contoso` .

- **Atributo de endereço de e-mail da AAD**: Intune recebe este atributo do Azure Ative Directory (AAD). Escolha como é gerado o endereço de e-mail para o utilizador. As opções são:
  - **Nome principal**do utilizador : Utiliza o nome principal completo como endereço de e-mail, como `user1@contoso.com` ou `user1` .
  - **Endereço Principal SMTP**: Utiliza o endereço SMTP primário para iniciar sessão no Exchange, tais como `user1@contoso.com` .

### <a name="security"></a>Segurança

- **SSL**: **Ativar** resulta na utilização da comunicação SSL (Secure Sockets Layer) ao enviar e-mails, ao receber e-mails e ao comunicar com o servidor Exchange. **Desativação** não requer SSL.

### <a name="synchronization"></a>Sincronização

- **Quantidade de e-mail para sincronizar**: Selecione o número de dias de e-mail que pretende sincronizar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. **Selecione Ilimitado** para sincronizar todos os e-mails disponíveis.
- **Agenda de sincronização**: selecione o agendamento através do qual os dispositivos sincronizam os dados do servidor Exchange. Também pode selecionar À medida que **as Mensagens chegam,** que sincroniza os dados assim que chegam. Ou, selecione **Manual** para que o utilizador do dispositivo inicie a sincronização.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

### <a name="content-sync"></a>Sincronização de conteúdos

- Tipo de **conteúdo a sincronizar:** Selecione os tipos de conteúdo que pretende sincronizar para os dispositivos. As opções são:
  - **Contactos**: **Sincroniza** os contactos. **Desligado** não sincroniza automaticamente os contactos. Os utilizadores sincronizam manualmente.
  - **Calendário**: **Sincroniza** o calendário. **Desligado** não sincroniza automaticamente os contactos. Os utilizadores sincronizam manualmente.
  - **Tarefas**: **Sincronizar** as tarefas. **Desligado** não sincroniza automaticamente as tarefas. Os utilizadores sincronizam manualmente.

## <a name="next-steps"></a>Próximos passos

Também pode configurar as definições de e-mail no [Android,](email-settings-android.md) [Android Enterprise](email-settings-android-enterprise.md)e [iOS/iPadOS.](email-settings-ios.md) 

[Saiba mais sobre as definições de e-mail em Intune](email-settings-configure.md).

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).
