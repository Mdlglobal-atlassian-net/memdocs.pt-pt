---
title: Segurança e privacidade das consultas
titleSuffix: Configuration Manager
description: Compreenda as melhores práticas de segurança e privacidade quando consultar informações a partir da base de dados do site.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714613"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Segurança e privacidade para consultas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Consultas no Gestor de Configuração permitem-lhe obter informações da base de dados do site de acordo com critérios que especifica. O Gestor de Configuração recolhe informações sobre base de dados do site durante o funcionamento padrão. Por exemplo, utilizando informações que foram recolhidas durante a descoberta ou inventário, pode configurar uma consulta para identificar dispositivos que satisfaçam critérios especificados.  

 Para mais informações sobre consultas, consulte [Introdução a consultas](../../../core/servers/manage/introduction-to-queries.md). Para obter as melhores práticas de segurança e informações de privacidade sobre as operações do Gestor de Configuração que recolhem os dados que pode obter através de consultas, consulte segurança e privacidade para O Gestor de [Configuração](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Boas práticas de segurança para consultas

 Use esta segurança como melhores práticas para consultas.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Quando exportar ou importar uma consulta que seja guardada para um local de rede, proteja a localização e o canal de rede.|Limite quem pode aceder à pasta de rede.<br /><br /> Utilize a assinatura do Bloco de Mensagens do Servidor (SMB) ou a segurança do Protocolo de Internet (IPsec) entre a localização da rede e o servidor do site para evitar que um intruso adulterasse os dados da consulta antes de ser importado.|  

## <a name="next-steps"></a>Passos seguintes
  
[Segurança e privacidade do Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
