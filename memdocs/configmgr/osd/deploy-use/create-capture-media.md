---
title: Criar suportes de dados de captura
titleSuffix: Configuration Manager
description: Utilize suportes de captura no Gestor de Configuração para capturar uma imagem de OS a partir de um computador de referência.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbbec355356a74d61f263fe2b16d44c0cd15ba80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711148"
---
# <a name="create-capture-media"></a>Criar suportes de dados de captura

*Aplica-se a: Gestor de Configuração (ramo atual)*

Capturar meios no Gestor de Configuração permite-lhe capturar uma imagem de OS a partir de um computador de referência. Os meios de captura contêm a imagem de arranque que inicia o computador de referência e a sequência de tarefas que captura a imagem de OS. Utilize meios de captura para o cenário para criar uma sequência de [tarefas para capturar um OS](create-a-task-sequence-to-capture-an-operating-system.md).  


## <a name="prerequisites"></a>Pré-requisitos

Antes de criar meios de captura utilizando o Assistente de Mídia create Task Sequence, certifique-se de que todas estas condições estão satisfeitas.

### <a name="boot-image"></a>Imagem de arranque

Considere os seguintes pontos sobre a imagem de arranque que utiliza na sequência de tarefas para implantar o Sistema Operativo:

- A arquitetura da imagem de arranque deve ser adequada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.
- Certifique-se de que a imagem de arranque contém os controladores de rede e armazenamento que são necessários para fornecer o computador de destino.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas

Distribua todos os conteúdos que a sequência de tarefas requer para pelo menos um ponto de distribuição. Este conteúdo inclui a imagem de arranque, a imagem do OS e outros ficheiros associados. O assistente recolhe o conteúdo a partir do ponto de distribuição quando cria os meios de captura.

A sua conta de utilizador precisa, pelo **menos, de ler** os direitos de acesso à biblioteca de conteúdos nesse ponto de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a pen USB amovível

Se estiver a utilizar uma unidade USB amovível, ligue-a ao computador onde executa o assistente de Create Task Sequence Media. A unidade USB deve ser detetável pelo Windows como um dispositivo de remoção. Quando cria o suporte de dados, o assistente escreve diretamente na pen USB.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída

Antes de executar o Assistente de Mídia de Sequência de Tarefas Criar meios de comunicação para um conjunto de CD ou DVD, crie uma pasta para os ficheiros de saída que cria. Os meios de comunicação que cria para um conjunto de CD ou DVD são escritos como um . Ficheiro ISO diretamente na pasta.


## <a name="process"></a>Processo

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione Criar Meios de Sequência de **Tarefas**. Esta ação inicia o Assistente de Mídia de Sequência de Tarefas Create Task Sequence.  

3. Na página **Select Media Type,** selecione Capturar meios de **comunicação**.  

4. Na página **Media Type,** especifique se os meios de comunicação são uma **unidade USB amovível** ou um **conjunto de CD/DVD**. Em seguida, configure as seguintes opções:  

    > [!IMPORTANT]  
    > Os meios de comunicação usam um sistema de ficheiros FAT32. Não é possível criar suportes numa unidade USB cujo conteúdo contém um ficheiro com mais de 4 GB de tamanho.  

    - Se selecionar unidade **USB amovível,** selecione a unidade onde pretende armazenar o conteúdo.  

        - **Formato unidade USB amovível (FAT32) e faça o arranque:** Por padrão, deixe o Gestor de Configuração preparar a unidade USB. Muitos dispositivos UEFI mais recentes requerem uma partição FAT32 sabotável. No entanto, este formato também limita o tamanho dos ficheiros e a capacidade global da unidade. Se já formatado e configurar a unidade amovível, desative esta opção.

    - Se selecionar **o conjunto de CD/DVD,** especifique a capacidade dos meios de comunicação (tamanho dos meios de**comunicação**) e o nome e o caminho do ficheiro de saída **(ficheiro Media**). O assistente escreve os ficheiros de saída nesta localização. Por exemplo: `\\servername\folder\outputfile.iso`  

        Se a capacidade dos meios de comunicação for demasiado pequena para armazenar todo o conteúdo, cria vários ficheiros. Em seguida, você precisa armazenar o conteúdo em vários CDs ou DVDs. Quando requer vários ficheiros de meios de comunicação, o Gestor de Configuração adiciona um número de sequência ao nome de cada ficheiro de saída que cria.  

        > [!IMPORTANT]  
        > Se selecionar uma imagem .iso existente, o Assistente de Criação de Suporte de Dados da Sequência de Tarefas elimina essa imagem da unidade ou partilha logo que avança para a página seguinte do assistente. A imagem existente será eliminada, mesmo que em seguida cancele o assistente.  

    - **Pasta de encenação**<!--1359388-->: O processo de criação de meios de comunicação pode requerer muito espaço de condução temporária. Por defeito, esta localização é `%UserProfile%\AppData\Local\Temp`semelhante ao seguinte caminho: . A partir da versão 1902, para lhe dar maior flexibilidade com onde armazenar estes ficheiros temporários, altere este valor para outra unidade e caminho.  

    - **Etiqueta dos meios de comunicação**<!--1359388-->: A partir da versão 1902, adicione um rótulo aos meios de sequência de tarefas. Esta etiqueta ajuda-o a identificar melhor os meios de comunicação depois de o criar. O valor predefinido é `Configuration Manager`. Este campo de texto aparece nos seguintes locais:  

        - Se montar um ficheiro ISO, o Windows apresenta esta etiqueta como o nome da unidade montada  

        - Se forformar uma unidade USB, utiliza os primeiros 11 caracteres da etiqueta como nome  

        - O Gestor de Configuração `MediaLabel.txt` escreve um ficheiro de texto chamado à raiz dos meios de comunicação. Por predefinição, o ficheiro inclui `label=Configuration Manager`uma única linha de texto: . Se personalizar a etiqueta para meios de comunicação, esta linha utiliza a sua etiqueta personalizada em vez do valor predefinido.  

    - **Incluir ficheiro autorun.inf nos meios de comunicação**<!-- 4090666 -->: A partir da versão 1906, o Gestor de Configuração não adiciona um ficheiro autorun.inf por padrão. Este ficheiro é geralmente bloqueado por produtos antimalware. Para obter mais informações sobre a funcionalidade AutoRun do Windows, consulte [criar uma aplicação CD-ROM ativada por AutoRun](https://docs.microsoft.com/windows/desktop/shell/autoplay). Se ainda necessário para o seu cenário, selecione esta opção para incluir o ficheiro.  

5. Na página de **imagem Boot,** especifique as seguintes opções:  

    > [!IMPORTANT]  
    > A arquitetura da imagem de arranque que distribui deve ser adequada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.  

    - **Imagem de arranque**: Selecione a imagem de arranque para iniciar o computador de destino.  

    - **Ponto de distribuição**: Selecione o ponto de distribuição que tem a imagem de arranque. O assistente obtém a imagem de arranque do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        > A sua conta de utilizador precisa, pelo menos, **de ler** permissões para a biblioteca de conteúdos no ponto de distribuição.  

6. Conclua o assistente.  


## <a name="next-steps"></a>Passos seguintes

[Criar uma sequência de tarefas para capturar um SO](create-a-task-sequence-to-capture-an-operating-system.md)
