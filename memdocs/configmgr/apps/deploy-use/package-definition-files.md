---
title: Ficheiros de definição de pacote
titleSuffix: Configuration Manager
description: Saiba usar ficheiros de definição de pacotes para criar pacotes e programas no Gestor de Configuração
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710140"
---
# <a name="package-definition-files"></a>Ficheiros de definição de pacote

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os ficheiros de definição de pacotes são scripts para ajudá-lo a automatizar a criação de [Pacotes e programas](packages-and-programs.md) em 'Gestor de Configuração'. Eles fornecem todas as informações que o Gestor de Configuração precisa para criar um pacote e programa, exceto a localização dos ficheiros de origem do pacote.

## <a name="about-the-package-definition-file-format"></a>Sobre o formato de ficheiro de definição de pacote

Cada ficheiro de definição de pacote é um ficheiro de texto ASCII ou UTF-8 que utiliza o formato de ficheiro .ini. Contém as seguintes secções:  

### <a name="pdf"></a>[PDF]

Esta secção identifica o ficheiro como um ficheiro de definição de pacote. Contém as seguintes informações:  

- **Versão**: Especifique a versão do formato de ficheiro de definição de pacote que o ficheiro utiliza. Esta versão corresponde à versão do Gestor de Configuração para a qual foi escrita. Esta entrada é necessária.  

### <a name="package-definition"></a>[Definição de Pacote]

Especifique as propriedades do pacote e programa. Fornece as seguintes informações:  

- **Nome**: o nome do pacote, até 50 carateres.  

- **Versão** (opcional): A versão do pacote, até 32 caracteres.  

- **Ícone** (opcional): O ficheiro que contém o ícone a utilizar para este pacote. Se especificado, este ícone substitui o ícone de pacote predefinido na consola 'Gestor de Configuração'.

- **Publicador**: o publicador do pacote, até 32 carateres.

- **Idioma**: o idioma do pacote, até 32 carateres.

- **Comentário** (opcional): Um comentário sobre o pacote, até 127 caracteres.

- **ContémNoFiles**: Esta entrada indica se a embalagem tem algum ficheiro de origem.  

- **Programas**: Os programas que define para este pacote. Cada nome do programa corresponde a uma secção **[Programa]** neste ficheiro de definição de pacote.  

    Exemplo:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: o nome do ficheiro de formato MIF (Management Information Format) que contém o estado de pacote, até 50 carateres.  

- **MIFName**: O nome da embalagem para correspondência MIF, até 50 caracteres.  

- **MIFVersion**: O número de versão do pacote para correspondência MIF, até 32 caracteres.  

- **MIFPublisher**: O editor de software do pacote para correspondência MIF, até 32 caracteres.  

### <a name="program"></a>[Programa]

Inclua uma secção [Programa] para cada programa que especifique na entrada de **Programas** na secção **[Definição de Pacote].** Esta secção define cada programa. Cada secção do programa fornece as seguintes informações:  

- **Nome**: o nome do programa, até 50 carateres. Esta entrada deve ser exclusiva num pacote.  

- **Ícone** (opcional): Especifique o ficheiro que contém o ícone a utilizar para este programa. Este ícone substitui o ícone do programa predefinido na consola 'Gestor de Configuração'. O cliente também exibe este ícone quando implementa o programa numa coleção.

- **Comentário** (opcional): Um comentário sobre o programa, até 127 caracteres.

- **Linha de comando**: Especifique a linha de comando para o programa, até 127 caracteres. O comando é relativo à pasta de origem do pacote.

- **StartIn**: Especifique a pasta de trabalho para o programa, até 127 caracteres. Esta entrada pode ser um caminho absoluto no computador cliente ou um caminho relativo à pasta de origem do pacote.

- **Executar**: Especifique o modo de programa no qual o programa funciona. Pode especificar **Minimizado**, **Maximizado** ou **Oculto**. Se não incluir esta entrada, o programa funciona em modo normal.  

- **AfterRunning**: Especifique qualquer ação especial que ocorra após o programa terminar com sucesso. As opções disponíveis são **SMSRestart**, **ProgramRestart** ou **SMSLogoff**. Se não incluir esta entrada, o programa não executa uma ação especial.  

- **EstimouDiskSpace**: Especifique a quantidade de espaço em disco que o programa de software necessita para ser executado no computador. O valor predefinido é **Desconhecido.** Pode definir o valor como um número inteiro maior ou igual a zero. Se especificar um valor, inclua também as unidades pelo valor.  

    Exemplo:  

    `EstimatedDiskSpace=38MB`  

