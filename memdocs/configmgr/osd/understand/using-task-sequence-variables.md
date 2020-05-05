---
title: Como utilizar variáveis de sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba como usar as variáveis numa sequência de tarefas do Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c043cfabc411dbd5ae4984110fc2904d37669300
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717826"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Como utilizar variáveis de sequência de tarefas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

 O motor de sequência de tarefas na função de implementação do SISTEMA de Configuração utiliza muitas variáveis para controlar os seus comportamentos. Utilize estas variáveis para:

- Definir condições em passos  
- Alterar comportamentos para passos específicos  
- Uso em scripts para ações mais complexas  

Para uma referência de todas as variáveis de sequência de tarefas disponíveis, consulte variáveis de sequência de [tarefas](task-sequence-variables.md).

## <a name="types-of-variables"></a><a name="bkmk_types"></a>Tipos de variáveis

Existem vários tipos de variáveis:  

- [Incorporado](#bkmk_built-in)  
- [Ação](#bkmk_action)  
- [Personalizado](#bkmk_custom)  
- [Apenas para leitura](#bkmk_read-only)  
- [Matriz](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a>Variáveis incorporadas

As variáveis incorporadas fornecem informações sobre o ambiente onde a sequência de tarefas funciona. Os seus valores estão disponíveis em toda a sequência de tarefas. Tipicamente, o motor de sequência de tarefas inicializa variáveis incorporadas antes de correr quaisquer passos.

Por exemplo, `_SMSTSLogPath` é uma variável ambiental que especifica o caminho para o qual os componentes do Gestor de Configuração escrevem ficheiros de registo. Qualquer passo de sequência de tarefas pode aceder a esta variável ambiental.

A sequência de tarefas avalia algumas variáveis antes de cada passo. Por exemplo, `_SMSTSCurrentActionName` enumera o nome do passo atual.

### <a name="action-variables"></a><a name="bkmk_action"></a>Variáveis de ação

As variáveis de ação da sequência de tarefas especificam as definições de configuração que um único passo de sequência de tarefas utiliza. Por predefinição, o passo inicializa as suas definições antes de ser executado. Estas definições só estão disponíveis enquanto o passo da sequência de tarefas associada é executado. A sequência de tarefas adiciona o valor variável de ação ao ambiente antes de passar o passo. Em seguida, remove o valor do ambiente após o passo.

Por exemplo, adicione o passo da **Linha de Comando executar** a uma sequência de tarefas. Este passo inclui um **Start In** propriedade. A sequência de tarefas armazena `WorkingDirectory` um valor predefinido para esta propriedade como variável. A sequência de tarefas inicializa este valor antes de executar o passo da Linha de **Comando de Execução.** Enquanto este passo está em execução, `WorkingDirectory` aceda ao valor de propriedade Start **In** a partir do valor. Após o passo concluído, a sequência de `WorkingDirectory` tarefas remove o valor da variável do ambiente. Se a sequência de tarefas incluir outro passo `WorkingDirectory` da Linha de Comando de **Execução,** inicializa uma nova variável. Nessa altura, a sequência de tarefas define a variável para o valor inicial para o passo atual. Para mais informações, consulte [WorkingDirectory](task-sequence-variables.md#WorkingDirectory).  

O valor *padrão* para uma variável de ação está presente quando o passo corre. Se definir um *novo* valor, está disponível para vários passos na sequência de tarefas. Se anular um valor predefinido, o novo valor permanece no ambiente. Este novo valor sobrepõe-se ao valor padrão para outros passos na sequência de tarefas. Por exemplo, adicione um passo variável de sequência de **tarefas como** o primeiro passo da sequência de tarefas. Este passo define `WorkingDirectory` a `C:\`variável para . Qualquer passo **da Linha de Comando de Execução** na sequência de tarefas utiliza o novo valor de diretório inicial.  

Alguns passos de sequência de tarefas marcam certas variáveis de ação como *saída*. Passos mais tarde na sequência de tarefas leia estas variáveis de saída.

> [!Note]  
> Nem todos os passos da sequência de tarefas têm variáveis de ação. Por exemplo, embora existam variáveis associadas à ação **Enable BitLocker,** não existem variáveis associadas à ação **Desativação BitLocker.**  

### <a name="custom-variables"></a><a name="bkmk_custom"></a>Variáveis personalizadas

Estas variáveis são qualquer que o Gestor de Configuração não crie. Inicialize as suas próprias variáveis para usar como condições, em linhas de comando ou em scripts.

Quando especificar um nome para uma nova variável de sequência de tarefas, siga estas orientações:  

- O nome variável da sequência de tarefas`_`pode incluir letras, números, o carácter de sublinhado ( e um hífen ).`-`  

- Os nomes variáveis de sequência de tarefatêm um comprimento mínimo de um caracteres e um comprimento máximo de 256 caracteres.  

- As variáveis definidas pelo utilizador`A-Z` `a-z`devem começar com uma letra (ou ).  

- Os nomes variáveis definidos pelo utilizador não podem começar com o caráter de sublinhado. Apenas variáveis de sequência de tarefas apenas de leitura são precedidas pelo carácter de sublinhado.  

- Os nomes variáveis da sequência de tarefas não são sensíveis aos casos. Por `OSDVAR` exemplo, `osdvar` e são a mesma variável de sequência de tarefas.  

- Os nomes variáveis da sequência de tarefas não podem começar ou terminar com um espaço. Também não podem ter espaços embutidos. A sequência de tarefas ignora quaisquer espaços no início ou no fim de um nome variável.  

Não há limite definido para quantas variáveis de sequência de tarefas podes criar. No entanto, o número de variáveis é limitado pelo tamanho do ambiente de sequência de tarefas. O limite de tamanho total para o ambiente da sequência de tarefas é de 32 MB.  

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a>Variáveis apenas de leitura

Não se pode alterar o valor de algumas variáveis, que são apenas leituras. Normalmente, o nome começa`_`com um caráter de sublinhado ( ). A sequência de tarefas usa-os para as suas operações. As variáveis apenas de leitura são visíveis no ambiente da sequência de tarefas.

Estas variáveis são úteis em scripts ou linhas de comando. Por exemplo, executar uma linha de comando e `_SMSTSLogPath` canalizar a saída para um ficheiro de registo com os outros ficheiros de registo.

> [!NOTE]  
> As variáveis de sequência de tarefas apenas de leitura podem ser lidas por passos numa sequência de tarefas, mas não podem ser definidas. Por exemplo, utilize uma variável de leitura apenas como parte da linha de comando para um passo da Linha de **Comando de Execução.** Não é possível definir uma variável apenas para leitura utilizando o passo variável da sequência de **tarefas definida.**  

### <a name="array-variables"></a><a name="bkmk_array"></a>Variáveis de matriz

A sequência de tarefas armazena algumas variáveis como uma matriz. Cada elemento da matriz representa as definições para um único objeto. Utilize estas variáveis quando um dispositivo tem mais de um objeto para configurar. Os seguintes passos de sequência de tarefas utilizam variáveis de matriz:

- [Aplicar Definições de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [Formatar e Particionar Disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a>Como definir variáveis

Para variáveis ou variáveis personalizadas que não são apenas leitura, existem vários métodos para inicializar e definir o valor da variável:  

- [Definir passo variável de sequência](#bkmk_set-ts-step) de tarefas
- Definir passo [de Variáveis Dinâmicas](#bkmk_set-dyn-step)
- Executar passo [do script PowerShell](#bkmk_run-ps)
- [Variáveis de recolha e dispositivo](#bkmk_set-coll-var)  
- [Objeto TSEnvironment COM](#bkmk_set-com)  
- [Comando prestart](#bkmk_set-prestart)  
- [Assistente de sequência de tarefas](#bkmk_set-tswiz)
- [Assistente de mídia de sequência de tarefas](#bkmk_set-media)  

Eliminar uma variável do ambiente utilizando os mesmos métodos que criar uma variável. Para eliminar uma variável, detete o valor variável para uma corda vazia.  

Pode combinar métodos para definir uma variável de sequência de tarefas para valores diferentes para a mesma sequência. Por exemplo, defino os valores predefinidos utilizando o editor da sequência de tarefas e, em seguida, definir valores personalizados usando um script.

Se definir a mesma variável por métodos diferentes, o motor de sequência de tarefas utiliza a seguinte ordem:  

1. Avalia primeiro as variáveis de recolha.  

2. Variáveis específicas do dispositivo sobrepõem-se à mesma variável definida numa coleção.  

3. As variáveis definidas por qualquer método durante a sequência de tarefas têm precedência sobre variáveis de recolha ou dispositivo.  

### <a name="general-limitations-for-task-sequence-variable-values"></a>Limitações gerais para valores variáveis de sequência de tarefas

- Os valores variáveis da sequência de tarefas não podem ser mais de 4.000 caracteres.  

- Não se pode mudar uma variável de sequência de tarefas só de leitura. As variáveis apenas de leitura têm`_`nomes que começam com um caráter de sublinhado ( ).  

- Os valores variáveis da sequência de tarefas podem ser sensíveis ao caso dependendo da utilização do valor. Na maioria dos casos, os valores variáveis da sequência de tarefas não são sensíveis aos casos. Uma variável que inclui uma palavra-passe é sensível a casos.  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a>Definir variável de sequência de tarefas

Utilize este passo na sequência de tarefas para definir uma única variável para um único valor.

Para mais informações, consulte [definir variável de sequência](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)de tarefas .

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a>Definir Variáveis Dinâmicas

Utilize este passo na sequência de tarefas para definir uma ou mais variáveis de sequência de tarefas. Define regras neste passo para determinar quais variáveis e valores usar.

Para mais informações, consulte [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a>Executar o script PowerShell

<!-- 6315548 -->

Utilize este passo na sequência de tarefas para utilizar um script PowerShell para definir uma variável de sequência de tarefas.

Pode especificar um nome de script a partir de um pacote ou introduzir diretamente um script PowerShell no passo. Em seguida, use a propriedade passo para **a variável de sequência** de tarefas para salvar a saída do script para uma variável de sequência de tarefas personalizada.

Para obter mais informações sobre este passo, consulte [executar o Script PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).

> [!NOTE]
> Também pode utilizar um script PowerShell para definir uma ou mais variáveis com o objeto **TSEnvironment.** Para obter mais informações, consulte [como utilizar variáveis numa sequência](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) de tarefas de execução no SDK do Gestor de Configuração.

#### <a name="example-scenario-with-run-powershell-script-step"></a>Cenário de exemplo com passo de script PowerShell run

O seu ambiente tem utilizadores em vários países, por isso pretende consultar a língua osso para definir como uma condição em múltiplos passos **de Aplicação de Aplicação de Idiomas** específicos.

1. Adicione uma instância do **Script PowerShell executar** à sequência de tarefas antes dos passos **de Aplicar o OS.**

1. Utilize a opção de **introduzir um script PowerShell** para especificar o seguinte comando:

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    Para obter mais informações sobre o cmdlet, consulte [Get-Culture](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-culture). Para obter mais informações sobre os nomes de línguaIS DE duas letras, consulte [a lista dos códigos ISO 639-1](https://wikipedia.org/wiki/List_of_ISO_639-1_codes).

1. Para a opção de **saída para variável**de sequência de tarefas, especifique `CurrentOSLanguage`.

    ![Screenshot do exemplo Executar powerShell Passo de script](media/run-powershell-script-example-language.png)

1. No passo **O Aplicar** para a imagem em língua inglesa, crie a seguinte condição:`Task Sequence Variable CurrentOSLanguage equals "en"`

    ![Screenshot da condição de exemplo no passo de Aplicar o OS](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > Para obter mais informações sobre como criar uma condição num passo, consulte [Como aceder a variáveis - Condição do passo](#bkmk_access-condition).

1. Guarde e implante a sequência de tarefas.

Quando o passo **do Script Run PowerShell** funciona num dispositivo com a `en`versão em inglês do Windows, o comando devolve o valor . Em seguida, poupa esse valor na variável personalizada. Quando o passo **De Aplicar os** para a imagem em língua inglesa corre no mesmo dispositivo, a condição avalia-se verdadeiramente. Se tiver várias instâncias do passo **De Sem Aplicação** para diferentes línguas, a sequência de tarefas corre dinamicamente o passo que corresponde à linguagem OS.

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a>Variáveis de recolha e dispositivo

Pode definir variáveis de sequência de tarefas personalizadas para dispositivos e coleções. As variáveis que define para um dispositivo são referidas como variáveis de sequência de tarefas por dispositivo. As variáveis definidas para uma coleção são designadas variáveis de sequência de tarefas por coleção. Se houver um conflito, as variáveis por dispositivo têm precedência sobre variáveis por coleção. Este comportamento significa que as variáveis de sequência de tarefas atribuídas a um dispositivo específico têm automaticamente uma prioridade superior às variáveis atribuídas à recolha que contém o dispositivo.  

Por exemplo, o dispositivo XYZ é um membro da coleção ABC. Atribui a MyVariable à coleção ABC com um valor de 1. Também atribui a MyVariable ao dispositivo XYZ com um valor de 2. A variável atribuída ao XYZ tem uma prioridade maior do que a variável que é atribuída à recolha ABC. Quando uma sequência de tarefas com esta variável corre em XYZ, a MyVariable tem um valor de 2.

Pode ocultar variáveis por dispositivo e por coleção para que não sejam visíveis na consola Do Gestor de Configuração. Quando utilizar a opção **Não exiba este valor na consola 'Gestor**de Configuração', o valor da variável não é apresentado na consola. A variável ainda pode ser usada pela sequência de tarefas quando funciona. Se já não quer que estas variáveis sejam ocultadas, apague-as primeiro. Em seguida, redefinir as variáveis sem selecionar a opção de escondê-las.  

> [!WARNING]  
> A definição para Não exibir este valor na consola 'Gestor de **Configuração'** aplica-se apenas à consola 'Gestor de Configuração'. Os valores das variáveis ainda são apresentados no ficheiro de registo da sequência de tarefas **(smsts.log).**

Você pode gerir variáveis por dispositivo em um local primário ou em um site de administração central. O Gestor de Configuração não suporta mais de 1.000 variáveis atribuídas para um dispositivo.  

> [!IMPORTANT]  
> Quando utilizar variáveis por coleção para sequências de tarefas, considere os seguintes comportamentos:  
>
> - As alterações às coleções são sempre replicadas em toda a hierarquia. Quaisquer alterações que faça às variáveis de recolha aplicam-se não só aos membros do site atual, mas a todos os membros da coleção em toda a hierarquia.  
>  
> - Ao eliminar uma coleção, esta ação também elimina as variáveis de sequência de tarefas que configurapara a recolha.  

#### <a name="create-task-sequence-variables-for-a-device"></a>Criar variáveis de sequência de tarefas para um *dispositivo*

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de **Dispositivos.**  

2. Selecione o dispositivo-alvo e selecione **Propriedades**.  

3. Na caixa de diálogo **Properties,** mude para o separador **Variáveis.**  

4. Para cada variável que pretende criar, selecione o **novo** ícone. Especifique o **nome** e o **valor** da variável de sequência de tarefas. Se quiser esconder a variável para que não seja visível na consola 'Gestor de Configuração', selecione a opção **Não exiba este valor na consola 'Gestor**de Configuração'.  

5. Depois de adicionar todas as variáveis às propriedades do dispositivo, selecione **OK**.  

#### <a name="create-task-sequence-variables-for-a-collection"></a>Criar variáveis de sequência de tarefas para uma *coleção*

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de Recolhas de **Dispositivos.** Selecione a recolha do alvo e escolha **propriedades**.  

2. Na caixa de diálogo **Properties,** mude para o separador **Variáveis de Recolha.**  

3. Para cada variável que pretende criar, selecione o **novo** ícone. Especifique o **nome** e o **valor** da variável de sequência de tarefas. Se quiser esconder a variável para que não seja visível na consola 'Gestor de Configuração', selecione a opção **Não exiba este valor na consola 'Gestor**de Configuração'.  

4. Opcionalmente, especifique a prioridade para o Gestor de Configuração utilizar quando as variáveis da sequência de tarefas forem avaliadas.  

5. Depois de adicionar todas as variáveis às propriedades da coleção, selecione **OK**.  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a>Objeto TSEnvironment COM

Para trabalhar com variáveis de um script, use o objeto **TSEnvironment.**

Para obter mais informações, consulte [como utilizar variáveis numa sequência](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) de tarefas de execução no SDK do Gestor de Configuração.

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a>Comando prestart

O comando prestart é um script ou executável que é executado no Windows PE antes de o utilizador selecionar a sequência de tarefas. O comando prestart pode consultar uma variável ou solicitar ao utilizador informações e, em seguida, guardá-la no ambiente. Utilize o objeto [TSEnvironment](#bkmk_set-com) COM para ler e escrever variáveis a partir do comando prestart.

Para mais informações, consulte os [comandos da Prestat para meios](prestart-commands-for-task-sequence-media.md)de sequência de tarefas .

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a>Assistente de sequência de tarefas

A partir da versão 1906, depois de selecionar uma sequência de tarefas na janela do Assistente da Sequência de Tarefas, a página para editar variáveis de sequência de tarefas inclui um botão **Edit.** Pode utilizar atalhos de teclado acessíveis para editar as variáveis. Esta mudança ajuda nos casos em que um rato não está disponível.<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a>Assistente de mídia de sequência de tarefas

Especifique variáveis para sequências de tarefas que são executadas a partir de meios de comunicação. Ao utilizar os meios de comunicação para implantar o SISTEMA, adicione as variáveis da sequência de tarefas e especifique os seus valores quando criar os meios de comunicação. As variáveis e os seus valores são armazenados nos meios de comunicação.  

> [!NOTE]  
> As sequências de tarefas são armazenadas em meios autónomos. No entanto, todos os outros tipos de meios de comunicação, como os meios de comunicação pré-encenados, recuperam a sequência de tarefas a partir de um ponto de gestão.  

Quando executa uma sequência de tarefas a partir de meios de **comunicação,** pode adicionar uma variável na página de Personalização do assistente.

Utilize as variáveis de suporte de dados em vez de variáveis por coleção ou por computador. Se a sequência de tarefas estiver a funcionar a partir de variáveis de mídia, por computador e por coleção não se aplicam e não são usadas.  

> [!TIP]  
> A sequência de tarefas escreve a linha de comando ID do pacote e prestat para o ficheiro **CreateTSMedia.log** no computador que executa a consola Do Gestor de Configuração. Este ficheiro de registo inclui o valor para quaisquer variáveis de sequência de tarefas. Reveja este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

Para mais informações, consulte Criar meios de sequência de [tarefas](../deploy-use/create-task-sequence-media.md).

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a>Como aceder a variáveis

Depois de especificar a variável e o seu valor utilizando um dos métodos da secção anterior, utilize-a nas suas sequências de tarefas. Por exemplo, aceder a valores predefinidos para variáveis de sequência de tarefas incorporadas ou condicionar o valor de uma variável.  

Utilize os seguintes métodos para aceder a valores variáveis no ambiente de sequência de tarefas:

- [Usar em um passo](#bkmk_access-step)  
- [Condição do passo](#bkmk_access-condition)  
- [Script personalizado](#bkmk_access-script)  
- [Ficheiro de resposta de configuração do Windows](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a>Usar em um passo

Especifique um valor variável para uma definição num passo de sequência de tarefas. No editor da sequência de tarefas, edite o passo e especifique o nome variável como o valor de campo. Encerre o nome variável`%`em sinais por cento ( ).

Por exemplo, utilize o nome variável como parte do campo da Linha de **Comando** do passo da Linha de **Comando de Execução.** A seguinte linha de comando escreve o nome do computador num ficheiro de texto.

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a>Condição do passo

Utilize variáveis de sequência de tarefas incorporadas ou personalizadas como parte de uma condição num passo ou grupo. A sequência de tarefaavalia o valor variável antes de correr o passo ou o grupo.

Para adicionar uma condição que avalia um valor variável, faça os seguintes passos:  

1. No editor da sequência de tarefas, selecione o passo ou grupo ao qual pretende adicionar a condição.  

2. Mude para o separador **Opções** para o passo ou grupo. Clique em **Adicionar Condição**, e selecione Variável de sequência de **tarefas**.  

3. Na caixa de diálogo **variável sequência** de tarefas, especifique as seguintes definições:  

    - **Variável**: O nome da variável. Por exemplo, `_SMSTSInWinPE`.  

    - **Condição**: A condição para avaliar o valor variável. Por exemplo, **é igual**.  

    - **Valor**: O valor da variável a verificar. Por exemplo, `false`.  

Os três exemplos acima formam uma condição comum para testar se a sequência de tarefas está a funcionar a partir de uma imagem de arranque no Windows PE:

> **Variável de sequência de tarefas**`_SMSTSInWinPE equals "false"`

Consulte esta condição no grupo **'Ficheiros de Captura' e Definições** do modelo de sequência de tarefas predefinido para instalar uma imagem de OS existente.

Para mais informações sobre as condições, consulte o editor da [sequência de tarefas - Condições](task-sequence-editor.md#bkmk_conditions).

### <a name="custom-script"></a><a name="bkmk_access-script"></a>Script personalizado

Leia e escreva variáveis utilizando o objeto **Microsoft.SMS.TSEnvironment** COM enquanto a sequência de tarefas está em execução.

O exemplo do Windows PowerShell que se segue questiona a **variável _SMSTSLogPath** para obter a localização de registo atual. O script também define uma variável personalizada.

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a>Ficheiro de resposta de configuração do Windows

O ficheiro de resposta de configuração do Windows que fornece pode ter variáveis de sequência de tarefas incorporadas. Utilize o `%varname%`formulário, onde o *nome* é o nome da variável. O passo **De Configuração Windows e ConfigMgr** substitui a cadeia de nome variável pelo valor variável real. Estas variáveis de sequência de tarefaincorporadas não podem ser usadas em campos apenas numéricos num ficheiro de resposta sem vigilância.xml.

Para mais informações, consulte [Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).

## <a name="see-also"></a>Consulte também

- [Passos de sequência de tarefas](task-sequence-steps.md)

- [Variáveis de sequência de tarefas](task-sequence-variables.md)

- [Considerações sobre planeamento para automatizar tarefas](../plan-design/planning-considerations-for-automating-tasks.md)

- [Editor de sequência de tarefas](task-sequence-editor.md)
