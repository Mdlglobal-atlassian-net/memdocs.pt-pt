---
title: Bloquear aplicações sem autenticação moderna no Intune
titleSuffix: Microsoft Intune
description: Saiba mais sobre aplicações e autenticação moderna (ADAL) utilizando o Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f529a80403d27cf9d12c03c6090670095bf569fa
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329969"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Bloquear aplicações que não utilizam a autenticação moderna (ADAL)

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

O Acesso Condicional baseado em aplicativos com políticas de proteção de aplicações depende de aplicações usando [a autenticação moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a), que é uma implementação do OAuth2. A maioria das aplicações atuais do Office de ambiente de trabalho e móveis utiliza a autenticação moderna. No entanto, existem aplicações de terceiros e aplicações antigas do Office que utilizam outros métodos de autenticação, como a autenticação básica e a autenticação baseada em formulários.

## <a name="block-access-to-apps"></a>Bloquear o acesso a aplicações

Para bloquear o acesso às aplicações que não utilizam a autenticação moderna, utilize as políticas de proteção de aplicações do Intune para implementar o acesso condicional. Para mais informações, consulte o [Acesso Condicional baseado em Aplicativos com Intune](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Informações adicionais

Para obter mais informações sobre o acesso condicional do Microsoft Azure AD, veja os seguintes tópicos:
- [O que é o Acesso Condicional no Diretório Ativo Azure?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Como funciona o Acesso Condicional baseado em aplicativos](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Configurar o SharePoint Online e trocar online para acesso condicional ao diretório ativo azure](https://docs.microsoft.com/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Passos seguintes

- [Acesso Condicional baseado em aplicativos com Intune](app-based-conditional-access-intune.md)
