---
title: Exceções da política de transferência de dados para aplicações
titleSuffix: Microsoft Intune
description: Crie exceções à política de proteção de dados intune App (APP).
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f9015e3a-c22c-42eb-90e6-ba48dee3a41d
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af0e541a21a07c60cde84affca5bfc5a16989d65
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79326269"
---
# <a name="how-to-create-exceptions-to-the-intune-app-protection-policy-app-data-transfer-policy"></a>Como criar exceções à política de proteção de aplicações intune (APP) política de transferência de dados

Como administrador, pode criar exceções à política de proteção de aplicações intune (APP). Uma exceção permite-lhe escolher especificamente que aplicações não geridas podem transferir dados de e para aplicações geridas. O seu TI deve confiar nas aplicações não geridas que inclui na lista de exceção. 

>[!WARNING] 
> Será responsável por fazer alterações à política de exceção de transferência de dados. As adições a esta política permitem que as aplicações não geridas (aplicações que não são geridas pelo Intune) acedam a dados protegidos por aplicações geridas. Este acesso a dados protegidos poderá resultar em falhas de segurança dos dados. Adicione exceções de transferência de dados apenas para as aplicações que a sua organização tem de utilizar, mas que não suportam as Políticas de Proteção de Aplicações do Intune. Além disso, adicione exceções apenas para aplicações que considera não representarem riscos de fuga de dados.

Dentro de uma Política de Proteção de Aplicações Intune, a definição **permitir que a app transfira dados para outras aplicações** **geridas** pela Policy significa que a aplicação pode transferir dados apenas para aplicações geridas pela Intune. Se necessitar de permitir que os dados sejam transferidos para aplicações específicas que não suportem a Intune APP, pode criar exceções a esta política utilizando **aplicações Select para isentar**. As isenções permitem que aplicações geridas pela Intune invoquem aplicações não geridas com base no protocolo URL (iOS/iPadOS) ou no nome do pacote (Android). Por predefinição, o Intune adiciona aplicações nativas fundamentais à lista de exceções. 

> [!NOTE]
> Modificar ou adicionar exceções de política de transferência de dados não afeta as outras Políticas de Proteção de Aplicações, tal como restrições de ações de cortar, copiar e colar. 

## <a name="ios-data-transfer-exceptions"></a>Exceções de transferência de dados em dispositivos iOS
Para uma política direcionada para iOS/iPadOS, pode configurar exceções de transferência de dados através do protocolo URL. Para adicionar uma exceção, verifique a documentação fornecida pelo programador da aplicação para encontrar informações acerca dos protocolos de URL suportados. Para obter mais informações sobre as exceções à transferência de dados iOS/iPadOS, consulte as definições da política de proteção de [aplicações iOS/iPadOS - Isenções](app-protection-policy-settings-ios.md#data-transfer-exemptions)de transferência de dados .

> [!NOTE]
> A Microsoft não possui um método para localizar manualmente o protocolo URL que permite criar exceções para aplicações de terceiros. 

## <a name="android-data-transfer-exceptions"></a>Exceções de transferência de dados em dispositivos Android
Para uma política destinada a dispositivos Android, pode configurar as exceções de transferência de dados pelo nome do pacote de aplicação. Pode procurar a aplicação para a qual pretende adicionar uma exceção na página da loja **Google Play**, para encontrar o nome do pacote de aplicação. Para obter mais informações sobre as exceções à transferência de dados do Android, consulte as definições de política de proteção de [aplicações Android - isenções de transferência de dados.](app-protection-policy-settings-android.md#data-transfer-exemptions)


>[!TIP]
> Pode localizar o ID do pacote de uma aplicação ao navegar para a aplicação na Google Play Store. O ID do pacote está contido no URL da página da aplicação. Por exemplo, o ID do pacote da aplicação Microsoft Word é **com.microsoft.office.word**.

### <a name="example"></a>Exemplo
Adicionar o pacote **WebEx** como uma exceção à politica de transferência de dados da MAM permite que as ligações WebEx numa mensagem de e-mail do Outlook gerido sejam abertas diretamente na aplicação WebEx. A transferência de dados é restrita noutras aplicações não geridas.

- exemplo iOS/iPadOS **Webex:** Para isentar a aplicação **Webex** de modo a que seja permitida a sua invocação por aplicações geridas pela Intune, deve adicionar uma exceção de transferência de dados para a seguinte cadeia:<code>wbx</code>
    
- exemplo do iOS/iPadOS **Maps:** Para isentar a aplicação nativa **do Maps** para que seja permitida a sua invocação por aplicações geridas pela Intune, deve adicionar uma exceção de transferência de dados para a seguinte cadeia:<code>maps</code>

- Exemplo do Android **Webex:** Para isentar a aplicação **Webex** para que seja permitida a sua invocação por aplicações geridas por Intune, deve adicionar uma exceção de transferência de dados para a seguinte cadeia:<code>com.cisco.webex.meetings</code>
    
- Exemplo do Android **SMS:** Para isentar a aplicação **SMS** nativa para que seja permitida a sua invocação por aplicações geridas pela Intune em diferentes aplicações de mensagens e dispositivos Android, deve adicionar exceções à transferência de dados para as seguintes cadeias: 
    <code>com.google.android.apps.messaging</code>
    
    <code>com.android.mms</code>
    
    <code>com.samsung.android.messaging</code>

## <a name="next-steps"></a>Passos seguintes

- [Criar e implementar políticas de proteção de aplicações](app-protection-policies.md)
- [Definições de política de proteção de aplicações iOS/iPadOS - Isenções de transferência de dados](app-protection-policy-settings-ios.md#data-transfer-exemptions)
- [Definições de políticas de proteção de aplicações Android – isenções de transferência de dados](app-protection-policy-settings-android.md#data-transfer-exemptions)
