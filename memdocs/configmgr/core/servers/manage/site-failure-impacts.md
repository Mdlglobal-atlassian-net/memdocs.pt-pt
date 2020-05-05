---
title: Impactos de falha do site
titleSuffix: Configuration Manager
description: Compreenda os efeitos de várias falhas num site do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723895"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Impactos de falha no site no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O servidor do site e qualquer outro sistema de site pode falhar e causar uma perda dos serviços que regularmente fornecem. Se instalar vários sistemas de sites no mesmo computador, e esse computador falhar, todos os serviços regularmente fornecidos por esses sistemas de site já não estão disponíveis.

Parte do seu processo de planeamento deve incluir a compreensão do impacto no serviço que presta à sua organização. Como cada sistema de site no site fornece diferentes funcionalidades, o impacto de uma falha no site difere, dependendo do papel do sistema de site que falhou. 

Utilize [opções de alta disponibilidade](../deploy/configure/high-availability-options.md) para ajudar a mitigar a falha de qualquer sistema. Também planeie e pratique uma estratégia de [backup e recuperação](backup-and-recovery.md) para reduzir o tempo de tempo que o serviço não está disponível.

As seguintes secções descrevem o impacto quando o sistema de site especificado não está operacional:


### <a name="site-server"></a>Servidor do site

- Nenhuma administração do site é possível. Não é possível ligar a consola ao site.  

- O ponto de gestão recolhe informações do cliente e cache-lo até que o servidor do site esteja novamente on-line.  

- Os utilizadores podem executar implementações existentes, e os clientes podem descarregar conteúdo a partir de pontos de distribuição.  


### <a name="site-database"></a>Base de dados do site

- Nenhuma administração do site é possível.  

- Se o cliente do Gestor de Configuração já tiver uma atribuição de políticas com novas políticas, e se o ponto de gestão tiver cache o órgão de política, o cliente pode fazer um pedido de órgão de política e receber a resposta do órgão de política. No entanto, o site não pode servir quaisquer novos pedidos de atribuição de políticas.  

- Os clientes podem executar implementações, apenas se já receberam a apólice, e os ficheiros de origem associados já estão cached localmente no cliente.  


### <a name="management-point"></a>Ponto de gestão

- Embora possa criar novas implementações, os clientes não as recebem até que um ponto de gestão esteja online.  

- Os clientes ainda recolhem inventário, medição de software e informações sobre o estado. Armazenam estes dados localmente até que o ponto de gestão esteja disponível.  

- Os clientes podem executar implementações, apenas se já receberam a apólice, e os ficheiros de origem associados já estão cached localmente no cliente.  


### <a name="distribution-point"></a>Ponto de distribuição

- Os clientes do Gestor de Configuração podem executar implementações, apenas se os ficheiros de origem associados já tiverem sido descarregados localmente ou estiverem disponíveis numa fonte de pares.

