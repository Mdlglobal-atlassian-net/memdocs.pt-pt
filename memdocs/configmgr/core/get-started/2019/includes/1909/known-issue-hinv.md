---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716174"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a>Relatórios de inventário de hardware

<!--5468413-->
Se tentar executar um relatório que dependa do inventário de hardware, devolve um erro. Por exemplo, um relatório BitLocker devolve um erro semelhante à seguinte mensagem:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

Pode também ver o seguinte erro no ficheiro **dataldr.log:**

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Os painéis de consola que dependem do inventário de hardware também podem ser afetados.

Este problema deve-se a uma alteração de esquemas de base de dados em tabelas específicas de inventário de hardware.

#### <a name="workaround"></a>Solução

A supõeção é retirar o atributo pré-existente da base de dados. O componente do site dataloader pode então criar um novo atributo. Executar o seguinte script SQL no servidor de base de dados do site para corrigir o esquema da tabela:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