- **EstimativaRunTime**: Especifique a duração estimada em minutos que espera que o programa seja executado no computador cliente. O valor predefinido é **de 120**. Pode definir o valor como um número inteiro maior que zero, ou **Desconhecido.**  

    Exemplo:  

    `EstimatedRunTime=25`  

- **Clientes Suportados**: Especifique os processadores e sistemas operativos em que este programa funciona. Separe as plataformas por vírgulas. Se não incluir esta entrada, o cliente não verifica as plataformas suportadas para este programa.  

- **SuportadoClientMinVersionX**, **SupportEdClientMaxVersionX**: Especifique a gama de início a fim para os números de versão para os sistemas operativos especificados na entrada de **Clientes Suportados.**  

    Exemplo:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **Requisitos adicionais de Programa** (opcional): Fornecer qualquer outra informação ou requisitos para computadores clientes, até 127 caracteres.

- **CanRunWhen**: Especifique o estado do utilizador que o programa necessita para ser executado no computador cliente. Os valores disponíveis são **UserLoggedOn**, **NoUserLoggedOn** ou **AnyUserStatus**. O valor predefinido é **UserLoggedOn**.  

- **UserInputRequired**: Especifique se o programa requer interação com o utilizador. Os valores disponíveis são **Verdadeiro** ou **Falso**. O valor padrão é **Verdadeiro**. Esta entrada está definida para **Falso** se **o CanRunWhen** não estiver definido para **userLoggedOn**.  

- **AdminRightsRequired**: Especifique se o programa requer credenciais administrativas no computador para executar. Os valores disponíveis são **Verdadeiro** ou **Falso**. O valor predefinido é **Falso.** Esta entrada está definida para **True** se **canRunWhen** não estiver definido para **UserLoggedOn**.  

- **UseInstallAccount**: Especifique se o programa utiliza a conta de instalação do software cliente quando funciona em computadores clientes. Por predefinição, este valor é **Falso**. Este valor é também **Falso** se **CanRunWhen** estiver definido como **UserLoggedOn**.  

- **DriveLetterConnection**: Especifique se o programa requer uma ligação de letra de unidade aos ficheiros do pacote no ponto de distribuição. Pode especificar **Verdadeiro** ou **Falso**. O valor predefinido é **Falso,** que permite ao programa utilizar uma ligação universal de nomeação (UNC). Quando este valor é definido para **True**, o cliente usa a próxima letra disponível, começando por Z: e continuando para trás.  

- **Especifique Drive** (opcional): Especifique uma letra de unidade que o programa requer para se ligar aos ficheiros do pacote no ponto de distribuição. Esta definição obriga à utilização da letra de unidade especificada para as ligações do cliente aos pontos de distribuição.

- **Religue O DriveAtLogon**: Especifique se o computador volta a ligar-se ao ponto de distribuição quando o utilizador iniciar a sua entrada. Os valores disponíveis são **Verdadeiro** ou **Falso**. O valor predefinido é **Falso.**  

- **Programa Dependente**: Especifique um programa neste pacote que deve ser executado antes do programa atual. Esta entrada utiliza `DependentProgram=<ProgramName>`o `<ProgramName>` formato, onde está a entrada **nome** para esse programa no ficheiro de definição de pacote. Se não houver programas dependentes, deixe esta entrada em branco.  

    Exemplos:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Tarefa**: Especifique como o programa é atribuído aos utilizadores. Este valor pode ser:

    - **FirstUser**: Apenas o primeiro utilizador que se inscreve no cliente executa o programa
    - **EveryUser**: Todos os utilizadores que assinam executa o programa

    Quando **o CanRunQuando** não está definido para **userLoggedOn,** esta entrada está definida para **FirstUser**.  

- **Desativado**: Especifique se pode implementar este programa para os clientes. Os valores disponíveis são **Verdadeiro** ou **Falso**. O valor predefinido é **Falso.**  


## <a name="use-a-package-definition-file"></a>Utilize um ficheiro de definição de pacote  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Pacotes.**  

2. No separador **Casa** da fita, no grupo **Criar,** escolha **Criar pacote a partir de Definição**.  

3. Na página **definição** de pacote do **Pacote Criar do Assistente de Definição,** escolha um ficheiro de definição de pacote existente. Para abrir um novo ficheiro de definição de pacote, escolha **Navegar**. Depois de especificar um novo ficheiro de definição de pacote, selecione-o na lista de definição do **Pacote.**

4. Na página **Source Files,** especifique informações sobre quaisquer ficheiros de origem necessários para o pacote e programa.  

5. Se o pacote necessitar de ficheiros de origem, na página **da Pasta Fonte,** especifique a localização a partir de onde o site pode obter os ficheiros de origem.  

6. Conclua o assistente.  


## <a name="see-also"></a>Consulte também

[Pacotes e programas](packages-and-programs.md)
