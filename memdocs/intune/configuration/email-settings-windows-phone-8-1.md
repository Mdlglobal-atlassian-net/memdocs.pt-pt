---
title: Definições de e-mail do Microsoft Intune para o Windows Phone 8.1
titleSuffix: ''
description: Saiba mais sobre as definições do Intune que pode utilizar para configurar ligações de e-mail em dispositivos com o Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 369e856b26ecbf8a7d6d7f8c0a87a9bfdf69e318
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086914"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>Definições de perfis de e-mail no Microsoft Intune para dispositivos com o Windows Phone 8.1

Este artigo mostra-lhe as definições de perfis de e-mail que pode configurar para os seus dispositivos com Windows Phone 8.1.

>[!IMPORTANT]
>Os perfis de e-mail do Windows Phone 8.1 também são aplicados aos dispositivos do Windows 10.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [e-mail do Windows Phone 8.1](email-settings-configure.md).

## <a name="email-settings"></a>Definições de e-mail

- **Servidor de e-mail**: introduza o nome de anfitrião do seu servidor Exchange. Por exemplo, introduza `outlook.office365.com`.
- **Nome da conta**: introduza o nome a apresentar da conta de e-mail. Este nome será apresentado nos dispositivos dos utilizadores.
- **Atributo de nome de utilizador do AAD**: este nome é o atributo que o Intune obtém do Azure Active Directory (AAD). O Intune gera de forma dinâmica o nome de utilizador utilizado por este perfil. As opções são:
  - **Nome principal do utilizador**: Obtém o nome, como `user1` ou `user1@contoso.com`.
  - **Endereço Principal SMTP**: Obtém o nome em formato de endereço de e-mail, como `user1@contoso.com`.
  - **Nome da Conta SAM**: precisa do domínio, como `domain\user1`. Introduza também:
    - **Fonte**de nome do domínio do utilizador : As suas opções:
      - **AAD** (Diretório Ativo Azure): Introduza o nome de **domínio do utilizador a partir de AAD**. Opte por obter o **nome de domínio Completo** ou o atributo de nome **NetBIOS** do utilizador.
      - **Personalizado**: Introduza o nome de **domínio personalizado para utilizar**. Introduza um valor que Intune utiliza para o nome de domínio, como `contoso.com` ou `contoso`.

- **Atributo de endereço de e-mail da AAD**: Intune recebe este atributo do Azure Ative Directory (AAD). Escolha como é gerado o endereço de e-mail para o utilizador. As opções são:
  - **Nome principal**do utilizador : Utiliza o nome principal completo como endereço de e-mail, como `user1@contoso.com` ou `user1`.
  - **Endereço Principal SMTP**: Utiliza o endereço SMTP primário para iniciar sessão no Exchange, como `user1@contoso.com`.

## <a name="security-settings"></a>Definições de segurança

- **SSL**: **Ativar** resulta na utilização da comunicação SSL (Secure Sockets Layer) ao enviar e-mails, ao receber e-mails e ao comunicar com o servidor Exchange. **Desativação** não requer SSL.

## <a name="synchronization-settings"></a>Definições de sincronização

- **Quantidade de e-mails a sincronizar**: selecione o número de dias de e-mails que pretende sincronizar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. **Selecione Ilimitado** para sincronizar todos os e-mails disponíveis.
- **Agenda de sincronização**: selecione o agendamento através do qual os dispositivos sincronizam os dados do servidor Exchange. Também pode selecionar À medida que **as Mensagens chegam,** que sincroniza os dados assim que chegam. Ou, selecione **Manual** para que o utilizador do dispositivo inicie a sincronização.

## <a name="content-sync-settings"></a>Definições de sincronização de conteúdo

- **Tipo de conteúdo a sincronizar:** Selecione os tipos de conteúdo que pretende sincronizar para dispositivos:
  - **Contactos**: **Sincroniza** os contactos. **Desligado** não sincroniza automaticamente os contactos. Os utilizadores sincronizam manualmente.
  - **Calendário**: **Sincroniza** o calendário. **Desligado** não sincroniza automaticamente os contactos. Os utilizadores sincronizam manualmente.
  - **Tarefas**: **Sincronizar** as tarefas. **Desligado** não sincroniza automaticamente as tarefas. Os utilizadores sincronizam manualmente.

## <a name="next-steps"></a>Próximos passos

Também pode configurar as definições de e-mail no [Android,](email-settings-android.md) [Android Enterprise,](email-settings-android-enterprise.md) [iOS/iPadOS](email-settings-ios.md)e [Windows 10](email-settings-windows-10.md).

[Configure as definições de e-mail em Intune](email-settings-configure.md).
