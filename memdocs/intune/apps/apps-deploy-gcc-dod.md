---
title: Aplicativos para ambientes GCC High e DoD
titleSuffix: Microsoft Intune
description: Saiba mais sobre aplicações que envolvam ambientes GCC High e DoD usando o Microsoft Intune.
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
ms.assetid: 29329f86-1aa5-434f-9925-8dc28bf35348
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d37bf060f11be9e295a9ef2743fa0ba33844df7
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79325889"
---
# <a name="deploying-apps-using-intune-on-the-gcc-high-and-dod-environments"></a>Implementação de aplicações que utilizam o Intune nos Ambientes Altos e DoD da GCC 

O Microsoft Intune pode ser usado por administradores de inquilinos para distribuir aplicações à sua força de trabalho. A mão de obra é a funcionária da empresa, os utilizadores das aplicações. Existem muitos tipos de aplicações que podem ser implementadas a partir de Intune em ambientes GCC High ou DoD. Se um administrador precisar de carregar e distribuir uma aplicação do Windows destinada a um público GCC High ou DoD que seja feita sob medida, criada por fornecedores de terceiros, ou como uma aplicação offline descarregada da [Microsoft Store for Business,](https://businessstore.microsoft.com/store)o administrador pode optar por distribuí-la como uma [aplicação de linha de negócios.](apps-add.md#app-types-in-microsoft-intune)  

> [!NOTE]
> Para ambientes comerciais, um administrador de inquilino pode sincronizar a sua Loja de Negócios com Intune, no entanto, para ambientes GCC High e DoD, este serviço não está disponível. Os administradores nesta situação devem implementar uma aplicação através do upload diretamente para Intune.  

## <a name="add-line-of-business-apps-using-intune"></a>Adicione aplicativos de linha de negócio usando Intune 

Para adicionar uma aplicação de linha de negócio destinada a um ambiente GCC High ou DoD utilizando o Intune, pode seguir as instruções da [aplicação DoL.](lob-apps-windows.md) Pode optar por implementar primeiro o Portal da Empresa a partir da Microsoft Store for Business. Se optar por utilizar o Portal da Empresa, pode instalar e implementar manualmente o Portal da Empresa. Para mais informações, consulte [como configurar a aplicação Microsoft Intune Company Portal](company-portal-app.md). 

## <a name="distribute-offline-apps-from-the-store-for-business-using-intune"></a>Distribua aplicativos offline da Loja para Negócios usando Intune  

Se precisar de [descarregar uma aplicação licenciada offline](https://docs.microsoft.com/microsoft-store/distribute-offline-apps#download-an-offline-licensed-app) a partir da Microsoft Store for Business, siga estes passos para descarregar a aplicação: 

1. Inscreva-se na [Loja para Negócios.](https://businessstore.microsoft.com/)
2. Selecione **Gerir** > **definições**.
3. Under **Shopping Experience**, set Show offline **apps** to **On**.

Ao comprar aplicativos, se estiver disponível uma versão offline, pode optar por alterar o tipo de licença para offline. Depois de obter a aplicação, pode então geri-la selecionando Produtos **de Gestão** > **& Serviços** na [Loja para Negócios](https://businessstore.microsoft.com/). Além disso, pode descarregar a app e as suas dependências. Em seguida, pode implementar esta aplicação descarregada (e as suas dependências) para utilizadores que utilizem O Intune.  

## <a name="syncing-intune-to-the-store-for-business"></a>Sincronização Intune à Loja para Negócios 

Num ambiente comercial (não governamental), um administrador pode sincronizar intune com a Microsoft Store for Business. Esta não é uma característica disponível nos ambientes governamentais. Para mais detalhes sobre as diferenças entre Intune em ambientes comerciais e Intune para ambientes governamentais, consulte [Enterprise Mobility + Security for US Government Service Description](https://docs.microsoft.com/enterprise-mobility-security/solutions/ems-govt-service-description).  

Para sincronizar instonante na sua conta Store for Business, consulte [como gerir as aplicações que adquiriu na Microsoft Store para Negócios com](windows-store-for-business.md)o Microsoft Intune .  

## <a name="compliance"></a>Conformidade 

Reveja as declarações de privacidade e conformidade das aplicações e compare-as com os requisitos de conformidade, segurança e privacidade da sua organização ao avaliar o uso adequado destes serviços.   

## <a name="next-steps"></a>Passos seguintes

Para saber mais sobre a implementação e atribuição de apps, consulte [as aplicações De atribuição para grupos com](apps-deploy.md)o Microsoft Intune .

 
