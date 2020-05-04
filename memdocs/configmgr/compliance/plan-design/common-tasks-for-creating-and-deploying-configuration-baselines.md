---
title: 'Tarefas comuns para as linhas de base de configuração '
titleSuffix: Configuration Manager
description: Saiba como criar e implementar as linhas de base de configuração do Gestor de Configuração.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52e83639029db9eeb4ef64657e70e3dc11aab8f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712205"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-configuration-manager"></a>Tarefas comuns para criar e implementar linhas de base de configuração com O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico contém cenários comuns para ajudá-lo a aprender como criar e implementar as linhas de base de configuração do Gestor de Configuração.  

 Se já está familiarizado com as definições de conformidade, pode encontrar documentação detalhada sobre todas as funcionalidades que utiliza nas linhas de base de [configuração Create](../../compliance/deploy-use/create-configuration-baselines.md) e implementar tópicos de base de [configuração.](../../compliance/deploy-use/deploy-configuration-baselines.md)  

 Antes de começar, leia Iniciar as [definições de conformidade](../../compliance/get-started/get-started-with-compliance-settings.md) para aprender alguns fundamentos sobre as definições de conformidade, e também ler [Plan para e configurar as definições](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) de conformidade para implementar quaisquer pré-requisitos necessários.  

## <a name="create-a-configuration-baseline"></a>Criar uma linha de base de configuração  
 Neste exemplo, criou um item de configuração apenas para PCs windows 10 que executam o cliente do Gestor de Configuração.  

 Este item de configuração impõe uma palavra-passe obrigatória de, pelo menos, 6 carateres em PCs Windows 10. O item de configuração tem o nome **Imposição de Palavras-passe do Windows 10**.  

Utilize o seguinte procedimento para aprender a adicionar este item de configuração a uma linha de base de configuração para prepará-lo para a sua implementação.  

1. Na consola do Gestor de Configuração, clique em **Ativos e** > **Definições** > de Conformidade **.**  

2. No separador **Base** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

3. Na caixa de diálogo **'Criar Configuração',** configure as seguintes definições:  

   -   **Nome** - Introduza **Palavras-passe do Windows 10** (ou outro nome à sua escolha)  

4. Clique em **adicionar** > itens de**configuração**.  

5. Na caixa de diálogo **Adicionar Itens de Configuração** , selecione o item de configuração **Imposição de Palavras-passe do Windows 10** anteriormente criado e, em seguida, clique em **Adicionar**.  

6. Clique em OK para fechar a caixa de diálogo **de configuração de** adicionar itens e voltar à caixa de diálogo **'Criar Configuração' Baseline.**

7. Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** .  

   Pode agora ver a linha de base de configuração no nó de Base de **Configuração** da consola 'Gestor de Configuração'.  

## <a name="deploy-the-configuration-baseline"></a>Implementar a linha de base de configuração  
 Neste exemplo, implementa a linha de base de configuração que criou no procedimento anterior para uma coleção de computadores.  

1. Na consola do Gestor de Configuração, clique em **Ativos e** > **Definições** > de Conformidade **.**  

2. Na lista de linhas de base de configuração, selecione **Palavras-passe do Windows 10**.  

3. No separador **Home Page**, no grupo **Implementação**, clique em **Implementar**.  

4. Na caixa de diálogo de configuração de **configuração,** configure as seguintes definições:  

   -   **Linhas de base de configuração selecionadas** - Certifique-se de que a linha base de configuração **Palavras-passe do Windows 10** foi adicionada automaticamente a esta lista.  

   -   **Remediar regras não conformes quando suportadas** - Verifique esta caixa para se certificar de que se as definições corretas não estiverem presentes em dispositivos direcionados, então são remediadas pelo Gestor de Configuração.  

   -   **Recolha** - Clique em **Navegar** para escolher a recolha de computadores em que a linha de base de configuração é avaliada e remediada para a conformidade. Neste exemplo, a linha de base de configuração foi implementada na coleção **Todos os Clientes de Servidor e de Ambiente de Trabalho** incorporada.  

       > [!TIP]  
       >  Não se preocupe se a coleção que escolheu contiver computadores ou dispositivos que não executam o Windows 10. Desde que configure plataformas suportadas no item de configuração que criou, apenas os Computadores Windows 10 são avaliados para o cumprimento.  

   -   Se necessário, configure o calendário pelo qual a linha de base de configuração é avaliada. Caso contrário, mantenha a predefinição de **7 Dias**.  

5. Clique em **OK** para fechar a caixa de diálogo **Implementar Linhas de Base de Configuração** e criar a implementação.  

   Se pretender ver rapidamente as estatísticas de compatibilidade para esta implementação, na área de trabalho **Monitorização** , clique em **Implementações**. Na parte inferior do ecrã, vê-se um gráfico de Estatísticas de **Conformidade.**  

## <a name="next-steps"></a>Passos seguintes 

Para obter informações mais detalhadas sobre como monitorizar as linhas de base de configuração, consulte [as definições](../../compliance/deploy-use/monitor-compliance-settings.md)de conformidade do Monitor .  
