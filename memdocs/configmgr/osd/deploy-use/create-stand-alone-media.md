---
title: Criar suportes de dados autónomos
titleSuffix: Configuration Manager
description: Utilize meios autónomos para implantar o SISTEMA num computador sem ligação à rede.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e477d08ed97fe46bbe51b62a0ed024d437c2626
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711008"
---
# <a name="create-stand-alone-media"></a>Criar suportes de dados autónomos

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os meios autónomos no Gestor de Configuração contêm tudo o que é necessário para implantar o SISTEMA num computador sem uma ligação de rede.

Utilize meios autónomos com os seguintes cenários de implantação do SO:  

- [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>Utilização

Os meios autónomos incluem a sequência de tarefas que automatiza os passos para instalar o SISTEMA e todos os outros conteúdos necessários. Este conteúdo inclui a imagem de arranque, imagem DE OS e controladores de dispositivos. Como os meios de comunicação autónomos armazenam tudo para implantar o SISTEMA, requer mais espaço em disco do que o necessário para outros tipos de meios.

Quando cria meios autónomos num site de administração central, o cliente recupera o código de site atribuído a Partir do Diretório Ativo. Os meios de comunicação autónomos criados em sites infantis atribuem automaticamente ao cliente o código do site para esse site.  


## <a name="prerequisites"></a>Pré-requisitos

Antes de criar meios autónomos utilizando o Assistente de Mídia create Task Sequence, certifique-se de que todas estas condições estão satisfeitas.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Criar uma sequência de tarefas para implantar um SO

Como parte dos meios autónomos, especifique a sequência de tarefas para implantar um SISTEMA. Para mais informações, consulte Criar uma sequência de [tarefas para instalar um OS](create-a-task-sequence-to-install-an-operating-system.md).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Ações não apoiadas para meios de comunicação autónomos

As seguintes ações não são apoiadas para meios de comunicação autónomos:

- Os [condutores de aplicação automática](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) entram na sequência de tarefas. Os meios de comunicação autónomos não suportam a aplicação automática de controladores de dispositivos do catálogo do condutor. Utilize o passo [do Pacote do Condutor Aplicado](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) para disponibilizar um conjunto específico de controladores para a Configuração do Windows.  

- O [descarregamento do conteúdo](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) do pacote na sequência de tarefas. A informação do ponto de gestão não está disponível em meios autónomos, por isso o passo falha em tentar enumerar os locais de conteúdo.  

- Instalação de atualizações de software.  

- Instalação de software antes de implementar o SISTEMA.  

- Sequências de tarefas personalizadas para implementações não-S.  

- Associação de utilizadores ao computador de destino para suportar a afinidade dispositivo/utilizador.  

- O pacote dinâmico instala-se através da etapa de Instalação de [Pacotes.](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- A aplicação dinâmica instala-se através da etapa de [Instalação.](../understand/task-sequence-steps.md#BKMK_InstallApplication)

- O pacote de **cliente de pré-produção Use quando estiver disponível** na configuração do Conjunto Windows e na sequência de tarefas **ConfigMgr.** Para mais informações sobre esta definição, consulte [Configurar Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> Pode ocorrer um erro se a sua sequência de tarefas incluir o passo [do Pacote de Instalação](../understand/task-sequence-steps.md#BKMK_InstallPackage) e criar os meios autónomos num site de administração central. O site da administração central não tem as políticas de configuração do cliente necessárias. Estas políticas são necessárias para ativar o agente de distribuição de software quando a sequência de tarefas funciona. O seguinte erro pode aparecer no ficheiro **CreateTsMedia.log:**  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> Para meios autónomos que incluam um passo **de Pacote de Instalação,** crie os meios autónomos num site primário que tenha o agente de distribuição de software ativado.
>
> Em alternativa, utilize um passo de linha de comando de [execução](../understand/task-sequence-steps.md#BKMK_RunCommandLine) personalizado. Adicione-o após o passo de [Configuração Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) e antes do primeiro passo do **Pacote de Instalação.** O passo **da Linha de Comando executar** executa o seguinte comando WMIC para ativar o agente de distribuição de software antes do primeiro passo do Pacote de Instalação:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas

Distribua todos os conteúdos que a sequência de tarefas requer para pelo menos um ponto de distribuição. Este conteúdo inclui a imagem de arranque, a imagem do OS e outros ficheiros associados. O assistente recolhe o conteúdo a partir do ponto de distribuição quando cria os meios de comunicação.

A sua conta de utilizador precisa, pelo **menos, de ler** os direitos de acesso à biblioteca de conteúdos nesse ponto de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a pen USB amovível

Se estiver a utilizar uma unidade USB amovível, ligue-a ao computador onde executa o assistente de Create Task Sequence Media. A unidade USB deve ser detetável pelo Windows como um dispositivo de remoção. Quando cria o suporte de dados, o assistente escreve diretamente na pen USB.

O suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar meios autónomos numa unidade USB amovível cujo conteúdo contém um ficheiro com mais de 4 GB de tamanho.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída

Antes de executar o Assistente de Mídia de Sequência de Tarefas Criar meios de comunicação para um conjunto de CD ou DVD, crie uma pasta para os ficheiros de saída que cria. Os meios de comunicação que cria para um conjunto de CD ou DVD são escritos como um . Ficheiro ISO diretamente na pasta.


## <a name="process"></a>Processo

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione Criar Meios de Sequência de **Tarefas**. Esta ação inicia o Assistente de Mídia de Sequência de Tarefas Create Task Sequence.  

3. Na página **Select Media Type,** especifique as seguintes opções:  

    - Selecione **suporte autónomo**.  

    - Opcionalmente, se pretender apenas permitir que o Sistema operativo seja implantado sem necessitar de entrada do utilizador, selecione Permitir a **implementação do sistema operativo sem supervisão**.  

        > [!IMPORTANT]  
        > Ao selecionar esta opção, o utilizador não é solicitado para informações de configuração de rede ou para sequências de tarefas opcionais. Se configurar os meios de proteção de palavras-passe, o utilizador ainda é solicitado para obter uma palavra-passe.  

4. Na página **Media Type,** especifique se os meios de comunicação são uma **unidade USB amovível** ou um **conjunto de CD/DVD**. Em seguida, configure as seguintes opções:  

    > [!IMPORTANT]  
    > Os meios de comunicação usam um sistema de ficheiros FAT32. Não é possível criar suportes numa unidade USB cujo conteúdo contém um ficheiro com mais de 4 GB de tamanho.  

    - Se selecionar unidade **USB amovível,** selecione a unidade onde pretende armazenar o conteúdo.  

        - **Formato unidade USB amovível (FAT32) e faça o arranque:** Por padrão, deixe o Gestor de Configuração preparar a unidade USB. Muitos dispositivos UEFI mais recentes requerem uma partição FAT32 sabotável. No entanto, este formato também limita o tamanho dos ficheiros e a capacidade global da unidade. Se já formatado e configurar a unidade amovível, desative esta opção.

    - Se selecionar **o conjunto de CD/DVD,** especifique a capacidade dos meios de comunicação (tamanho dos meios de**comunicação**) e o nome e o caminho do ficheiro de saída **(ficheiro Media**). O assistente escreve os ficheiros de saída nesta localização. Por exemplo: `\\servername\folder\outputfile.iso`  

        Se a capacidade dos meios de comunicação for demasiado pequena para armazenar todo o conteúdo, cria vários ficheiros. Em seguida, você precisa armazenar o conteúdo em vários CDs ou DVDs. Quando requer vários ficheiros de meios de comunicação, o Gestor de Configuração adiciona um número de sequência ao nome de cada ficheiro de saída que cria.  

        Se implementar uma aplicação juntamente com o S, e a aplicação não conseguir encaixar num único meio de comunicação, o Gestor de Configuração armazena a aplicação em vários meios de comunicação. Quando os meios de comunicação autónomos são executados, o Gestor de Configuração solicita ao utilizador para os próximos meios onde a aplicação é armazenada.  

        > [!IMPORTANT]  
        > Se selecionar uma imagem .iso existente, o Assistente de Criação de Suporte de Dados da Sequência de Tarefas elimina essa imagem da unidade ou partilha logo que avança para a página seguinte do assistente. A imagem existente será eliminada, mesmo que em seguida cancele o assistente.  

    - **Pasta de encenação**<!--1359388-->: O processo de criação de meios de comunicação pode requerer muito espaço de condução temporária. Por defeito, esta localização é `%UserProfile%\AppData\Local\Temp`semelhante ao seguinte caminho: . A partir da versão 1902, para lhe dar maior flexibilidade com onde armazenar estes ficheiros temporários, altere este valor para outra unidade e caminho.  

    - **Etiqueta dos meios de comunicação**<!--1359388-->: A partir da versão 1902, adicione um rótulo aos meios de sequência de tarefas. Esta etiqueta ajuda-o a identificar melhor os meios de comunicação depois de o criar. O valor predefinido é `Configuration Manager`. Este campo de texto aparece nos seguintes locais:  

        - Se montar um ficheiro ISO, o Windows apresenta esta etiqueta como o nome da unidade montada  

        - Se forformar uma unidade USB, utiliza os primeiros 11 caracteres da etiqueta como nome  

        - O Gestor de Configuração `MediaLabel.txt` escreve um ficheiro de texto chamado à raiz dos meios de comunicação. Por predefinição, o ficheiro inclui `label=Configuration Manager`uma única linha de texto: . Se personalizar a etiqueta para meios de comunicação, esta linha utiliza a sua etiqueta personalizada em vez do valor predefinido.  

    - **Incluir ficheiro autorun.inf nos meios de comunicação**<!-- 4090666 -->: A partir da versão 1906, o Gestor de Configuração não adiciona um ficheiro autorun.inf por padrão. Este ficheiro é geralmente bloqueado por produtos antimalware. Para obter mais informações sobre a funcionalidade AutoRun do Windows, consulte [criar uma aplicação CD-ROM ativada por AutoRun](https://docs.microsoft.com/windows/desktop/shell/autoplay). Se ainda necessário para o seu cenário, selecione esta opção para incluir o ficheiro.  

5. Na página **de Segurança,** especifique as seguintes opções:

    - **Proteja os meios com uma palavra-passe**: Introduza uma senha forte para ajudar a proteger os meios de acesso não autorizados. Quando especifica uma palavra-passe, o utilizador deve fornecer essa palavra-passe para utilizar os meios de comunicação.  

        > [!IMPORTANT]  
        > Como uma boa prática de segurança, atribua sempre uma palavra-passe para ajudar a proteger os meios de comunicação.  
        >
        > Nos meios autónomos, apenas encripta os passos da sequência de tarefas e as suas variáveis. Não encripta o conteúdo restante dos meios de comunicação. Não inclua nenhuma informação sensível nos scripts de sequência de tarefas. Armazenar e implementar todas as informações sensíveis utilizando variáveis de sequência de tarefas.  

    - **Selecione o intervalo**de datapara que este suporte autónomo seja válido: Definir datas de início e expiração opcionais nos meios de comunicação. Esta definição é desativada por defeito. As datas são comparadas com o tempo de sistema no computador antes que os meios de comunicação autónomos sejam executados. Quando o tempo do sistema é mais cedo do que a hora de início ou mais tarde do que o tempo de validade, os meios de comunicação autónomos não começam. Estas opções também estão disponíveis utilizando o cmdlet [New-CMStandaloneMedia](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps) PowerShell.  

6. Na página **de CD/DVD autónomo,** selecione a sequência de tarefas que implementa o SISTEMA. Só é possível selecionar as sequências de tarefas associadas a uma imagem de arranque. Verifique a lista de conteúdos referenciados pela sequência de tarefas.  

    - **Detete dependências de aplicações associadas e adicione-as a este meio de comunicação**: Adicione também conteúdo aos meios de comunicação para dependências de aplicações.  

        > [!TIP]  
        > Se não vir as dependências esperadas da aplicação, desmarque e, em seguida, reselecione esta opção para atualizar a lista.  

7. Na página **Select Application,** especifique o conteúdo adicional da aplicação para incluir como parte do ficheiro de suporte de dados.  

8. Na página **Select Package,** especifique o conteúdo adicional do pacote para incluir como parte do ficheiro de mídia.  

9. Na página **Select Driver Package,** especifique o conteúdo adicional do pacote do condutor para incluir como parte do ficheiro de mídia.  

10. Na página pontos de **distribuição,** especifique os pontos de distribuição que contêm o conteúdo necessário.  

    O Gestor de Configuração apenas exibe pontos de distribuição que tenham o conteúdo. Distribua todos os conteúdos associados à sequência de tarefas para pelo menos um ponto de distribuição antes de continuar. Depois de distribuir o conteúdo, refresque a lista de pontos de distribuição. Remova quaisquer pontos de distribuição que já tenha selecionado nesta página, vá para a página anterior e, em seguida, volte para a página Pontos de **Distribuição.** Em alternativa, reinicie o assistente. Para mais informações, consulte [Distribuir conteúdo referenciado por uma sequência](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) de tarefas e gerir a [infraestrutura](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)de conteúdo e conteúdo .  

11. Na página de **Personalização,** especifique as seguintes opções:  

    - Adicione quaisquer variáveis que a sequência de tarefas utilize.  

    - **Ativar**o comando prestart : Especifique quaisquer comandos prestart que pretenda executar antes da sequência de tarefas ser executada. Os comandos prestart são um script ou um executável que pode interagir com o utilizador no Windows PE antes da sequência de tarefas ser executada. Para mais informações, consulte os [comandos da Prestat para meios](../understand/prestart-commands-for-task-sequence-media.md)de sequência de tarefas .  

        > [!TIP]  
        > Durante a criação de meios de comunicação, a sequência de tarefas escreve o id do pacote e a linha de comando prestart, incluindo o valor para quaisquer variáveis de sequência de tarefas, para o ficheiro **CreateTSMedia.log** no computador que executa a consola Do Gestor de Configuração. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

        Se o comando prestart necessitar de qualquer conteúdo, selecione a opção **de Incluir ficheiros para o comando prestart**.  

12. Conclua o assistente.  

Os ficheiros de mídia autónomos (. ISO) são criados na pasta de destino. Se selecionar **o conjunto de CD/DVD,** copie os ficheiros de saída para um conjunto de CDs ou DVDs.


## <a name="next-steps"></a>Passos seguintes

[Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
