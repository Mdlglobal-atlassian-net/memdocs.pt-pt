---
title: Criar suportes de dados de arranque
titleSuffix: Configuration Manager
description: Utilize suportes de arranque no 'Gestor de Configuração' para instalar uma nova versão do Windows ou substituir um computador.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44c570fc2844093b190e388727dd3799bcbcdb92
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714053"
---
# <a name="create-bootable-media"></a>Criar suportes de dados de arranque

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os suportes de arranque no 'Gestor de Configuração' contêm a imagem de arranque, comandos de prestação opcionais e ficheiros associados e ficheiros Do Gestor de Configuração. Utilize meios pré-encenados para os seguintes cenários de implantação do SO:  

- [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Substituir um computador existente e transferir definições](replace-an-existing-computer-and-transfer-settings.md)  


## <a name="usage"></a>Utilização

O seguinte processo ocorre quando inicia os meios de comunicação instáveis:

1. O computador de destino começa
1. Liga-se à rede
1. Recupera o seguinte conteúdo do site:
    - A sequência de tarefas especificada
    - Imagem de OS
    - Qualquer outro conteúdo necessário

Como a sequência de tarefas não está nos meios de comunicação, pode alterar a sequência de tarefas ou o conteúdo sem ter de recriar os meios de comunicação.

Os pacotes nos meios de comunicação não estão encriptados. Para se certificar de que o conteúdo do pacote está protegido de utilizadores não autorizados, tome as medidas de segurança adequadas. Por exemplo, adicione uma palavra-passe aos meios de comunicação.

## <a name="prerequisites"></a>Pré-requisitos

Antes de criar meios de arranque utilizando o Assistente de Mídia create Task Sequence, certifique-se de que todas estas condições estão satisfeitas.

### <a name="boot-image"></a>Imagem de arranque

Considere os seguintes pontos sobre a imagem de arranque que utiliza na sequência de tarefas para implantar o Sistema Operativo:

- A arquitetura da imagem de arranque deve ser adequada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.
- Certifique-se de que a imagem de arranque contém os controladores de rede e armazenamento que são necessários para fornecer o computador de destino.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Criar uma sequência de tarefas para implantar um SO

