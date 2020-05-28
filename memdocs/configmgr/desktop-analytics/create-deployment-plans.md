---
title: Como criar planos de implantação
titleSuffix: Configuration Manager
description: Um guia de como criar planos de implementação no Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ac9b5ddd85904c90709a9450d6d2a9ffd379ddb9
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268764"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Como criar planos de implementação no Desktop Analytics

Este artigo fornece os passos para a criação de um plano de implementação no Desktop Analytics. Antes de começar, primeiro [aprenda sobre os planos de implantação.](about-deployment-plans.md)

## <a name="create-a-plan-for-windows-10"></a>Criar um plano para o Windows 10

Siga os passos nesta secção para utilizar o Desktop Analytics para criar um plano para implementar o Windows 10.

1. Abra o [portal Desktop Analytics](https://aka.ms/desktopanalytics). Utilize credenciais que tenham pelo menos permissões de Colaboradores do **Espaço de Trabalho.**  

2. Selecione **Planos de Implantação** no grupo Gerir.  

3. No painel de Planos de **Implantação,** selecione **Criar**.  

4. No painel do **plano de implementação Criar,** configure as seguintes definições:  

    - **Nome**: Um nome único para o plano de implantação  

    - **Produtos e versões**: Escolha qual versão do Windows 10 para implementar. A Microsoft recomenda a criação de planos de implementação que utilizem a versão mais recente.  

    - **Grupos de dispositivos**: Selecione um ou mais grupos da mesma hierarquia. Estes grupos são coleções de [dispositivos](connect-configmgr.md#bkmk_Collections) sincronizadas do Gestor de Configuração.

        Se ligar várias hierarquias do Gestor de Configuração à mesma instância desktop Analytics, um nome de exibição para a hierarquia prefixa o nome da coleção na configuração piloto global. Este nome é a propriedade **Display Name** na ligação Desktop Analytics na consola 'Gestor de Configuração'.<!-- 4814075 -->

        > [!NOTE]
        > O suporte para várias hierarquias requer a versão 1910 ou mais tarde do Gestor de Configuração.
        >
        > Se selecionar coleções para várias hierarquias, o portal apresenta um aviso. Não se pode criar o plano de implantação com coleções de várias hierarquias.<!-- 4814075 -->

    - **Regras de prontidão**: Estas regras ajudam a determinar quais os dispositivos que se qualificam para a atualização. Para mais informações, consulte [as regras de prontidão](#readiness-rules).  

    - **Data de conclusão**: Escolha a data pela qual o Windows deve ser totalmente implantado em todos os dispositivos visados.  

5. Selecione **Criar**. O novo plano aparece na lista de planos de implantação enquanto está a ser processado. Para acelerar o processamento, solicite uma atualização de dados a pedido. Para mais informações, consulte [desktop Analytics FAQ](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Abra o plano de implementação selecionando o seu nome.  

7. No menu do plano de implementação, no grupo **Preparar,** selecione **Identificar a importância**.  

    1. No separador **Apps,** selecione para mostrar apenas ativos **não revistos.**  

    2. Selecione cada aplicação e, em seguida, **selecione Editar**. Pode selecionar mais do que uma aplicação para editar ao mesmo tempo.  

    3. Escolha um nível de importância na lista **de Importância.** Se pretender que o Desktop Analytics valide a aplicação durante o piloto, selecione **Critical** ou **Important**. Não valida aplicações marcadas como **Não Importantes.** Avalie a sua [compatibilidade](compat-assessment.md) e outros conhecimentos de plano ao atribuir níveis de importância.  

        Ao atribuir níveis de importância, também pode escolher a decisão de Upgrade.  

    4. Selecione **Guardar** quando estiver completo.  

8. No menu do plano de implementação, no grupo **Preparar,** selecione **Identificar o piloto**.  

    1. Reveja os dispositivos recomendados para o piloto.  

    2. Selecione cada dispositivo e selecione **Adicionar ao Piloto**. Se não concordar com a recomendação, **selecione Substitua**.  

        Para obter mais informações sobre como o Desktop Analytics faz estas recomendações, selecione o ícone de informação no canto superior direito do painel **piloto identificar.**

## <a name="readiness-rules"></a>Regras de prontidão

Estas regras ajudam-no a determinar quais os dispositivos que se qualificam para a atualização no local. Pode definir estas regras quando criar o plano de implementação, ou editá-las mais tarde.

Para alterar as regras de prontidão:

1. No portal Desktop Analytics, selecione o plano de implementação.
1. Ao lado do nome, **selecione Editar**.
1. Selecione **regras de prontidão**.
1. Selecione **Windows OS**.
1. Faça alterações conforme necessário e selecione **Guardar**.

Para atualizações **do Windows OS,** existem duas regras disponíveis: controladores de dispositivos e aplicações windows.

### <a name="device-drivers"></a>Controladores de dispositivo

Configure se os seus dispositivos obtêm controladores a partir do Windows Update. Este valor está **desligado** por defeito. Ative esta regra quando estiver a utilizar o Windows Update para o Negócios para gerir as atualizações, incluindo os controladores. Se estiver a utilizar o 'Gestor de Configuração' para gerir atualizações de software, desgenhe esta regra para **desligar**.

### <a name="windows-applications"></a>Aplicações do Windows

As aplicações que o Desktop Analytics mostra como *notáveis* baseiam-se no baixo limiar de contagem de instalações. Estabeleça este limiar nas regras de prontidão para o plano de implantação. Por predefinição, este limiar é de **2,0%.** Pode alterar o valor de `0.0` `10.0` .


## <a name="next-steps"></a>Próximos passos

Avançar para o próximo artigo para implantar em dispositivos piloto.
> [!div class="nextstepaction"]  
> [Implementar para piloto](deploy-pilot.md)  
