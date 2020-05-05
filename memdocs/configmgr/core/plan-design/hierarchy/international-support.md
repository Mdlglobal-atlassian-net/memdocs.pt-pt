---
title: Suporte internacional
titleSuffix: Configuration Manager
description: Configure O Gestor de Configuração para cumprir os requisitos internacionais específicos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720941"
---
# <a name="international-support-in-configuration-manager"></a>Suporte internacional em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As seguintes secções fornecem detalhes técnicos para ajudá-lo a tornar o Gestor de Configuração em conformidade com requisitos internacionais específicos.  

## <a name="gb18030-requirements"></a>Requisitos da GB18030  
 O Gestor de Configuração cumpre os padrões definidos em GB18030 para que possa utilizar o Gestor de Configuração na China. Uma implementação do Gestor de Configuração deve ter as seguintes configurações para satisfazer os requisitos gb18030:  

-   Cada computador do servidor do site e computador SQL Server que utiliza com o Gestor de Configuração devem utilizar um sistema operativo chinês.  

-   Cada base de dados do site e cada instância do SQL Server da hierarquia deve utilizar o mesmo agrupamento, e tem de ser um dos seguintes:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Estas colagens de bases de dados são uma exceção aos requisitos que são anotados no [Suporte para versões SQL Server para O Gestor](../../../core/plan-design/configs/support-for-sql-server-versions.md)de Configuração .  

-   Tem de colocar um ficheiro com o nome **GB18030.SMS** na pasta raiz do volume do sistema de cada computador do servidor do site da hierarquia. Este ficheiro não contém quaisquer dados e pode ser um ficheiro de texto vazio com um nome que satisfaça este requisito.  
