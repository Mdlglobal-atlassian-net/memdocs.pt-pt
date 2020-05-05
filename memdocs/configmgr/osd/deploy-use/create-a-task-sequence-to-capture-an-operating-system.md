---
title: Criar uma sequência de tarefas para capturar um SO
titleSuffix: Configuration Manager
description: Uma sequência de tarefas de construção e captura constrói um computador de referência que pode incluir controladores específicos e atualizações de software juntamente com o SISTEMA.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ceb63560c6000b1a76116d0791c98219a66066b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723069"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>Criar uma sequência de tarefas para capturar um SO

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando utiliza uma sequência de tarefas para implantar um SISTEMA num computador no 'Gestor de Configuração', o computador instala a imagem de OS que especifica na sequência de tarefas. Pode personalizar a imagem do OS para que inclua controladores específicos, aplicações e atualizações de software. Primeiro utilize uma sequência de tarefas de construção e captura para construir um computador de referência. Em seguida, capture a imagem de OS desse computador de referência. Se já tem um computador de referência disponível para capturar, crie uma sequência de tarefas personalizada para capturar o SISTEMA.

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a>Sobre a sequência de tarefas de construção e captura

A sequência de tarefas de construção e captura:

- Divisórias e formatos do computador de referência
- Instala o SO
- Instala o cliente do Gestor de Configuração
- Instala aplicações
- Aplica atualizações de software
- Captura o SISTEMA a partir do computador de referência

Os pacotes associados à sequência de tarefas, tais como aplicações, devem estar disponíveis nos pontos de distribuição antes de implementar a sequência de tarefas de construção e captura.

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a>Requisitos

Antes de criar uma sequência de tarefas para instalar um SISTEMA, certifique-se de que os seguintes componentes estão no lugar:  

### <a name="required"></a>Necessário

- [Imagem de arranque](../get-started/manage-boot-images.md)

