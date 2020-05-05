---
title: Gerir imagens do SO
titleSuffix: Configuration Manager
description: Aprenda os métodos para gerir as imagens os armazenadas nos ficheiros de imagem do Windows (WIM).
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 190a203494cecfd28c198197f3a582adff745265
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724119"
---
# <a name="manage-os-images-with-configuration-manager"></a>Gerir imagens de OS com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As imagens osso no 'Gestor de Configuração' são armazenadas no formato de ficheiro sinuoso (WIM) da imagem do Windows. Estas imagens são uma coleção comprimido de ficheiros de referência e pastas usadas para instalar e configurar um novo SISTEMA num computador. Muitos cenários de implantação do OS requerem uma imagem de OS.


## <a name="os-image-types"></a>Tipos de imagem osso

Pode utilizar uma [imagem de Os padrão](#default-image)ou construir a imagem de OS a partir de um computador de [referência](#bkmk_capture) que configura. Quando constrói o computador de referência, adiciona ficheiros DE, controladores, ficheiros de suporte, atualizações de software, ferramentas e aplicações ao SISTEMA. Depois captura-o para criar o ficheiro de imagem.

### <a name="default-image"></a>Imagem predefinida

Os ficheiros de instalação do Windows incluem a imagem padrão do SISTEMA. Esta imagem é uma imagem básica do OS que contém um conjunto padrão de controladores. Quando utilizar a imagem padrão do OS, utilize passos de sequência de tarefas para instalar aplicações e fazer outras configurações após a instalação do SISTEMA num dispositivo. Localize a imagem de OS `\Sources\install.wim`predefinida nos ficheiros de origem do Windows: .  

#### <a name="default-image-advantages"></a>Vantagens de imagem padrão

- O tamanho de imagem é menor do que uma imagem capturada.  

- Instalar apps e configurações com passos de sequência de tarefas é mais dinâmico. Por exemplo, altere as configurações e aplicações que instalam na sequência de tarefas, sem ter de reimagem do dispositivo.  

#### <a name="default-image-disadvantages"></a>Desvantagens de imagem padrão

- A instalação de SO pode demorar mais tempo. A instalação da aplicação e outras configurações ocorrem após o fim da instalação do S.  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a>Imagem capturada de um computador de referência

Para criar uma imagem de OS personalizada, construa um computador de referência com o SISTEMA desejado. Em seguida, instale aplicações e configure as definições. Capture a imagem DE Os do computador de referência para criar o ficheiro WIM. Construa manualmente o computador de referência ou utilize uma sequência de tarefas para automatizar alguns ou todos os passos de construção. Para mais informações, consulte [Personalizar imagens DO .](customize-operating-system-images.md)  

#### <a name="captured-image-advantages"></a>Vantagens de imagem capturadas

- A instalação pode ser mais rápida do que utilizando a imagem predefinida. Por exemplo, as aplicações podem ser pré-instaladas com a imagem de OS capturada. Depois, não é necessário instalar essas mesmas aplicações utilizando passos de sequência de tarefas.  

#### <a name="captured-image-disadvantages"></a>Desvantagens de imagem capturadas

- O tamanho da imagem é potencialmente maior do que a imagem padrão.  

- Precisa criar uma nova imagem quando necessitar de atualizações para aplicações e ferramentas.  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a>Adicione uma imagem de OS  

Antes de poder utilizar uma imagem de OS, adicione-a ao site do Gestor de Configuração.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de **Imagens do Sistema Operativo.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione **Adicionar Imagem do Sistema Operativo**. Esta ação inicia o Assistente de Imagem do Sistema Operativo Add.  

3. Na página Fonte de **Dados,** especifique as seguintes informações:

    - **Caminho** da rede para o ficheiro de imagem SO. Por exemplo, `\\server\share\path\image.wim`.

    - Extrair um índice de **imagem específico do ficheiro WIM especificado** e, em seguida, selecionar um índice de imagem da lista.<!--3719699--> A partir da versão 1902, esta opção importa automaticamente um único índice em vez de todos os índices de imagem no ficheiro. A utilização desta opção resulta num ficheiro de imagem mais pequeno e numa manutenção offline mais rápida. Também suporta o processo de otimização do [serviço de imagem,](#bkmk_resetbase)para um ficheiro de imagem menor após a aplicação de atualizações de software.  

        > [!Note]  
        > O Gestor de Configuração não modifica o ficheiro de imagem de origem. Cria um novo ficheiro de imagem no mesmo diretório de origem.
        >
        > Este processo de extração pode falhar em ficheiros de imagem extremamente grandes, por exemplo, mais de 60 GB. O erro DISM é `Not enough storage is available to process this command.` a linha de comando que o Gestor de Configuração utiliza está no smsprov.log e dism.log. Executar manualmente o mesmo comando e, em seguida, importar a imagem.<!-- SCCMDocs-pr issue 3502 -->  

    - A partir da versão 1906, se quiser pré-cache conteúdo num cliente, especifique a **Arquitetura** e **Linguagem** da imagem. Para mais informações, consulte o [conteúdo pré-cache da Configure](../deploy-use/configure-precache-content.md).<!--4224642-->  

4. Na página **Geral,** especifique as seguintes informações. Esta informação é útil para fins de identificação quando você tem mais do que uma imagem de SO.  

    - **Nome**: Um nome único para a imagem. Por predefinição, o nome vem do nome do ficheiro WIM.  

    - **Versão**: Um identificador de versão opcional. Esta propriedade não precisa ser a versão soda da imagem. É frequentemente a versão da sua organização para o pacote.  

    - **Comentário**: Uma breve descrição opcional.  

5. Conclua o assistente.  

Para o equivalente de cmdlet PowerShell deste assistente de consola, consulte [New-CMOperatingSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps).

Em seguida, distribua a imagem de So para pontos de distribuição.  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a>Distribuir conteúdo para pontos de distribuição  

Distribua as imagens do OS para pontos de distribuição iguais aos de outros conteúdos. Antes de implementar a sequência de tarefas, distribua a imagem de OS para pelo menos um ponto de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a>Prepare a imagem de OS para implementações multicast  

Utilize implementações multicast para permitir que mais de um computador descarregue simultaneamente uma imagem de SO. A imagem é multicast para os clientes pelo ponto de distribuição, em vez de cada cliente descarregar uma cópia da imagem do ponto de distribuição sobre uma ligação separada. Quando escolher o método de implementação do OS para [utilizar o multicast para implementar o Windows sobre a rede,](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)configure a imagem de OS para suportar o multicast. Em seguida, distribua a imagem para um ponto de distribuição multicast.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de **Imagens do Sistema Operativo.**  

2. Selecione a imagem DE Os que pretende distribuir para um ponto de distribuição multicast.  

3. No separador **Casa** da fita, no grupo **Propriedades,** selecione **Propriedades**.  

4. Mude para o separador **Definições** de Distribuição e configure as seguintes opções:  

    - **Permitir que este pacote seja transferido através de multicast (apenas WinPE)**: Selecione esta opção para O Gestor de Configuração para implementar simultaneamente imagens OS utilizando multicast.  

    - **Criptografe pacotes multicast**: Especifique se o site encripta a imagem antes de ser enviada para o ponto de distribuição. Se a imagem contiver informações sensíveis, utilize esta opção. Se a imagem não estiver encriptada, o seu conteúdo é visível em texto claro na rede. Em seguida, um utilizador não autorizado poderia intercetar e ver o conteúdo da imagem.  

    - **Transferir este pacote apenas através de multicast**: especifique se pretende que o ponto de distribuição implemente a imagem apenas durante uma sessão multicast.  

         Se selecionar **transferir este pacote apenas através de multicast,** também deve especificar a opção de implementação da sequência de tarefas para descarregar conteúdo localmente quando necessário pela sequência de **tarefas de execução**. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](../deploy-use/deploy-a-task-sequence.md).  

5. Selecione **OK** para guardar as definições e fechar as propriedades da imagem.  
