---
title: Utilizar o Armazém de Dados do Intune
titleSuffix: Microsoft Intune
description: Utilize o Armazém de Dados do Intune para criar relatórios que forneçam informações sobre o ambiente móvel da sua empresa.
keywords: Armazém de Dados do Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 57019B11-DF9B-4D8A-95FE-254C75398DDE
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: dad1ecb2ed86158e510b0f554e3fd7e12e21a814
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331829"
---
# <a name="use-the-microsoft-intune-data-warehouse"></a>Utilizar o Data Warehouse do Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Utilize o Armazém de Dados do Intune para criar relatórios que forneçam informações sobre o ambiente móvel da sua empresa. Por exemplo, alguns dos relatórios incluem:
- Tendência de utilizadores a inscrever-se no Intune para poder otimizar as suas aquisições de licenças
- Discriminação de versões de SO e aplicações para poder rever o estado dos dispositivos móveis
- Tendências de conformidade de dispositivos e inscrições para poder implementar atualizações à política de forma simples

## <a name="data-warehouse-benefits"></a>Benefícios do Data Warehouse

O Armazém de Dados dá-lhe acesso a mais informações sobre o seu ambiente móvel do que o portal do Azure. Com o Armazém de Dados do Intune, pode aceder a:

- Dados históricos do Intune
- Dados atualizados diariamente
- Um modelo de dados com utilização do padrão OData

> [!Note]
> Se for uma gestão de dispositivos móveis cogerida (MDM) com o Microsoft Endpoint Configuration Manager e o Microsoft Intune, tem de recuperar os seus dados do 'Configuração Manager'. O Armazém de Dados do Intune contém apenas dados do Intune. Pode utilizar um dashboard Power BI do Gestor de Configuração para os seus relatórios personalizados. Para mais informações, consulte " Anunciando o modelo de[solução Power BI para Configuração Manager](https://powerbi.microsoft.com/blog/sccm-solution-template)" e "[Conteúdo de Power BI para A Dinâmica 365](https://docs.microsoft.com/dynamics365/unified-operations/dev-itpro/analytics/power-bi-home-page)."

> [!Important]  
> Agora, pode utilizar a versão v1.0 do Armazém de Dados do Intune, ao definir o parâmetro de consulta `api-version=v1.0`. As atualizações para coleções no Armazém de Dados são acumulativas por natureza e não interrompem cenários existentes.<br><br>
> Pode experimentar as nossas funcionalidades mais recentes do Armazém de Dados com a versão beta. Para utilizar a versão beta, o seu URL tem de conter o parâmetro de consulta `api-version=beta`. A versão beta oferece funcionalidades antes de estas estarem disponíveis globalmente como um serviço suportado. À medida que o Intune adiciona novas funcionalidades, a versão beta poderá alterar o contrato de dados e comportamento. Todos os códigos personalizados ou ferramentas de relatórios dependentes da versão beta poderão interromper as atualizações contínuas.

## <a name="next-steps"></a>Próximos passos

- Obtenha uma ligação e utilize o Power BI para obter informações. Para obter instruções, consulte [Connect to the Data Warehouse with Power BI (Ligar ao Armazém de Dados do Intune com o Power BI – em inglês)](reports-proc-get-a-link-powerbi.md).
- Com a sua ligação, crie um relatório personalizado com o Power BI. Para obter instruções, veja [Create a report from the OData feed with Power BI (Criar um relatório a partir do feed OData com o Power BI)](reports-proc-create-with-odata.md).
- Para saber mais sobre a API do Data Warehouse do Intune, o modelo de dados e as relações entre entidades,<!-- , and an example of creating a custom client to retrieve data,--> veja [API do Data Warehouse do Intune](reports-nav-intune-data-warehouse.md).
