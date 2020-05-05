---
title: Ativos em Desktop Analytics
titleSuffix: Configuration Manager
description: Conheça dispositivos, condutores e aplicações no Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722551"
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

Configure a **importância** das aplicações definindo uma das seguintes categorias:

- Crítica
- Importante
- Ignorar
- Não revisto
- Não é importante.<!-- 3587232 -->

Selecione a aplicação da lista e selecione **Editar**. Esta ação apresenta detalhes para a aplicação. Selecione **o** menu importance drop-down e detete tede um valor. Também pode atribuir um **Proprietário.** Se fizer alterações, selecione **Guardar**.

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

Num plano de implementação, também pode definir a **decisão de Upgrade**. Para mais informações, consulte [os ativos do Plano](about-deployment-plans.md#plan-assets)

### <a name="usage"></a>Utilização

<!-- 5533890 -->

- **Total de instalações**: Este valor é o número de instalações da aplicação selecionada em todos os dispositivos inscritos no Desktop Analytics.

- **Percentagem de instalação**: Este valor é a percentagem de instalação da aplicação selecionada contra dispositivos inscritos no Desktop Analytics.

- **Os dispositivos lançaram esta aplicação nos últimos 30 dias**: Este valor é a contagem de dispositivos onde um utilizador lançou a aplicação selecionada. Apenas inclui dispositivos que reportaram uso nos últimos 30 dias. Esta contagem está em todos os seus dispositivos matriculados com desktop Analytics em execução em qualquer versão do Windows 10. É possível que esta contagem possa variar para um plano de implantação.

## <a name="next-steps"></a>Passos seguintes

- [Conheça os planos de implementação do Desktop Analytics](about-deployment-plans.md)  

- [Conheça a segurança e atualizações de funcionalidades](about-updates.md)  

- [Avaliação da compatibilidade no Desktop Analytics](compat-assessment.md)  
