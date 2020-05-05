---
title: What happened to hybrid MDM? (O que aconteceu à MDM híbrida?)
titleSuffix: Configuration Manager
description: Conheça a depreciação da gestão de dispositivos móveis híbridos (MDM) no Gestor de Configuração
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d07a014cdcb3f371a90028ec09be3c0c939b8424
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721816"
---
# <a name="what-happened-to-hybrid-mdm"></a>What happened to hybrid MDM? (O que aconteceu à MDM híbrida?)

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!WARNING]
> A Microsoft retirou a oferta híbrida de serviço MDM a partir de 1 de setembro de 2019. Quaisquer dispositivos MDM híbridos restantes não receberão políticas, aplicações ou atualizações de segurança.

## <a name="remove-hybrid-mdm"></a>Remover MDM híbrido

Se o site do Gestor de Configuração tiver uma Subscrição Intune da Microsoft, tem de o remover.

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir **os Serviços Cloud**e selecionar o nó de **subscrição Microsoft Intune.** Elimine a subscrição intune existente.

1. No "Remover o Assistente de **Subscrição Intune da Microsoft",** selecione a opção de remover a **subscrição intune da Microsoft do Selectmanager**, e, em **seguida,** clique em Next .

1. Conclua o assistente.

## <a name="deprecation-announcement"></a>Anúncio de depreciação

A seguinte nota é o anúncio de depreciação original:

> [!NOTE]  
> A partir de 14 de agosto de 2018, a gestão de dispositivos móveis híbridos é uma [característica depreciada.](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md) A partir do lançamento do serviço Intune de 1902, previsto para o final de fevereiro de 2019, os novos clientes não conseguem criar uma nova ligação híbrida.
> <!--Intune feature 2683117-->  
> Desde o lançamento no Azure há mais de um ano, a Intune adicionou centenas de novas capacidades de serviço seletivas e líderes de mercado. Agora oferece muito mais capacidades do que as oferecidas através da gestão de dispositivos móveis híbridos (MDM). A Intune on Azure proporciona uma experiência administrativa mais integrada e simplificada para as suas necessidades de mobilidade empresarial.
>
> Como resultado, a maioria dos clientes escolhe Intune em Azure em vez de MDM híbrido. O número de clientes que usam MDM híbrido continua a diminuir à medida que mais clientes se movem para a nuvem. Assim, no dia 1 de setembro de 2019, a Microsoft vai retirar a oferta híbrida de serviço MDM.
>
> Esta alteração não afeta o Diretor de Configuração no local ou [a cogestão para dispositivos Windows 10](../../comanage/overview.md). Se não tiver a certeza se está a utilizar MDM híbrido, vá ao espaço de trabalho da **Administração** da consola Do Gestor de Configuração, expanda **os Serviços Cloud**e selecione **Microsoft Intune Subscriptions**. Se tiver uma subscrição Microsoft Intune configurada, o seu inquilino está configurado para MDM híbrido.
>
> **Como é que isto me afeta?**
>
> - A Microsoft irá suportar o seu uso híbrido de MDM para o próximo ano. A funcionalidade continuará a receber grandes correções de bugs. A Microsoft irá suportar a funcionalidade existente em novas versões DES, como a inscrição no iOS 12. Não haverá novas funcionalidades para o MDM híbrido.  
>
> - Se migrar para Intune em Azure antes do fim da oferta híbrida de MDM, não deverá haver impacto final do utilizador.  
>
> - No dia 1 de setembro de 2019, quaisquer dispositivos MDM híbridos restantes deixarão de receber políticas, apps ou atualizações de segurança.  
>
> - O licenciamento continua o mesmo. Insintonizado nas licenças Azure estão incluídos com MDM híbrido.  
>
> - A funcionalidade DE MDM no Local do Gestor de Configuração não é depreciada. A partir da versão 1810 do Gestor de Configuração, pode utilizar o MDM no local sem uma ligação Intune. Para mais informações, consulte [uma ligação Intune já não é necessária para novas implementações de MDM no local.](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm)
>
> - A funcionalidade de acesso condicional no local do Gestor de Configuração também é depreciada com MDM híbrido. Se utilizar o acesso condicional aos dispositivos geridos com o cliente do Gestor de Configuração, certifique-se de que estão protegidos antes de migrar.
>     1. Criar políticas de acesso condicional em Azure
>     2. Configurar políticas de conformidade no portal Intune
>     3. Termine a migração híbrida e coloque a autoridade do MDM em Intune
>     4. Ativar a cogestão
>     5. Mover as políticas de cogestão da carga de trabalho para Intune
>
>     Para mais informações, consulte [Acesso condicional com cogestão.](../../comanage/quickstart-conditional-access.md)
>
> **O que preciso de fazer para me preparar para esta alteração?**
>
> - Comece a planear a sua migração para MDM da consola ConfigMgr para O Azure. Muitos clientes, incluindo o Microsoft IT, passaram por este processo. Para mais informações, consulte este estudo de caso da [Microsoft](https://aka.ms/Intune_MSFT).  
>
> - Contacte o seu parceiro de registo ou fastTrack para obter assistência. [FastTrack para microsoft 365](https://aka.ms/hybrid_fasttrack) pode ajudar na sua migração de MDM híbrido para Intune no Azure.
>
> Para mais informações, consulte [o post do blog de suporte Intune](https://aka.ms/hybrid_notification).

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre funcionalidades suportadas para a gestão de dispositivos MDM, consulte os seguintes artigos:

- [O que é Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)
- [O que é MDM no local?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Gestão de dispositivos com o Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