- [Imagem de OS](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>Necessário (se utilizado)

- [Pacotes](../get-started/manage-drivers.md) de controlador que contenham os controladores Windows necessários para suportar hardware no computador de referência. Para mais informações sobre os passos de sequências de tarefas para gerir controladores, consulte [Use task sequences to install device drivers](../get-started/manage-drivers.md#BKMK_TSDrivers).

- [Atualizações de software](../../sum/get-started/synchronize-software-updates.md)

- [Aplicações](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> Criar uma sequência de tarefas de compilação e captura

Utilize o procedimento seguinte para utilizar uma sequência de tarefas para construir um computador de referência e capturar o SISTEMA.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

1. No separador **Home** da fita, no grupo **Criar,** selecione Criar sequência de **tarefas** para iniciar o Assistente de Sequência de Tarefas Criar.  

1. Na página **Criar uma Nova Sequência de Tarefas** , selecione **Construir e capturar uma imagem do sistema operativo de referência**.  

1. Na página **informação** da sequência de tarefas, especifique as seguintes definições:  

    - **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    - **Descrição**: Especificar uma descrição opcional para a sequência de tarefas. Por exemplo, descreva o SISTEMA que a sequência de tarefas cria.

    - **Imagem de arranque**: Especifique a imagem de arranque a utilizar com esta sequência de tarefas.  

        > [!IMPORTANT]  
        > A arquitetura da imagem de arranque deve ser compatível com a arquitetura de hardware do computador de destino.  

1. Na página De instalar o **Windows,** especifique as seguintes definições:  

    - **Pacote de imagem**: Especifique o pacote de imagem OS, que contém os ficheiros necessários para instalar o SISTEMA.  

    - **Índice de imagem**: Especifique o índice do S O para instalar na imagem. Se a imagem do OS contiver várias versões, selecione a versão que pretende instalar.  

    - **Chave do produto**: Se necessário, especifique a chave do produto para a instalação do Sistema operativo Windows. Pode especificar chaves de licenciamento em volume codificadas e chaves de produto padrão. Se utilizar uma chave de produto não codificada, separe cada`-`grupo de cinco caracteres com um traço (). Por exemplo: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Modo**de licenciamento do servidor : Se necessário, especifique que a licença do servidor é **por assento,** **por servidor,** ou que nenhuma licença é especificada. Se a licença do servidor for **Por servidor**, especifique também o número máximo de ligações de servidor.  

    - Especifique como configurar a conta de administrador para o Sistema Operativo implantado:  

        - **Gera a palavra-passe do administrador local aleatoriamente e desative a conta em todas as plataformas suportadas**: Criar uma senha aleatória para a conta de administrador local. Desative a conta quando o Windows estiver configurado.

        - **Ative a conta e especifique a palavra-passe do administrador local**: Utilize a mesma palavra-passe para a conta do administrador local em todos os computadores onde implementa este SISTEMA.

1. Na página **da Rede Configurar,** especifique as seguintes definições:

    - **Junte-se**a um grupo de trabalho : Especifique se deve adicionar o computador de destino a um grupo de trabalho quando o SISTEMA estiver implantado.  

    - **Junte-se**a um domínio : Especifique se adicionar o computador de destino a um domínio quando o SISTEMA estiver implantado. Em **Domínio**, especifique o nome do domínio.  

        > [!IMPORTANT]  
        > Pode navegar para localizar domínios na floresta local. Especifique o nome de domínio para uma floresta remota.

        Também pode especificar uma unidade organizacional (UO). Esta definição é opcional e especifica o nome distinto LDAP X.500 da OU para criar a conta de computador, se ainda não existir.  

    - **Conta**: especifique o nome de utilizador e palavra-passe da conta que tem permissões para aderir ao domínio especificado. Por `domain\user` exemplo: `%variable%`ou .  

        > [!IMPORTANT]  
        > Se pretender migrar as definições de domínio ou as definições do grupo de trabalho durante a implementação, certifique-se de que introduz as credenciais de domínio apropriadas aqui.  

1. Na página 'Gestor de **Configuração de Instalação',** especifique o pacote de cliente do Gestor de Configuração. Este pacote contém os ficheiros de origem para instalar o cliente do Gestor de Configuração. Especifique também quaisquer propriedades adicionais necessárias para instalar o cliente.  

    Para mais informações, consulte sobre as propriedades de [instalação do cliente.](../../core/clients/deploy/about-client-installation-properties.md)

1. Na página **Incluir Atualizações,** especifique se deve instalar atualizações de software necessárias, todas as atualizações de software ou nenhuma atualização de software. Se especificar para instalar atualizações de software, o Gestor de Configuração instala apenas as atualizações de software que são direcionadas para as coleções de que o computador de destino é membro.  

1. Na página De instalação de **aplicações,** especifique as aplicações a instalar no computador de destino. Se especificar várias aplicações, poderá também especificar que a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

    > [!NOTE]
    > A página de **Preparação** do Sistema aparece a seguir no assistente, mas já não é usada. Selecione **Seguinte** para continuar.

1. Na página **Images Properties,** especifique as seguintes definições para a imagem de OS:

    - **Criado por**: Especifique o nome do utilizador para notar como criador da imagem de OS.  

    - **Versão**: Especifique o número da sua versão associado à imagem de OS. Este atributo não precisa de ser a versão S, uma vez que o site armazena esse valor separadamente.

    - **Descrição**: Especifique a sua descrição da imagem de OS.  

1. Na página **Imagem de Captura,** especifique as seguintes definições:

    - **Caminho**: Especifique uma pasta de rede partilhada onde o Gestor de Configuração deve armazenar o ficheiro de imagem de saída (.wim). Este ficheiro contém a imagem de OS que é baseada nas definições que especifica neste assistente. Se especificar uma pasta que contenha uma . Ficheiro WIM, está escrito.  

    - **Conta**: especifique a conta do Windows que tem permissões para a partilha de rede onde está armazenada a imagem.  

1. Conclua o assistente.  

Para adicionar passos adicionais à sequência de tarefas, selecione-a e escolha **editar**. Para obter mais informações sobre como editar uma sequência de tarefas, consulte [Utilize o editor da sequência de tarefas](../understand/task-sequence-editor.md).  

Implemente a sequência de tarefas num computador de referência de uma das seguintes formas:  

- Se o computador de referência já for um cliente do Gestor de Configuração, implemente a sequência de tarefas de construção e captura para uma coleção que contenha o computador de referência. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md).

- Se o computador de referência não for um cliente do Gestor de Configuração, ou se pretender executar manualmente a sequência de tarefas no computador de referência, utilize o Assistente de Mídia de Sequência de **Tarefas Create** para criar suportes de arranque. Para mais informações, consulte [Criar meios de sapateado.](create-bootable-media.md)  

Depois de capturar a imagem, pode implantá-la para outros computadores. Para obter mais informações sobre como implementar a imagem de OS capturada, consulte Criar uma sequência de [tarefas para instalar um OS](create-a-task-sequence-to-install-an-operating-system.md).  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a>Captura de um computador de referência existente

Quando já tiver um computador de referência pronto a capturar, crie uma sequência de tarefas que apenas capture o SISTEMA a partir do computador de referência. Utilize o passo de sequência de imagem do **sistema operativo de captura** para capturar uma ou mais imagens de um computador de referência e armazená-las num ficheiro de imagem (.wim) na parte de rede especificada. Inicie o computador de referência no Windows PE com uma imagem de arranque. A sequência de tarefas captura cada disco rígido no computador de referência como uma imagem separada dentro do ficheiro .wim. Se o computador referenciado tiver várias unidades, o ficheiro .wim resultante contém uma imagem separada para cada volume. Apenas captura volumes que são formatados como NTFS ou FAT32. Salta volumes com outros formatos ou volumes USB.  

Utilize o seguinte procedimento para capturar uma imagem de OS a partir de um computador de referência existente:

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

1. No separador **Home** da fita, no grupo **Criar,** selecione Criar sequência de **tarefas**. Esta ação inicia o Assistente de Sequência de Tarefas Create.  

1. Na página **Criar uma Nova Sequência de Tarefas** , selecione **Criar uma nova sequência de tarefas personalizada**.  

1. Na página **informação** da sequência de tarefas, especifique um nome para a sequência de tarefas. Adicione opcionalmente uma descrição para a sequência de tarefas.  

1. Especifique uma imagem de arranque para a sequência de tarefas. O Gestor de Configuração utiliza esta imagem de arranque para iniciar o computador de referência com o Windows PE. Para mais informações, consulte [Gerir imagens](../get-started/manage-boot-images.md)de arranque .  

1. Conclua o assistente.  

1. No nó de sequências de **tarefas,** selecione a nova sequência de tarefas. Em seguida, no separador **Home** da fita, no grupo sequência de **tarefas,** selecione **Editar**. Esta ação abre o editor da sequência de tarefas.  

1. Se o cliente do Gestor de Configuração estiver instalado no computador de referência:

    Vá ao menu **Adicionar,** selecione **Imagens,** e depois escolha [Prepare o Cliente ConfigMgr para capturar](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Este passo generaliza o cliente do Gestor de Configuração no computador de referência.

    > [!Note]  
    > A sequência de tarefas não suporta desinstalar o cliente do Gestor de Configuração.

1. Vá ao menu **Adicionar,** selecione **Imagens,** e escolha [Preparar windows para capturar](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Este passo executa o Sysprep e, em seguida, reinicia o computador para a imagem de arranque do Windows PE especificada para a sequência de tarefas. Para que esta ação esteja concluída com sucesso, não se junte ao computador de referência a um domínio.

1. Vá ao menu **Adicionar,** selecione **Imagens,** e escolha [capturar imagem do sistema operativo](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage). Este passo só vai desde o Windows PE para capturar os discos rígidos no computador de referência. Configure as seguintes definições:

    - **Nome** e **Descrição**: opcionalmente, pode alterar o nome do passo da sequência de tarefas e fornecer uma descrição.  

    - **Destino**: especifique uma pasta de rede partilhada onde guardar o ficheiro .WIM resultante. Este ficheiro contém a imagem DE Os com base nas definições que especifica utilizando este assistente. Se especificar uma pasta que contenha uma . Ficheiro WIM, está escrito.  

    - **Descrição,** **Versão,** e **Criado por**: Opcionalmente, fornecer detalhes sobre a imagem para capturar.  

    - **Conta para captura da imagem do sistema operativo**: especifique a conta do Windows que tem permissões para a partilha de rede especificada. Selecione **Definir** para especificar o nome dessa conta Windows.  

Selecione **OK** para guardar as suas alterações e fechar o editor de sequência de tarefas.  

Implemente a sequência de tarefas num computador de referência de uma das seguintes formas:  

- Se o computador de referência já for um cliente do Gestor de Configuração, implemente a sequência de tarefas de captura para uma coleção que contenha o computador de referência. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md).

- Se o computador de referência não for um cliente do Gestor de Configuração, ou se pretender executar manualmente a sequência de tarefas no computador de referência, utilize o Assistente de Mídia de Sequência de **Tarefas Create** para criar suportes de captura. Para mais informações, consulte [Criar meios de captura.](create-capture-media.md)  

Depois de capturar a imagem, pode implantá-la para outros computadores. Para obter mais informações sobre como implementar a imagem de OS capturada, consulte Criar uma sequência de [tarefas para instalar um OS](create-a-task-sequence-to-install-an-operating-system.md).

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a>Sequência de tarefas de exemplo

Utilize a tabela seguinte como guia enquanto cria uma sequência de tarefas que constrói e captura uma imagem de OS. A tabela ajuda-o a decidir a sequência geral para os passos da sua sequência de tarefas, e como organizar e estruturar esses passos em grupos lógicos. A sequência de tarefas que cria pode variar a partir desta amostra. Pode conter mais ou menos passos e grupos.

> [!NOTE]  
> Utilize sempre o Assistente de Criação de Sequência de Tarefas para criar este tipo de sequência de tarefas.
>
> O assistente adiciona passos à sequência de tarefas com nomes ligeiramente diferentes que o que veria se adicionasse manualmente os mesmos passos.

### <a name="group-build-the-reference-machine"></a>Grupo: Construir a Máquina de Referência

Este grupo contém as ações necessárias para compilar um computador de referência.

|Passo da sequência de tarefas|Descrição|  
|-------------------------------|---------------|  
|**Reiniciar no Windows PE**|Reinicie o computador de destino para a imagem de arranque atribuída à sequência de tarefas. Este passo mostra uma mensagem ao utilizador de que o computador será reiniciado para que a instalação possa continuar.<br /><br />Este passo utiliza a `_SMSTSInWinPE` variável de sequência de tarefas apenas de leitura. Se o valor associado `false`for igual a , então o passo da sequência de tarefas continua.|
|**Particionar Disco 0 - BIOS**|Partição e formatar o disco rígido no computador de destino no modo BIOS. O número do `0`disco predefinido é .<br /><br />Este passo utiliza várias variáveis de sequência de tarefas apenas de leitura. Por exemplo, só funciona se a cache do cliente do Gestor de Configuração não existir, e não funciona se o computador estiver configurado para UEFI.|
|**Particionar Disco 0 - UEFI**|Partição e formatar o disco rígido no computador de destino no modo UEFI. O número do `0`disco predefinido é .<br /><br />Este passo utiliza várias variáveis de sequência de tarefas apenas de leitura. Por exemplo, só funciona se a cache do cliente do Gestor de Configuração não existir, e só funciona se o computador estiver configurado para UEFI.|
|**Aplicar Sistema Operativo**|Instale a imagem de OS especificada no computador de destino. Este passo elimina primeiro todos os ficheiros do volume, com a lém dos ficheiros de controlo específicos do Gestor de Configuração. Em seguida, aplica todas as imagens de volume contidas no ficheiro WIM ao correspondente volume sequencial de disco no computador-alvo.|
|**Aplicar Definições do Windows**|Configure as definições do Windows para o computador de destino.|
|**Aplicar Definições de Rede**|Especifique as informações de configuração da rede ou do grupo de trabalho para o computador de destino.|
|**Aplicar Controladores de Dispositivo**|Combine e instale os controladores como parte desta implementação do SISTEMA. Para mais informações, consulte [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).<br /><br />Este passo utiliza a `_SMSTSMediaType` variável de sequência de tarefas apenas de leitura. Se o valor associado não `FullMedia`for igual, este passo não corre.|
|**Configurar windows e configurar gestor**|Instale o software cliente do Gestor de Configuração. O Gestor de Configuração instala e regista o cliente do Gestor de Configuração GUID. Inclua quaisquer propriedades de **instalação necessárias.**|
|**Instalar Atualizações**|Especifique como as atualizações de software são instaladas no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que este passo corra. Nessa altura, a avaliação é semelhante a qualquer outro cliente gerido pelo Gestor de Configuração. Para mais informações, consulte [Instalar Atualizações de Software](../understand/install-software-updates.md).<br /><br />Este passo utiliza a `_SMSTSMediaType` variável de sequência de tarefas apenas de leitura. Se o valor associado não `FullMedia`for igual, este passo não corre.|
|**Instalar Aplicações**|Especifica quaisquer aplicações para instalar no computador de referência.|

### <a name="group-capture-the-reference-machine"></a>Grupo: Capturar a Máquina de Referência

Este grupo contém os passos necessários para preparar e capturar um computador de referência.

|Passo da sequência de tarefas|Descrição|  
|-------------------------------|---------------|  
|**Preparar o Cliente do Gestor de Configuração**|Generalize o cliente do Gestor de Configuração no computador de referência.|
|**Preparar os Os**|Executa sysprep para generalizar windows. Em seguida, reinicia o computador na imagem de arranque do Windows PE especificada para a sequência de tarefas.|
|**Capturar o Computador de Referência**|Captura a imagem para a partilha de rede especificada e . Ficheiro WIM.|

> [!IMPORTANT]
> Depois de capturar uma imagem de um computador de referência, não capture outra imagem de SO do computador de referência. As entradas de registo são criadas durante a configuração inicial. Crie um novo computador de referência cada vez que capturar a imagem de SO. Se planeia utilizar o mesmo computador de referência para criar futuras imagens de SO, primeiro desinstale e reinstale o cliente do Gestor de Configuração.

## <a name="next-steps"></a>Passos seguintes

[Métodos para implementar sistemas operativos empresariais](methods-to-deploy-enterprise-operating-systems.md)
