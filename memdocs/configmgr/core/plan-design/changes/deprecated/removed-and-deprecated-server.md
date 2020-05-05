---
title: Depreciado para servidores de site
titleSuffix: Configuration Manager
description: Saiba mais sobre os produtos e sistemas operativos que o Gestor de Configuração já não suporta para servidores do site.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719478"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Removidoe depreciado para servidores do site do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo descreve produtos e sistemas operativos que são removidos do suporte para servidores do site do Gestor de Configuração, ou serão removidos numa futura atualização (depreciada). Fornece aviso prévio sobre futuras alterações que podem afetar o seu uso do Gestor de Configuração.  

Esta informação pode mudar no futuro. Pode não incluir cada funcionalidade depreciada, produto ou sistema operativo.  

## <a name="server-os"></a>Servidor OS  

|Sistemas operativos|Preterição anunciada pela primeira vez|Suporte removido|
|-|-|-|
|Windows Server 2008 R2 com SP1|10 de julho de 2015| Versão 1702|
|Windows Server 2008 com SP2|10 de julho de 2015|Versão 1511|

## <a name="sql-server"></a>SQL Server

|Versões do SQL Server|Preterição anunciada pela primeira vez|Suporte removido|
|-|-|-|
|SQL Server 2008 R2|10 de julho de 2015|Versão 1702|
|SQL Server 2008|10 de julho de 2015|Versão 1511|

Se necessitar de atualizar a sua versão do SQL Server, recomendamos os seguintes métodos, de fácil a mais complexo:

1. [Atualize o Servidor SQL no lugar](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (recomendado).  

2. Instale uma nova versão do SQL Server num novo computador. Em seguida, para apontar o servidor do seu site para o novo Servidor SQL, [utilize a opção](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) de movimento de base de dados da configuração do Gestor de Configuração.  

3. Utilize [cópias de segurança e recuperação.](../../../servers/manage/backup-and-recovery.md)  

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações, veja os artigos seguintes:

- [Removidas e preteridas](removed-and-deprecated.md)  

- [Ciclo de vida do suporte da Microsoft](https://support.microsoft.com/lifecycle)  

- [Suporte para versões de ramificação atuais do Gestor de Configuração](../../../servers/manage/current-branch-versions-supported.md)  
