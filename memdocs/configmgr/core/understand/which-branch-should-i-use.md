---
title: Que ramo devo usar
titleSuffix: Configuration Manager
description: Saiba as diferenças entre os ramos disponíveis do Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7a505296fe51aae996d429fe7da2033d3a787ff
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722565"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Que via do Configuration Manager devo utilizar?

*Aplica-se a: Gestor de Configuração (atual ramo & serviço de pré-visualização técnica) & System Center Configuration Manager (ramo de manutenção a longo prazo)*

Existem três ramos de Gestor de Configuração disponíveis:

- Ramo atual
- Long-Term Servicing Channel
- Ramo de pré-visualização técnica

Use este artigo para ajudá-lo a escolher o ramo certo.

> [!TIP]  
> Todos os sítios numa hierarquia devem gerir o mesmo ramo. Não é suportado ter uma hierarquia com diferentes ramos em diferentes locais.

## <a name="current-branch"></a>Ramo atual

Este ramo é licenciado para uso em ambiente de produção. Utilize este ramo para obter as mais recentes funcionalidades e funcionalidades. Se tiver uma das seguintes licenças, pode utilizar este ramo:  

- Centro de Dados do Centro de Sistemas
- Padrão do Centro de Sistema
- System Center Configuration Manager
- Direitos de subscrição equivalentes  

Para obter mais informações sobre as opções de Garantia de Software e licenciamento, consulte [licenciamento e balcões para O Gestor](learn-more-editions.md) de Configuração e perguntas [frequentes para sucursais e licenciamento do Gestor de Configuração.](product-and-licensing-faq.md)

