---
title: Utilização de dados de diagnóstico
titleSuffix: Configuration Manager
description: Saiba como a Microsoft utiliza os dados de diagnóstico e de utilização que o Gestor de Configuração recolhe.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715614"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Como a Microsoft utiliza diagnósticos de Configuração Manager e dados de utilização

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os dados de diagnóstico e utilização que o Gestor de Configuração recolhe fornecem à Microsoft um feedback quase imediato sobre como o produto está a funcionar e é usado para ajustar futuras atualizações. A Microsoft também pode ver dados de configuração que os ajudam a engendrar e testar as configurações que utiliza na produção. Por exemplo:

- As versões do servidor do Windows utilizadas nos servidores do site

- Pacotes de idiomas instalados

- O delta do esquema SQL relativamente à predefinição do produto

Estes dados ajudam a equipa de engenharia a planear futuros testes para garantir que tem a melhor experiência com as configurações mais comuns. Estes dados são cruciais para se ajustarem e adaptarem-se rapidamente com um ciclo de libertação frequente.

Igualmente importante é como os dados de diagnóstico e uso não são usados. A Microsoft não utiliza estes dados para:

- Auditorias de licenciamento, como comparar a utilização de cliente contra contratos de licença

- Auditoria de produtos que estão fora de suporte

- Publicidade com base em dados disponíveis, tais como utilização de recursos ou geolocalização (fuso horário)

A Microsoft utiliza dados disponíveis para melhorar o produto. Por exemplo:

- O suporte inicial oferecido pelo atual ramo do Gestor de Configuração limitou a linha de tempo de suporte para o Windows Server 2008 R2. A Microsoft analisou os dados de utilização de clientes que tinham atualizado para o ramo atual do Gestor de Configuração. Identificaram então a necessidade de rever e alargar esta linha temporal para apoiar os clientes que ainda utilizam este SISTEMA.

- A Microsoft melhorou as verificações pré-requisitos para a instalação de uma atualização. Removeram regras obsoletas, contabilizaram casos adicionais e remediaram automaticamente algumas questões.  

> [!div class="nextstepaction"]
> [Como o Configuration Manager recolhe dados](how-diagnostics-and-usage-data-is-collected.md)
