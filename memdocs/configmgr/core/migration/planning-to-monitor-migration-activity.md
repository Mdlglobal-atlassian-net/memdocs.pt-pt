---
title: Monitorizar a migração
titleSuffix: Configuration Manager
description: Aprenda a usar a consola Do Gestor de Configuração para monitorizar o progresso e o sucesso dos trabalhos migratórios.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713003"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>Planejamento monitorizar atividade de migração em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Com o Gestor de Configuração, pode monitorizar a migração na consola Do Gestor de Configuração que se conecta à hierarquia de destino. Na consola de Configuração Manager no espaço de trabalho **da Administração,** você pode usar o nó **migratório** para monitorizar o progresso e o sucesso dos trabalhos migratórios. Pode ver informações sumárias para cada trabalho de migração que identifique objetos que migraram, os objetos que ainda não migraram, e o número de objetos que estão excluídos de um trabalho de migração. Verá também pormenores sobre eventuais problemas de migração.  

## <a name="view-migration-progress"></a>Ver progresso migratório  
 Para ver o progresso de um trabalho de migração, utilize qualquer uma das seguintes ações:  

-   No espaço de trabalho da **Administração** da consola De Configuração Manager, expanda o nó **de Empregos** migratórios, selecione um trabalho de migração e, em seguida, selecione o separador **Objetos no Trabalho.**  

-   Utilize os ficheiros de registo do Gestor de Configuração para rever o progresso da migração ou para identificar quaisquer problemas. O Gestor de Migração é o processo de Gestor de Configuração que rastreia as ações de migração e regista-as no ficheiro migmctrl.log no ** \&\>\\lt;InstallationPath LOGS** no servidor do site.  

    > [!NOTE]  
    >  Se um trabalho de migração falhar, reveja os detalhes no ficheiro migmctrl.log o mais rápido possível. As entradas de registo de migração são continuamente adicionadas ao ficheiro e sobrepõem detalhes antigos. Se as entradas forem substituídas, poderá não ser capaz de identificar se algum problema que possa encontrar com os objetos migrados está relacionado com questões de migração. A atividade de migração\-está registada no local de alto nível da hierarquia, independentemente do site a que a consola do Gestor de Configuração se conecta quando configura a migração.  

-   Utilize o relatório do Gestor de Configuração. O Gestor de\-Configuração fornece vários relatórios incorporados para migração, ou pode editar esses relatórios de acordo com os seus requisitos. Para obter mais informações sobre os relatórios do Gestor de Configuração, consulte [Introdução a relatórios](../servers/manage/introduction-to-reporting.md).  
