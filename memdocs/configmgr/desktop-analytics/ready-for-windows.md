---
title: Pronto para Windows
titleSuffix: Configuration Manager
description: Sobre a reforma do site Ready for Windows
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 75dd74e3c1019c9819b44a0ffa8936eeb9eee366
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268356"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Pronto para a reforma moderna do ambiente de trabalho FAQ

<!-- placeholder -->

## <a name="general"></a>Geral

### <a name="what-happened-to-the-ready-for-windows-website"></a>O que aconteceu ao site Ready for Windows?

Muitos clientes têm desafios em obter e manter-se atuais com o Windows 10 e office 365 ProPlus. O principal desafio é testar aplicações, porque este processo é tipicamente manual. É demorado para administradores de TI e proprietários de aplicações analisarem continuamente as aplicações existentes e, em seguida, remediar quaisquer problemas que surjam.

O *Diretório ready para desktop moderno* listado soluções de software que são suportadas e em uso em dispositivos comerciais que executam o Windows 10 e o Office 365 ProPlus. O diretório ajuda os gestores de TI que estão a considerar as versões mais recentes do Windows 10 e do Office 365 para as suas implementações.

O feedback dos gestores de TI é que querem estas informações integradas com as ferramentas que já utilizam para planear os seus planos de implementação. Utilize funcionalidades de prontidão [do Desktop Analytics](https://aka.ms/dadocs) e do Office [365 ProPlus](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) no Gestor de Configuração para planear e gerir os seus projetos de upgrade do Windows 10 e do Office 365 ProPlus. 

> [!Note]
> A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver referências ao nome antigo na consola do Gestor de Configuração e documentação de suporte enquanto a consola está a ser atualizada.

### <a name="what-is-desktop-analytics"></a>O que é a Análise de Computadores?

[Desktop Analytics](https://aka.ms/dadocs) é um serviço baseado na nuvem que se integra com o Gestor de Configuração. O serviço fornece informações e inteligência para que tome decisões mais informadas sobre a prontidão da atualização dos seus pontos finais windows. Combina os dados específicos da sua organização com insights agregados dos milhões de dispositivos Windows ligados aos serviços de cloud da Microsoft.

-    Obtenha uma visão abrangente dos pontos finais, aplicações e motoristas sob gestão na sua organização.

-    Avalie a aplicação e a compatibilidade do condutor com as mais recentes atualizações de funcionalidades do Windows. Receba recomendações de mitigação para questões conhecidas, bem como insights avançados para aplicações de linha de negócio.

-    Utilize inteligência artificial (IA) a partir da nuvem da Microsoft para otimizar o conjunto de dispositivos piloto que representam adequadamente o seu ambiente geral.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Por que devo usar desktop analytics para os meus planos de implementação do Windows?

Desktop Analytics fornece os seguintes benefícios:

-    Inventário de **dispositivos e software**: Inventário de fatores-chave como apps e versões do Windows.

-    **Identificação do piloto**: Identificação do conjunto mais pequeno de dispositivos que proporcionam a maior cobertura de fatores. Foca-se nos fatores que são mais importantes para um piloto de atualizações e atualizações do Windows. Garantir que o piloto é mais bem sucedido permite-lhe continuar mais rapidamente e com confiança para amplas implementações na produção.

-    **Identificação de problemas**: Utilizando dados de mercado agregados juntamente com dados do seu ambiente, o serviço prevê potenciais problemas para obter e manter-se atual com o Windows. Em seguida, sugere potenciais atenuações.

-    **Integração do Gestor**de Configuração : Permite a sua infraestrutura existente no local. Utilize estes dados e análises para implementar e gerir o Windows nos seus dispositivos.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>O que significa o *estado de Ready for Windows* no Desktop Analytics?

O Estado de **Adoção baseia-se** em informações de dispositivos comerciais que partilham dados com a Microsoft. O estado está integrado com declarações de suporte de fornecedores de software.

O Desktop Analytics fornece o estado de adoção de cada versão de um ativo encontrado em dispositivos comerciais. Este estado não inclui dados de dispositivos de consumo ou dispositivos que não partilhem dados. O estado pode não ser representativo da taxa de adoção em todos os dispositivos do Windows 10.

Para mais informações, consulte a avaliação da [compatibilidade.](compat-assessment.md)

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Que ativos obtêm o estado *de Ready for Windows* no Desktop Analytics? 

Os ativos têm o estado *Ready for Windows* na análise do Ambiente de Trabalho se:

-    O fornecedor de software declara apoio à solução.
-    Os clientes implementaram-no num número significativo de dispositivos comerciais do Windows 10 que estão a partilhar informações com a Microsoft.
-    O ativo é relevante para os utilizadores comerciais.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Que insights adicionais recebo no Desktop Analytics?

O Desktop Analytics fornece um inventário dos [dispositivos e das suas aplicações instaladas,](about-assets.md)bem como [informações avançadas](compat-assessment.md#advanced-insights) para aplicações de linha de negócio. 

## <a name="software-providers"></a>Fornecedores de software

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>Ainda posso listar a minha solução de software no Desktop Analytics?

Publique uma declaração de suporte de que o seu produto funciona com windows 10 ou 64 bits de 32 bits ou Office 365 ProPlus. Para mostrar as suas soluções no Desktop Analytics, fale com o seu contacto com a Microsoft.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Como é que a listagem das minhas soluções pode beneficiar-me?

Milhares de administradores de TI gerem milhões de dispositivos com Configuração Manager e Desktop Analytics. Utilizam estas ferramentas para planear e atualizar com confiança as suas organizações para a versão mais recente do Windows 10 e do Office 365 ProPlus. Também as usam para tomar decisões de compra para soluções de software.

A Microsoft integra declarações de suporte de fornecedores de software com as informações de adoção que recebem de dispositivos comerciais. As organizações de todo o mundo usam estes dados em desktop Analytics e ferramentas de prontidão do Office. 

Se as suas declarações de suporte não estiverem corretamente associadas aos ativos, fale com o seu contacto com a Microsoft.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>Posso ver métricas detalhadas de desempenho nos meus bens?

Avalie o desempenho das suas soluções com relatórios de saúde e métricas através do centro de desenvolvimento: 

- [Loja Windows](https://docs.microsoft.com/windows/uwp/publish/health-report)
- [Ambiente de Trabalho](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
- [Suplementos do Office](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>Como posso desenvolver ativos compatíveis para o Windows 10 e o Office 365 ProPlus?

Certifique-se de que as suas aplicações de desktop são compatíveis agora e mantenha-se compatível com o Windows 10 no futuro. Para mais informações, consulte a [compatibilidade da aplicação para programadores](https://developer.microsoft.com/windows/desktop/app-compatibility).

Se desenvolver soluções para o Office 365 ProPlus, consulte [as melhores práticas de Desenvolvimento para add-ins COM, VSTO e VBA no Office](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).
