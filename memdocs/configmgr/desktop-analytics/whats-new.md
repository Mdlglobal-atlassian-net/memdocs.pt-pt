---
title: Novidades no Desktop Analytics
titleSuffix: Configuration Manager
description: Um resumo das novas funcionalidades no mais recente lançamento mensal do serviço de cloud Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ce882f6bfc7a0d724688d5df59051dae17d54498
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693146"
---
# <a name="whats-new-in-desktop-analytics"></a>Novidades no Desktop Analytics

Saiba o que há de novo todos os meses no Desktop Analytics.

> [!TIP]
> Cada atualização mensal pode demorar até três dias para ser lançada. É possível que algumas funcionalidades sejam implementadas durante várias semanas e que não estejam disponíveis para todos os clientes na primeira semana.

Para ser notificado quando esta página for atualizada, copie e cole o seguinte URL no seu leitor de feed RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="march-2020"></a>Março de 2020

### <a name="support-for-multiple-hierarchies"></a>Apoio a múltiplas hierarquias

<!-- 4814075, 6079184 -->

Agora pode ligar várias hierarquias do Gestor de Configuração a um único inquilino do Azure Ative Directory com um único ID comercial para Desktop Analytics. O portal categoriza dispositivos de diferentes hierarquias e melhora as experiências para pilotos globais e planos de implantação.

- Ao configurar o seu piloto global, se incluir coleções que contenham mais de 20% do total dos seus dispositivos matriculados, o portal apresenta um aviso.
- Quando cria um plano de implantação, se selecionar coleções para várias hierarquias, o portal exibe um aviso.

> [!NOTE]
> O suporte para várias hierarquias requer a versão 1910 ou mais tarde do Gestor de Configuração.

Para obter mais informações, veja os artigos seguintes:

- [Piloto global](deploy-pilot.md#bkmk_GlobalPilot)
- [Como criar planos de implantação](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>Identificar salvaguardas de compatibilidade

<!-- 5746559 -->

Os dados de compatibilidade do Windows classificam algumas aplicações e controladores com uma *salvaguarda*– o que pode fazer com que a atualização para o Windows 10 falhe ou recue. O Desktop Analytics pode agora ajudá-lo a identificar estas salvaguardas com antecedência, para que possa remediar o ativo antes de implementar a atualização. Para mais informações, consulte a avaliação da [compatibilidade - Salvaguardas](compat-assessment.md#safeguards).

## <a name="january-2020"></a>Janeiro de 2020

### <a name="additional-app-usage-detail"></a>Detalhe adicional de utilização de aplicativos

<!-- 5533890 -->

Quando seleciona uma aplicação para ver mais informações, o painel de detalhes agora inclui informações adicionais de utilização. Pode utilizar estes dados para ajudar a compreender a amplitude da instalação para uma aplicação, bem como dispositivos em que os utilizadores utilizam regularmente a aplicação. Para mais informações, consulte [sobre os ativos - Utilização de apps](about-assets.md#usage).

### <a name="provide-feedback-on-desktop-analytics"></a>Fornecer feedback sobre desktop Analytics

<!-- 5451636 -->

Para partilhar o seu feedback sobre desktop Analytics, selecione o ícone **Enviar um Sorriso** na parte superior do portal do lado direito. Para mais informações, consulte [Partilhar feedback](get-support.md#bkmk_feedback)do produto .

## <a name="october-2019"></a>Outubro de 2019

### <a name="improvements-to-compatibility-recommendations"></a>Melhorias nas recomendações de compatibilidade

<!-- 3594545 -->

O Desktop Analytics fornece agora detalhes adicionais quando deteta que a atualização do Windows irá remover total ou parcialmente uma aplicação ou controlador. Para mais informações, consulte a avaliação da [compatibilidade.](compat-assessment.md#asset-is-removed-during-upgrade)

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Migrar do Windows Analytics para inquilino existente

<!-- 5202803 -->

Agora pode migrar as inputs de um espaço de trabalho existente no Windows Analytics após o embarque para desktop Analytics.

## <a name="september-2019"></a>Setembro de 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Emigrar inputs do Windows Analytics

<!-- 4252663 -->

Durante o embarque, pode agora migrar as inputs de um espaço de trabalho existente no Windows Analytics.

### <a name="offboard-from-desktop-analytics"></a>Offboard de Desktop Analytics

<!-- 4972396 -->

Se configurar o Desktop Analytics no seu ambiente, mas quiser parar de utilizar o serviço, pode agora fechar a sua conta. Se mudar de ideia em 90 dias, pode reativar a conta. Para mais informações, consulte [Como fechar a sua conta.](account-close.md)

## <a name="august-2019"></a>Agosto de 2019

### <a name="reset-your-account"></a>Repor a conta

<!-- 3733897 -->

Se configurar o Desktop Analytics no seu ambiente, mas quiser recomeçar com o embarque e a inscrição, pode agora reiniciá-lo. Para obter mais informações sobre o processo, consulte [Redefinir a sua conta](account-reset.md).

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Decisão de upgrade automático de aplicações de sistema e loja

<!-- 3587232 -->

Para ajudar a reduzir os seus esforços ao anotar aplicações notáveis, certos tipos de aplicações são automaticamente marcados como *não importantes*. A decisão de atualização do plano de implementação destas aplicações também está marcada como *Ready*. As seguintes aplicações são compatíveis e devem continuar a funcionar depois de atualizar o Windows:

- Aplicativos e componentes do sistema publicados pela Microsoft

- Apps geridas e atualizadas a partir da Microsoft Store

Para mais informações, consulte a [decisão de atualização automática do sistema e armazenar aplicações.](about-assets.md#bkmk_plan-autoapp)

## <a name="whats-new-in-configuration-manager"></a>Quais as novidades no Gestor de Configuração

Os docs desktop Analytics referem-se sempre à funcionalidade na versão mais recente do ramo atual do Gestor de Configuração. Para obter mais informações sobre as mais recentes alterações no Gestor de Configuração, consulte os seguintes artigos:

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [Novidades na versão 1906](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>Características depreciadas

Quando a Microsoft planeia remover uma funcionalidade significativa do serviço Desktop Analytics, essa alteração será anunciada antecipadamente como uma funcionalidade de Preprecated Do Gestor de Configuração. Para mais informações, consulte [as funcionalidades deprecatadas.](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)
