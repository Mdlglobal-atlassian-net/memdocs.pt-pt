---
title: Comandos de pré-início para suporte de dados da sequência de tarefas
titleSuffix: Configuration Manager
description: Crie um script para usar para o comando prestart, distribua o conteúdo associado ao comando prestart e configure o comando prestart nos meios de comunicação.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9dd921d58e6ef777017af3e2eb24dbf4bd611fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717462"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>Comandos prestart para meios de sequência de tarefas em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode criar um comando prestart no Gestor de Configuração para utilizar com suportes de arranque, meios autónomos e meios pré-encenados. O comando de pré-início é um script ou executável que é executado antes da seleção da sequência de tarefas e pode interagir com o utilizador no Windows PE. O comando de pré-início pode solicitar informações a um utilizador e guardá-las no ambiente da sequência de tarefas ou consultar uma variável da sequência de tarefas para obter informações. Quando o computador de destino arranca, a linha de comandos é executada antes de a política ser transferida do ponto de gestão. Utilize os procedimentos seguintes para criar um script que será utilizado no comando de pré-início, distribuir o conteúdo associado ao comando de pré-início e configurar o comando de pré-início no suporte de dados.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Criar um ficheiro de script para utilizar no Comando de Pré-início  
 É possível ler e escrever as variáveis da sequência de tarefas, utilizando o objeto Microsoft.SMS.TSEnvironment COM enquanto a sequência de tarefas está em execução. O exemplo a seguir ilustra um ficheiro de script do Visual Basic que consulta a variável da sequência de tarefas _SMSTSLogPath para obter a localização do registo atual. O script também define uma variável personalizada.  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Criar um Pacote para o Ficheiro de Script e Distribuir o Conteúdo  
 Depois de criar o script ou executável para o comando de pré-início, tem de criar uma origem de pacote para alojar os ficheiros para o script ou executável, criar um pacote para os ficheiros (não é necessário nenhum programa) e depois distribuir o conteúdo para um ponto de distribuição.  

 Para obter mais informações sobre a criação de um pacote, consulte [Pacotes e programas.](../../apps/deploy-use/packages-and-programs.md)  

 Para mais informações sobre a distribuição de conteúdo, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Configurar o Comando de Pré-início no Suporte de Dados  
 No Assistente de Criação do Suporte de Dados da Sequência de Tarefas, é possível configurar um comando de pré-início para suportes de dados autónomos, suportes de dados de arranque ou suportes de dados de pré-configuração. Para obter mais informações sobre os tipos de mídia, consulte Criar meios de sequência de [tarefas](../deploy-use/create-task-sequence-media.md). Utilize o procedimento seguinte para criar um comando de pré-início no suporte de dados.  

#### <a name="to-create-a-prestart-command-in-media"></a>Para criar um comando de pré-início no suporte de dados  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, clique em Sequências de **Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4.  Na página **Selecionar Tipo de Suporte de Dados** , selecione **Suporte de dados autónomo**, **Suporte de dados de arranque**ou **Suporte de dados de pré-configuração**e, em seguida, clique em **Seguinte**.  

5.  Navegue para a página **Personalização** do assistente. Para obter mais informações sobre a configuração das outras páginas no assistente, consulte Criar meios de sequência de [tarefas](../deploy-use/create-task-sequence-media.md).  

6.  Na página **Personalização** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Selecione **Ativar comando de pré-início**.  

    -   Na caixa de texto **Linha de comandos** , introduza o script ou executável que criou para o comando de pré-início.  

        > [!IMPORTANT]  
        >  Utilize **cmd /C <\> comando prestart** para especificar o comando prestart. Por exemplo, se tiver utilizado o nome TSScript.vbs para o script do comando de pré-início, deve introduzir **cmd /C TSScript.vbs** na linha de comandos. Se **cmd /C** abrir uma nova janela do interpretador de comandos do Windows e utilizar a variável de ambiente Path para localizar o script ou executável do comando de pré-início. Também é possível especificar o caminho completo para o comando de pré-início, mas a letra da unidade pode ser diferente em computadores com configurações de unidades diferentes.  

    -   Selecione **Incluir ficheiros para o comando de pré-início**.  

    -   Clique em **Definir** para selecionar o pacote que está associado aos ficheiros de comando de pré-início.  

    -   Clique em **Procurar** para selecionar o ponto de distribuição que aloja o conteúdo para o comando de pré-início.  

7.  Conclua o assistente.  
