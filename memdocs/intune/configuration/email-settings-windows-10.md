---
title: Definições de e-mail para dispositivos com o Windows 10 no Microsoft Intune – Azure | Microsoft Docs
description: Crie um perfil de e-mail de configuração de dispositivos que utiliza os servidores Exchange e obtém atributos do Azure Active Directory. Também pode ativar o SSL e sincronizar e-mails e agendas em dispositivos com o Windows 10 através do Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa861a266f89b82fdd2d6e73d30fdc2e58da33b4
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086916"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>Definições de perfil de e-mail para dispositivos que executam o Windows 10 no Microsoft Intune

Utilize as definições de perfil de e-mail para configurar a aplicação Mail nos seus dispositivos que executam o Windows 10 e mais recentes.

## <a name="before-you-begin"></a>Antes de começar

[Criar o perfil.](email-settings-configure.md)

## <a name="email-settings"></a>Definições de e-mail

- **Servidor de e-mail**: introduza o nome de anfitrião do seu servidor Exchange. Por exemplo, introduza `outlook.office365.com`.
- **Nome da conta**: introduza o nome a apresentar da conta de e-mail. Este nome será apresentado nos dispositivos dos utilizadores.
- **Atributo de nome de utilizador do AAD**: este nome é o atributo que o Intune obtém do Azure Active Directory (AAD). O Intune gera de forma dinâmica o nome de utilizador utilizado por este perfil. As opções são:
  - **Nome principal do utilizador**: `user1` Obtém o nome, como ou `user1@contoso.com`.
  - **Endereço Principal SMTP**: Obtém o nome `user1@contoso.com`no formato de endereço de e-mail, como .
  - **Nome da Conta SAM**: precisa do domínio, como `domain\user1`. Introduza também:  
    - **Origem de nome de domínio do utilizador**: selecione **AAD** (Azure Active Directory) ou **Personalizado**.

      Ao optar por obter os atributos do **AAD**, introduza:
      - **Atributo de nome de domínio do utilizador a partir de AAD**: Opte por obter o **nome de domínio completo** ou o atributo de **nome NetBIOS** do utilizador.

      Ao optar por utilizar atributos **Personalizados**, introduza:
      - **Nome de domínio personalizado a utilizar**: Introduza um valor `contoso.com` `contoso`que Intune utiliza para o nome de domínio, como ou .

- **Atributo de endereço de e-mail da AAD**: Intune recebe este atributo do Azure Ative Directory (AAD). Escolha como é gerado o endereço de e-mail para o utilizador. As opções são:
  - **Nome principal**do utilizador : Utiliza o nome `user1@contoso.com` principal `user1`completo como endereço de e-mail, como ou .
  - **Endereço Principal SMTP**: Utiliza o endereço SMTP primário para `user1@contoso.com`iniciar sessão no Exchange, tais como .

### <a name="security"></a>Segurança

- **SSL**: **Ativar** resulta na utilização da comunicação SSL (Secure Sockets Layer) ao enviar e-mails, ao receber e-mails e ao comunicar com o servidor Exchange. **Desativação** não requer SSL.

### <a name="synchronization"></a>Sincronização

- **Quantidade de e-mails a sincronizar**: selecione o número de dias de e-mails que pretende sincronizar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. **Selecione Ilimitado** para sincronizar todos os e-mails disponíveis.
- **Agenda de sincronização**: selecione o agendamento através do qual os dispositivos sincronizam os dados do servidor Exchange. Também pode selecionar À medida que **as Mensagens chegam,** que sincroniza os dados assim que chegam. Ou, selecione **Manual** para que o utilizador do dispositivo inicie a sincronização.

### <a name="content-sync"></a>Sincronização de conteúdos

- **Tipo de conteúdo a sincronizar:** Selecione os tipos de conteúdo que pretende sincronizar para dispositivos:
  - **Contactos**: **Sincroniza** os contactos. **Desligado** não sincroniza automaticamente os contactos. Os utilizadores sincronizam manualmente.
  - **Calendário**: **Sincroniza** o calendário. **Desligado** não sincroniza automaticamente os contactos. Os utilizadores sincronizam manualmente.
  - **Tarefas**: **Sincronizar** as tarefas. **Desligado** não sincroniza automaticamente as tarefas. Os utilizadores sincronizam manualmente.

## <a name="next-steps"></a>Passos seguintes

Também pode configurar as definições de e-mail no [Android,](email-settings-android.md) [Android Enterprise](email-settings-android-enterprise.md)e [iOS/iPadOS.](email-settings-ios.md) 

[Configure as definições de e-mail em Intune](email-settings-configure.md).
