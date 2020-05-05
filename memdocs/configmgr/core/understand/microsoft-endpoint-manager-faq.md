---
title: FAQs do Microsoft Endpoint Configuration Manager
titleSuffix: Configuration Manager
description: Perguntas frequentes sobre o Microsoft Endpoint Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05aeca86071ea823d3ebc3cf493bea4d418bad27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722691"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>FAQs do Microsoft Endpoint Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual, ramo de pré-visualização técnica)*

A partir da versão 1910, o Gestor de Configuração faz agora parte do Microsoft Endpoint Manager. Este artigo fornece respostas a perguntas frequentes.

## <a name="summary"></a>Resumo

Comece por ver o seguinte vídeo de dois minutos de Brad Anderson, vice-presidente corporativo da Microsoft para a Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>FAQs

### <a name="what-is-microsoft-endpoint-manager"></a>O que é o Microsoft Endpoint Manager?

O Microsoft Endpoint Manager é uma solução integrada para gerir todos os seus dispositivos. A Microsoft reúne o Gestor de Configuração e insoniza com licenciamento simplificado. Continue a alavancar os investimentos existentes no Gestor de Configuração, aproveitando ao mesmo ritmo o poder da nuvem da Microsoft.

As seguintes soluções de gestão da Microsoft fazem agora parte da marca **Microsoft Endpoint Manager:**

- [Gestor de configuração](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Análise de Computadores](../../desktop-analytics/overview.md)
- [Piloto automático](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Outras funcionalidades na [Consola de Gestão](https://go.microsoft.com/fwlink/?linkid=2109094) de Dispositivos

Para mais informações, consulte as seguintes publicações de Brad Anderson, vice-presidente corporativo da Microsoft para a Microsoft 365:

- [Post de blog de anúncio](https://aka.ms/cmannounce)
- [Papel de visão](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Que coisas mudam no Gestor de Configuração com o Microsoft Endpoint Manager?

Na versão 1910, para além da mudança de nome, o Gestor de Configuração ainda funciona da mesma forma.

Mais notavelmente, os nomes das pastas iniciar foram alterados para componentes comuns, tais como a consola do Gestor de [Configuração](../servers/manage/admin-console.md#bkmk_open) e [o Centro de Software](software-center.md#bkmk_open).

### <a name="how-do-we-refer-to-the-product-now"></a>Como nos referimos ao produto agora?

- Ao referir-se a toda a solução que inclui todos os componentes: **Microsoft Endpoint Manager**

- Ao referir-se ao componente no local:
  - Na primeira referência, use o nome completo da marca: **Microsoft Endpoint Configuration Manager**
  - Para uso geral: **Gestor de Configuração**
  - Para uso limitado pelo espaço: **ConfigMgr**, apenas nos casos em que o nome de uso geral não se encaixe

### <a name="are-there-any-licensing-changes"></a>Há alguma alteração no licenciamento?

Sim! Conforme anunciado no Microsoft Ignite 2019, se tiver licença para O Gestor de Configuração, também está licenciado para a Intune [cogerir](../../comanage/overview.md) os seus PCs windows. Para mais informações, consulte o [Produto e licenciando as FAQ.](product-and-licensing-faq.md#bkmk_mem)

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>Por que ainda vejo "System Center Configuration Manager" em alguns lugares?

Leva tempo para fazer alterações em todos os produtos, serviços e materiais de apoio como documentação.

Há também alguns componentes fundamentais que podem nunca mudar. O principal serviço Windows nos servidores do site ainda está **SMS_Executive**. O repositório GitHub que suporta esta documentação continuará a ser **SCCMDocs**.

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre as [novidades nas versões incrementais do Gestor de Configuração.](../plan-design/changes/whats-new-incremental-versions.md)
