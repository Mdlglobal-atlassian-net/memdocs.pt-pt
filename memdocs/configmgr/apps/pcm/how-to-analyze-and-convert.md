---
title: Como analisar e converter pacotes
titleSuffix: Configuration Manager
description: Saiba como analisar e converter pacotes com Gestor de Conversão de Pacotes em Gestor de Configuração.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f72e7330909bc5653e69790e38ae043e539cc239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709937"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Como analisar e converter pacotes com Gestor de Conversão de Pacotes

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1357861-->

Antes de converter um pacote, primeiro analise-o. Dependendo dos resultados da análise, pode então fazer uma das seguintes tarefas:

- **Converta** o pacote numa aplicação. Na lista **pacote** na consola, o estado de prontidão apresenta **Automático**.  

- **Fixe e converta** o pacote, anexe coleções e crie condições globais. Na lista **pacote** na consola, o estado de prontidão apresenta **Automático**.  

- **Fixe e converta** a embalagem. Na lista **pacote** na consola, o estado de prontidão exibe **Manual**.  

- Deixe o pacote não convertido. Na lista **pacote** na consola, o estado de prontidão **apresenta Não Aplicável**.  



## <a name="how-to-analyze-packages"></a><a name="bkmk_analyze"></a>Como analisar pacotes

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **a Gestão**de Aplicações e selecionar o nó dos **Pacotes.**  

2. Selecione o pacote para converter. No separador **Casa** da fita, no grupo conversão de **pacotes,** selecione **Pacote de Análise**. O Gestor de Conversão de Pacotes analisa o pacote.  

3. Para ver o estado de prontidão do pacote, adicione a coluna **de prontidão** à lista de pacotes. O estado de prontidão do pacote determina a sua próxima ação:  

    - **Automático**: [Como converter pacotes](#bkmk_convert)  

        Para também anexar coleções e criar condições globais com um estado de prontidão **automática,** consulte [como corrigir e converter pacotes.](#bkmk_fix)  

    - **Manual**: [Como fixar e converter pacotes](#bkmk_fix)

    - **Não Aplicável**: Este pacote está em falta de conteúdo ou programa necessários. Adicione qualquer conteúdo ou programa em falta e análise de novo. Ou deixá-lo num estado não convertido e continuar a implantá-lo como um pacote.  

    - **Desconhecido**: Primeiro executar a tarefa **de Analisar,** ou esperar pela próxima análise programada. Se o Estado não mudar, consulte o Gestor de Conversão de [Pacotes De Resolução](troubleshoot-pcm.md)de Problemas.<!-- SCCMDocs#2044 -->

## <a name="how-to-convert-packages"></a><a name="bkmk_convert"></a>Como converter pacotes

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **a Gestão**de Aplicações e selecionar o nó dos **Pacotes.**  

2. Selecione a embalagem para converter com um estado de prontidão de **Automático**. No separador **Casa** da fita, no grupo conversão de **pacotes,** selecione **Converte Package**. O pacote de conversão para assistente de aplicação abre.  

3. No Pacote Converte para Assistente de Aplicação, reveja a lista de pacotes selecionados. Remova quaisquer pacotes que não queira converter e selecione **OK**. O Gestor de Conversão de Pacotes converte o pacote. A janela Completa de Conversão lista o Estado de Conversão das novas aplicações.  

    > [!Note]  
    > Ao converter um pacote, o site regista a data e a hora da conversão como a hora UTC.  

4. Siga as instruções na janela. Selecione ou **Ver aplicações** ou **Fechar**.  



## <a name="how-to-fix-and-convert-packages"></a><a name="bkmk_fix"></a>Como corrigir e converter pacotes

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **a Gestão**de Aplicações e selecionar o nó dos **Pacotes.**  

2. Selecione um pacote com um estado **de** prontidão manual ou **automático**. No separador **Casa** da fita, no grupo Conversão de **Pacotes,** selecione **Fix e Converte**.  

3. No Assistente de Conversão de Pacotes, reveja as informações na página de **Seleção** de **Pacotes,** observando os itens a corrigir . Em seguida, selecione **Seguinte**.  

4. Na página De Revisão da **Dependência,** reveja se o pacote estiver dependente de outros pacotes listados e, em seguida, selecione **Next**.  

    > [!Note]  
    > Se não converteu nenhum dos pacotes dependentes listados, converta primeiro esses pacotes. Em seguida, reiniciar o processo de conversão do pacote.  
    >  
    > Se não for necessária uma dependência, apague-a ou ignore-a e continue o processo de conversão.  

5. Na página Tipo de **Implementação,** reveja os tipos de implementação para a nova aplicação. Altere as suas prioridades ou elimine os tipos de implementação.  

6. Se algum dos novos tipos de implementação não tiver um método de deteção associado, a coluna Método de **Deteção** apresenta um ícone de advertência. Complete as seguintes ações:  

    1. Selecione **editar método de deteção**.  

    2. Selecione **Adicionar**.  

    3. Na caixa de diálogo da regra de deteção, especifique um **Tipo de Definição**.  

    4. Para o tipo de definição especificado, introduza as informações adicionais necessárias para a regra de deteção.  

    5. Selecione **OK**. Se necessário, repita este processo para adicionar múltiplos métodos de deteção a cada tipo de implementação.  

    6. Selecione **OK**. Verifique se a coluna Método de **Deteção** apresenta um ícone para confirmar um método de deteção corretamente especificado.  

7. Selecione **Seguinte**.  

8. Na página **de Seleção de Requisitos,** reveja os tipos de implementação da nova aplicação. Selecione um tipo de implementação e reveja os requisitos para esse tipo de implementação.  

    > [!Note]  
    > O assistente apenas apresenta os requisitos que o Gestor de Conversão de Pacotes converte. Não converte todas as consultas wQL em coleções de dispositivos em requisitos.  

9. Adicione requisitos para um tipo de implementação selecionado, se necessário.  

10. Selecione **Seguinte**.  

11. Complete o assistente para criar a aplicação.  

    > [!Note]  
    > Ao converter um pacote, o site regista a data e a hora da conversão como a hora UTC.  



## <a name="monitor"></a><a name="bkmk_monitor"></a>Monitor

Vá ao espaço de trabalho de **monitorização** da consola Do Gestor de Configuração e selecione **O Estado**de Conversão do Pacote . Este painel de instrumentos mostra o estado geral de análise e conversão dos pacotes no site. Uma nova tarefa de fundo resume automaticamente os dados da análise.

> [!Tip]  
> O Gestor de Conversão de Pacotes integrado com o Gestor de Configuração não requer que marque a análise dos pacotes. Esta ação é tratada pela tarefa integrada de resumição.

![Screenshot de exemplo Pacote Conversão Status dashboard](media/1357861-pcm-dashboard.png)
