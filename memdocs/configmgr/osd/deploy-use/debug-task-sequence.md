---
title: Depurar uma sequência de tarefas
titleSuffix: Configuration Manager
description: Utilize a ferramenta de depuração da sequência de tarefas para resolver uma sequência de tarefas.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66f460b7ba5c870a9ee81d10835ceb9f660cba89
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711036"
---
# <a name="debug-a-task-sequence"></a>Depurar uma sequência de tarefas

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3612274-->

A partir da versão de 1906, o debugger da sequência de tarefas é uma nova ferramenta de resolução de problemas. Implementa uma sequência de tarefas em modo dedepura para uma pequena coleção. Permite-lhe passar pela sequência de tarefas de forma controlada para ajudar na resolução de problemas e na investigação. O debugger funciona atualmente no mesmo dispositivo que o motor de sequência de tarefas, não é um desordeiro remoto.

> [!Note]  
> Nesta versão do Gestor de Configuração, o debugger da sequência de tarefas é uma funcionalidade de pré-lançamento. Para o ativar, consulte [as funcionalidades de pré-lançamento](../../core/servers/manage/pre-release-features.md).  


## <a name="prerequisites"></a>Pré-requisitos

- Atualizar o cliente do Gestor de Configuração no dispositivo-alvo

- Inscreva-se no dispositivo-alvo como utilizador no grupo **administradores locais.** O desbugger só concorre a administradores.

- Atualize a imagem de arranque associada à sequência de tarefas para se certificar de que tem a versão mais recente do cliente


## <a name="start-the-tool"></a>Inicie a ferramenta

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**

1. Selecione uma sequência de tarefas. No grupo de implantação da fita, selecione **Debug**.

    > [!Tip]  
    > Em alternativa, detete teda `TRUE` o **TSDebugMode** variável numa coleção ou objeto de computador para o qual a sequência de tarefas é implementada. Qualquer dispositivo que tenha este conjunto variável colocará qualquer sequência de tarefa saquires no modo de depuração.

1. Criar uma implantação de depuração. As definições de implementação são as mesmas que uma sequência de tarefa normal. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md#process).

    > [!Note]  
    > Só é possível selecionar uma pequena coleção para uma implementação de depuração. Apenas exibe coleções de dispositivos com 10 ou menos membros.

A partir da versão 1910, utilize a nova variável de sequência de **tarefas TSDebugOnError** para iniciar automaticamente o debugger quando a sequência de tarefas devolve um erro.<!-- 5012536 --> Para mais informações, consulte variáveis de sequência de [tarefas - TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError).

## <a name="use-the-tool"></a>Use a ferramenta

Quando a sequência de tarefas é executado no dispositivo, a janela Debugger de sequência de tarefas abre-se semelhante à seguinte imagem:

![Screenshot do debugger da sequência de tarefas](media/3612274-tsdebug.png)

O desbugger inclui os seguintes controlos:

- **Passo**: A partir da posição *atual,* executar apenas o próximo passo na sequência de tarefas.  

    > [!Note]  
    > Quando a sequência de tarefas está no modo de depuração, se um passo devolver um erro fatal, a sequência de tarefas não falha normalmente. Este comportamento dá-lhe a opção de voltar a tentar um passo depois de fazer uma mudança externa.

- **Executar**: Da posição *atual,* executar a sequência de tarefa normalmente até ao fim, o próximo ponto de *rutura,* ou se um passo falhar. Antes de utilizar esta ação, certifique-se de definir quaisquer pontos de rutura com a ação **set Break.**

- **Definir Corrente**: Selecione um passo no desordeiro e, em seguida, selecione **'set Current .**' Esta ação move *o* atual ponteiro para esse passo. Esta ação permite-lhe saltar degraus ou andar para trás.  

    > [!Warning]  
    > O debugger não considera o tipo de passo quando mudas a posição atual na sequência. Alguns passos podem definir variáveis de sequência de tarefas que são necessárias para avaliação de condições por etapas posteriores. Se ficar sem ordem, alguns passos podem falhar ou causar danos significativos num dispositivo. Use esta opção por sua conta e risco.  

- **set Break**: Selecione um passo no desordeiro e, em seguida, selecione **set Break**. Esta ação adiciona um ponto de *rutura* no debugger. Quando **executas** a sequência de tarefas, para ao *intervalo.*  

    - Antes de utilizar a ação **Run,** desloque os pontos de rutura.

    - A partir da versão 1910, se criares um ponto de rutura no debugger, e depois a sequência de tarefas reiniciar o computador, o debugger mantém os teus pontos de rutura após o reinício.<!-- 5012509 -->

    - Na versão 1906, os pontos de rutura não são guardados após o reinício do computador, como com o passo [restart Computer.](../understand/task-sequence-steps.md#BKMK_RestartComputer) Por exemplo, se iniciar o desbugger do Software Center para uma sequência de tarefas de imagem, não detete pausas na fase do Windows PE. Quando o computador reinicia no Windows PE, o debugger interrompe a sequência de tarefas para que possa definir as ruturas.

- **Clear All Breaks**: Remova todos os pontos de rutura.

- **Ficheiro de registo**: Abre o ficheiro de registo de sequência de tarefas atual, **smsts.log,** com [CMTrace](../../core/support/cmtrace.md). Pode ver entradas de registo quando o motor de sequência de tarefas é "À espera do desbugger".

- **Aviso cmd**: No Windows PE, abre um pedido de comando.

- **Cancelamento**: Feche o desbugger e falhe a sequência de tarefas.

- **Descontraia-se**e feche o desbugger, mas a sequência de tarefas continua a funcionar normalmente.

A janela variáveis de sequência de **tarefas** mostra os valores atuais para todas as variáveis no ambiente da sequência de tarefas. Para obter mais informações, consulte variáveis de sequência de [tarefas](../understand/task-sequence-variables.md). Se utilizar o passo variável da sequência de [tarefas definida](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) com a opção **de não exibir este valor,** o debugger não mostra o valor variável. Não se pode editar os valores variáveis no descabido.

> [!Note]
> Algumas variáveis de sequência de tarefas são apenas para uso interno, e não estão listadas na documentação de referência.

O debugger da sequência de tarefas continua a correr após um passo [do Restart Computer,](../understand/task-sequence-steps.md#BKMK_RestartComputer) mas tens de recriar quaisquer pontos de rutura. Mesmo que a sequência de tarefas possa não o exigir, uma vez que o debugger requer interação do utilizador, é necessário iniciar sessão no Windows para continuar. Se não assinar depois de uma hora para continuar a depurar, a sequência de tarefas falha.

Também entra numa sequência de tarefas para crianças com o passo da sequência de [tarefas de execução.](../understand/task-sequence-steps.md#child-task-sequence) A janela de debugger mostra os passos da sequência de tarefas da criança juntamente com a sequência de tarefa principal.


## <a name="known-issues"></a>Problemas conhecidos

Se direcionar tanto uma implementação normal como uma implementação de depuração para o mesmo dispositivo através de múltiplas implementações, o desordeiro da sequência de tarefas pode não ser lançado.


## <a name="see-also"></a>Consulte também

- [Acerca dos passos de sequência de tarefas](../understand/task-sequence-steps.md)
- [Variáveis de sequência de tarefas](../understand/task-sequence-variables.md)
- [Como utilizar variáveis de sequência de tarefas](../understand/using-task-sequence-variables.md)
- [Implementar uma sequência de tarefas](deploy-a-task-sequence.md)
