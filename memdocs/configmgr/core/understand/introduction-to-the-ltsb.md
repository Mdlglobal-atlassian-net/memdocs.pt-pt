---
title: Introdução ao LTSB
titleSuffix: Configuration Manager
description: Conheça o ramo de manutenção a longo prazo do Gestor de Configuração.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eda58982094860ccf075bcd2d1d8ed9e3d3bb2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722740"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Introdução ao ramo de manutenção a longo prazo do Gestor de Configuração

*Aplica-se a: System Center Configuration Manager (Ramo de Manutenção a Longo Prazo)*

O ramo de manutenção a longo prazo (LTSB) do Gestor de Configuração é um ramo distinto que é projetado como uma opção de instalação disponível para todos os clientes. No entanto, é a única opção para clientes que deixam caducar os seus direitos de garantia de software (SA) ou direitos de subscrição equivalentes para O Gestor de Configuração.

Com base na versão 1606 do Gestor de Configuração, o LTSB reduziu a funcionalidade em comparação com o atual ramo do Gestor de Configuração.

> [!TIP]   
> O Gestor de Configuração LTSB não está relacionado com o canal de manutenção de longo prazo do System Center (LTSC). Para mais informações, consulte a [visão geral das opções de lançamento do System Center](https://docs.microsoft.com/system-center/ltsc-and-sac-overview).

## <a name="features-that-arent-available"></a>Funcionalidades que não estão disponíveis

O atual ramo do Gestor de Configuração suporta a seguinte funcionalidade que não está disponível quando utiliza o LTSB:

- Atualizações na consola que adicionam novas funcionalidades e melhorias.
- Suporte para sistemas operativos recém-lançados para usar como servidores de site e clientes.
- On-premises MDM (MDM no local)
- O painel de instrumentos de manutenção e manutenção do Windows 10, incluindo suporte para versões recentes do Windows 10.  
- Suporte para futuras versões do Windows Server e Windows 10 LTSB
- Asset Intelligence
- Pontos de distribuição baseados na nuvem
- Troca online como um Conector de Intercâmbio    

Embora o suporte para estas funcionalidades não esteja disponível com o LTSB, algumas funcionalidades permanecem visíveis na consola Do Gestor de Configuração, mas não podem ser selecionadas ou usadas.

As integrações na nuvem, bem como quaisquer funcionalidades incluídas na versão atual do 'Gestor de Configuração' 1610 ou posterior, não estão disponíveis para o LTSB. Estas funcionalidades incluem, mas não se limitam ao seguinte:<!--SCCMDocs#1823-->

- Cogestão
- Análise de Computadores
- Gateway de gestão da cloud
- Integração do Azure Active Directory
- Aplicativos da Microsoft Store para Negócios

## <a name="find-ltsb-documentation"></a>Encontre documentação LTSB

O LTSB baseia-se na versão atual do ramo 1606. Utilize a documentação atual do [ramo,](https://docs.microsoft.com/sccm/)com ressalvas e limitações específicas do LTSB. Essas ressalvas e limitações são identificadas nos seguintes artigos:

- [Instalar o LTSC](install-the-ltsb.md)
- [Atualizar o LTSC para a via atual](convert-to-current-branch.md)
- [Configurações suportadas para o LTSC](supported-configurations-for-ltsb.md)
- [Gerir o LTSB do Gestor de Configuração](manage-the-ltsb.md)

Quando se refere a documentação atual do ramo para o LTSB, os detalhes que se aplicam à versão 1606 ou anterior também se aplicam ao LTSB. As funcionalidades ou detalhes que são introduzidos com a versão 1610 ou posteriormente não são suportados pelo LTSB.

## <a name="licensing-overview-for-the-ltsb"></a>Visão geral do licenciamento para o LTSB   

Os clientes com garantia de software ativa (SA) em licenças de Gestor de Configuração, ou com direitos de subscrição equivalentes a partir de 1 de outubro de 2016, têm direitos de utilização da versão 1606 de outubro de 2016 do Diretor de Configuração. Os clientes com direitos de Configuração Em ou depois de 1 de outubro de 2016, encontrarão duas opções licenciadas após a instalação: filial atual e ramo de manutenção de longo prazo (LTSB).

Os clientes que tenham direitos perpétuos ao System Center Configuration Manager, ou que permitam que a SA ou a subscrição caducem após o dia 1 de outubro, podem instalar a versão do System Center Configuration Manager LTSB que está atual no momento do lapso.

Para obter mais informações sobre estas licenças, consulte os [termos e condições Completos para os produtos que adquiriu através](https://go.microsoft.com/fwlink/?LinkId=800052)de programas de licenciamento de volume da Microsoft .

Para obter mais informações sobre o licenciamento para sucursais do Gestor de Configuração, consulte o licenciamento e os balcões do Gestor de [Configuração.](learn-more-editions.md)

## <a name="next-steps"></a>Passos Seguintes

Se decidir que o Gestor de Configuração LTSB é o ramo correto para o seu ambiente, instale um novo site [LTSB](install-the-ltsb.md#install-a-new-site) como parte de uma nova hierarquia, ou atualize um site e hierarquia do [System Center 2012.](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager)
