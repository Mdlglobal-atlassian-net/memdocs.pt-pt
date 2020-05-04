---
title: Dados de diagnóstico e utilização FAQ
titleSuffix: Configuration Manager
description: Perguntas frequentes sobre dados de diagnóstico e utilização para O Gestor de Configuração
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60634ed8e275ff8496a08969054aa912a81b9d07
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709545"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>Perguntas mais frequentes sobre diagnósticos e dados de utilização

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo fornece respostas a perguntas frequentes sobre diagnóstico e dados de utilização no Gestor de Configuração.

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a>Posso desligar os dados de diagnóstico e uso?

Para ajudar a gerir quando o site envia dados, utilize o ponto de ligação de serviço no modo offline. Em seguida, utilize a ferramenta de ligação de serviço para enviar manualmente os dados. Para obter mais informações, veja os artigos seguintes:

- [Sobre o ponto de ligação de serviço](../../servers/deploy/configure/about-the-service-connection-point.md)
- [Utilizar a ferramenta de ligação de serviços](../../servers/manage/use-the-service-connection-tool.md)

Para suportar novas versões do Windows 10 e serviços na nuvem como o Microsoft Intune, é necessário atualizar regularmente o atual ramo do Gestor de Configuração. A Microsoft requer pelo menos o nível básico de diagnóstico e dados de utilização. Estes dados são utilizados para manter o produto atualizado, melhorar a experiência de atualização e melhorar a qualidade e segurança do produto.

Não são enviados dados para o serviço quando o ponto de ligação ao serviço se encontra em modo offline. Quando muda para o modo on-line ou utiliza a ferramenta de ligação ao serviço, envia dados para o serviço para verificar se há atualizações.

Também pode escolher o nível de dados que o Gestor de Configuração recolhe. Para mais informações, consulte [Níveis de dados de utilização de diagnóstico](levels-overview.md).

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> O que é o período de retenção de dados?

A Microsoft armazena dados de diagnóstico e utilização do Gestor de Configuração durante um ano.

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a>Os diagnósticos e os dados de utilização são enviados quando a configuração é executado?

Não. Os diagnósticos e dados de utilização são apenas enviados depois do site ser instalado e estar operacional.

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> Os dados são enviados com que frequência?

Os procedimentos armazenados pela SQL funcionam de sete em sete dias a partir da data em que instalou o site.

- No modo online, o ponto de ligação ao serviço faz o upload dos dados após a execução das consultas.

- No modo offline, utiliza a ferramenta de ligação de serviço para fazer o upload dos dados. (Os dados só estão inicialmente disponíveis para utilização offline sete dias após a instalação do site.)  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> Os dados podem ser utilizados para formar um mapa de rede?

Não. Estes dados não incluem quaisquer detalhes da rede, tais como endereços IP ou informações geográficas detalhadas. Para mais informações, consulte [Níveis de dados de utilização de diagnóstico](levels-overview.md#bkmk_versions)e encontre mais detalhes para a versão que está a utilizar.

Os dados incluem informações sobre fusos horários de cada site. Esta informação pode fornecer informações sobre a ampla geolocalização e dispersão global de sítios numa hierarquia.

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a>Consegue ver dados em tabelas SQL personalizadas?

Não. O Gestor de Configuração recolhe dados de diagnóstico e utilização através de procedimentos armazenados pela SQL. Estes procedimentos armazenados são contra tabelas de produtos predefinidas na base de dados. Todas estas tabelas SQL são pré-fixadas com **TEL_**. Como parte da consulta de deteção do esquema SQL, todos os nomes de tabela estão têm um hash para comparação contra as predefinições conhecidas. Este comportamento determina que as tabelas personalizadas existem na base de dados. A presença de tabelas personalizadas informa a Microsoft de que este nitidou o esquema da base de dados a partir do predefinido. Não inclui nenhum dos dados armazenados dentro dessas tabelas.

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a>Consegue ver outras bases de dados?

Não. Os procedimentos armazenados para recolher dados limitam-se à base de dados do site do Gestor de Configuração. A Microsoft não consegue ver os nomes de outras bases de dados, nem quaisquer dados noutras bases de dados.

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a>Algum dado é enviado para outros serviços integrados na nuvem?

Sim, quando integra esses serviços com o Gestor de Configuração. Como parte da interação com qualquer serviço na nuvem, o Gestor de Configuração envia alguns dados para esse serviço. Estes dados são específicos desse serviço na nuvem e separam-se dos diagnósticos do Gestor de Configuração e dos dados de utilização. Para obter mais informações sobre os dados específicos utilizados na interação com outro serviço na nuvem, consulte a documentação para esse serviço.

Por exemplo, os seguintes serviços na nuvem fazem parte do Microsoft Endpoint Manager:

- [Privacidade de dados do Desktop Analytics](../../../desktop-analytics/privacy.md)
- [Dados pessoais e privacidade no Intune](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Requisitos do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a>O Gestor de Configuração recolhe dados pessoais?

Não. A configuração não recolhe nem transmite quaisquer dados pessoais ou dados do cliente. É um produto no local que você implanta diretamente, gere e opera. Os dados de diagnóstico e utilização que a Microsoft recolhe melhoram a experiência de instalação, qualidade e segurança de futuras versões.

Para obter mais informações sobre os dados do Gestor de Configuração, consulte [Níveis de dados de utilização de diagnóstico](levels-overview.md).
