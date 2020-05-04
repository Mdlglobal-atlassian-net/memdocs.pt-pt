---
title: Tarefas comuns de gestão da conformidade
titleSuffix: Configuration Manager
description: Conheça as definições de conformidade do Gestor de Configuração trabalhando em alguns cenários comuns.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1ccb0f0a042a0dd82817e030f96bbbc729e752f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712177"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Tarefas comuns para gerir a conformidade com dispositivos com o cliente do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo dá-lhe uma introdução à utilização de definições de conformidade do Gestor de Configuração, orientando-o através de alguns cenários comuns que poderá encontrar.  

 Se já está familiarizado com as definições de conformidade, pode encontrar informações detalhadas sobre todas as funcionalidades que utiliza em itens de [Configuração para dispositivos geridos com o cliente Do Gestor](../../compliance/deploy-use/create-configuration-items.md)de Configuração .  

 Antes de começar, leia Iniciar as [definições de conformidade](../../compliance/get-started/get-started-with-compliance-settings.md) para aprender alguns fundamentos sobre as definições de conformidade. Leia [o Plano e configure as definições](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) de conformidade para obter informações sobre os pré-requisitos necessários.  

## <a name="general-information-for-each-scenario"></a>Informações gerais para cada cenário  
 Em cada cenário, irá criar um item de configuração que realiza uma tarefa específica. Para abrir o Assistente de Configuração Criar e começar, tome estes passos:  

1.  Na consola do Gestor de Configuração, selecione Itens de configuração de**configuração**de > **definições**de conformidade de **Ativos e conformidade.** >   

1.  No separador **Home,** no grupo **Criar,** selecione **Create Configuration Item**.  

1.  Na página **geral** do Assistente de Configuração Create, mostrado na seguinte imagem, especifique um nome e descrição para o item de configuração. Em seguida, escolha o tipo de artigo de configuração apropriado para cada cenário neste artigo.  

     ![Página geral do Assistente de Configuração Criar](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Cenário: Desative Bluetooth nos dispositivos do Windows 10

 Neste cenário, o seu departamento de segurança determinou que a capacidade Bluetooth nos dispositivos poderia ser usada para transmitir informações corporativas sensíveis fora da empresa. Atualizou recentemente todos os seus computadores para o Windows 10. Decidiu desativar o Bluetooth nestes dispositivos.  

1. Na página **geral** do Assistente de Configuração Criar, selecione o tipo de item de configuração **do Windows 10** e, em seguida, selecione **Next**.  

2. Na página **Plataformas Suportadas** do assistente, selecione todas as plataformas Windows 10.  

3. Na página Definições do **Dispositivo,** selecione **Dispositivo**, e, em seguida, selecione **Next**.  

4. Na página **Dispositivo** , selecione **Proibido** como o valor de **Bluetooth**.  

5. Selecione **Remediar definições incompatíveis** para garantir que a alteração é aplicada a todos os dispositivos Windows 10.  

6. Conclua o assistente para criar o item de configuração.  

 Agora pode utilizar a informação nas [tarefas Comuns para criar e implementar linhas](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) de base de configuração com o artigo do Gestor de Configuração para ajudá-lo a implementar a configuração que criou para dispositivos.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Cenário: Remediar um valor de registo incorreto em computadores de secretária Windows

> [!NOTE] 
> Nos computadores Mac que executam o cliente do Gestor de Configuração, tem duas opções para avaliar a conformidade:  
> - Avaliar um ficheiro de preferências (plist) do Mac OS X.
> - Utilizar um script personalizado e avaliar os resultados devolvidos pelo script.  
>
>Para mais informações, consulte [como criar itens de configuração para dispositivos Mac OS X geridos com o cliente Do Gestor](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)de Configuração .  

 Neste cenário, descobre que uma importante aplicação de linha de negócio não funciona corretamente em alguns computadores windows 8.1 que gere. Você determina que isto é porque uma chave de registo chamada **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuração\Configuração\Configuração** 1 está definida para um valor de **0** em alguns computadores. Para que a app line-of-business seja executada com sucesso, este valor tem de ser definido para **1**.  

 Neste procedimento, irá criar um item de configuração que monitoriza e remedia automaticamente quaisquer valores-chave de registo incorretos que sejam encontrados.  

1. Na página **geral** do Assistente de Configuração Criar, selecione o tipo de configuração **do Windows Desktops e Servers (personalizado)** e, em seguida, selecione **Next**.  

2. Na página plataformas **suportadas** do assistente, selecione **o Windows 8.1** (para garantir que o item de configuração se aplica apenas aos computadores afetados).  

3. Na página **Definições,** selecione **Novo** para criar uma nova definição.  

4. No separador **Geral** da caixa de diálogo **Criar Definição,** configure estas definições:  

   -   **Definição** > **de exemplo** de nome  

   -   **Definição do valor** > **do registo**  

   -   **Tipo de dados** > **Integer** (porque o valor contém apenas um número)  

   -   **HKEY_LOCAL_MACHINE da colmeia** > **HKEY_LOCAL_MACHINE**  

   -   **Software** > **chave\Woodgrove\APP\Configuração\Configuração**  

   -   **Valor** > **1** (o valor exigido)  

5. No separador Regras de **Conformidade** da caixa de diálogo **Criar Definição,** selecione **New**. Na caixa de diálogo **'Criar Regra',** configure estas definições:  

   -   **Regra** > **do exemplo** de nome  

   -   **Definição selecionada** > Verifique se a definição selecionada é **definição exemplo**.

   -   **Tipo de** > regra**Valor**  

   -   **A definição deve respeitar a seguinte regra** > Verificar se o nome de definição está correto e configurar a opção para especificar que o valor de definição deve ser igual a **1**.  

   -   **Remediar regras não conformes quando suportadas** > Selecione esta caixa de verificação para garantir que o Gestor de Configuração irá redefinir o valor da chave de registo para o valor correto se estiver errado.  

6. Conclua o assistente para criar o item de configuração.  

 Agora pode utilizar a informação nas [tarefas Comuns para criar e implementar artigos](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) de base de configuração para ajudá-lo a implementar a configuração que criou para dispositivos.  

## <a name="next-steps"></a>Passos seguintes

[Criar e implementar linhas de base da configuração](common-tasks-for-creating-and-deploying-configuration-baselines.md)
