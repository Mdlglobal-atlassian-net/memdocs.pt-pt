---
title: Ver inventário de software com explorador de recursos
titleSuffix: Configuration Manager
description: Utilize o Resource Explorer para visualizar o inventário de software no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710658"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Como usar o Resource Explorer para ver o inventário de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o Resource Explorer no Gestor de Configuração para visualizar informações sobre o inventário de software que foi recolhida a partir de computadores da sua hierarquia.  

> [!NOTE]  
>  O Resource Explorer não apresentará quaisquer dados de inventário até que um ciclo de inventário de software tenha sido executado no cliente.  

 O Resource Explorer fornece as seguintes informações sobre o inventário de software:  

-   **Software**:  

    -   **Ficheiros Recolhidos** - Ficheiros que foram recolhidos durante o inventário de software.  

    -   **Detalhes do ficheiro** - Ficheiros que foram inventariados durante o inventário de software que não estão associados a um produto ou fabricante específico.  

    -   **Última varredura** de software - Data e hora do último inventário de software e recolha de ficheiros para o computador cliente.  

    -   **Detalhes do Produto** - Produtos de software que foram inventariados por inventário de software, agrupados pelo fabricante.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para executar o Explorador de Recursos a partir da consola do Configuration Manager  

1.  Na consola De Configuração Manager, escolha **Ativos e Conformidade**

2.  No espaço de trabalho **De Ativos e Compliance,** escolha **Dispositivos** ou abra qualquer recolha que apresente dispositivos.  

3.  Escolha o computador que contém o inventário que pretende visualizar e, em seguida, no separador **Home** > **Grupo dispositivos,** escolha **Start** > **Resource Explorer**.

4.  Pode clicar em qualquer item no painel direito da janela do Explorador de Recursos e escolher **propriedades** para ver as informações de inventário recolhidas num formato mais legível.  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> Ver e gerir ficheiros de diagnóstico recolhidos

Começando na versão de 2002 do Gestor de Configuração, utilize o Resource Explorer para visualizar e gerir os ficheiros recolhidos quando utilizar a notificação do cliente para [recolher registos](../client-notification.md#client-diagnostics)de clientes. 

1. A partir do nó de **Dispositivos,** clique à direita no dispositivo para o que pretende visualizar os registos.
1. Selecione **Iniciar,** depois **Explorador de Recursos.**
1. Do Explorador de **Recursos,** clique em **Ficheiros de Diagnóstico**.
1. Na lista **de Ficheiros de Diagnóstico,** pode ver a data de recolha dos ficheiros. O formato de nome `Support_<guid>.zip`dos registos do cliente é .
1. Clique à direita no ficheiro zip e selecione uma das seguintes opções:
    - **Centro de Suporte Aberto**: Lança Centro de [Suporte](../../../support/support-center.md).
    - **Cópia**: Copia as informações da linha do Explorador de Recursos.
    - **Ver ficheiro**: Abre a pasta onde o ficheiro zip está localizado com o File Explorer.
    - **Guardar**: Abre um diálogo 'Guardar ficheiro' para o ficheiro selecionado.
    - **Exportação**: Guarde as colunas do Explorador de Recursos mostradas em **Ficheiros de Diagnóstico**.
    - **Atualização**: Atualiza a lista de ficheiros.
    - **Propriedades**: Devolve as propriedades no ficheiro selecionado. 

[![Reveja e guarde os registos de clientes do Resource Explorer](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>Passos seguintes

[Utilize o Centro de Suporte](../../../support/support-center.md) para visualizar ficheiros de diagnóstico recolhidos.
