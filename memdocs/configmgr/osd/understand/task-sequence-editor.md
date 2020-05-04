---
title: Utilizar o editor de sequência de tarefas
titleSuffix: Configuration Manager
description: Entenda como usar o editor de sequência de tarefas na consola 'Gestor de Configuração'
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047ae9e276ac94b633d1dc30814ed641cd34d03
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711428"
---
# <a name="use-the-task-sequence-editor"></a>Utilizar o editor de sequência de tarefas

*Aplica-se a: Gestor de Configuração (ramo atual)*

Editar sequências de tarefas na consola do Gestor de Configuração utilizando o Editor da Sequência de **Tarefas**. Use o editor para:  

- Abra uma visão apenas de leitura da sequência de tarefas

- Adicione ou remova passos da sequência de tarefas  

- Alterar a ordem dos passos da sequência de tarefas  

- Adicionar ou remover grupos de passos  

- Copiar e colar passos entre sequências de tarefas

- Definir opções de passo como se a sequência de tarefas continua quando ocorre um erro  

- Adicionar condições aos passos e grupos de uma sequência de tarefas  

- Copiar e colar condições entre passos numa sequência de tarefas

- Procure na sequência de tarefas para localizar rapidamente passos

Antes de poder editar uma sequência de tarefas, tem de a criar. Para mais informações, consulte [Gerir e criar sequências](../deploy-use/manage-task-sequences-to-automate-tasks.md)de tarefas .

## <a name="about-the-task-sequence-editor"></a>Sobre o editor de sequência de tarefas

O editor da sequência de tarefas inclui os seguintes componentes:

