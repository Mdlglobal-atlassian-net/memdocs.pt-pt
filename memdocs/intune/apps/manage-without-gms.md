---
title: Como utilizar o Intune em ambientes sem o Google Mobile Services
titleSuffix: Microsoft Intune
description: Saiba como usar o Intune em ambientes sem o Google Mobile Services.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6b9f5a560b0f44b8ff256034b51cb9057faf0ec2
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80576834"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Como utilizar o Intune em ambientes sem o Google Mobile Services

O Microsoft Intune utiliza o Google Mobile Services (GMS) para comunicar com o portal da empresa Microsoft Intune na gestão de dispositivos Android. Em alguns casos, os dispositivos podem, temporariamente ou permanentemente, não ter acesso ao GMS. Por exemplo, um dispositivo pode ser enviado sem GMS, ou o dispositivo pode estar ligado a uma rede fechada onde o GMS não esteja disponível. Este documento resume as diferenças e limitações que poderá observar ao instalar e utilizar o Intune para gerir dispositivos Android sem GMS.

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>Instale a aplicação Intune Company Portal sem acesso à Google Play Store 

### <a name="for-users-outside-of-mainland-china"></a>Para utilizadores fora da China continental 

Se o Google Play não estiver disponível, os dispositivos Android podem descarregar o Portal da [Empresa Intune](../user-help/install-the-company-portal-app-android.md) microsoft para Android e carregar lateralmente a aplicação. Quando instalada desta maneira, a aplicação não recebe atualizações nem correções automaticamente. Deve ter a certeza de atualizar e remendar a aplicação manualmente. 

### <a name="for-users-in-mainland-china"></a>Para utilizadores na China continental 

Como a Google Play Store não está atualmente disponível na China continental, os dispositivos Android devem obter aplicações de marketplaces de aplicações chinesas. Para mais informações, consulte [Instalar a aplicação Portal da Empresa na China continental.](../user-help/install-company-portal-android-china.md)

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>Limitações da gestão do administrador do dispositivo Intune quando o GMS está indisponível 

### <a name="unavailable-intune-features"></a>Funcionalidades Indisponíveis Intune

Algumas funcionalidades intune dependem de componentes de GMS, como a loja Google Play ou os serviços Google Play. Uma vez que estes componentes não estão disponíveis em ambientes sem GMS, as seguintes funcionalidades na consola de administrador Intune podem não estar disponíveis.  

| Cenário  | Funcionalidades  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Políticas de conformidade do dispositivo  | Ao criar ou editar políticas de conformidade para administrador de dispositivos Android, todas as opções listadas no **Google Play Protect** não estão disponíveis.  |
| Políticas de proteção de aplicações (lançamento condicional)  | **O atestado** do dispositivo SafetyNet e a necessidade de **uma verificação** de ameaças nas condições do dispositivo de aplicações não podem ser utilizados para o lançamento condicional.  |
| Aplicações do cliente  | Aplicações do tipo **Android** não estão disponíveis. Utilize **a app Line-of-business** para implementar e gerir aplicações.  |
| Defesa Contra Ameaças para Dispositivos Móveis  | Trabalhe com o seu fornecedor de MTD para perceber se a sua solução está integrada com a Intune, se está disponível na região de interesse, e se depende de GMS.  |

### <a name="some-tasks-may-be-delayed"></a>Algumas tarefas podem ser adiadas 

Nos ambientes onde o GMS está disponível, intune baseia-se em notificações push para acelerar as tarefas para terminar. Por exemplo, se tentar limpar remotamente o dispositivo, as notificações geralmente chegam ao dispositivo em segundos. Em condições em que o GMS não esteja disponível, as notificações push também podem não estar disponíveis. Por isso, o Intune deve esperar pelo tempo de check-in do próximo dispositivo para completar as tarefas.  

Os dispositivos Android matriculados reportam-se ao Intune a cada 8 horas. Por exemplo, se um dispositivo reportar a Intune às 13:00 e as tarefas remotas forem emitidas às 13:05, intune entrará em contato com o dispositivo às 21:00 para completar as tarefas. 

As seguintes tarefas podem requerer até 8 horas para terminar: 

**Consola intonizada:**
- Eliminação completa
- Eliminação seletiva
- Implementações de aplicações novas ou atualizadas
- Bloqueio remoto
- Repor código de acesso

**Aplicativo Intune Company Portal para Android**:
- Remoção remota do dispositivo
- Reset do dispositivo
- Instalação de aplicações disponíveis de linha de negócio

**Intune Company Portal website:**
- Remoção do dispositivo (local e remoto)
- Reset do dispositivo
- Repor código de acesso do dispositivo

Se o dispositivo se matriculou recentemente, o cumprimento, o incumprimento e o check-in de configuração são mais frequentes. Para obter mais informações sobre check-ins de dispositivos, consulte [questões comuns, problemas e resoluções com políticas e perfis de dispositivos no Microsoft Intune](../configuration/device-profile-troubleshoot.md). 

## <a name="next-steps"></a>Próximos passos

- [Atribuir aplicativos a grupos com o Microsoft Intune](../apps/apps-deploy.md)
