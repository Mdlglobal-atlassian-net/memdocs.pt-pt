---
title: O Configuration Manager e o Windows como um Serviço
titleSuffix: Configuration Manager
description: Obtenha informações básicas sobre a adoção da filial atual do Gestor de Configuração para suportar o Windows como um serviço.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718554"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>O Configuration Manager e o Windows como um Serviço

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração fornece um controlo abrangente sobre as atualizações de funcionalidades para o Windows 10. Para adotar totalmente o Windows como modelo de serviço, também deve adotar o modelo atual de ramificação do Gestor de Configuração. Para se manter atual no Windows 10, requer que se mantenha atual no Gestor de Configuração para a melhor experiência. As novas versões do 'Gestor de Configuração' são necessárias para tirar o máximo partido das novas funcionalidades da empresa para o Windows 10. Este artigo destina-se a ser uma página de aterragem para os principais artigos necessários para adotar o ramo atual do Gestor de Configuração. A filial atual do Gestor de Configuração leva-o a caminho do Windows como um serviço.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Principais artigos sobre a adoção de sucursais atuais do Gestor de Configuração

| Artigo        | Descrição          | 
| ------------- |-------------|
|[Visão geral da sucursal atual do Gestor de Configuração](../plan-design/changes/whats-new-incremental-versions.md)|Fornece um breve resumo dos pontos-chave para o novo modelo de manutenção para O Gestor de Configuração (Ramo Atual)|
|[Apoiar o ciclo de vida](../servers/manage/current-branch-versions-supported.md)|Explica o novo modelo de suporte e manutenção.|
|[Itens removidos e depreciados](../plan-design/changes/deprecated/removed-and-deprecated.md)|Fornece aviso prévio sobre futuras alterações que podem afetar a sua utilização do Gestor de Configuração.|
|[Atualizações para o ramo atual do Gestor de Configuração](../servers/manage/updates.md)|Explica o método fácil na consola de aplicar atualizações de funcionalidades ao Diretor de Configuração.|
|[Obter as atualizações disponíveis](../servers/manage/install-in-console-updates.md#get-available-updates)|Explica os dois modos disponíveis para obter novas atualizações de funcionalidades do Gestor de Configuração.|
|[Lista de verificação de atualizações](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Fornece listas de verificação específicas da versão atualizada, se aplicável.| 
|[Instalar novas atualizações de funcionalidades do Gestor de Configuração](../servers/manage/install-in-console-updates.md#bkmk_install)|Explica os simples passos de instalação para atualizações de funcionalidades.|
|[Suporte para o Windows 10](../plan-design/configs/support-for-windows-10.md)|Fornece uma matriz de suporte para versões Windows 10 (e ADK).|
|[Pré-visualizações técnicas para gestor de configuração](../get-started/technical-preview.md)|Fornece informações sobre o programa de pré-visualização técnica ConfigMgr.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Principais artigos sobre a adoção do Windows como um serviço

| Artigo        | Descrição          |
| ------------- |-------------|
|[Gerir o Windows como um serviço](../../osd/deploy-use/manage-windows-as-a-service.md)|Explica como utilizar os planos de manutenção para implementar atualizações de funcionalidades do Windows 10.|
|[Atualizar o Windows 10 através de sequência de tarefas](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|Os detalhes da criação de uma sequência de tarefas para atualizar o Windows 10 com recomendações adicionais.|
|[Implementações faseadas](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|As implementações faseadas automatizam um lançamento coordenado e sequenciado de uma sequência de tarefas em várias coleções.|  
|[Optimize Windows 10 update delivery (Otimizar a entrega das atualizações do Windows 10)](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Utilize o Gestor de Configuração para gerir o conteúdo da atualização para se manter atualizado com o Windows 10.|
|[Use Desktop Analytics](../../desktop-analytics/overview.md)|O Desktop Analytics permite-lhe avaliar e analisar a prontidão dos dispositivos no seu ambiente para uma atualização para o Windows 10.|
|[Atualização do Windows para integração de negócios (opcional)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Explica como definir e implementar as políticas de Atualização do Windows para Negócios (WUfB) utilizando o Gestor de Configuração.|
|[Utilize a cogestão com a Microsoft Intune e o Windows Update para Negócios (opcional)](../../comanage/overview.md)|Fornece uma visão geral da cogestão|


## <a name="related-articles"></a>Artigos relacionados

- [Upgrade no local para o gerente de configuração atual do System Center 2012 Diretor de Configuração](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Plano de migração para o ramo atual do Gestor de Configuração](../migration/planning-for-migration.md)
