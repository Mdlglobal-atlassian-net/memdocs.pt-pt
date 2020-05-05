---
title: Visualizador de Avaliação de Coleção
titleSuffix: Configuration Manager
description: Utilize o Visualizador de Avaliação de Recolha de Recolha para visualizar e resolver problemas o processo de avaliação da recolha no Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723419"
---
# <a name="collection-evaluation-viewer"></a>Visualizador de Avaliação de Coleção

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Visualizador de Avaliação de Recolha é uma das ferramentas do Gestor de [Configuração.](tools.md) Use-o para visualizar e resolver problemas o processo de avaliação da recolha no servidor do site principal.

A ferramenta apresenta as seguintes informações:  

- Informação histórica e ao vivo para avaliações completas e incrementais de recolha  

- O estado da fila de avaliação  

- O tempo para as avaliações de recolha para completar  

- Quais coleções estão atualmente a ser avaliadas  

- O tempo estimado que uma avaliação de coleção começará e completará  



## <a name="about-collection-evaluation"></a>Sobre a avaliação da coleção

O processo de avaliação da recolha decorre através da avaliação das regras de adesão de uma coleção para atualizar os seus membros. O site coloca uma coleção que está a avaliar numa de quatro filas diferentes:  

- **Fila Manual**: Para as coleções que um administrador selecionou manualmente para avaliação da consola  

- **Nova Fila**: Para coleções recém-criadas  

- **Fila Completa**: Para cobranças devidas para avaliação completa  

- **Fila Incremental**: Para coleções com avaliação incremental  

Há quatro fios que correm para avaliar as coleções nas filas acima. Cada fila inclui uma série de matrizes, e cada matriz inclui as coleções a avaliar. O fio que está a correr para a fila seleciona uma coleção da matriz e executa a avaliação. O comprimento da fila indica o número de matrizes na fila.



## <a name="requirements"></a>Requisitos

- Executar a ferramenta no servidor do site  

- Executar a ferramenta por um utilizador administrativo com pelo menos o papel **de Analista de Leitura**  

- O utilizador também requer **ler** permissão para a base de dados do site em SQL



## <a name="usage"></a>Utilização

Executar **CEViewer.exe**. O menu principal da ferramenta contém os seguintes separadores: 

