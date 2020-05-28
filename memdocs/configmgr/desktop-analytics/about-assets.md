---
title: Ativos em Desktop Analytics
titleSuffix: Configuration Manager
description: Conheça dispositivos, condutores e aplicações no Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: d5900fd4cb4fdebea23e626ffbe17c5289712b31
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268917"
---
# <a name="assets-in-desktop-analytics"></a>Ativos em Desktop Analytics

Após os dispositivos reportarem dados ao Desktop Analytics, fornece um inventário dos seguintes ativos:

- Dispositivos
- Aplicações instaladas  

No portal de serviço, selecione **Assets** no menu Desktop Analytics.

## <a name="devices"></a>Dispositivos

O separador **Dispositivos** exibe informações-chave sobre todos os dispositivos da sua organização que se inscreve no Desktop Analytics. Pode ordenar em qualquer coluna ou filtro valores específicos.

> [!NOTE]  
> Se o painel de instrumentos não estiver a reportar o número de dispositivos que espera ver para o seu ambiente, consulte a resolução de [problemas do Desktop Analytics](troubleshooting.md).  

Num plano de implantação, há mais detalhes sobre dispositivos. Para mais informações, consulte [os ativos do Plano](about-deployment-plans.md#plan-assets)

## <a name="apps"></a>Aplicações

O separador **Apps** mostra todas as aplicações instaladas que o serviço deteta nos seus dispositivos Windows.

As aplicações **notáveis** são instaladas em mais de 2% dos dispositivos matriculados.

A definição de detalhes da **Aplicação** é desativada por padrão, pelo que este separador combina todas as versões de apps com o mesmo nome e editor.<!-- 5542186 --> O comportamento padrão ajuda a reduzir o número total de aplicações que vê, o que ajuda a reduzir os seus esforços para anotar as aplicações. A contagem de aplicações no azulejo **Noteworthy Apps** também reflete esta configuração. Por exemplo, em vez de listar centenas de casos de Microsoft Edge, há um exemplo para todas as versões. Pode tomar decisões uma vez para todas as versões. Se precisar de tomar decisões sobre versões específicas de uma aplicação, ligue esta definição. Também pode configurar esta definição quando trabalhar com um plano de implementação. Para mais informações, consulte [os ativos do Plano.](about-deployment-plans.md#plan-assets)

Selecione a aplicação da lista e selecione **Editar**. Esta ação apresenta detalhes para a aplicação. Selecione **o** menu importance drop-down e detete tede um valor. Também pode atribuir um **Proprietário.** Se fizer alterações, selecione **Guardar**.

Configure a **importância** das aplicações definindo uma das seguintes categorias:

- Crítico
- Importante
- Ignorar
- Não revisto
- Não é importante.<!-- 3587232 -->

Quando a **aplicação versa a** definição de detalhes está desligada, os detalhes da aplicação mostram o número de versões e idiomas da aplicação que combina. Se guardar quaisquer alterações aos detalhes da aplicação, aplica-se a todas as versões. Por exemplo, defino a **Importância** ou **proprietário**. Alguns valores mostrarão "Multiple", o que significa que não há um valor consistente em todas as versões.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" />Decisão de upgrade automático de aplicações de sistema e loja

<!-- 3587232 -->
Identificar **a Importância** e **a Decisão** de Upgrade é fundamental para todas as aplicações notáveis no workflow desktop Analytics. Para ajudar a reduzir os seus esforços ao anotar estas aplicações, certos tipos de aplicações são automaticamente marcados como *não importantes*. A decisão de atualização do plano de implementação destas aplicações também está marcada como *Ready*. As seguintes aplicações são compatíveis e devem continuar a funcionar depois de atualizar o Windows:

- Aplicativos e componentes do sistema publicados pela Microsoft

- Apps geridas e atualizadas a partir da Microsoft Store

> [!TIP]
> Gerencie as inputs para qualquer aplicação a nível global ou por plano de implementação.
>
> 1. No portal Desktop Analytics, no menu **Gerir,** selecione **Assets**. Em seguida, selecione **Apps**.
>
> 2. Utilize as colunas **Tipo** e **Categoria** para gerir estas categorias de aplicações:
>
>    - Para aplicativos de loja, filtrar **Tipo** como **Moderno**
>    - Para aplicações do sistema, **categoria** de filtro como **processo de fundo** ou componente **windows**

Num plano de implementação, também pode definir a **decisão de Upgrade**. Para mais informações, consulte [os ativos do Plano.](about-deployment-plans.md#plan-assets)

### <a name="usage"></a>Utilização

<!-- 5533890 -->

- **Total de instalações**: Este valor é o número de instalações da aplicação selecionada em todos os dispositivos inscritos no Desktop Analytics.

- **Percentagem de instalação**: Este valor é a percentagem de instalação da aplicação selecionada contra dispositivos inscritos no Desktop Analytics.

- **Os dispositivos lançaram esta aplicação nos últimos 30 dias**: Este valor é a contagem de dispositivos onde um utilizador lançou a aplicação selecionada. Apenas inclui dispositivos que reportaram uso nos últimos 30 dias. Esta contagem está em todos os seus dispositivos matriculados com desktop Analytics em execução em qualquer versão do Windows 10. É possível que esta contagem possa variar para um plano de implantação.

## <a name="next-steps"></a>Próximos passos

- [Conheça os planos de implementação do Desktop Analytics](about-deployment-plans.md)  

- [Conheça a segurança e atualizações de funcionalidades](about-updates.md)  

- [Avaliação da compatibilidade no Desktop Analytics](compat-assessment.md)  
