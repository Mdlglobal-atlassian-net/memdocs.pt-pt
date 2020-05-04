---
title: Introdução às consultas
titleSuffix: Configuration Manager
description: Crie e execute consultas para localizar objetos numa hierarquia do Gestor de Configuração que corresponda aos seus critérios de consulta.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713822"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Introdução a consultas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode criar e executar consultas para localizar objetos numa hierarquia do Gestor de Configuração que corresponda aos seus critérios de consulta. Estes objetos incluem itens como tipos específicos de computadores ou grupos de utilizadores. As consultas podem devolver a maioria dos tipos de objetos do Gestor de Configuração, que incluem sites, coleções, aplicações e dados de inventário.  

## <a name="query-creation-overview"></a>Visão geral da criação de consultas

 Quando cria uma consulta, tem de especificar um mínimo de dois parâmetros: onde pretende pesquisar e o que pretende procurar. Por exemplo, para encontrar a quantidade de espaço de disco rígido disponível em todos os computadores num site do Gestor de Configuração, pode criar uma consulta para pesquisar a classe de atributo **silógico** e o atributo **free space (MB)** para o espaço de disco rígido disponível.  

 Depois de criar uma consulta inicial, pode especificar critérios de consulta adicionais. Por exemplo, pode especificar que os resultados da consulta incluem apenas os computadores que estão atribuídos a um site especificado. Também pode alterar a forma como os resultados são apresentados para que possa ver os resultados numa ordem que seja significativa para si. Por exemplo, pode especificar que os resultados são classificados pela quantidade de espaço de disco rígido livre, em ordem ascendente ou descendente.  

 Quando se cria uma consulta, é armazenada pelo Gestor de Configuração e exibida no nó **de Consultas** no espaço de trabalho **de Monitorização.** A partir deste local, pode criar novas consultas e executar, atualizar e gerir consultas existentes.  

 Também pode importar uma consulta para uma regra de consulta numa coleção de Gestor de Configuração. Para mais informações, consulte [Como criar coleções.](../../../core/clients/manage/collections/create-collections.md)  

## <a name="next-steps"></a>Passos seguintes

 [Como criar consultas](../../../core/servers/manage/create-queries.md)