A Microsoft planeia lançar atualizações para o ramo atual do Gestor de Configuração algumas vezes por ano. Cada versão de atualização permanece em suporte durante 18 meses a partir da data de lançamento da sua disponibilidade geral (GA). É prestado apoio técnico durante todo o período de apoio. No entanto, a nossa estrutura de suporte é dinâmica, evoluindo para duas fases distintas de manutenção que dependem da disponibilidade da versão atual do ramo mais recente. (Para obter mais informações, consulte as [versões atuais](../servers/manage/current-branch-versions-supported.md)do Suporte para O Gestor de Configuração . As atualizações para versões mais recentes estão disponíveis como atualizações na consola.

Para instalar o ramo atual como um novo site, utilize meios de [base.](../servers/manage/updates.md#bkmk_Baselines) Utilize também os meios de base para atualizar a partir do System Center 2012 Configuration Manager com o Service Pack 2 ou system Center 2012 R2 Configuration Manager com o Service Pack 1. O acesso a este meio depende de como a sua organização licencia o Gestor de Configuração.

Também pode utilizar os meios de base para instalar um novo site que é uma edição de avaliação do ramo atual. A edição de avaliação não requer licença. Pode utilizar a edição de avaliação durante 180 dias. Suporta upgrade para uma edição licenciada da filial atual. Para instalar apenas uma edição de avaliação, obtenha-a no Centro de [Avaliação TechNet.](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)

> [!NOTE]
> Utilize os meios de base para instalar sites para uma nova hierarquia do Gestor de Configuração. Se já instalou uma versão de base, utilize atualizações na consola para atualizar os seus sites para uma nova versão.  
>
> Os sites que são atualizados utilizando atualizações na consola resultam em sites que são os mesmos que o novo site instalado usando os meios de base.
>
> Para mais informações, consulte [Atualizações para Gestor de Configuração](../servers/manage/updates.md).  

### <a name="features-of-the-current-branch"></a>Características do ramo atual

- Recebe [atualizações na consola](../servers/manage/install-in-console-updates.md) que disponibilizam novas funcionalidades para utilização.
- Recebe atualizações na consola que fornecem correções de segurança e qualidade às funcionalidades existentes.
- Suporta atualizações fora da banda quando necessário. Para mais informações, consulte [Utilize a ferramenta de registo de atualização](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) ou utilize o [instalador de 'hotfix'.](../servers/manage/use-the-hotfix-installer-to-install-updates.md)
- Integra-se com serviços baseados na nuvem.
- Suporta a [migração de dados](../migration/migrate-data-between-hierarchies.md) de e para outras instalações do Gestor de Configuração.
- Suporta a atualização de versões anteriores do Gestor de Configuração.
- Suporta a instalação como edição de avaliação, a partir da qual poderá posteriormente fazer upgrade para uma instalação totalmente licenciada.

A Microsoft recomenda que atualize para a versão mais recente logo após o seu lançamento. Pode esperar até 18 meses antes de atualizar para uma versão mais recente. Também pode saltar uma atualização para instalar a versão mais recente disponível. Uma vez que cada versão é cumulativa, se saltar uma atualização e instalar a versão mais recente, ainda tem acesso a todas as funcionalidades e melhorias de versões anteriores.

Para mais informações, consulte [Suporte para versões de ramificação atuais](../servers/manage/current-branch-versions-supported.md).

### <a name="current-branch-update-options"></a>Opções de atualização de ramo atuais

- Com o Software Assurance ativo, pode instalar atualizações na consola para versões de ramo atuais.  
- Não há opção de converter a filial atual num ramo técnico de pré-visualização. Os balcões de pré-visualização técnicos são instalações separadas que não requerem licença.
- Não há opção de converter o seu ramo atual para o ramo de manutenção a longo prazo (LTSB). Deve desinstalar o ramo atual e, em seguida, instalar o LTSB como uma nova instalação.

## <a name="long-term-servicing-branch"></a>Long-Term Servicing Channel

Esta sucursal está licenciada para utilização em produção para clientes do Gestor de Configuração que estão a usar a filial atual e permitiram que o seu Gestor de Configuração de Garantia de Software (SA) ou direitos de subscrição equivalentes expirassem após 1 de outubro de 2016. Para mais informações sobre garantia de software e opções de licenciamento, consulte [licenciamento e balcões para Gestor](learn-more-editions.md) de Configuração e perguntas [frequentes para sucursais e licenciamento do Gestor de Configuração.](product-and-licensing-faq.md)

O LTSB baseia-se na versão 1606. Este ramo não recebe atualizações na consola que oferecem novas funcionalidades ou atualizam as capacidades existentes. No entanto, são fornecidas correções críticas de segurança. Para instalar o LTSB, tem de utilizar os meios de [base](../servers/manage/updates.md#bkmk_Baselines) da versão 1606 que obtém com o System Center 2016. Versões de base posteriores não suportam a instalação do LTSB.

Para instalar o LTSB como um novo site ou como uma atualização de um site de Configuração do System Center 2012 suportado, utilize os [suportes de base](../servers/manage/updates.md#bkmk_Baselines) da versão 1606 que obtém com o System Center 2016. Pode utilizar os meios de base para instalar um novo site que executa a versão 1606 da filial atual, ou um novo site que gere o ramo de manutenção a longo prazo.

> [!TIP]  
> Para conhecer o System Center 2016, consulte a documentação do [System Center 2016.](https://docs.microsoft.com/system-center/index) Esta documentação também identifica como obter o System Center 2016, que requer um contrato de licença da Microsoft ou direitos semelhantes.  
>  
> Para encontrar a versão 1606 do Gestor de Configuração no Centro de Serviços de Licenciamento de Volume `System Center 2016`(VLSC), vá ao **separador Downloads e Chaves** do [VLSC,](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx)procure, e depois selecione o System Center **2016 Datacenter** ou **system center 2016 Standard**.  
>  
> Pode também obter uma edição de avaliação do System Center 2016 do [TechNet Evaluation Center.](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview)  

### <a name="features-of-the-ltsb"></a>Características do LTSB

- Recebe atualizações na consola que fornecem correções críticas de segurança.
- Fornece uma opção de instalação quando o seu contrato SA ou direitos equivalentes ao Gestor de Configuração expirarem.
- Suporta a atualização (conversão) para a sucursal atual quando tiver um contrato sato atual ou direitos equivalentes ao Gestor de Configuração.

### <a name="ltsb-limitations"></a>Limitações LTSB

O LTSB baseia-se na versão atual da sucursal 1606 e tem as seguintes limitações:

- O LTSB é suportado por 10 anos de atualizações críticas de segurança após a sua disponibilidade geral (outubro de 2016), após o que expira o suporte a esta sucursal. Para obter mais informações sobre o ciclo de vida de suporte, consulte a [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).
- Suporta uma lista limitada de sistemas operativos de servidores e clientes e tecnologias relacionadas, como as versões SQL Server. Para obter mais informações, consulte [configurações suportadas para o ramo](supported-configurations-for-ltsb.md)de manutenção a longo prazo .
- Não recebe atualizações para novas funcionalidades
- Não suporta as seguintes capacidades:
  - Funcionalidades ligadas à nuvem como cogestão ou Desktop Analytics
  - On-premises MDM (MDM no local)
  - O painel de assistência do Windows 10, planos de manutenção ou canal semi-anual do Windows 10
  - Futuras versões do Windows 10 LTSB e Windows Server
  - Inteligência de ativos
  - Quaisquer funcionalidades de pré-lançamento

### <a name="ltsb-update-options"></a>Opções de atualização LTSB

- Pode converter a sua instalação LTSB numa instalação de ramificação atual. A conversão para a sucursal atual é suportada antes ou depois de expirar o suporte para o LTSB.

  Para converter, tem de ter um acordo ativo de Garantia de Software com a Microsoft. Para obter mais informações, veja os artigos seguintes:

  - [Atualize o ramo de manutenção a longo prazo para o ramo atual](convert-to-current-branch.md)
  - [Licenciamento e balcões para Gestor de Configuração](learn-more-editions.md)
  - [Versões de base e atualização](../servers/manage/updates.md#bkmk_Baselines)

- Não há opção de converter o LTSB num ramo técnico de pré-visualização. Os balcões de pré-visualização técnicos são instalações separadas que não requerem licença.

- Não é possível atualizar uma edição de avaliação da filial atual para uma instalação LTSB.

## <a name="technical-preview-branch"></a>Ramo de pré-visualização técnica

O ramo de pré-visualização técnica é para ser usado em ambiente de laboratório. Conheça e experimente as mais recentes funcionalidades que estão a ser desenvolvidas para O Gestor de Configuração. Não é suportado num ambiente de produção, e não requer que tenha um contrato de licença de Garantia de Software.

Para instalar um novo site que gere o ramo de pré-visualização técnica, utilize os mais recentes suportes de [base para o ramo de pré-visualização técnica](../get-started/technical-preview.md#bkmk_install). Depois de instalar o ramo de pré-visualização técnica, novas versões estão disponíveis como atualizações na consola todos os meses.

### <a name="features-of-the-technical-preview-branch"></a>Características do ramo de pré-visualização técnica

- Com base em versões de base recentes do ramo atual
- Recebe atualizações na consola que atualizam a sua instalação para a versão mais recente do ramo de pré-visualização técnica
- Inclui novas funcionalidades que estão a ser desenvolvidas e para as quais a Microsoft quer o seu feedback
- Recebe atualizações que se aplicam apenas ao ramo de pré-visualização técnica

### <a name="technical-preview-limitations"></a>Limitações técnicas de pré-visualização

- [O suporte é limitado](../get-started/technical-preview.md#bkmk_reqs), incluindo apenas um único site primário e até 10 clientes.  
- Não é possível atualizá-lo ou migrar para uma sucursal atual ou instalação LTSB.
- Não suporta os seguintes comportamentos:
  - Utilize a migração para importar ou exportar dados para outra instalação do Gestor de Configuração
  - Upgrade de uma versão anterior do Gestor de Configuração
  - Instalar como edição de avaliação

As funcionalidades que são introduzidas pela primeira vez num ramo de pré-visualização técnica são muitas vezes adicionadas ao ramo atual numa atualização posterior. Cada nova versão do ramo de pré-visualização técnica inclui as funcionalidades de ramos de pré-visualização técnicos anteriores, mesmo depois de estas funcionalidades terem sido adicionadas ao ramo atual.

Para mais informações, consulte a [pré-visualização Técnica para O Gestor](../get-started/technical-preview.md)de Configuração .

### <a name="technical-preview-update-options"></a>Opções técnicas de atualização de pré-visualização

- Pode instalar qualquer atualização na consola para uma nova versão técnica do ramo de pré-visualização.

- Não há opção de converter um ramo de pré-visualização técnico para o ramo atual ou LTSB.

## <a name="identify-your-version-and-branch"></a>Identifique a sua versão e o seu ramo

### <a name="version"></a>Versão

Para verificar a versão do seu site, na consola vá ao **About Configuration Manager** no canto superior esquerdo da consola. Este diálogo exibe a **versão Do Site**. Para obter uma lista de versões do site, consulte as [versões Baseline e update](../servers/manage/updates.md#bkmk_Baselines).

### <a name="branch"></a>Ramo

Para confirmar o ramo do seu site, na consola vá aos**Sites**de**Configuração** > do Site **da Administração,** > e abra **as Definições da Hierarquia**. Se houver uma opção ativa para se converter ao ramo atual, o site executa a versão LTSB. Quando o site executa o ramo atual, a consola desativa esta opção.

Para obter mais informações sobre as diferentes versões do Gestor de Configuração, consulte [as versões Baseline e update](../servers/manage/updates.md#bkmk_Baselines).
