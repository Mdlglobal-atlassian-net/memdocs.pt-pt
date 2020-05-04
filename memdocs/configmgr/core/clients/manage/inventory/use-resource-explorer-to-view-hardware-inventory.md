---
title: Como utilizar o Explorador de Recursos
titleSuffix: Configuration Manager
description: Utilize o Resource Explorer para visualizar o inventário de hardware no Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710679"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Como usar o Resource Explorer para ver o inventário de hardware no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o Resource Explorer no Gestor de Configuração para visualizar informações sobre o inventário de hardware. O site recolhe esta informação de clientes da sua hierarquia.  

> [!Tip]  
>  O Resource Explorer não exibe quaisquer dados até que um ciclo de inventário de hardware seja executado no cliente ao qual está a ligar.  



## <a name="overview"></a>Descrição geral

O Resource Explorer tem as seguintes secções relacionadas com o inventário de hardware:  

- **Hardware**: Mostra o mais recente inventário de hardware recolhido do dispositivo cliente especificado.  

    - O nó **Workstation Status** mostra a hora e a data do último inventário de hardware do dispositivo.  

- História do **Hardware**: Um histórico de itens inventariados que mudaram desde o último ciclo de inventário de hardware.  

    - Expanda um item para ver um nó **atual** e um ou mais nós com a data histórica. Compare a informação no nó atual com um dos nódoshistóricos para ver os itens que mudaram.  

> [!NOTE]  
> Por padrão, o Gestor de Configuração elimina os dados de inventário de hardware que estão inativos há 90 dias. Ajuste este número de dias na tarefa de manutenção do site **Delete Aged Inventory History.** Para mais informações, consulte [as tarefas de manutenção.](../../../servers/manage/maintenance-tasks.md)  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a>Como abrir o Explorador de Recursos   

1.  Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de **Dispositivos.** Também pode selecionar qualquer coleção no nó **de Recolha de Dispositivos.**  

2.  Selecione um dispositivo. Na fita, no separador **Home** e no grupo **dispositivos,** clique em **Iniciar**, e, em seguida, selecione **Resource Explorer**.   

> [!Tip]  
> No Resource Explorer, clique num item no painel de resultados certos para ações adicionais. Clique em **Propriedades** para ver esse item num formato diferente.  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a>Utilização de grandes valores inteiros
<!--1357880-->
Nas versões 1802 e anteriores do Gestor de Configuração, o inventário de hardware tem um limite para os inteiros superiores a 4.294.967.296 (2^32). Este limite pode ser atingido para atributos como tamanhos de disco rígido em bytes. O ponto de gestão não processa valores inteiros acima deste limite, pelo que nenhum valor é armazenado na base de dados. 

A partir da versão 1806, o limite é aumentado para 18.446.744.073.709.551.616 (2^64). 

Para uma propriedade com um valor que não muda, como o tamanho total do disco, você pode não ver imediatamente o valor após a modernização do site. A maioria do inventário de hardware é um relatório delta. O cliente só envia valores que mudam. Para contornar este comportamento, adicione outra propriedade à mesma classe. Esta ação faz com que o cliente atualize todas as propriedades da classe que mudaram. 



## <a name="see-also"></a>Consulte também

Para obter informações sobre como visualizar o inventário de hardware de clientes que executam o Linux e o UNIX, consulte [como monitorizar os clientes dos servidores Linux e UNIX](../monitor-clients-for-linux-and-unix-servers.md).  

O Resource Explorer também mostra o Inventário de Software. Para mais informações, consulte [Como utilizar o Resource Explorer para visualizar](use-resource-explorer-to-view-software-inventory.md)o inventário de software .
