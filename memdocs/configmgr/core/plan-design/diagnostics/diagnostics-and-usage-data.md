---
title: Dados de diagnóstico e de utilização
titleSuffix: Configuration Manager
description: Conheça os dados de diagnóstico e utilização que o Gestor de Configuração recolhe sobre si mesmo.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904404"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Diagnósticos e dados de utilização para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração recolhe dados de diagnóstico e utilização sobre si mesmo, que é usado pela Microsoft para melhorar a experiência de instalação, qualidade e segurança de futuras versões.  

Cada hierarquia do Gestor de Configuração permite diagnósticos e dados de utilização. É composto por consultas do SQL Server que funcionam semanalmente em cada site primário e no site da administração central (CAS). Quando a hierarquia usa um CAS, os sites primários infantis replicam os seus dados para esse CAS. No site de alto nível da sua hierarquia, o ponto de [ligação](../../servers/deploy/configure/about-the-service-connection-point.md) de serviço submete esta informação quando verifica as atualizações. Se o ponto de ligação ao serviço estiver no modo offline, transfira as informações utilizando a ferramenta de [ligação](../../servers/manage/use-the-service-connection-tool.md)de serviço .

> [!NOTE]  
> O Gestor de Configuração recolhe dados apenas a partir da base de dados do servidor SQL do site, e não recolhe dados diretamente de clientes ou servidores do site.  

Para mais informações, consulte a [declaração de privacidade](https://privacy.microsoft.com/privacystatement)da Microsoft .  

> [!div class="nextstepaction"]
> [Como a Microsoft utiliza dados de diagnóstico e de utilização](how-diagnostics-and-usage-data-is-used.md)
