---
title: Atualizações em Desktop Analytics
titleSuffix: Configuration Manager
description: Conheça a segurança e as atualizações de funcionalidades no Desktop Analytics.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 1c79db413f8e37424b84d98d51fb584d168e3819
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268934"
---
# <a name="updates-in-desktop-analytics"></a>Atualizações em Desktop Analytics

No portal Desktop Analytics, veja o estado da segurança e atualizações de funcionalidades. Selecione estes nódosos no grupo Monitor do menu principal desktop Analytics. Estes nódeos dão-lhe informações sobre o estado destas atualizações no seu ambiente.


## <a name="security-updates"></a>Atualizações de segurança

Para rever o estado atual das atualizações de segurança, selecione **atualizações** de segurança na secção **Monitor** do Desktop Analytics:

![Náuino de atualizações de segurança do Desktop Analytics](media/security-updates.png)

Esta versão resume as atualizações de *segurança* para dispositivos que estão a executar o Windows 10. Os dispositivos na tabela de barras são categorizados pelas seguintes etiquetas:

#### <a name="latest"></a>Últimas

Os dispositivos estão a executar a mais recente atualização de segurança para esta versão e canal.

#### <a name="latest-1"></a>Último-1

Os dispositivos estão a executar uma atualização de segurança uma versão mais antiga do que a mais recente atualização disponível nesse canal.

#### <a name="older"></a>Mais antiga

Os dispositivos estão a executar uma atualização de segurança mais antiga do que o Last-1.

#### <a name="not-measured"></a>Não medido

O Desktop Analytics não avaliou o dispositivo. Este estado inclui dispositivos com dispositivos Windows 7, Windows 8.1 ou Windows 10 registados para o Programa Insider do Windows.  

Para ver as tendências de adoção para atualizações de segurança, selecione **Ver Mais** para uma versão específica do Windows. O gráfico de área empilhado categoriza os dispositivos pela atualização de segurança que instalaram ao longo do tempo.

Para rever o estado de implementação das atualizações de segurança, selecione **Ver tudo**. Esta visualização lista os dispositivos nas seguintes categorias:

- Não iniciadas
- Em curso
- Concluído
- Precisa de atenção - Dispositivos (classificados pelo nome do dispositivo)
- Precisa de atenção - Questões (ordenadas por tipo de edição)

Para mostrar aos dispositivos novas informações que o serviço ainda está a ser processado, selecione **Ver dados recentes**. O Desktop Analytics mostrará esta informação após a sua próxima atualização completa de dados.

  > [!IMPORTANT]
  > A opção Desktop Analytics para **ver dados recentes** é depreciada. Esta ação será removida num futuro lançamento do serviço Desktop Analytics. Para mais informações, consulte [as funcionalidades deprecatadas.](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)<!--7080949-->  

## <a name="feature-updates"></a>Atualizações de funcionalidades

Para rever o estado atual das atualizações de funcionalidades, selecione atualizações de **funcionalidades** na secção **Monitor** do Desktop Analytics:

![Recurso atualiza o nó do Desktop Analytics](media/feature-updates.png)

Esta versão resume as atualizações de *funcionalidades* para dispositivos que estão a executar o Windows 10.

Para obter mais informações sobre os períodos de serviço, consulte [a ficha de dados do ciclo](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)de vida do Windows .  

Os dispositivos na tabela de barras são categorizados pelas seguintes etiquetas:

#### <a name="in-service"></a>Em serviço

Os dispositivos estão a executar a mais recente atualização de funcionalidades para esta versão e canal.  

#### <a name="near-end-of-service"></a>Fim próximo do serviço

Os dispositivos estão a executar uma atualização de funcionalidades que está dentro de 90 dias após o fim do serviço.

#### <a name="end-of-service"></a>Fim do serviço

Os dispositivos estão a executar uma atualização de funcionalidades que já passou da data final do serviço. Estas datas são específicas das edições Da Enterprise e education do Windows. Não se candidatam às edições Home, Pro, Pro Education ou Pro for Workstations. Para mais informações, consulte [a ficha técnica do ciclo](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)de vida do Windows .

#### <a name="not-measured"></a>Não medido

O Desktop Analytics não avaliou o dispositivo. Este estado inclui dispositivos com dispositivos Windows 7, Windows 8.1 ou Windows 10 registados para o Programa Insider do Windows.

Selecione o azulejo para ver as tendências de adoção para atualizações de funcionalidades. O gráfico de área empilhado categoriza os dispositivos pela atualização de funcionalidades que instalaram ao longo do tempo.

## <a name="next-steps"></a>Próximos passos

- [Conheça os ativos do Desktop Analytics](about-assets.md): dispositivos, controladores e apps  

- [Conheça os planos de implantação](about-deployment-plans.md)  
