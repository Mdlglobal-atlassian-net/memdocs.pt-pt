---
title: Ferramenta de Execução de Resumo do Medidor
titleSuffix: Configuration Manager
description: Utilize a Ferramenta de Resumição do Medidor de Execução para desencadear as tarefas de sumreização de medição de software no Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723174"
---
# <a name="run-meter-summarization-tool"></a>Ferramenta de Execução de Resumo do Medidor

*Aplica-se a: Gestor de Configuração (ramo atual)*

A Ferramenta de Resumização do Medidor de Execução é uma das ferramentas do Gestor de [Configuração.](tools.md) Utilize-o para acionar imediatamente as tarefas de manutenção para a resumição de medição de software em locais primários. Por padrão, estas tarefas funcionam conforme programado nas tarefas de Manutenção do **Local,** que começam depois das 00:00 todos os dias. 

Estas tarefas resumem os dados na tabela **MeterData** SQL e escrevem os resultados sumários nas tabelas **FileUsageSummary** e **MonthlyUsageSummary.** Depois vê-se o resultado resumido em relatórios de medição de software. Qualquer utilizador administrativo do Gestor de Configuração que possa ligar-se à base de dados do site primário pode utilizar esta ferramenta para executar a resumição. 

Esta ferramenta executa o Resumo de Utilização de **Ficheiros** e o software mensal de utilização **sumário** medindo tarefas de resumição de dados. Resume todos os dados dos contadores existentes sem o habitual período de espera de 12 horas. Execute-o no servidor SQL que acolhe a base de dados do site. Se a resumição for bem `0`sucedida, o código de saída está definido para . Se houve um erro, o `1`código de saída é.



## <a name="usage"></a>Utilização

### <a name="command-line"></a>Linha de Comandos

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Opções

#### <a name="database-name"></a>Nome da base de dados
O nome da base de dados do site no servidor SQL.

#### <a name="delay-in-hours-for-summarization"></a>Atraso nas horas de resumição
A ferramenta resume a utilização de medição de software gerada antes do atraso. Por defeito, este atraso é zero.


### <a name="example"></a>Exemplo

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Resumindo o uso de medição de software gerado há 12 horas

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Consulte também

- [Tarefas de manutenção](../servers/manage/maintenance-tasks.md)
- [Monitorizar a utilização da aplicação com a medição de software](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
