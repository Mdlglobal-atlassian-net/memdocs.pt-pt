---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716118"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a>As sequências de tarefas não estão disponíveis para PXE ou meios de comunicação

<!--5578298-->
Se implementar uma sequência de tarefas para PXE ou meios de comunicação (USB ou DVD), o cliente não recebe a apólice. A seguinte mensagem está em **smsts.log:**

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Solução

Inicie a sequência de tarefas do Centro de Software.
