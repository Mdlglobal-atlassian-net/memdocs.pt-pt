---
title: Introdução à gestão de energia
titleSuffix: Configuration Manager
description: Obtenha uma introdução à gestão de energia no Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 400fe3113207217504317eeb8ef8bbce4ab6a298
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715222"
---
# <a name="introduction-to-power-management-in-configuration-manager"></a>Introdução à gestão de energia no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A Power Management in Configuration Manager aborda a necessidade que muitas organizações têm de monitorizar e reduzir o consumo de energia dos seus computadores. A funcionalidade tira partido das funcionalidades de gestão de energia incorporadas no Windows para aplicar definições relevantes e consistentes aos computadores da organização. Pode aplicar diferentes definições de energia aos computadores durante as horas de expediente e fora do expediente. Por exemplo, pode pretender aplicar um esquema de energia mais restritivo aos computadores durante as horas de expediente. Nos casos em que os computadores tenham de estar sempre ligados, pode impedir que as definições de gestão de energia sejam aplicadas.  

 A gestão de energia no Gestor de Configuração inclui vários relatórios para o ajudar a analisar o consumo de energia e as definições de energia do computador na sua organização. Também pode utilizar os relatórios para ajudar a resolver problemas relacionados com a gestão de energia.  

 Para um fluxo de trabalho detalhado sobre como configurar e utilizar a gestão de energia, consulte a lista de [verificação do Administrador para a gestão de energia](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  A gestão de energia do Gestor de Configuração não é suportada em máquinas virtuais. Não pode aplicar esquemas de energia a máquinas virtuais, nem reportar os dados de energia dos mesmos.  

## <a name="the-power-management-workflow"></a>Fluxo de trabalho de gestão de energia  
 Utilize as três fases seguintes para planear e implementar a gestão de energia no Gestor de Configuração.  

### <a name="monitoring-and-planning-phase"></a>Fase de monitorização e planeamento  
 A Power Management utiliza o inventário de hardware do Gestor de Configuração para recolher dados sobre a utilização do computador e as definições de energia para computadores no site. Existem vários relatórios que pode utilizar para analisar estes dados e determinar as definições de gestão de energia ideais para os computadores. Por exemplo, durante a fasee de monitorização e planeamento do fluxo de trabalho de gestão de energia, pode criar coleções baseadas nos dados incluídos no relatório **Capacidades de Energia** e utilizar esses dados para identificar os computadores sem capacidade de gestão de energia. Em seguida, pode excluir esses computadores da gestão de energia.  

> [!IMPORTANT]  
>  Não aplique esquemas de energia aos computadores no seu site até recolher e analisar os dados de energia dos computadores cliente. Se aplicar novas definições de gestão de energia aos computadores sem examinar primeiro as definições existentes, isto pode representar um aumento do consumo de energia.  

### <a name="enforcement-phase"></a>Fase de imposição  
 A gestão de energia permite criar esquemas de energia que pode aplicar às coleções de computadores no seu site. Estes esquemas de energia configuram as definições de gestão de energia do Windows nos computadores. Pode utilizar os planos de alimentação que estão incluídos no Configurmanager, ou pode configurar os seus próprios planos de alimentação personalizados. Pode utilizar os dados de energia recolhidos durante a fase de monitorização e planeamento como uma linha de base para o ajudar a avaliar a poupança de energia depois de aplicar um esquema de energia aos computadores. Para mais informações, consulte a lista de [verificação do Administrador para a gestão de energia](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Fase de conformidade  
 Na fase de conformidade, pode executar relatórios que ajudam a avaliar a utilização de energia e a poupança de energia na sua organização. Também pode executar relatórios que descrevem as melhorias na quantidade de CO2 gerada por computadores. Também estão disponíveis relatórios que ajudam a validar que as definições de energia foram aplicadas corretamente aos computadores e a resolver problemas relacionados com a funcionalidade de gestão de energia.  