Como parte dos meios de arranque, especifique a sequência de tarefas para implantar o Sistema Operativo. Para mais informações, consulte Criar uma sequência de [tarefas para instalar um OS](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas

Distribua todos os conteúdos que a sequência de tarefas requer para pelo menos um ponto de distribuição. Este conteúdo inclui a imagem de arranque e outros ficheiros prestart associados. O assistente recolhe o conteúdo a partir do ponto de distribuição quando cria os meios de arranque.

A sua conta de utilizador precisa, pelo **menos, de ler** os direitos de acesso à biblioteca de conteúdos nesse ponto de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a pen USB amovível

Se estiver a utilizar uma unidade USB amovível, ligue-a ao computador onde executa o assistente de Create Task Sequence Media. A unidade USB deve ser detetável pelo Windows como um dispositivo de remoção. Quando cria o suporte de dados, o assistente escreve diretamente na pen USB.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída

Antes de executar o Assistente de Mídia de Sequência de Tarefas Criar meios de comunicação para um conjunto de CD ou DVD, crie uma pasta para os ficheiros de saída que cria. Os meios de comunicação que cria para um conjunto de CD ou DVD são escritos como um . Ficheiro ISO diretamente na pasta.


## <a name="process"></a>Processo

 > [!NOTE]  
 > Para os ambientes PKI, uma vez que a Root CA é especificada no local primário, certifique-se de que os meios de arranque são criados no local principal. O site CAS não dispõe da informação Root CA para criar corretamente os meios de arranque.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione Criar Meios de Sequência de **Tarefas**. Esta ação inicia o Assistente de Mídia de Sequência de Tarefas Create Task Sequence.  

3. Na página **Select Media Type,** especifique as seguintes opções:  

    - Selecione **Suporte de dados de arranque**.  

    - Opcionalmente, se pretender apenas permitir que o Sistema operativo seja implantado sem necessitar de entrada do utilizador, selecione Permitir a **implementação do sistema operativo sem supervisão**.  

        > [!IMPORTANT]  
        > Ao selecionar esta opção, o utilizador não é solicitado para informações de configuração de rede ou para sequências de tarefas opcionais. Se configurar os meios de proteção de palavras-passe, o utilizador ainda é solicitado para obter uma palavra-passe.  

4. Na página de **Media Management,** especifique uma das seguintes opções:  

    - **Meios dinâmicos**: Permitir que um ponto de gestão redirecione os meios de comunicação para outro ponto de gestão, com base na localização do cliente nos limites do site.  

    - Meios de comunicação **baseados no site**: Os meios de comunicação apenas contactam o ponto de gestão especificado.  

5. Na página **Media Type,** especifique se os meios de comunicação são uma **unidade USB amovível** ou um **conjunto de CD/DVD**. Em seguida, configure as seguintes opções:  

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

6. Na página **de Segurança,** especifique as seguintes opções:  

    - **Ativar suporte de computador desconhecido**: Permitir que os meios de comunicação implementem um SISTEMA para um computador que não seja gerido pelo Gestor de Configuração. Não há registo destes computadores na base de dados do Diretor de Configuração. Para mais informações, consulte [Prepare-se para implementações de computadordesconhecidas](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Proteja os meios com uma palavra-passe**: Introduza uma senha forte para ajudar a proteger os meios de acesso não autorizados. Quando especificar uma palavra-passe, o utilizador terá de fornecer essa palavra-passe para utilizar o suporte de dados de arranque.  

        > [!IMPORTANT]  
        > Como procedimento de segurança recomendado, atribua sempre uma palavra-passe para ajudar a proteger o suporte de dados de arranque.  

    - Para comunicações HTTP, selecione **Criar certificado de mídia auto-assinado**. Em seguida, especifique a data de início e expiração do certificado.  
    
      > [!NOTE]  
      > Se selecionar esta opção, os pontos de gestão HTTPS não estarão disponíveis para seleção na página de **imagem Boot** deste assistente.

    - Para comunicações HTTPS, selecione **certificado Import PKI**. Em seguida, especifique o certificado de importação e a sua palavra-passe.  

        Para obter mais informações sobre este certificado de cliente que as imagens de arranque utilizem, consulte [os requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Afinidade do dispositivo do utilizador**: Para apoiar a gestão centrada no utilizador no Gestor de Configuração, especifique como pretende que os meios de comunicação associem os utilizadores ao computador de destino. Para obter mais informações sobre como a implementação do OS suporta a afinidade do dispositivo do utilizador, consulte [os utilizadores associados com um computador](../get-started/associate-users-with-a-destination-computer.md)de destino .  

        - **Permitir a finidade**do dispositivo do utilizador com a aprovação automática : Os meios de comunicação associam automaticamente os utilizadores ao computador de destino. Esta funcionalidade baseia-se nas ações da sequência de tarefas que implementa o SISTEMA. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino quando implementa o S para o computador de destino.  

        - **Permitir a afinidade do utilizador pendente da aprovação do administrador**: Os meios de comunicação associam os utilizadores ao computador de destino após a aprovação. Esta funcionalidade baseia-se no âmbito da sequência de tarefas que implementa o SISTEMA. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino, mas aguarda a aprovação de um utilizador administrativo antes da implementação do SISTEMA.  

        - **Não permita a finção**do dispositivo do utilizador : Os meios de comunicação não associam os utilizadores ao computador de destino. Neste cenário, a sequência de tarefas não associa os utilizadores ao computador de destino quando implementa o SISTEMA.  

7. Na página de **imagem Boot,** especifique as seguintes opções:  

    > [!IMPORTANT]  
    > A arquitetura da imagem de arranque que distribui deve ser adequada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.  

    - **Imagem de arranque**: Selecione a imagem de arranque para iniciar o computador de destino.  

    - **Ponto de distribuição**: Selecione o ponto de distribuição que tem a imagem de arranque. O assistente obtém a imagem de arranque do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        > A sua conta de utilizador precisa, pelo menos, **de ler** permissões para a biblioteca de conteúdos no ponto de distribuição.  

    - **Ponto de gestão**: Apenas para *meios baseados no site,* selecione um ponto de gestão de um site primário.  

    - **Pontos de gestão associados**: Apenas para *meios dinâmicos*, selecione os pontos de gestão do site primário a utilizar e uma ordem prioritária para a comunicação inicial.  
    
        > [!NOTE]  
        > Os pontos de gestão ativados HTTPS só serão apresentados quando um certificado PKI for especificado na página de **Segurança** deste assistente.  

8. Na página de **Personalização,** especifique as seguintes opções:  

    - Adicione quaisquer variáveis que a sequência de tarefas utilize.  

    - **Ativar**o comando prestart : Especifique quaisquer comandos prestart que pretenda executar antes da sequência de tarefas ser executada. Os comandos prestart são um script ou um executável que pode interagir com o utilizador no Windows PE antes da sequência de tarefas ser executada. Para mais informações, consulte os [comandos da Prestat para meios](../understand/prestart-commands-for-task-sequence-media.md)de sequência de tarefas .  

        > [!TIP]  
        > Durante a criação de meios de comunicação, a sequência de tarefas escreve o id do pacote e a linha de comando prestart, incluindo o valor para quaisquer variáveis de sequência de tarefas, para o ficheiro **CreateTSMedia.log** no computador que executa a consola Do Gestor de Configuração. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

        Se o comando prestart necessitar de qualquer conteúdo, selecione a opção **de Incluir ficheiros para o comando prestart**.  

9. Conclua o assistente.  


## <a name="alternate-method"></a>Método alternativo

Pode criar suportes de arranque numa unidade USB amovível quando a unidade não está ligada ao computador que executa a consola Do Gestor de Configuração.

1. [Crie os meios de arranque da sequência](#process)de tarefas . Na página do **tipo Media,** selecione **conjunto de CD/DVD**. O assistente escreve os ficheiros de saída para o local que especifica. Por exemplo: `\\servername\folder\outputfile.iso`.  

2. Prepare a unidade USB amovível. A unidade deve ser formatada, vazia e sabotável.

3. Monte o ISO a partir da localização da partilha e transfira os ficheiros da ISO para a unidade USB.


## <a name="next-steps"></a>Passos seguintes

[Utilizar suportes de dados de arranque para implementar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  
