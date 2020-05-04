---
title: Monitor linux/UNIX clientes
titleSuffix: Configuration Manager
description: Monitorize os clientes em servidores Linux e UNIX no Gestor de Configuração.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715362"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Como monitorizar os clientes dos servidores Linux e UNIX no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX. 
> 
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

Pode visualizar informações de servidores Linux e UNIX na consola 'Gestor de Configuração', utilizando os mesmos métodos que utiliza para visualizar informações de clientes baseados no Windows.  

 As informações que pode ver incluem:  

- Detalhes de estado dos clientes, nos painéis de consola do Gestor de Configuração  

- Detalhes sobre clientes nos relatórios do Gestor de Configuração padrão  

- Detalhes de inventário no Explorador de Recursos  

  As seguintes secções descrevem como obter estes detalhes do explorador de recursos e relatórios.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a>Use o explorador de recursos para ver o inventário para servidores Linux e UNIX  

 Depois de um cliente do Gestor de Configuração submeter o inventário de hardware ao site do Gestor de Configuração, pode utilizar o Resource Explorer para visualizar esta informação. O cliente do Gestor de Configuração do Linux e da UNIX não adiciona novas classes ou vistas para inventário ao Explorador de Recursos. Os dados de inventário de Linux e UNIX são mapeados para as classes WMI existentes. Pode ver os detalhes de inventário para os seus servidores Linux e UNIX nas classificações baseadas no Windows utilizando o Explorador de Recursos.  

 Por exemplo, é possível recolher a lista de todos os programas instalados nativamente encontrados nos seus servidores Linux e UNIX. Exemplos de programas instalados nativamente incluem **.rpms** no Linux ou **.pkgs** no Solaris. Depois de o inventário ter sido submetido por um cliente Linux ou UNIX, pode ver a lista de todos os programas linux ou UNIX instalados de forma nativa no Resource Explorer na consola Do Gestor de Configuração.  

 Para obter informações sobre como usar o Resource Explorer, consulte [como utilizar o Resource Explorer para visualizar](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)o inventário de hardware .  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Como utilizar Relatórios para Ver Informações de Servidores Linux e UNIX  
 Os relatórios para o Gestor de Configuração incluem informações dos servidores Linux e UNIX, juntamente com informações de computadores baseados no Windows. Não são necessárias configurações adicionais para integrar os dados de Linux e UNIX nos relatórios.  

 Por exemplo, se executar o relatório chamado Contagem de Versões de Sistemas Operativos, este apresenta a lista dos diferentes sistemas operativos e o número de clientes que estão a executar cada sistema operativo. O relatório baseia-se nas informações de inventário de hardware que foram enviadas pelos diferentes clientes do Gestor de Configuração que funcionam nos diferentes sistemas operativos.  

 Também é possível criar relatórios personalizados específicos para os dados do servidor Linux e UNIX. A propriedade **Legenda** da classe de inventário de hardware **Sistema Operativo** é um atributo útil que poderá utilizar para identificar Sistemas Operativos específicos na consulta do relatório.  

 Para obter informações sobre relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../servers/manage/introduction-to-reporting.md).  
