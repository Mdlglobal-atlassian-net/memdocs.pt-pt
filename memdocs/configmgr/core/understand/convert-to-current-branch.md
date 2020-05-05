---
title: Atualize o LTSB para o ramo atual
titleSuffix: Configuration Manager
description: Aprenda a converter um site de serviços a longo prazo (LTSB) para um local de filial atual.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722957"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Atualize o ramo de manutenção a longo prazo para o ramo atual

*Aplica-se a: System Center Configuration Manager (Ramo de Manutenção a Longo Prazo)*

Utilize este tópico para aprender a atualizar (converter) um site e hierarquia que gere o Ramo de Manutenção a Longo Prazo (LTSB) de Gestor de Configuração para o Ramo Atual.

Quando tiver um acordo de garantia de software atual (ou direitos de licenciamento semelhantes) que lhe conceda direitos de utilização da Filial Atual, pode converter a sua instalação do LTSB para a Filial Atual.  Esta é uma conversão de sentido único porque não há suporte para converter um site da Filial Atual para o LTSB.

Se tiver vários sites, só precisa de converter o site de topo da sua hierarquia. Depois de convertido o site de topo:
- Os locais primários infantis convertem-se automaticamente.
- Tem de atualizar manualmente os sites secundários a partir da consola 'Gestor de Configuração'.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Executar configuração para converter o Ramo de Manutenção a Longo Prazo
No site de topo da sua hierarquia, pode executar configuração do Gestor de Configuração a partir de meios de base de base elegíveis e selecionar **a manutenção**do Site .  Em seguida, quando apresentado com a página de licenciamento, selecione a opção para o Ramo Atual e complete o assistente.

Quando o seu site se tiver convertido para o Ramo Atual, funcionalidades e capacidades anteriormente indisponíveis estarão disponíveis para utilização.

> [!NOTE]  
> Os meios de base qualificados são um meio de comunicação que tem uma versão igual ou posterior à sua instalação LTSB.

Por exemplo, como o LTSB é baseado na versão 1606, não é possível utilizar os meios de base 1511 para converter para o Ramo Atual. Em vez disso, executa a configuração a partir da mesma versão 1606 que usou para instalar o site LTSB, e escolha a opção de licenciamento para o Ramo Atual.  Alternadamente, se for lançada uma linha de base posterior da Sucursal Atual, pode executar a configuração a partir desse meio de base.

Para obter uma lista de versões de base, consulte **as versões Baseline e atualização** em [Atualizações para O Gestor](../servers/manage/updates.md)de Configuração .

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Utilize a consola 'Gestor de Configuração' para converter o ramo de manutenção a longo prazo
Se o seu site for executado no LTSB, pode utilizar a seguinte opção na consola 'Gestor de Configuração' para converter para o Ramo Atual:

 1. Na consola, vá aos**Sites**de**Configuração** > do Site **da Administração,** > e abra **as Definições da Hierarquia.**  

 2. Nas **Definições da Hierarquia,** mude para o separador **Licenciamento.** Selecione a opção de **converter para o Ramo Atual,** e depois escolha **Aplicar**.  

Quando o seu site se tiver convertido para o Ramo Atual, funcionalidades e capacidades anteriormente indisponíveis estarão disponíveis para utilização.
