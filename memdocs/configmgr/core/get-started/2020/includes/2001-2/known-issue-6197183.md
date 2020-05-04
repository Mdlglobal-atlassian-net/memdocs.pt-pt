---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712093"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a>Não pode criar ou editar algumas coleções

<!--6197183-->
Nesta versão do ramo de pré-visualização técnica, não é possível criar uma nova coleção. Também não é possível editar as propriedades de uma coleção de utilizadores existente.

Para resolver este problema, utilize os cmdlets do Gestor de Configuração PowerShell para criar novas coleções e editar as coleções de utilizadores existentes. Algumas das cmdlets disponíveis para gestão de coleções incluem:

- [Coleção New-CM](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Regra de adições CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