![Screenshot anotado da janela do editor de sequência de tarefas da amostra](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. O nome da sequência de tarefas
2. Procura. Para mais informações, consulte [Search](#bkmk_search).
3. **Propriedades** para o grupo selecionado ou passo na sequência

    Para obter mais informações sobre as propriedades e opções de um passo específico, consulte [os passos](task-sequence-steps.md)da sequência de tarefas .

4. **Opções** para o grupo selecionado ou passo na sequência

    Para obter mais informações sobre opções gerais em todos os passos, ou opções de um passo específico, consulte [sobre passos](task-sequence-steps.md)de sequência de tarefas .

    Para mais informações sobre como configurar as condições, consulte [Condições](#bkmk_conditions).

5. **Adicione** um grupo ou passos
6. **Remover** um grupo ou passos
7. Destrua todos os grupos ou expanda todos os grupos
8. Mover a posição de um grupo ou passo na sequência (mover-se para cima, mover-se para baixo)
9. A sequência de tarefas:
    - Consulte a ordem dos passos e dos grupos.
    - Expandir ou colapsar um grupo.
    - Quando desativa um passo ou grupo nas suas **Opções,** fica acinzentado na sequência.
    - O ícone de um passo muda para um erro vermelho se houver um problema com o passo. Por exemplo, falta um valor necessário.
10. **OK**: Guardar e fechar
11. **Cancelar**: Fechar sem guardar alterações
12. **Aplicar:** Guardar alterações e manter-se aberto

Pode redimensionar o editor da sequência de tarefas utilizando controlos windows padrão. Para redimensionar as larguras das duas vidraças principais, use o rato para selecionar a barra entre a sequência de tarefas e as propriedades do passo e, em seguida, arrastá-la para a esquerda ou para a direita.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a>Ver uma sequência de tarefas

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

2. Na lista de sequência de **tarefas,** selecione a sequência de tarefas que pretende ver.  

3. No separador **Home** da fita, no grupo sequência de **tarefas,** selecione **Visualização**.

    > [!TIP]
    > Esta ação é o padrão. Se clicar duas vezes numa sequência de tarefas, **verá** a sequência de tarefas.

Esta ação abre o editor da sequência de tarefas no modo de leitura. Neste modo pode fazer as seguintes ações:

- Ver todos os grupos, passos, propriedades e opções
- Expandir e colapsar grupos
- Pesquisar a sequência de tarefas
- Redimensionar a janela do editor

Neste modo de leitura, não é possível fazer alterações, incluindo copiar um passo ou condição. Esta ação também não bloqueia a sequência de tarefas para a edição. Para obter mais informações sobre estas fechaduras, consulte [Recuperar o bloqueio para a edição](#bkmk_sedo)de sequências de tarefas .

Para efetuar alterações numa sequência de tarefas, feche o editor da sequência de tarefas que tem aberto no modo de leitura. Em seguida, [edite](#bkmk_edit) a sequência de tarefas.

> [!NOTE]  
> Quando vê ou edita uma sequência de tarefas criada pelo Assistente de Sequência de Tarefas Create, o nome do passo pode ser a ação ou o tipo do passo. Por exemplo, pode ver um passo que tem o nome "Disco de Partição 0", que é a ação para um passo de formato tipo e disco de [partição](task-sequence-steps.md#BKMK_FormatandPartitionDisk). Todos os passos de sequência de tarefas são documentados pelo seu *tipo,* não necessariamente pelo nome do passo que o editor exibe.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> Editar uma sequência de tarefas

Utilize o seguinte procedimento para modificar uma sequência de tarefas existente:  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

2. Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende editar.  

3. No separador **Home** da fita, no grupo sequência de **tarefas,** selecione **Editar**. Em seguida, faça qualquer uma das seguintes ações:  

    - **Adicione um passo:** Selecione, selecione uma categoria e, em seguida, selecione o passo a adicionar. **Add** Por exemplo, para adicionar o passo linha de [comando executar:](task-sequence-steps.md#BKMK_RunCommandLine) selecione **Adicionar,** escolha a categoria **Geral** e, em seguida, selecione **Executar Linha**de Comando . Esta ação adiciona o passo após o passo atualmente selecionado.

    - **Adicione um grupo**: Selecione **Adicionar**, e, em seguida, escolha **Novo Grupo**. Depois de adicionar um grupo, adicione-lhe passos.  

    - **Alterar a ordem**: Selecione o passo ou o grupo que pretende reencomendar. Em seguida, use os ícones **Move Up** ou **Move Down.** Apenas pode mover um passo ou um grupo de cada vez. Estas ações também estão disponíveis quando clica à direita num grupo ou passo.

        Pode cortar, copiar e colar um grupo ou um passo. Clique no item e selecione a ação. Também pode utilizar atalhos padrão de teclado para cada ação:

        - Corte: **CTRL** + **X**
        - Cópia: **CTRL** + **C**
        - Pasta: **CTRL** + **V**

    - **Retire um passo ou grupo:** Selecione o passo ou o grupo e escolha **Remover**.  

4. Selecione **OK** para guardar as suas alterações e feche a janela. **Selecione Cancelar** para descartar as alterações e fechar a janela. Selecione **Aplicar** para guardar as suas alterações e manter o editor de sequência de tarefas aberto.  

Para obter uma lista dos passos de sequência de tarefas disponíveis, consulte [os passos](task-sequence-steps.md)da sequência de tarefas .  

> [!IMPORTANT]  
> Se a sequência de tarefas tiver referências não associadas a um objeto como resultado da edição, o editor requer que corrija a referência antes de poder fechar. As possíveis ações incluem:  
>
> - Corrija a referência
> - Eliminar o objeto não referenciado da sequência de tarefas  
> - Desative temporariamente o passo da sequência de tarefas falhada até que a referência quebrada seja corrigida ou removida  

Pode abrir mais do que uma instância do editor da sequência de tarefas ao mesmo tempo. Este comportamento permite comparar múltiplas sequências de tarefas, ou copiar e colar passos entre elas. Podeeditar **Edit** uma sequência de tarefas e **ver** outra, mas não pode fazer ambas as ações na mesma sequência de tarefas.

## <a name="conditions"></a><a name="bkmk_conditions"></a>Condições

Utilize condições para controlar o funcionar da sequência de tarefas. Adicione condições a um único passo ou a um grupo de passos. A sequência de tarefas avalia as condições antes de passar o passo no dispositivo. Só passa o passo se as condições avaliarem a verdade. Se uma condição avaliar falsamente, então a sequência de tarefas ignora o grupo ou passo.

Utilize o separador **Opções** para gerir as condições:

![Gerir as condições no separador opções do editor de sequência de tarefas](media/4621098-copy-paste-ts-condition.png)

Estão disponíveis os seguintes tipos de condições:

- **Se declaração**: Utilize uma declaração *se* para as condições do grupo. Pode avaliar **todas as condições**, **qualquer condição,** ou **nenhuma.**

- **Variável de sequência de tarefas**. Avalie o valor atual de qualquer variável de sequência de [tarefas](task-sequence-variables.md) incorporada, ação, personalizada ou apenas de leitura no ambiente de sequência de tarefas. Para mais informações, consulte [as condições do Passo.](using-task-sequence-variables.md#bkmk_access-condition)

    > [!NOTE]
    > Pode utilizar uma variável de matriz nesta condição, mas tem de especificar o membro da matriz específico. Por exemplo, `OSDAdapter0EnableDHCP` especifica se o *primeiro* adaptador de rede permite o DHCP. Para mais informações, consulte [as variáveis Array](using-task-sequence-variables.md#bkmk_array).

- **Versão OS**: Avaliar a versão OS do dispositivo onde a sequência de tarefas é executado. Esta lista é a versão geral do OS utilizada em todo o Gestor de Configuração. Para avaliar uma versão os mais detalhada, como uma versão específica do Windows 10, utilize a condição **De Consulta WMI.**

- **Linguagem OS**: Avalie a linguagem OS do dispositivo onde a sequência de tarefas é executado. Esta lista inclui os 257 idiomas que o Windows suporta.

- **Propriedades do ficheiro**: Avalie a versão ou o carimbo temporal de qualquer ficheiro no dispositivo onde a sequência de tarefas é executado.

- **Propriedades**da pasta : Avalie o carimbo de tempo de qualquer pasta no dispositivo onde a sequência de tarefas é executado.

- **Regulação do registo**: Avalie qualquer valor-chave de registo do dispositivo onde a sequência de tarefas funciona.

- **Consulta WMI**: Especifique o espaço de nome e a consulta para avaliar no dispositivo onde a sequência de tarefas é executado.

- **Software instalado**: Especifique um ficheiro do Instalador do Windows para carregar as informações do produto para combinar com o dispositivo onde a sequência de tarefas funciona. Pode comparar-se com um produto específico ou com qualquer versão do produto.

### <a name="cmdlets-for-conditions"></a>Cmdlets para condições

Gerir as condições com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Arquivo de condições get-CMTSStepcondition](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Pasta de Condições get-CMTSStep](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Condição de condicionar get-CMTSStep](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Sistema de Funcionamento get-CMTSStepCondition](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Registo de Condições de Saúde Get-CMTSStepCondition](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionvariable](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>Condições de cópia e pasta

<!-- 4621098 -->

Para reutilizar as condições de um passo para o outro, a partir da versão 1910 pode agora copiar e colar condições no editor da sequência de tarefas. Selecione uma condição para cortá-la ou copiá-la. Se uma condição tem filhos, copia todo o quarteirão. Se houver uma condição na área de sobre-a-placa, pode colá-la com as seguintes opções:

- Pasta antes
- Pasta depois
- Pasta em (aplica-se apenas às condições aninhadas)

Utilize atalhos de teclado padrão para copiar **(CTRL** + **C**) e cortar **(CTRL** + **X**). O atalho padrão do teclado **CTRL** + **V** faz a **Pasta após** a ação.

Há também novas opções para mover as condições para cima ou para baixo na lista.

> [!Note]  
> Pode copiar e colar condições entre passos numa sequência de tarefas. Não suporta esta ação entre diferentes sequências de tarefas.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a>Recuperar o bloqueio para edição

<!--3699337-->
Se a consola do Gestor de Configuração deixar de responder, pode ser bloqueado para não fazer mais alterações até que o bloqueio expire após 30 minutos. Esta fechadura faz parte do sistema SEDO (Edição Serializada de Objetos Distribuídos). Para mais informações, consulte [O Gestor de Configuração SEDO](../../develop/core/understand/sedo.md).

A partir da versão 1906, pode limpar o bloqueio numa sequência de tarefas. Esta ação aplica-se apenas à sua conta de utilizador que tenha o cadeado e no mesmo dispositivo a partir do qual o site concedeu o bloqueio. Quando tentar aceder a uma sequência de tarefas bloqueada, pode agora **descartar alterações**e continuar a editar o objeto. Estas alterações perder-se-iam quando o cadeado expirasse.

> [!TIP]
> A partir da versão 1910, pode limpar o bloqueio de qualquer objeto na consola 'Gestor de Configuração'. Para mais informações, consulte [A utilização da consola 'Gestor de Configuração'.](../../core/servers/manage/admin-console.md#bkmk_sedo)<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a>Pesquisar

<!-- 4621085 -->

Se tiver uma grande sequência de tarefas com muitos grupos e passos, pode ser difícil encontrar passos específicos. A partir da versão 1910, pode agora pesquisar no editor da sequência de tarefas. Esta ação permite localizar mais rapidamente os passos na sequência de tarefas.

![Pesquisar no editor de sequência de tarefas](media/4621085-task-sequence-search.png)

Insira um termo de pesquisa para começar. Pode analisar a sua pesquisa utilizando os seguintes tipos:

- Nome do passo
- Descrição do passo
- Tipo de passo
- Nome do grupo
- Descrição do grupo
- Nome da variável
- Condições
- Outros conteúdos, por exemplo, cordas como valores variáveis ou linhas de comando

Permite todos os âmbitos por defeito.

Também pode filtrar todos os passos com os seguintes atributos:

- Continue no erro
- Tem condições

Não ativa nenhum dos filtros por defeito.

Ao pesquisar, a janela do editor realça em amarelo os passos que correspondem aos seus critérios de pesquisa.

Aceda rapidamente a estes campos de pesquisa e navegue nos resultados da pesquisa com os seguintes atalhos de teclado:

- **CTRL** + **F:** introduza uma cadeia de pesquisa
- **CTRL** + **O**: selecione as opções de pesquisa para examinar os resultados
- **F3** ou **Enter**: passo em frente através dos resultados
- **SHIFT** + **F3**: retroceda através dos resultados

## <a name="see-also"></a>Consulte também

- [Gerir e criar sequências de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [Acerca dos passos de sequência de tarefas](task-sequence-steps.md)

- [Como utilizar variáveis de sequência de tarefas](using-task-sequence-variables.md)

- [Usando a consola De Configuração Manager](../../core/servers/manage/admin-console.md)
