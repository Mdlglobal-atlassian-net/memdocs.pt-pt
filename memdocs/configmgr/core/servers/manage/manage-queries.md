---
title: Gerir consultas
titleSuffix: Configuration Manager
description: Aprenda a gerir as suas consultas. Inclui uma tabela para referência detalhada.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713752"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Como gerir consultas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo pode ajudá-lo a gerir consultas no Gestor de Configuração.  

 Para obter informações sobre como criar consultas, consulte [Como criar consultas.](../../../core/servers/manage/create-queries.md)  

## <a name="manage-queries"></a>Gerir consultas
 Na área de trabalho **Monitorização** , selecione **Consultas**, selecione a consulta que pretende gerir e, em seguida, selecione uma tarefa de gestão.  

 A tabela seguinte fornece informações sobre as tarefas de gestão.  

|Tarefa de gestão|Detalhes| 
|---------------------|-------------|
|**Executar**|Executa a consulta selecionada e exibe os resultados na consola 'Gestor de Configuração'.|
|**Instalar Cliente**|Abre o **Assistente de Cliente de Instalação,** que permite instalar o cliente Do Gestor de Configuração em computadores devolvidos pela consulta selecionada.<br /><br /> Esta opção não está disponível para consultas que devolm dispositivos móveis, utilizadores ou grupos de utilizadores. <br /><br /> Para obter mais informações sobre como instalar clientes do Gestor de Configuração utilizando o impulso do cliente, consulte [os clientes de implementação para computadores Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Exportar**|Abre o Feiticeiro de **Objetos de Exportação**. Este assistente permite-lhe exportar a consulta para um ficheiro De formato de Objeto Gerido (MOF) que pode depois importar noutro site.
|**Mover**|Abre a caixa de diálogo **move Selected Itens.** Esta caixa de diálogo permite-lhe mover a consulta selecionada para uma pasta que criou anteriormente sob o nó de **Consultas.**|

## <a name="next-steps"></a>Passos seguintes 
 [Criar consultas](../../../core/servers/manage/create-queries.md)
