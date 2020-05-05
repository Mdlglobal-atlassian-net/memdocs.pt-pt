---
title: Criar implementações faseadas
titleSuffix: Configuration Manager
description: Utilize implementações faseadas para automatizar o lançamento do software a várias coleções.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5af0b7c90225a1f42d55767a0296d7e2263f956f
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110462"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Criar implementações faseadas com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As implementações faseadas automatizam um lançamento coordenado e sequenciado de software em várias coleções. Por exemplo, implemente software para uma coleção piloto e, em seguida, continue automaticamente o lançamento com base em critérios de sucesso. Criar implementações faseadas com o padrão de duas fases, ou configurar manualmente várias fases. 

Criar implementações faseadas para os seguintes objetos:
- **Sequência de tarefas**  
    - A implementação faseada de sequências de tarefas não suporta pXE ou instalação de meios de comunicação   
- **Aplicação** (a partir da versão 1806) <!--1358147-->  
- **Atualização de software** (a partir da versão 1810) <!--1358146-->  
    - Não pode usar uma regra de implementação automática com uma implementação faseada

> [!Tip]  
> A função de implementação faseada foi introduzida pela primeira vez na versão 1802 como uma [função de pré-lançamento](../../core/servers/manage/pre-release-features.md). Começando com a versão 1806, já não é uma funcionalidade de pré-lançamento.<!--1356837-->  



## <a name="prerequisites"></a>Pré-requisitos

