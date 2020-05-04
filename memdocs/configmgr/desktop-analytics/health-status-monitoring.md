---
title: Monitorização do estado de funcionamento
titleSuffix: Configuration Manager
description: Saiba como funciona a monitorização do estado de saúde no Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 359fdec13ee6bfd43e66d4bf9cec70c5a3188a32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712758"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Monitorização do estado de saúde no Desktop Analytics

Ao [implementar uma atualização para a produção,](deploy-prod.md)utilize o Desktop Analytics para ajudar a monitorizar o estado de saúde dos seus dispositivos. Este artigo explica em pormenor como funciona a monitorização da saúde.

Para obter mais informações sobre como utilizar esta funcionalidade, consulte [Monitorize a saúde dos dispositivos atualizados](deploy-prod.md#bkmk_monitor).

![Screenshot da página monitor a saúde do Desktop Analytics](media/monitor-health.png)

> [!NOTE]  
> O Desktop Analytics apenas recolhe dados de saúde de dispositivos que fornecem dados de utilização que pode usar como denominador. Isto significa que não inclui dispositivos que executam o Windows 7 e o Windows 10 que não estão definidos para partilhar dados de diagnóstico ao nível do Enhanced (Limited). Se mais de 10% dos dispositivos que executam o Windows 10 estiverem definidos para partilhar dados de diagnóstico em outros níveis que não o Enhanced (Limited), a página de **saúde monitor** aapresentar um aviso na área do banner.  

Para ver mais informações sobre uma aplicação específica, selecione-a na lista.

## <a name="apps"></a>Aplicações

### <a name="health-status-factors"></a>Fatores de estado da saúde

![Fatores de estado de saúde para uma aplicação no Desktop Analytics](media/monitor-health-status-factors.png)

Desktop Analytics monitoriza os seguintes fatores de estado de saúde para aplicações:

- **% Dispositivos com falhas**: Nas últimas duas semanas, o número de dispositivos em que esta aplicação em particular se despenhou dividida pelo número de dispositivos em que a aplicação foi utilizada. Esta visão permite-lhe ver se a estabilidade da aplicação aumentou ou diminuiu na nova versão do SISTEMA. Desktop Analytics calcula esta percentagem para os seguintes conjuntos:  

  - **Após a atualização**: Dispositivos que tenham atualizado para a versão o-alvo o SISTEMA especificada no plano de implementação. Para reduzir o número de ativos com dados insuficientes, o Desktop Analytics recolhe estes dados para todos os seus dispositivos atualizados. Este conjunto inclui os dispositivos que não estão no plano de implementação.  

  - **Antes da atualização**: Dispositivos que se encontram numa versão So mais cedo do que o especificado no plano de implementação. Esta lista não inclui dispositivos que executam o Windows 7.  

  - **Avg comercial**: A taxa média de colisão (avg) em todos os dispositivos comerciais. Esta média é calculada em *todas as* versões da app. Se a sua versão mostrar uma taxa de crash acima da média comercial, pode haver uma versão mais estável disponível.  

- **% Sessões com acidentes**: Semelhante à anterior, mas conta a percentagem de sessões com acidentes nas últimas duas semanas.  

Para determinar o estado de saúde de uma aplicação, o Desktop Analytics requer dados de pelo menos 20 dispositivos. Caso contrário, reporta **dados insuficientes** para a aplicação. O serviço calcula o estado de saúde com base na taxa de colisão da *sessão* destes dispositivos. A taxa de colisão do dispositivo é fornecida apenas para informações. Não é usado no cálculo do estado de saúde.

### <a name="usage"></a>Utilização

<!-- 5533890 -->

- **Dispositivos ativos**: Este valor é a contagem de dispositivos onde um utilizador lançou a aplicação selecionada nas últimas duas semanas. Baseia-se em dispositivos no plano de implementação selecionado que executa a versão direcionada do Windows 10.

- **Sessões**: Este valor é o número total de vezes que um utilizador lançou a aplicação selecionada na versão direcionada do Windows.

### <a name="additional-tabs"></a>Separadores adicionais

Na parte inferior da página de detalhes da aplicação, os seguintes três separadores podem ajudá-lo a resolver problemas:

- **Outras versões**: Uma lista de versões alternativas desta aplicação. Para cada versão, mostra as alterações relativas às taxas de colisão dentro da sua organização e da média comercial. Se encontrar uma versão posterior da app com uma taxa de crash mais baixa, atualizar a aplicação pode ajudar.  

    Também mostra se a versão tem insights avançados. Para mais informações, consulte a avaliação da [compatibilidade.](compat-assessment.md)  

- **Principais questões**: Uma lista das iDs de falha mais frequentes por exemplo. Um ID de falha identifica os vestígios da pilha associados ao acidente. Pode utilizar este ID quando ligar para o fornecedor de aplicações para obter suporte.  

- **Falhas recentes**: Uma lista de dispositivos em que a aplicação se despenhou recentemente. Pode filtrar por id de falha e outros critérios. Utilize estas informações para resolver o problema, recolhendo registos ou tentando correções em dispositivos específicos antes de tentar uma implementação mais ampla.  

Se encontrar uma regressão de saúde grave que não consegue corrigir, altere a decisão de **Upgrade** da aplicação para **Unable**. Esta ação impede a futura implementação da atualização para dispositivos com este ativo.

## <a name="see-also"></a>Consulte também

- [Avaliação da compatibilidade no Desktop Analytics](compat-assessment.md)  

- [Como implantar para produção com desktop Analytics](deploy-prod.md)  
