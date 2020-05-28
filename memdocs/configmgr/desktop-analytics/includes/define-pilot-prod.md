---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268793"
---
Utilize as seguintes definições para diferenciar entre piloto e produção:  

- **Piloto**: Um subconjunto dos seus dispositivos que pretende validar antes de se deslocar para um conjunto maior. Utilize o Desktop Analytics para marcar os dispositivos como únicos para o conjunto piloto. Os dispositivos do piloto estão prontos para atualizar quando nenhum ativo está bloqueado. Um ativo de bloqueio é marcado como *crítico* e *incapaz de* atualizar.  

- **Produção**: Todos os outros dispositivos matriculados no Desktop Analytics que não estão no piloto. Os dispositivos de produção estão prontos para atualizar quando todos os ativos forem assinados. O Desktop Analytics assina automaticamente quaisquer ativos não críticos.  
