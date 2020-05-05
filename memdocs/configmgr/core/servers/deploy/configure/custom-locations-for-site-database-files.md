---
title: Localizações de ficheiros de base de dados personalizadas
titleSuffix: Configuration Manager
description: Saiba como especificar localizações personalizadas para ficheiros de base de dados do Servidor SQL.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc7eb1a8ba721545bdee50d45887ab9d3aa8e952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721011"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Localizações personalizadas para ficheiros de base de dados do site do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

 O Gestor de Configuração suporta localizações personalizadas para ficheiros de base de dados do Servidor SQL.  

> [!NOTE]  
>  A opção de especificar localizações de ficheiros não predefinidos não está disponível quando utiliza um cluster do Servidor SQL.  

 Durante a **instalação** de um novo site primário ou central de administração, pode:  

-   **Especifique as localizações de ficheiros não predefinidos para a base**de dados do site: Configuração do Gestor de Configuração e cria a base de dados do site utilizando estas localizações.  

-   **Especifique a utilização de uma base de dados do SQL Server pré-criada que utiliza localizações de ficheiros personalizadas**: Configuração do Gestor de Configuração utiliza essa base de dados pré-criada e as suas localizações de ficheiros pré-configuradas.  

Após a **configuração,** pode alterar a localização dos ficheiros da base de dados do site. Isto requer que pare o site e edite a localização do ficheiro no Servidor SQL:  

-   No servidor do site do Gestor de Configuração, pare o serviço **SMS_Executive.**  

-   Utilize a documentação para a sua versão do SQL Server para guiá-lo sobre como mover uma base de dados de utilizador. Por exemplo, se utilizar o SQL Server 2014, consulte as bases de dados dos [utilizadores em](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) Tecnologia.  

-   Depois de concluir o movimento de ficheiros da base de dados, reinicie o serviço **SMS_Executive** no servidor do site do Gestor de Configuração.  
