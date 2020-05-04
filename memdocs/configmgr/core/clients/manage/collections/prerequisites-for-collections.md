---
title: Requisitos de cobranças
titleSuffix: Configuration Manager
description: Obtenha pré-requisitos para a utilização de coleções no Gestor de Configuração.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714501"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Pré-requisitos para coleções em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As coleções no Gestor de Configuração contêm apenas dependências dentro do produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve ser instalada para que possa executar relatórios para coleções. Para mais informações, consulte [Introdução a relatórios.](../../../servers/manage/introduction-to-reporting.md)|  
|Devem ter sido concedidas permissões de segurança específicas para gerir coleções|Deve ter as seguintes permissões de segurança para gerir definições de conformidade:<br /><br /> - Criar e gerir coleções: **Criar,** **Eliminar,** **Modificar,** Modificar a **Pasta,** **Mover objeto,** **Ler** e **Ler Recursos** para o Objeto **de Recolha.**<br /><br /> - Para gerir as definições de recolha: Modificar a **definição** de recolha para o Objeto **de Recolha.**<br /><br /> A permissão **Modificar Pasta** é necessária para todas as pastas de coleção, incluindo a pasta de raiz.|  
