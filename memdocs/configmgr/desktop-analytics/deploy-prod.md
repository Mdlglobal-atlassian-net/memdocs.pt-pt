---
title: Como implantar para a produção
titleSuffix: Configuration Manager
description: Um guia de como ser implantado para um grupo de produção desktop Analytics.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7a14da1505e89dfd61a3dc4f13385fbf5c21d41
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723657"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Como implantar para produção com desktop Analytics

Depois de ter [enviado para piloto](deploy-pilot.md) e ter revisto o estado dos seus ativos, está pronto para atualizar o resto do seu ambiente de produção.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Existem três peças principais para realizar a implementação de atualizações para dispositivos de produção:

1. [Rever os ativos que necessitem de uma decisão](#bkmk_review)de atualização : Para tornar os dispositivos prontos para a implantação da produção, os seus ativos devem ter a sua decisão de atualização definida para **Ready** or **Ready, reparações necessárias**.  

2. [Implemente para dispositivos prontos:](#bkmk_deploy)Utilize o Gestor de Configuração para atualizar os dispositivos prontos. O Desktop Analytics fornece a lista de dispositivos prontos para a implantação da produção e relatórios para monitorizar o sucesso da implementação.  

3. [Monitorize a saúde dos dispositivos atualizados](#bkmk_monitor): À medida que a implementação da atualização avança, monitorize a saúde de importantes ativos. Se alguns precisarem de atenção, problemas e resolver estes problemas. Se decidir que os problemas não podem ser corrigidos, pare a implementação para os dispositivos afetados, definindo a sua decisão de upgrade para **Unable**.  

> [!NOTE]  
> Quando estiver confiante no sucesso da implantação do piloto, inicie a implantação da produção a qualquer momento. Não há necessidade de que todos os dispositivos piloto cheguem primeiro ao estado "concluído".  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a>Rever os ativos que precisam de uma decisão de atualização

O Desktop Analytics guia-o através do processo de revisão dos seus ativos para implementação de produção. No portal Azure, vá a planos de **implantação,** selecione um plano de implementação e, em seguida, selecione **a produção prepare** no menu esquerdo.

![Screenshot da visão de produção de prepare no Desktop Analytics](media/prepare-production.png)

Reveja o estado das suas aplicações. Utilize essa informação para definir a decisão de atualização para cada um desses ativos.

Utilize cada um dos separadores para rever o estado das aplicações. Em cada vista aparatada, pode filtrar os resultados para mostrar dispositivos que estão no caminho certo para a atualização, precisam da sua atenção, dispositivos com resultados mistos e esses dispositivos em estado indeterminado.

Selecione **Objetivos de Encontro** para filtrar a vista para ativos que provavelmente estejam prontos para a implantação da produção com base nos seguintes critérios:

- Risco: uma avaliação prévia dos riscos conhecidos para atualizar dispositivos que tenham este ativo instalado  

- Estado de saúde: uma avaliação pós-actualização dos dispositivos noutras implementações e se tiveram problemas após a instalação da atualização. Para obter mais informações sobre saúde, consulte [Monitorize a saúde dos dispositivos atualizados](#bkmk_monitor).  

Para aprovar um ativo para atualização, selecione o nome na lista e, em seguida, selecione uma das seguintes opções da lista de decisão de **Upgrade:**

- Revisão em curso
- Pronto
- Pronto (com reparação)
- Incapaz
- Não revisto

Para definir este valor para várias aplicações ao mesmo tempo, utilize a primeira coluna para **selecionar este item**, e depois escolha definir **a decisão**de upgrade .

![Definir opção de decisão de upgrade em várias aplicações](media/prep-prod-set-upgrade-decision.png)

Selecione **nenhum dado** para ver ativos que não possam ser classificados. Estes ativos geralmente são ativos que não têm cobertura suficiente para desktop Analytics para realizar uma análise do risco ou estado de saúde. Para melhorar a cobertura, adicione dispositivos adicionais com estes ativos ao piloto ou peça aos utilizadores piloto para experimentarem estes ativos.

Pode também haver ativos no estado de **Atenção Necessário** ou **Resultados Mistos.** Estes ativos podem necessitar de uma revisão adicional antes de tomar uma decisão de atualização para eles.

Reveja todas as aplicações. Uma vez que um determinado dispositivo tenha uma decisão positiva de atualização para todos os ativos, então o seu Estado muda para "pronto para produção". Consulte a contagem atual na página principal do plano de implementação selecionando o terceiro passo de implementação, **Deploy**.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a>Implementar para dispositivos prontos

O Gestor de Configuração utiliza os dados do Desktop Analytics para criar uma recolha para a implementação da produção. Não implemente a sequência de tarefas usando uma implantação tradicional. Utilize o seguinte procedimento para criar uma implementação integrada no Desktop Analytics:

Se seguiu o processo recomendado para [implantar em dispositivos piloto,](deploy-pilot.md#deploy-to-pilot-devices)a implementação faseada do Gestor de Configuração está pronta. À medida que marca os ativos como *prontos,* o Desktop Analytics sincroniza automaticamente esses dispositivos para o Gestor de Configuração. Estes dispositivos são adicionados à coleção de produção. Quando a implementação faseada passa para a segunda fase, estes dispositivos de produção recebem a implementação da atualização.

Se configurar a implementação faseada para **iniciar manualmente a implementação da segunda fase,** então terá de movê-la manualmente para a fase seguinte. Para obter mais informações, consulte [Gerir e monitorizar as implementações faseadas](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move).

Se criou uma única implementação integrada no Desktop Analytics para a coleção de pilotos, então precisa de repetir esse processo para ser implantado na coleção de produção.


### <a name="address-deployment-alerts"></a>Alertas de implementação de endereços

Tal como acontece com a implementação do piloto, o Desktop Analytics aconselha-o a quaisquer problemas que necessitem da sua atenção durante a implementação da produção. No Desktop Analytics, vá ao plano de implementação e selecione o estado de **implantação** no menu esquerdo. A visão do estado de implementação lista os dispositivos nas seguintes categorias:  

- Não iniciadas
- Em curso
- Concluído
- Precisa de atenção - Dispositivos (classificados pelo nome do dispositivo)
- Precisa de atenção - Questões (ordenadas por tipo de edição)

![Screenshot do Estado de implantação da produção do Desktop Analytics](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a>Monitorizar a saúde dos dispositivos atualizados

A página de **produção da Prepare** centra-se em ajudá-lo a tomar decisões de upgrade para os seus ativos. Esta página por defeito mostra apenas os ativos que ainda não estão no estado **Ready.** A página de **saúde monitora** os problemas de saúde em qualquer ativo notável, mesmo os ativos que estão marcados **Ready**. Se descobrir problemas, pode resolver problemas e corrigir o problema, ou alterar a decisão de upgrade para **Unable**. Ao alterar a decisão de upgrade, esta ação impede futuras atualizações em dispositivos com esse ativo.

Filtre esta página por ativos com os seguintes estados de saúde:

| Filtro de estado de saúde | Descrição |
|----------------------|-------------|
| **Atenção necessária** | (Filtro predefinido) Desktop Analytics deteta uma regressão estatisticamente significativa a alguma métrica de saúde para esse ativo
| **Objetivos de cumprimento** | Desktop Analytics não deteta regressão no comportamento |
| **Dados insuficientes** | Desktop Analytics não tem dados suficientes sobre este ativo para fazer quaisquer recomendações |
| **Sem dados** | Ainda não há dados de utilização disponíveis para este ativo |

Para mostrar uma visão não filtrada de todos os ativos, selecione o filtro atual. Esta ação remove o filtro.

> [!NOTE]  
> Para reduzir o número de ativos com dados insuficientes, o Desktop Analytics monitoriza os ativos em todos os seus dispositivos que atualizaram para a versão target Do Windows especificada no seu plano de implementação. Estes dispositivos incluem os que não estão incluídos no plano de implementação específico.  

A ordem de classificação padrão é pelo número de dispositivos que tiveram um incidente com esse ativo em particular, para que você possa ver rapidamente quais estão a causar mais problemas. Por exemplo, ao visualizar **Apps**, classifica por Dispositivos com falhas de **aplicações nas últimas duas semanas.**

Se quiser olhar para a saúde de todos os ativos, mesmo aqueles ativos com dados insuficientes para o Desktop Analytics fazer inferências estatísticas, utilize o seguinte processo:

1. Selecione a queda nos **Dispositivos com incidentes na coluna das últimas duas semanas.** Adicione um filtro apenas aos ativos que tiveram incidentes em algum número mínimo de dispositivos para serem interessantes. Por exemplo, mostrar itens com valores **superiores** a 100.  

2. Selecione a queda nos **dispositivos % com incidentes na** coluna das últimas duas semanas e selecione para ordenar por **Descida**.  

    A opinião resultante mostra os ativos com a maior taxa de incidentes num número mínimo de incidentes.  

3. Selecione um ativo para obter mais detalhes ou alterar a sua decisão de upgrade.  

Para mais informações, consulte a monitorização do estado de [saúde.](health-status-monitoring.md)