- [Ligação](#bkmk_connect): Estabelecer a ligação inicial ao servidor principal do site e ao Servidor SQL  

- [Avaliação Completa](#bkmk_full-eval): Lista as informações detalhadas sobre todas as avaliações completas passadas   

- [Avaliação incremental](#bkmk_incremental-eval): Lista as informações detalhadas sobre todas as avaliações incrementais passadas  

- [Todas as filas](#bkmk_all-q): Resume as avaliações de coleção atuais para as quatro filas  

- [Fila Manual](#bkmk_manual-q): Lista as informações detalhadas sobre a avaliação de recolha atual na fila manual  

- [Nova Fila](#bkmk_new-q): Lista as informações detalhadas sobre a avaliação da coleção atual na nova fila  

- [Fila Completa](#bkmk_full-q): Lista as informações detalhadas sobre a avaliação de recolha atual na fila completa  

- [Fila Incremental](#bkmk_incremental-q): Lista as informações detalhadas sobre a avaliação de recolha atual na fila incremental  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Ligar o separador

Este separador permite-lhe estabelecer a ligação inicial ao servidor do site primário. A ferramenta também estabelece uma ligação ao servidor SQL que acolhe a base de dados do site.

As ligações ao servidor principal do site e aos servidores SQL utilizam a credencial de utilizador assinada atualmente. As ligações ao site da administração central ou a um local secundário não são suportadas. Nenhum processo de avaliação de recolha decorre nesses sites.

Assim que a ferramenta estabelecer com sucesso uma ligação, consulte uma notificação na parte inferior do Visualizador de Avaliação de Recolha que confirma a ligação da ferramenta ao servidor SQL. 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a>Separador de avaliação completa

Mostra informações detalhadas sobre avaliações de recolha completa passadas. Há oito colunas:  

- **Nome**da coleção : Nome da coleção  

- **ID do site**: Id do site da coleção   

- **Tempo de execução**: Quanto tempo durou a última avaliação de coleção, em segundos  

- **Última avaliação Tempo**de Conclusão : Quando a última avaliação de recolha concluída  

- **Tempo de avaliação seguinte**: Quando a próxima avaliação completa começar  

- **Alterações dos membros**: O membro muda na última avaliação de recolha. Estas alterações são mais (membros adicionados) ou menos (membros removidos).  

- **Último Tempo de Mudança de Membro**: O tempo mais recente em que houve uma alteração na avaliação da coleção  

- **Por cento**: A percentagem de tempo de avaliação desta coleção ao longo do tempo total de avaliação (todas as coleções)  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a>Separador de avaliação incremental

Mostra informações detalhadas sobre avaliações de recolha incremental passadas. Há sete colunas:  

- **Nome**da coleção : Nome da coleção  

- **ID do site**: Id do site da coleção   

- **Tempo de execução**: Quanto tempo durou a última avaliação de coleção, em segundos  

- **Última avaliação Tempo**de Conclusão : Quando a última avaliação de recolha concluída  

- **Alterações dos membros**: O membro muda na última avaliação de recolha. Estas alterações são mais (membros adicionados) ou menos (membros removidos).  

- **Último Tempo de Mudança de Membro**: O tempo mais recente em que houve uma alteração na avaliação da coleção  

- **Por cento**: A percentagem de tempo de avaliação desta coleção ao longo do tempo total de avaliação (todas as coleções)  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a>Todos os separadores de filas

Resume as avaliações de coleção ao vivo para as quatro filas. Há seis secções:  

- **Resumo**: Lista o número total de recolha e o comprimento da fila para todas as coleções nas quatro filas  

- **Avaliação de Execução**: Listas que a recolha está atualmente a ser avaliada em cada fila, e quanto tempo está a decorrer  

- **Atualização Manual**: Mostra um breve resumo das coleções que estão a ser avaliadas, o tempo estimado de conclusão e a ordem da avaliação na fila manual  

- **Nova Coleção**: Mostra um breve resumo das coleções que estão a ser avaliadas, o tempo estimado de conclusão e a ordem da avaliação na nova fila de recolhas  

- **Avaliação completa**: Mostra um breve resumo das coleções que estão a ser avaliadas, o tempo estimado de conclusão e a ordem da avaliação na fila de avaliação completa  

- **Avaliação Incremental**: Mostra um breve resumo das coleções que estão a ser avaliadas, o tempo estimado de conclusão e a ordem da avaliação na fila de avaliação incremental  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a>Separador de fila manual

Mostra informações sobre a avaliação da recolha manual que está a ser avaliada. A ordem na lista é a ordem em que a coleção será avaliada. Há quatro colunas:  

- **Nome**da coleção : Nome da coleção  

- **ID do site**: Id do site da coleção   

- **Tempo estimado de conclusão**: Quando a avaliação é estimada para concluir  

- Tempo estimado de **execução**: Quanto tempo a avaliação é estimada para ser executada, em dia:hora:minuto:segundo formato  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a>Novo separador fila

Mostra a informação ao vivo sobre a nova avaliação da coleção que está a ser avaliada. A ordem na lista é a ordem em que a coleção será avaliada. Há quatro colunas:  

- **Nome**da coleção : Nome da coleção  

- **ID do site**: Id do site da coleção   

- **Tempo estimado de conclusão**: Quando a avaliação é estimada para concluir  

- Tempo estimado de **execução**: Quanto tempo a avaliação é estimada para ser executada, em dia:hora:minuto:segundo formato  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a>Separador de fila completa

Mostra informações sobre a avaliação completa da recolha que está a ser avaliada. A ordem na lista é a ordem em que a coleção será avaliada. Há quatro colunas:  

- **Nome**da coleção : Nome da coleção  

- **ID do site**: Id do site da coleção   

- **Tempo estimado de conclusão**: Quando a avaliação é estimada para concluir  

- Tempo estimado de **execução**: Quanto tempo a avaliação é estimada para ser executada, em dia:hora:minuto:segundo formato  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a>Separador de fila incremental

Mostra informações sobre a avaliação incremental da recolha atualmente a ser avaliada. A ordem na lista é a ordem em que a coleção será avaliada. Há quatro colunas:  

- **Nome**da coleção : Nome da coleção  

- **ID do site**: Id do site da coleção   

- **Tempo estimado de conclusão**: Quando a avaliação é estimada para concluir  

- Tempo estimado de **execução**: Quanto tempo a avaliação é estimada para ser executada, em dia:hora:minuto:segundo formato  



