---
title: Gerir & monitorizar implementações faseadas
titleSuffix: Configuration Manager
description: Compreenda como gerir e monitorizar implementações faseadas para software no Gestor de Configuração.
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 419b91365d80062baabc289d0dbcf064c89b71a0
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110479"
---
# <a name="manage-and-monitor-phased-deployments"></a>Gerir e monitorizar as implementações faseadas

Este artigo descreve como gerir e monitorizar implementações faseadas. As tarefas de gestão incluem iniciar manualmente a próxima fase e suspender ou retomar uma fase. 

Primeiro, é necessário criar uma implantação faseada: 
- [Aplicação](create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Atualização de software](create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Sequência de tarefas](create-phased-deployment-for-task-sequence.md)  



## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a>Passar para a próxima fase

Quando selecionar a definição, **inicie manualmente a segunda fase de implantação,** o site não inicia automaticamente a próxima fase com base em critérios de sucesso. Tens de mover a implantação faseada para a próxima fase.  

1. Como iniciar esta ação varia com base no tipo de software implantado:  

    - **Aplicação** (apenas na versão 1806 ou posterior): Vá ao espaço de trabalho da Biblioteca de **Software,** expanda a Gestão de **Aplicações,** e selecione **Aplicações**.   

    - **Atualização de software** (apenas na versão 1810 ou posterior): Vá ao espaço de trabalho da Biblioteca de **Software** e, em seguida, selecione um dos seguintes nós:    
        - Atualizações de Software  
            - **Todas as atualizações de software**  
            - **Grupos de atualização de software**   
        - Assistência ao Windows 10, **todas as atualizações do Windows 10**  
        - Gabinete 365 Gestão de Clientes, **Gabinete 365 Atualizações**  

    - **Sequência de tarefas**: Vá ao espaço de trabalho da Biblioteca de **Software,** expanda **sistemas operativos**e selecione sequências de **tarefas**.   

2. Selecione o software com a implementação faseada.  

3. No painel de detalhes, mude para o separador **De implantação faseada.**  

4. Selecione a implementação faseada e clique **em mover para a próxima fase** na fita.  

    ![Menu de clique direito mostrando ações em uma implementação faseada](media/Suspend-phased-deployment.PNG)



## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a>Suspender e retomar fases 

Pode suspender manualmente ou retomar uma implantação faseada. Por exemplo, cria-se uma implementação faseada para uma sequência de tarefas. Ao monitorizar a fase para o seu grupo piloto, nota um grande número de falhas. Suspende a implantação faseada para impedir que outros dispositivos executem a sequência de tarefas. Depois de resolver o problema, retoma a implementação faseada para continuar o lançamento. 

1. Como iniciar esta ação varia com base no tipo de software implantado:  

    - **Aplicação** (apenas na versão 1806 ou posterior): Vá ao espaço de trabalho da Biblioteca de **Software,** expanda a Gestão de **Aplicações,** e selecione **Aplicações**.   

    - **Atualização de software** (apenas na versão 1810 ou posterior): Vá ao espaço de trabalho da Biblioteca de **Software** e, em seguida, selecione um dos seguintes nós:    
        - Atualizações de Software  
            - **Todas as atualizações de software**  
            - **Grupos de atualização de software**   
        - Assistência ao Windows 10, **todas as atualizações do Windows 10**  
        - Gabinete 365 Gestão de Clientes, **Gabinete 365 Atualizações**  

    - **Sequência de tarefas**: Vá ao espaço de trabalho da Biblioteca de **Software,** expanda **sistemas operativos**e selecione sequências de **tarefas**. Selecione uma sequência de tarefas existente e, em seguida, clique em **Criar Implantação Faseada** na fita.  

2. Selecione o software com a implementação faseada.  

3. No painel de detalhes, mude para o separador **De implantação faseada.**  

4. Selecione a implementação faseada e clique **em Suspender** ou **Retomar** na fita. 

> [!NOTE]
> A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver o nome antigo no produto do Gestor de Configuração e documentação enquanto a consola está a ser atualizada. 

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="monitor"></a><a name="bkmk_monitor"></a>Monitor
<!--1358577-->
A partir da versão 1902, as implementações faseadas têm o seu próprio nó de monitorização dedicado, facilitando a identificação de implementações faseadas que criou e navegar para a visão de monitorização de implementação faseada. A partir do espaço de trabalho **de monitorização,** selecione **Implantações Faseadas**e, em seguida, clique duas vezes numa das implementações faseadas para ver o estado. <!--3555949-->

No Diretor de Configuração 1806 e 1810, pode ver a experiência de monitorização nativa para implementações faseadas. A partir do nó de **implantação** no espaço de trabalho **de monitorização,** selecione uma implantação faseada e, em seguida, clique no Estado de **Implantação Faseada** na fita.

![Painel de instrumentos de implantação faseado mostrando o estado de duas fases](media/1358577-phased-deployment-status.png)

Este painel de instrumentos mostra as seguintes informações para cada fase da implantação:  

- **Total de dispositivos** ou **recursos totais**: Quantos dispositivos são alvo desta fase.  

- **Estado**: O estado atual desta fase. Cada fase pode estar num dos seguintes estados:  

    - **Implementação criada**: A implementação faseada criou uma implementação do software para a recolha para esta fase. Os clientes são ativamente direcionados para este software.  

    - **Espera**: A fase anterior ainda não atingiu os critérios de sucesso para que a implantação continue nesta fase.  

    - **Suspenso**: Um administrador suspendeu a implantação.  

- **Progresso**: Os estados de implantação codificados por cores dos clientes. Por exemplo: Sucesso, Progresso, Erro, Requisitos Não Cumpridos e Desconhecidos. 

#### <a name="success-criteria-tile"></a>Critérios de sucesso azulejos

Utilize a lista de desativação da **fase selecionada** para alterar o visor do azulejo dos Critérios de **Sucesso.** Este azulejo compara o **Objetivo de Fase** com a conformidade atual da implantação. Com as definições padrão, o objetivo de fase é de 95%. Este valor significa que a implementação precisa de uma conformidade de 95% para passar à fase seguinte.

No exemplo, a meta de fase é de 65%, e a atual conformidade é de 66,7%. A implantação faseada passou automaticamente para a segunda fase, porque a primeira fase cumpria os critérios de sucesso.  

   ![Exemplo De Sucesso Critérios de azulejos do Estado de Implantação Faseada onde a meta é de 65%](media/pod-status-success-criteria-tile.png)

O objetivo de fase é o mesmo que a percentagem de sucesso de **implantação** nas Definições de Fase para a *próxima* fase. Para que a implantação faseada inicie a próxima fase, esta segunda fase define os critérios para o sucesso da primeira fase. Para ver esta definição: 

1. Vá ao objeto de implementação faseado do software e abra as Propriedades de Implantação Faseadas.  

2. Mude para o separador **Fases.** Selecione **a Fase 2** e clique em **Ver**.  

3. Na janela de fase Propriedades, mude para o separador Definições de **Fase.**  

4. Ver o valor da **percentagem** de sucesso de implantação nos Critérios de sucesso do grupo *de fases anteriores.*  

Por exemplo, as seguintes propriedades são para a mesma fase que os critérios de sucesso de azulejos acima indicados onde os critérios são de 65%:  
![Separador de definições de fase nas propriedades da fase](media/phase-properties-phase-settings.png)

