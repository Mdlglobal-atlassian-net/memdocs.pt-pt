---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723650"
---
Utilize as seguintes definições para diferenciar entre piloto e produção:  

- **Piloto**: Um subconjunto dos seus dispositivos que pretende validar antes de se deslocar para um conjunto maior. Utilize o Desktop Analytics para marcar os dispositivos como únicos para o conjunto piloto. Os dispositivos do piloto estão prontos para atualizar quando nenhum ativo está bloqueado. Um ativo de bloqueio é marcado como *crítico* e *incapaz de* atualizar.  

- **Produção**: Todos os outros dispositivos matriculados no Desktop Analytics que não estão no piloto. Os dispositivos de produção estão prontos para atualizar quando todos os ativos forem assinados. O Desktop Analytics assina automaticamente quaisquer ativos não críticos.  

