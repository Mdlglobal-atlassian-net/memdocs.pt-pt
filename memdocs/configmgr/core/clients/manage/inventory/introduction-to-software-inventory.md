---
title: Inventário de software
titleSuffix: Configuration Manager
description: Obtenha uma introdução ao inventário de software no Gestor de Configuração.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714396"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Introdução ao inventário de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o inventário de software para recolher informações sobre ficheiros em dispositivos clientes. O inventário de software também pode recolher ficheiros de dispositivos clientes e armazená-los no servidor do site. O inventário de software é recolhido quando seleciona o inventário de software Enable na definição de clientes nas definições dos **clientes.** Também pode agendar a operação nas definições do cliente.  

Depois de ativar o inventário de software e os clientes executarem um ciclo de inventário de software, o cliente envia a informação para um ponto de gestão no site do cliente. O ponto de gestão remete então as informações de inventário para o servidor do site do Gestor de Configuração, que armazena a informação na base de dados do site.

 Existem algumas formas de ver dados de inventário de software:  

- [Crie consultas](../../../../core/servers/manage/create-queries.md) que devolvam dispositivos com ficheiros especificados.   

- Crie [coleções baseadas em consultas](../../../../core/clients/manage/collections/introduction-to-collections.md) que incluam dispositivos com ficheiros especificados.   

- [Executar relatórios](../../../servers/manage/introduction-to-reporting.md) que forneçam detalhes sobre ficheiros em dispositivos.

- Utilize o [Resource Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) para examinar informações detalhadas sobre os ficheiros que foram inventariados e recolhidos a partir de dispositivos clientes.   

 Quando o inventário de software é executado num dispositivo cliente, o primeiro relatório é um inventário completo. Relatórios subsequentes contêm apenas informações de inventário delta. O servidor do site processa informações delta na ordem recebida. Se faltar informações delta para um cliente, o servidor do site rejeita mais informações delta e direciona o cliente para executar um inventário completo.  

 O Gestor de Configuração pode descobrir computadores de duas botas, mas apenas devolve informações de inventário do sistema operativo que está ativo no momento do inventário.  
