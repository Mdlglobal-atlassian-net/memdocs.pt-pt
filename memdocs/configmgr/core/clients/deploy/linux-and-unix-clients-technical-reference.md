---
title: Serviços e comandos de componentes de clientes UNIX/Linux
titleSuffix: Configuration Manager
description: Conheça os serviços de componentes e comandos sobre os clientes Linux e UNIX no Gestor de Configuração.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713346"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Serviços e comandos de componentes de clientes Linux e UNIX para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX. 
> 
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.


 A tabela seguinte identifica os serviços de componentes do cliente do cliente do Gestor de Configuração para o Linux e uniX.  

|Nome de ficheiro|Mais informações|  
|---------------|----------------------|  
|ccmexec.bin|Este serviço é semelhante ao serviço ccmexc de um cliente baseado no Windows. É responsável por todas as comunicações com funções do sistema do Site Do Gestor de Configuração, e também comunica com o serviço omiserver.bin para recolher o inventário de hardware do computador local.<br /><br /> Para uma lista de argumentos de linha de comando suportados, corra`ccmexec -h`|  
|omiserver.bin|Este serviço é o servidor CIM. O servidor CIM proporciona uma arquitetura para módulos de software incorporáveis, denominados fornecedores. Os fornecedores interagem com os recursos informáticos Linux e UNIX e recolhem os dados do inventário de hardware. Por exemplo, o **fornecedor de processos** para um computador Linux recolhe os dados associados aos processos do sistema operativo Linux.|  

 As tabelas seguintes listam os comandos que pode utilizar para iniciar, parar ou reiniciar os serviços do cliente (ccmexec.bin e omiserver.bin) em cada versão do Linux ou do UNIX. Quando iniciar ou parar o serviço ccmexec, o serviço omiserver também é iniciado ou parado.  

|Sistema operativo|Comandos|  
|----------------------|--------------|  
|Agente Universal<br /><br /> RHEL 4 e SLES 9|Início:`/etc/init d/ccmexecd start`<br /><br /> Paragem:`/etc/init d/ccmexecd stop`<br /><br /> Reiniciar:`/etc/init d/ccmexecd restart`|  
|Solaris 9|Início:`/etc/init d/ccmexecd start`<br /><br /> Paragem:`/etc/init d/ccmexecd stop`<br /><br /> Reiniciar:`/etc/init d/ccmexecd restart`|  
|Solaris 10|Iniciar:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Parar:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Iniciar:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Parar:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Iniciar:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Parar:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Início:`/sbin/init.d/ccmexecd start`<br /><br /> Paragem:`/sbin/init.d/ccmexecd stop`<br /><br /> Reiniciar:`/sbin/init.d/ccmexecd restart`|  