#### <a name="security-scope"></a>Âmbito de segurança
As implementações criadas por implementações faseadas não são visualizadas para qualquer utilizador administrativo que não tenha o âmbito de segurança **All.** Para obter mais informações, veja [Âmbitos de segurança](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

#### <a name="distribute-content"></a>Distribuir conteúdo
Antes de criar uma implementação faseada, distribua o conteúdo associado para um ponto de distribuição.<!--518293-->  

- **Aplicação**: Selecione a aplicação-alvo na consola e utilize a ação **Distribute Content** na fita. Para mais informações, consulte [Implementar e gerir conteúdos.](../../core/servers/deploy/configure/deploy-and-manage-content.md)   

- **Sequência de tarefas**: Tem de criar objetos referenciados como o pacote de atualização do SO antes de criar a sequência de tarefas. Distribua estes objetos antes de criar uma implantação. Utilize a ação **Distribute Content** em cada objeto ou na sequência de tarefas. Para visualizar o estado de todos os conteúdos referenciados, selecione a sequência de tarefas e mude para o separador **Referências** no painel de detalhes. Para mais informações, consulte o tipo específico de objeto em [Prepare-se para a implementação do OS](../get-started/prepare-for-operating-system-deployment.md).   

- **Atualização de software**: crie o pacote de implementação e distribua-o. Utilize o Assistente de Atualizações de Software de Descarregamento. Para mais informações, consulte [as atualizações](../../sum/deploy-use/download-software-updates.md)do software de download .  



## <a name="phase-settings"></a><a name="bkmk_settings"></a>Definições de fase

Estas definições são únicas para implementações faseadas. Configure estas definições ao criar ou editar as fases para controlar o agendamento e o comportamento do processo de implementação faseado. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Critérios para o sucesso da primeira fase  

- **Percentagem de sucesso**de implementação : Especifique a percentagem de dispositivos que precisam de completar com sucesso a implementação para que a primeira fase tenha sucesso. Por defeito, este valor é de 95%. Por outras palavras, o site considera a primeira fase bem sucedida quando o estado de conformidade para 95% dos dispositivos é **o Sucesso** para esta implementação. O site continua então para a segunda fase, e cria uma implementação do software para a próxima coleção.  
- **Número de dispositivos implementados com sucesso**: Adicionado na versão 1902 do Gestor de Configuração. Especifique o número de dispositivos que precisam de completar com sucesso a implementação para que a primeira fase tenha sucesso. Esta opção é útil quando o tamanho da coleção é variável, e você tem um número específico de dispositivos para mostrar sucesso antes de passar para a fase seguinte. <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Condições para iniciar segunda fase de implantação após sucesso da primeira fase  

- Iniciar automaticamente esta fase após um período de **diferimento (em dias)**: Escolha o número de dias para esperar antes de iniciar a segunda fase após o sucesso da primeira. Por defeito, este valor é um dia.  

- **Iniciar manualmente a segunda fase de implantação**: O site não inicia automaticamente a segunda fase após o sucesso da primeira fase. Esta opção requer que inicie manualmente a segunda fase. Para mais informações, consulte [Mover-se para a próxima fase](manage-monitor-phased-deployments.md#bkmk_move).  

    > [!Note]  
    > Esta opção não está disponível para implementações faseadas de aplicações.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Gradualmente disponibilize este software durante este período de tempo (em dias)
<!--1358578-->
A partir da versão 1806, configure esta definição para que o lançamento em cada fase aconteça gradualmente. Este comportamento ajuda a mitigar o risco de problemas de implementação, e diminui a carga na rede que é causada pela distribuição de conteúdo aos clientes. O site disponibiliza gradualmente o software dependendo da configuração para cada fase. Cada cliente numa fase tem um prazo em relação ao tempo que o software é disponibilizado. O intervalo de tempo entre o tempo disponível e o prazo é o mesmo para todos os clientes numa fase. O valor padrão desta definição é zero, por isso, por padrão, a implementação não é acelerada. Não desloque o valor acima dos 30.<!--SCCMDocs-pr issue 2767--> 

![Critérios de implementação faseados para definições de sucesso](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Configure o comportamento do prazo em relação ao momento em que o software é disponibilizado  

- **A instalação é necessária o mais rapidamente possível**: Estabeleça o prazo para a instalação no aparelho logo que o dispositivo seja direcionado.  

- **A instalação é necessária após este período de tempo**: Estabeleça um prazo para a instalação de um certo número de dias após o alvo do dispositivo. Por defeito, este valor é de sete dias.   


<!--### Examples
Include a timeline diagram
-->



## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a>Criar automaticamente uma implementação padrão em duas fases

1. Inicie o assistente de implementação faseada na consola do Gestor de Configuração. Esta ação varia em função do tipo de software que está a implementar:  

    - **Aplicação** (apenas na versão 1806 ou posterior): Ir à Biblioteca de **Software,** expandir gestão de **aplicações,** e selecionar **Aplicações**. Selecione uma aplicação existente e, em seguida, escolha **criar implantação faseada** na fita.  

    - **Atualização de software** (apenas na versão 1810 ou posterior): Vá à Biblioteca de **Software,** expanda **as Atualizações**de Software, e selecione **Todas as Atualizações**de Software . Selecione uma ou mais atualizações e, em seguida, escolha **criar implantação faseada** na fita.  

        Esta ação está disponível para atualizações de software a partir dos seguintes nós:  
        - Atualizações de Software  
            - **Todas as atualizações de software**  
            - **Grupos de atualização de software**   
        - Assistência ao Windows 10, **todas as atualizações do Windows 10**  
        - Gabinete 365 Gestão de Clientes, **Gabinete 365 Atualizações**  

    - **Sequência de tarefas**: Vá ao espaço de trabalho da Biblioteca de **Software,** expanda **sistemas operativos**e selecione sequências de **tarefas**. Selecione uma sequência de tarefas existente e, em seguida, escolha **criar implantação faseada** na fita.  

2. Na página **Geral,** dê à implementação faseada um **nome**, **descrição** (opcional) e selecione criar automaticamente uma implementação de **duas fases por defeito**.  

3. **Selecione Procurar** e escolha uma coleção-alvo para os campos **First Collection** e **Second Collection.** Para uma sequência de tarefas e atualizações de software, selecione a partir de coleções de dispositivos. Para uma aplicação, selecione a partir de coleções de utilizador ou dispositivos. Selecione **Seguinte**.  

    > [!Important]  
    > O assistente de implantação faseada create não o notifica se uma implementação é potencialmente de alto risco. Para mais informações, consulte [Definições para gerir implementações de alto risco](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) e a nota quando implementar uma sequência de [tarefas](deploy-a-task-sequence.md).  

4. Na página **Definições,** escolha uma opção para cada uma das definições de agendamento. Para mais informações, consulte [as definições de fase](#bkmk_settings). Selecione **Seguinte** quando estiver completo.  

5. Na página **Fases,** consulte as duas fases que o assistente cria para as coleções especificadas. Selecione **Seguinte**. Estas instruções cobrem o procedimento para criar automaticamente uma implementação em duas fases padrão. O assistente permite-lhe adicionar, remover, reencomendar, editar ou ver fases para uma implementação faseada. Para obter mais informações sobre estas ações adicionais, consulte [Criar uma implementação faseada com fases configuradas manualmente](#bkmk_manual).  

6. Confirme as suas seleções no separador **Resumo** e, em seguida, selecione **Next** para completar o assistente.  

> [!NOTE]
> A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver o nome antigo no produto do Gestor de Configuração e documentação enquanto a consola está a ser atualizada.  

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a>Criar uma implantação faseada com fases configuradas manualmente
<!--1358148--> 

A partir da versão 1806, crie uma implementação faseada com fases configuradas manualmente para uma sequência de tarefas. Adicione até 10 fases adicionais a partir do separador **Fases** do assistente de implantação faseada. 

> [!Note]  
> Não pode atualmente criar fases manualmente para uma aplicação. O assistente cria automaticamente duas fases para as implementações da aplicação.


1. Inicie o assistente de implementação faseada create para uma sequência de tarefas ou atualizações de software.  

2. Na página **geral** do assistente de implantação faseada Create, dê à implementação faseada um **nome**, **descrição** (opcional) e selecione **manualmente configurar todas as fases**.  

3. A partir da página Fases do assistente de implantação faseada, estão disponíveis as **seguintes** ações:  

    - **Filtre** a lista das fases de implantação. Introduza uma série de caracteres para uma correspondência incódida das colunas Ordem, Nome ou Coleção. 

    - **Adicione** uma nova fase:  

        1. Na página **geral** do Assistente de Fase adicionar, especifique um **Nome** para a fase e, em seguida, navegue para a Coleção de **Fase-Alvo**. As definições adicionais nesta página são as mesmas que quando normalmente implementam uma sequência de tarefas ou atualizações de software.  

        2. Na página **de Definições** de Fase do Assistente de Fase adicionar, configure as definições de agendamento e selecione **Seguinte** quando estiver completo. Para mais informações, consulte [Definições](#bkmk_settings).   

            > [!Note]  
            > Não é possível editar as definições de fase, **a percentagem** de sucesso de implantação ou **o número de dispositivos implementados com sucesso** (versão 1902 ou posterior), na primeira fase. Esta definição aplica-se apenas a fases que tenham uma fase anterior.  

        3. As definições nas páginas de **User Experience** e **Distribution Points** do Add Phase Wizard são as mesmas que quando normalmente implementam uma sequência de tarefas ou atualizações de software.  

        4. Reveja as definições na página **Resumo** e, em seguida, complete o Assistente de Fase adicionar.  

    - **Editar**: Esta ação abre a janela Propriedades da fase selecionada, que tem separadores iguais às páginas do Assistente de Fase adicionar.  

    - **Remover**: Esta ação elimina a fase selecionada.  

       > [!Warning]  
       > Não há confirmação, nem maneira de desfazer esta ação.  

    - **Move-se para cima** ou **para baixo**: O assistente ordena as fases através da forma como as adiciona. A fase mais recente é a última da lista. Para alterar a ordem, selecione uma fase e, em seguida, use estes botões para mover a localização da fase na lista.  

       > [!Important]  
       > Reveja as definições de fase depois de alterar a ordem. Certifique-se de que as seguintes definições ainda são consistentes com os seus requisitos para esta implementação faseada:  
       > 
       > - Critérios para o sucesso da fase anterior  
       > - Condições para iniciar esta fase de implantação após o sucesso da fase anterior   

5. Selecione **Seguinte**. Reveja as definições na página **Resumo** e, em seguida, complete o assistente de implementação faseada create.  


Depois de criar uma implementação faseada, abra as suas propriedades para fazer alterações:  

- **Adicione** fases adicionais a uma implantação faseada existente.  

- Se uma fase não estiver ativa, pode **editar,** **remover**ou **movê-la** para cima ou para baixo. Não se pode movê-lo antes de uma fase ativa.  

- Quando uma fase está ativa, é só para ler. Não pode editá-lo, removê-lo ou mover a sua localização na lista. A única opção é **ver** as propriedades da fase.  

- Uma implementação faseada de aplicação é sempre apenas leitura.  



## <a name="next-steps"></a>Passos seguintes

Gerir e monitorizar as implementações faseadas:
- [Aplicação](manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)
- [Atualização de software](manage-monitor-phased-deployments.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Sequência de tarefas](manage-monitor-phased-deployments.md)  

