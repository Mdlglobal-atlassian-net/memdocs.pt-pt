---
title: 'Inventário de Hardware '
titleSuffix: Configuration Manager
description: Obtenha uma introdução ao inventário de hardware no Gestor de Configuração.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714410"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Introdução ao inventário de hardware no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o inventário de hardware no Gestor de Configuração para recolher informações sobre a configuração de hardware dos dispositivos clientes na sua organização. Para recolher o inventário de hardware, deve selecionar o inventário de **hardware Enable na** definição de clientes nas definições do cliente.  

 Após o inventário de hardware ser ativado e o cliente executa um ciclo de inventário de hardware, o cliente envia a informação para um ponto de gestão no site do cliente. O ponto de gestão remete então as informações de inventário para o servidor do site do Gestor de Configuração, que armazena as informações de inventário na base de dados do site. O inventário de hardware é executado nos clientes, de acordo com a agenda que especificou nas definições de cliente.  
## <a name="view-hardware-inventory"></a>Ver inventário de hardware 

 Pode utilizar vários métodos para visualizar os dados de inventário de hardware que o Gestor de Configuração recolhe, incluindo estes métodos:  

- [Crie consultas que devolvam dispositivos baseados numa configuração específica](../../../../core/servers/manage/introduction-to-queries.md)do hardware .  

- [Crie coleções baseadas em consultas baseadas numa configuração específica do hardware.](../../../../core/clients/manage/collections/introduction-to-collections.md) As adesões a coleções baseadas em consultas são atualizadas automaticamente segundo uma agenda. Pode utilizar coleções para várias tarefas, incluindo a implementação de software.

- [Executar relatórios que exibem detalhes específicos sobre configurações](../../../servers/manage/introduction-to-reporting.md)de hardware na sua organização .

- [Use o Resource Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) para visualizar informações detalhadas sobre o inventário de hardware que é recolhido a partir de dispositivos clientes.

Quando executa o inventário de hardware num dispositivo cliente, os primeiros dados de inventário devolvidos pelo cliente são sempre um inventário completo. Os dados de inventário subsequentes contêm apenas informações de inventário delta. O servidor do site processa informações de inventário delta na ordem recebida. Se faltar informação delta para um cliente, o servidor do site rejeita informações adicionais do Delta e direciona o cliente para executar um ciclo de inventário completo.  

 O Gestor de Configuração fornece suporte limitado para computadores de arranque duplo. O Gestor de Configuração pode descobrir computadores de duas botas, mas devolve informações de inventário apenas do sistema operativo que está ativo quando o ciclo de inventário funciona.  

> [!NOTE]  
>  Para obter informações sobre como usar o inventário de hardware com clientes que executam o Linux e o UNIX, consulte o inventário de [hardware para linux e UNIX](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Expandir o inventário de hardware do Configuration Manager  
 Além do inventário de hardware incorporado no Gestor de Configuração, também pode utilizar um destes métodos para alargar o inventário de hardware para recolher mais informações:  

- Ativar, desativar, adicionar e remover as classes de inventário para inventário de hardware da consola Do Gestor de Configuração.  
- Utilize ficheiros NOIDMIF para recolher informações sobre dispositivos clientes que não podem ser inventariados pelo Gestor de Configuração. Por exemplo, pode pretender recolher informações sobre o número de ativos de dispositivo existentes apenas como uma etiqueta no dispositivo. O inventário NOIDMIF é associado automaticamente ao dispositivo cliente a partir do qual foi recolhido.  
- Utilize ficheiros IDMIF para recolher informações sobre ativos que não estejam associados a um cliente do Gestor de Configuração, por exemplo, projetores, fotocopiadoras e impressoras de rede.


## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre a utilização destes métodos para alargar o inventário de hardware do Gestor de Configuração, consulte [como configurar](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)o inventário de hardware .  
