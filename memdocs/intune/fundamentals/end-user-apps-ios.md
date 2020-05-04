---
title: Como os seus utilizadores iOS/iPadOS obtêm as suas aplicações
description: Métodos para disponibilizar aplicações iOS/iPadOS aos utilizadores finais
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79326865"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>Como os seus utilizadores iOS/iPadOS obtêm as suas aplicações

Utilize estas informações para saber como e onde é que os seus utilizadores finais podem obter as aplicações que distribuir através do Microsoft Intune.

**Aplicações obrigatórias** – aplicações exigidas pelo administrador e que são instaladas nos dispositivos com envolvimento mínimo do utilizador, dependendo da plataforma.

**Aplicações disponíveis** – aplicações fornecidas na lista de aplicações do Portal da Empresa e que os utilizadores podem optar por instalar.

**Aplicações geridas** – aplicações que podem ser geridas através de políticas e foram "encapsuladas" pelo Intune ou incorporadas no Intune App Software Development Kit (SDK). Estas aplicações podem ser geridas pelo Intune e podem ser-lhes aplicadas políticas de proteção de aplicações.

**Aplicações não geridas**--Apps que os utilizadores podem descarregar a partir da App Store iOS/iPadOS que não estão integradas com a aplicação Intune SDK. Intune não tem qualquer controlo sobre a distribuição, gestão ou limpeza seletiva destas aplicações.  

Os utilizadores inscritos obtêm as respetivas aplicações ao tocar nos seguintes mosaicos no ecrã Aplicações da aplicação Portal da Empresa:

- **Todas as Aplicações** direciona para uma lista de todas as aplicações no separador TODOS do [Site do Portal da Empresa](https://portal.manage.microsoft.com).

- **Aplicações Em Destaque** direciona os utilizadores para o separador EM DESTAQUE do site do Portal da Empresa.

- **Categorias** direciona para o separador CATEGORIAS do site do Portal da Empresa.

![Ecrã das aplicações do Portal da Empresa para iOS](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

Para obter mais informações sobre como adicionar aplicações, veja [Como adicionar uma aplicação ao Microsoft Intune](../apps/apps-add.md).

## <a name="app-management-takeover"></a>Aquisição de gestão de aplicações
Se uma aplicação já estiver instalada no dispositivo de um utilizador final, o dispositivo iOS/iPadOS mostra um alerta para permitir a gestão da app pela sua organização. O utilizador final deve permitir que a organização assuma a gestão da app antes que as configurações da aplicação possam ser aplicadas a um dispositivo gerido. Se o utilizador cancelar o alerta, o alerta aparecerá periodicamente enquanto o dispositivo for gerido e a aplicação for atribuída.  


![Imagem do alerta de Mudança de Gestão de Aplicações, mostrando opções de Cancelamento e Gestão.](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>Consulte também  

[Como os utilizadores de dispositivos Android obtêm as aplicações](end-user-apps-android.md)

[Como os utilizadores de dispositivos Windows obtêm as aplicações](end-user-apps-windows.md)
